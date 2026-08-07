# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

`jvlevinson/jvlevinson` — a GitHub **profile repository**. Because the repo name matches the account name, `README.md` renders as the landing page of <https://github.com/jvlevinson>. There is no application, build system, package manager, or test suite here; the entire repo is four tracked files:

| Path | Role |
|---|---|
| `README.md` | The profile page itself. Hand-edited. |
| `.github/workflows/metrics.yml` | CI that regenerates the metrics image. |
| `assets/github-metrics.svg` | **Generated artifact — never hand-edit.** |
| `.gitignore` | Ignores `.history/` and `experimental/`. |

## Branching — never commit to `main`

**All work happens on a branch. Never commit to `main` directly, and never merge directly into `main`.** Branches are numbered to match the chat session that produced them — session `00-YYYYMMDD-001-CS-*` → branch `001`. Integration into `main` is the owner's decision, made explicitly; do not initiate it.

Two consequences specific to this repo:

- Pushing a work branch does **not** trigger the metrics workflow — its `push:` trigger is scoped to `branches: [main]`. The daily `schedule:` still fires regardless of branch.
- The workflow hardcodes `committer_branch: main`, so if it ever runs from a branch it still commits its SVG to `main`. Editing the workflow on a branch does not sandbox its write target.

## The metrics loop (important before any commit)

`.github/workflows/metrics.yml` runs [`lowlighter/metrics`](https://github.com/lowlighter/metrics) and uses `output_action: commit` with `committer_branch: main`. It fires on **push to `main`**, on a **daily cron (00:00 UTC)**, and via `workflow_dispatch`.

Consequences:

- Every push you make to `main` triggers a workflow run that **pushes a follow-up commit back to `main`** (message: `Update metrics`, touching only `assets/github-metrics.svg`). The long chain of `Update metrics` commits in the log is this bot, not the author.
- **Always `git pull --rebase` before starting work**, or your push will be rejected by the bot's commit.
- Regenerating the SVG locally is pointless — CI overwrites it. To refresh it on demand, trigger the workflow (`gh workflow run "Update GitHub Metrics"`) rather than editing the asset.
- The job requires the `METRICS_TOKEN` secret, scoped to the `production` GitHub Environment. If runs fail with an auth error, that secret/environment binding is the first thing to check — not the workflow YAML.

## Editing README.md

- GitHub's markdown sanitizer **strips inline `style` attributes**. The `<div style="display: flex; ...">` wrappers around the shields.io badge groups therefore have no effect on the rendered page; badges simply flow inline. Don't invest in CSS-based layout — use tables, `<p align="center">`, or plain markdown for layout.
- Trailing double-spaces are load-bearing (they produce the line breaks inside the "Languages / Frameworks / …" skill blocks). Don't let a formatter trim them.
- The banner `<img>` at the top points at a LinkedIn CDN URL carrying an **expiry parameter** (`e=…`). It will 404 once that timestamp passes; if the banner is broken, the fix is to host the image in `assets/` and reference it relatively, as `README.md` already does for the metrics SVG.
- Several blocks are intentionally commented out (`## 🚀 Projects`, Twitter badge, LinkedIn/Twitter bullet links). Leave them commented unless asked to enable them — they are placeholders, not accidents.
- Content is first-person biography for Jordan V. Levinson. Never invent credentials, employers, metrics, or achievements; only edit what the user supplies.
