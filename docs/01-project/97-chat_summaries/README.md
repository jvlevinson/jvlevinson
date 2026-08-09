---
ai_context:
  model_requirements:
    context_window: 8k_tokens
    memory_format: sequential
    reasoning_depth: optional
    attention_focus: process
  context_dependencies:
    - /docs/01-project/README.md
  context_chain:
    previous: /docs/01-project/03-plans/README.md
    next: /docs/01-project/98-ai_notes/README.md
  metadata:
    created: 2026-08-07 03:27:45 PM CDT
    updated: 2026-08-07 03:27:45 PM CDT
    version: v1.0.0
    category: process
    status: active
    revision_id: ""
    parent_doc: "/docs/01-project/README.md"
    abstract: "Chronological records of AI working sessions on this repository."
---
# Chat Summaries

Chronological records of AI working sessions — what was asked, what changed, what was left open. These are the session-level companion to [98-ai_notes](/docs/01-project/98-ai_notes/README.md), which is organized by topic rather than by time.

## Structure

| Path | Holds |
|---|---|
| `/docs/01-project/97-chat_summaries/` | Full session summaries |
| `00-quick_chats/` | Short, single-purpose exchanges not worth a full summary |

## Writing a Summary

Copy [97-chat-summary-template.md](/docs/01-project/00-templates/97-chat-summary-template.md), then stamp it. The timestamp script drives session state through the same file:

```bash
bash .scripts/cmd/bash/update-timestamp.sh -f <file> -s created    # session start
bash .scripts/cmd/bash/update-timestamp.sh -f <file> -s active
bash .scripts/cmd/bash/update-timestamp.sh -f <file> -s paused     # or blocked / resume
bash .scripts/cmd/bash/update-timestamp.sh -f <file> -s ended      # session close
```

Each invocation also appends a line to `/reports/logs/running.log`. That log is gitignored, so it is local-only evidence — do not rely on it surviving a clone.

## Rules

- One file per session; never rewrite history in an old summary.
- Record what was **left unfinished** as explicitly as what was completed.
- Link forward to any plan or issue the session produced.

## Change Log

| Version | Date | Change |
|---|---|---|
| v1.0.0 | See `created` in frontmatter | Initial scaffold (Lite mode) |
