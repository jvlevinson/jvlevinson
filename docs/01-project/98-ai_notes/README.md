---
ai_context:
  model_requirements:
    context_window: 16k_tokens
    memory_format: hierarchical
    reasoning_depth: required
    attention_focus: technical
  context_dependencies:
    - /docs/01-project/README.md
  context_chain:
    previous: /docs/01-project/97-chat_summaries/README.md
    next: /docs/01-project/README.md
  metadata:
    created: 2026-08-07 03:27:45 PM CDT
    updated: 2026-08-07 03:27:45 PM CDT
    version: v1.0.0
    category: technical
    status: active
    revision_id: ""
    parent_doc: "/docs/01-project/README.md"
    abstract: "Topical, AI-optimized knowledge notes and their templates."
---
# AI Notes

Topical knowledge notes written to be consumed by an AI agent: chunked, cross-referenced, and dense. Organized by **subject**, unlike [97-chat_summaries](/docs/01-project/97-chat_summaries/README.md), which is organized by time.

## Structure

| Path | Holds |
|---|---|
| `/docs/01-project/98-ai_notes/` | The notes themselves |
| `00-templates/` | Note templates and authoring guides |
| `decisions/` | Decision records captured as AI notes |

## Templates

| Template | Use for |
|---|---|
| [00-note_template.md](/docs/01-project/98-ai_notes/00-templates/00-note_template.md) | Base structure for any new note |
| [01-chunking_guide.md](/docs/01-project/98-ai_notes/00-templates/01-chunking_guide.md) | How to segment content for retrieval |
| [01-organization_process-001-v1.0.0.md](/docs/01-project/98-ai_notes/00-templates/01-organization_process-001-v1.0.0.md) | Organizing a growing note collection |
| [02-cross_referencing-001-v1.0.0.md](/docs/01-project/98-ai_notes/00-templates/02-cross_referencing-001-v1.0.0.md) | Linking notes bidirectionally |
| [03-technical_specification-001-v1.0.0.md](/docs/01-project/98-ai_notes/00-templates/03-technical_specification-001-v1.0.0.md) | Technical specification notes |
| [04-decision_record-001-v1.0.0.md](/docs/01-project/98-ai_notes/00-templates/04-decision_record-001-v1.0.0.md) | Decision records for `decisions/` |
| [05-process_documentation-001-v1.0.0.md](/docs/01-project/98-ai_notes/00-templates/05-process_documentation-001-v1.0.0.md) | Process and workflow notes |

## Note on Decisions

`decisions/` here holds lightweight decision records. It is **not** the formal ADR chain — that lives in `08-decisions/`, which Lite mode did not create. If this repository grows to need real ADRs, scaffold `08-decisions/` and keep the two chains separate; do not cross-link them as equivalents.

## Change Log

| Version | Date | Change |
|---|---|---|
| v1.0.0 | See `created` in frontmatter | Initial scaffold (Lite mode) |
