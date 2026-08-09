---
ai_context:
  model_requirements:
    context_window: 8k_tokens
    memory_format: hierarchical
    reasoning_depth: optional
    attention_focus: process
  context_dependencies: []
  context_chain:
    previous: /README.md
    next: /docs/01-project/README.md
  metadata:
    created: 2026-08-07 03:27:45 PM CDT
    updated: 2026-08-07 03:27:45 PM CDT
    version: v1.0.0
    category: process
    status: active
    revision_id: ""
    parent_doc: "/docs/01-project/README.md"
    abstract: "Naming, linking, and frontmatter rules for this documentation system."
---
# Documentation Structure Guide

The rules that make this documentation system navigable by both humans and AI agents.

## Core Rules

1. **Numeric prefixing.** Every directory and document carries a numeric prefix that fixes its sort order. Low numbers are foundational (`00-templates`), high numbers are meta or terminal (`97-`, `98-`, `99-`). The prefix is part of the name, not decoration.
2. **Repo-rooted absolute links.** Write `/docs/01-project/README.md`, never `../README.md`. Relative links break the moment a file moves; repo-rooted links survive reorganization.
3. **`ai_context` frontmatter on every document.** No exceptions. It carries model requirements, dependency edges, and metadata. See [/docs/01-project/00-templates/00-ai_header.md](/docs/01-project/00-templates/00-ai_header.md) for field validation rules.
4. **File naming**: `NN-{date}-NNN-CS-{descriptor}.md`.
5. **Semantic versioning** (`vX.Y.Z`) in metadata. `created` is set once and never changes; `updated` changes on every edit.
6. **Never hand-type a timestamp.** Run the script; paste nothing.

## Main Areas

| Area | Purpose |
|---|---|
| [/docs/00-notes/](/docs/00-notes/) | Meta-documentation about the docs system itself (this file) |
| [/docs/01-project/00-templates/](/docs/01-project/00-templates/README.md) | Canonical templates — copy, never edit in place |
| [/docs/01-project/01-analysis/](/docs/01-project/01-analysis/README.md) | Assessments plus the issue/progress/completed tracking flow |
| [/docs/01-project/03-plans/](/docs/01-project/03-plans/README.md) | Testing, implementation, and historical plans |
| [/docs/01-project/97-chat_summaries/](/docs/01-project/97-chat_summaries/README.md) | Session records, chronological |
| [/docs/01-project/98-ai_notes/](/docs/01-project/98-ai_notes/README.md) | Topical AI-optimized knowledge notes |

This is a **Lite** scaffold. The full system additionally defines `02-concerns/`, `04-charts/`, `05-standards/`, `06-technical/`, `07-guides/`, `08-decisions/`, and `15-scripts/`. Their absence is deliberate, not an oversight.

## Timestamps

The timestamp script lives at `/.scripts/cmd/bash/update-timestamp.sh` (gitignored — local tooling, not distributed with the repo).

```bash
bash .scripts/cmd/bash/update-timestamp.sh -f <file> -s created   # new document
bash .scripts/cmd/bash/update-timestamp.sh -f <file>              # every later edit
```

It rewrites the 4-space-indented `created:`/`updated:` keys under `metadata:`, so preserve that indentation exactly or the script will silently no-op. It also appends to `/reports/logs/running.log`, which is gitignored and resolves relative to your **current working directory** — run it from the repository root.

## Starting Points

- Documentation hub: [/docs/01-project/README.md](/docs/01-project/README.md)
- Repository operating rules: [/CLAUDE.md](/CLAUDE.md)
- The published profile page: [/README.md](/README.md)

## Change Log

| Version | Date | Change |
|---|---|---|
| v1.0.0 | See `created` in frontmatter | Initial scaffold (Lite mode) |
