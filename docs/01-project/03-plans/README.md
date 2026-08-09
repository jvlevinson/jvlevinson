---
ai_context:
  model_requirements:
    context_window: 8k_tokens
    memory_format: sequential
    reasoning_depth: required
    attention_focus: process
  context_dependencies:
    - /docs/01-project/README.md
  context_chain:
    previous: /docs/01-project/01-analysis/README.md
    next: /docs/01-project/97-chat_summaries/README.md
  metadata:
    created: 2026-08-07 03:27:45 PM CDT
    updated: 2026-08-07 03:27:45 PM CDT
    version: v1.0.0
    category: process
    status: active
    revision_id: ""
    parent_doc: "/docs/01-project/README.md"
    abstract: "Testing, implementation, and historical plan documents."
---
# Plans

Phased plans produced before work begins. A plan is written, reviewed, then executed — it is not a running log (that belongs in [01-analysis tracking](/docs/01-project/01-analysis/README.md)).

## Structure

| Path | Holds |
|---|---|
| `00-testing/` | Test strategies and verification plans |
| `01-implementation/` | Active implementation plans, phased |
| `99-historical/` | Superseded or completed plans, kept for provenance |

## Lifecycle

1. Draft the plan in `01-implementation/` with `status: draft`.
2. On approval, flip to `status: active` (`-s active`).
3. On completion, set `-s completed` and move the file to `99-historical/`.

Never delete a plan — move it to `99-historical/`. The record of what was intended is worth more than a tidy directory.

## Conventions

- Plans are **phased**: each phase states its own entry condition, work, and exit criteria.
- Cross-reference the analysis document that motivated the plan via `context_dependencies`.
- Bump the minor version (`vX.Y.0`) when adding a phase; the patch version for edits within a phase.

## Change Log

| Version | Date | Change |
|---|---|---|
| v1.0.0 | See `created` in frontmatter | Initial scaffold (Lite mode) |
