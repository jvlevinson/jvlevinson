---
ai_context:
  model_requirements:
    context_window: 8k_tokens
    memory_format: hierarchical
    reasoning_depth: required
    attention_focus: analysis
  context_dependencies:
    - /docs/01-project/README.md
  context_chain:
    previous: /docs/01-project/00-templates/README.md
    next: /docs/01-project/03-plans/README.md
  metadata:
    created: 2026-08-07 03:27:45 PM CDT
    updated: 2026-08-07 03:27:45 PM CDT
    version: v1.0.0
    category: analysis
    status: active
    revision_id: ""
    parent_doc: "/docs/01-project/README.md"
    abstract: "Analysis output and the issue/progress tracking workflow."
---
# Analysis

Assessments, audits, and reviews of this repository, plus the tracking workflow that follows from them.

## Structure

| Path | Holds |
|---|---|
| `/docs/01-project/01-analysis/` | Analysis documents themselves |
| `00-tracking/00-issues/00-open_current/` | Open issues, one file per issue |
| `00-tracking/01-progress/` | In-flight work with status updates |
| `00-tracking/99-completed/` | Closed issues and finished work |

## Filing an Issue

1. Copy [01-tracking.md](/docs/01-project/00-templates/01-tracking.md) into `00-tracking/00-issues/00-open_current/`.
2. Name it `NN-{date}-NNN-CS-{descriptor}.md`.
3. Stamp it: `bash .scripts/cmd/bash/update-timestamp.sh -f <file> -s created`.
4. When work starts, move it to `01-progress/` and set status: `-s active`.
5. When it closes, move it to `99-completed/` and set status: `-s completed`.

Moving the file between directories *is* the state machine — the directory is the source of truth, and the `status` field in frontmatter must agree with it.

## Scope Note

This is a GitHub profile repository with no application code. Realistic analysis subjects are the CI metrics workflow, README rendering behavior, and link rot in `/README.md` (the banner image carries an expiring URL). See `/CLAUDE.md`.

## Change Log

| Version | Date | Change |
|---|---|---|
| v1.0.0 | See `created` in frontmatter | Initial scaffold (Lite mode) |
