# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

`jvlevinson/jvlevinson` — a GitHub **profile repository**. Because the repo name matches the account name, `README.md` renders as the landing page of <https://github.com/jvlevinson>. There is no application, build system, package manager, or test suite.

| Path | Role |
|---|---|
| `README.md` | The profile page itself. The only file that renders publicly. |
| `.gitignore` | See its own header comments — it documents its reasoning inline. |
| `docs/` | Lite documentation scaffold; see `/docs/01-project/README.md`. |

A profile README is **not** GitHub Pages. This repo has no Pages site (`has_pages: false`) and no `username.github.io` build. GitHub renders `README.md` directly on the profile page. Don't conflate the two.

## Branching — never commit to `main`

**All work happens on a branch. Never commit to `main` directly, and never merge directly into `main`.** Branches are numbered to match the chat session that produced them — session `00-YYYYMMDD-001-CS-*` → branch `001`. Integration into `main` is the owner's explicit decision; do not initiate it.

Note that **scheduled workflows only ever run from the default branch.** If a workflow is ever reintroduced here, changes to it are inert until they reach `main` — a fix that looks applied on a branch is not actually running.

## The metrics workflow was deliberately removed — do not reinstate it

Until 2026-08-07 this repo ran `lowlighter/metrics` on a daily cron to generate `assets/github-metrics.svg` and commit it back to `main`. Both the workflow and the SVG were **deleted on purpose**. If you are tempted to "restore the missing metrics image," don't — read this first:

- **It had been failing for 47 consecutive runs** since 2026-06-23, because the `METRICS_TOKEN` classic PAT hit its 1-year expiry (created 2025-06-22). Every run logged `Bad credentials`.
- **Upstream is frozen.** Last release v3.34 on 2023-09-13; last human commit on `master` 2023-12-18. The repo is not archived, but its 2026 activity is Dependabot noise.
- **The security posture is bad.** It is a composite action that writes every input — *including the PAT* — to a plaintext `.env` on the runner, takes passwordless root via `sudo mkdir -p`, and docker-pulls a **mutable** `ghcr.io` tag, so pinning the action to a SHA pins nothing. `@latest` is a mutable *branch*, not a tag.
- **The output actively misrepresented the owner.** The final SVG reported HTML 39.65% / SCSS 32.98% / JavaScript 16.6% and **zero TypeScript**, against a README positioning Python and TypeScript as daily drivers — because it could only see public repos (70 public vs 108 private).
- **It cost ~170 KB/day** in committed SVG churn; roughly 400 such commits are why this 3-file repo carries ~3.5 MB of history.

GitHub already renders the contribution heatmap, activity timeline, achievements, and pinned repositories natively on the profile page, above the README, for free. That covers what a reader actually values.

**Consequences of the removal:** the `Update metrics` commits on `main` have stopped, so the old "always `git pull --rebase` before working" hazard is gone. The `METRICS_TOKEN` repository secret and the `production` / `METRICS_TOKEN` environments are now unused and can be deleted. The 433 historical deployment records were left in place deliberately — they are cosmetic and invisible on the profile page.

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
