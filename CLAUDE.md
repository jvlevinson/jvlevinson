# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

`jvlevinson/jvlevinson` — a GitHub **profile repository**. Because the repo name matches the account name, `README.md` renders as the landing page of <https://github.com/jvlevinson>. There is no application, build system, package manager, or test suite.

| Path | Role |
|---|---|
| `README.md` | The profile page itself. The only file that renders publicly. |
| `.github/workflows/metrics.yml` | Daily CI that regenerates the metrics image. **Currently failing.** |
| `assets/github-metrics.svg` | **Generated artifact — never hand-edit.** Embedded at the bottom of the README. |
| `.gitignore` | See its own header comments — it documents its reasoning inline. |
| `docs/` | Lite documentation scaffold; see `/docs/01-project/README.md`. |

A profile README is **not** GitHub Pages. This repo has no Pages site (`has_pages: false`) and no `username.github.io` build. GitHub renders `README.md` directly on the profile page. Don't conflate the two.

## Branching — never commit to `main`

**All work happens on a branch. Never commit to `main` directly, and never merge directly into `main`.** Branches are numbered to match the chat session that produced them — session `00-YYYYMMDD-001-CS-*` → branch `001`. Integration into `main` is the owner's explicit decision; do not initiate it.

Note that **scheduled workflows only ever run from the default branch.** If a workflow is ever reintroduced here, changes to it are inert until they reach `main` — a fix that looks applied on a branch is not actually running.

## The metrics loop

`.github/workflows/metrics.yml` runs [`lowlighter/metrics`](https://github.com/lowlighter/metrics) with `output_action: commit` and `committer_branch: main`. It fires on **push to `main`**, on a **daily cron (00:00 UTC)**, and via `workflow_dispatch`. It is a wanted feature — keep it working.

- Every push to `main` triggers a run that **commits back to `main`** (message `Update metrics`, touching only `assets/github-metrics.svg`). The long chain of `Update metrics` commits is this bot, not the author. **`git pull --rebase` before starting work.**
- Regenerating the SVG locally is pointless — CI overwrites it. Refresh on demand with `gh workflow run "Update GitHub Metrics"`.

### Current failure — expired PAT

Failing since **2026-06-23**, every run logging `Bad credentials`. The `METRICS_TOKEN` repository secret was created **2025-06-22**; it hit the 1-year classic-PAT expiry. **The fix is rotating the token** — the owner handles this. The secret is repo-level and resolves fine; the `production` environment holds nothing, so the environment is not the problem.

When creating the replacement: **classic PAT with zero scopes.** The action writes every input including the PAT to a plaintext `.env` on the runner, so a `repo`-scoped token there is a standing credential to all 108 private repos. Fine-grained PATs are hard-blocked by the action.

### Known caveats — document, don't act on unilaterally

- Failing runs burn ~15m50s vs ~1m0s healthy, because the action's `retry()` sleeps after the *final* failed attempt too: 3 × 300s = 900s. `retries_delay: 0` fixes it.
- `@latest` is a mutable **branch**, not a tag — the repo is not actually pinned. Upstream's last release was 2023-09-13.
- The job-level `environment: production` key is what mints a GitHub Deployment record on every run — 433 of them so far, deploying nothing. Removing that key stops new ones; the historical records are cosmetic and were deliberately left alone.
- The SVG can only see public repos (70 public vs 108 private), so its language chart under-represents the owner's actual work.

These are improvements available on request — a SHA pin, `timeout-minutes`, the retry fix, dropping the `environment:` key. **None of them remove the metrics image.** Do not propose deleting the workflow again; that was considered and rejected.

## Editing README.md

**The README is the owner's voice. Do not restructure, condense, or "modernize" it without an explicit request for that.** A 2026-08-07 rewrite cut it from 173 lines to 48 — collapsing the badge groups into a table and flattening the prose — and was rejected outright. Improving the README means fixing what is broken *in place*, not replacing it. Ask before touching tone, length, or structure.

Known issues in the current README, documented but **not** to be "fixed" unilaterally:

- GitHub's markdown sanitizer **strips inline `style` attributes**, so the seven `<div style="display: flex">` wrappers around the badge groups do not render as flex. There is also an orphaned `</table>` at line 133 with no matching opener (verified: zero `<table` in the file), which GitHub silently drops. Layout that survives the sanitizer means tables, `<p align="center">`, or plain markdown.
- The banner `<img>` points at a LinkedIn CDN URL carrying an expiry parameter and currently returns **HTTP 403**. Hosting it in the repo would fix it.
- 3 of 31 `<img>` tags lack an `alt` attribute.
- Trailing double-spaces are load-bearing line breaks in the skills blocks. Don't let a formatter trim them.
- Content is first-person biography for Jordan V. Levinson. Never invent credentials, employers, metrics, or achievements; only edit what the owner supplies.

## Documentation and timestamps

Docs live under `docs/` with numeric prefixes; see `/docs/00-notes/02-documentation_structure_guide.md` for naming, linking, and frontmatter rules.

**Never hand-type a timestamp.** Use the deployed script (gitignored, local tooling):

```bash
bash .scripts/cmd/bash/update-timestamp.sh -f <file> -s created   # new document
bash .scripts/cmd/bash/update-timestamp.sh -f <file>              # every later edit
```

It rewrites the 4-space-indented `created:`/`updated:` keys under `metadata:` — preserve that indentation or it silently no-ops. It appends to `reports/logs/running.log` **relative to the current working directory**, so run it from the repository root.
