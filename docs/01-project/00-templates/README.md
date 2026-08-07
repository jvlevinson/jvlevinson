---
ai_context:
  model_requirements:
    context_window: 8k_tokens
    memory_format: tabular
    reasoning_depth: optional
    attention_focus: process
  context_dependencies:
    - /docs/01-project/README.md
  context_chain:
    previous: /docs/01-project/README.md
    next: /docs/01-project/01-analysis/README.md
  metadata:
    created: 2026-08-07 03:27:45 PM CDT
    updated: 2026-08-07 03:27:45 PM CDT
    version: v1.0.0
    category: process
    status: active
    revision_id: ""
    parent_doc: "/docs/01-project/README.md"
    abstract: "Index of canonical document templates available in this project."
---
# Templates

Canonical templates copied from `~/.claude/templates/`. **Do not edit these in place** — copy one into its destination section, then fill it in. The `<...>` placeholders are intentional and are what distinguishes a template from a document.

## Available Templates

| Template | Use for |
|---|---|
| [00-ai_header.md](/docs/01-project/00-templates/00-ai_header.md) | The `ai_context` frontmatter block + field validation rules. Read this first. |
| [00-ai_tech_header.md](/docs/01-project/00-templates/00-ai_tech_header.md) | Header variant for technical documents |
| [01-tracking.md](/docs/01-project/00-templates/01-tracking.md) | Issue and progress tracking documents (`/docs/01-project/01-analysis/00-tracking/`) |
| [02-guide.md](/docs/01-project/00-templates/02-guide.md) | How-to guides and tutorials |
| [03-technical.md](/docs/01-project/00-templates/03-technical.md) | Technical specifications and design documents |
| [97-chat-summary-template.md](/docs/01-project/00-templates/97-chat-summary-template.md) | AI session summaries (`/docs/01-project/97-chat_summaries/`) |

AI-note templates live separately, in [/docs/01-project/98-ai_notes/00-templates/](/docs/01-project/98-ai_notes/README.md).

## Not Included in This Scaffold

Lite mode omits two template tiers that exist in the global set:

- `00a-standards/` — documentation, validation, and review standards
- `00b-examples/` — worked examples (technical, process, analysis, plans)

The ADR template (`08-adr-template.md`) is also absent, because Lite mode does not create `08-decisions/`. Add any of these by re-running the init in Full mode or copying from `~/.claude/templates/`.

## Usage

```bash
cp docs/01-project/00-templates/03-technical.md docs/01-project/<section>/<NN>-<date>-<NNN>-CS-<descriptor>.md
# fill in the ai_context frontmatter, then:
bash .scripts/cmd/bash/update-timestamp.sh -f <new-file> -s created
```

## Change Log

| Version | Date | Change |
|---|---|---|
| v1.0.0 | See `created` in frontmatter | Initial scaffold (Lite mode) |
