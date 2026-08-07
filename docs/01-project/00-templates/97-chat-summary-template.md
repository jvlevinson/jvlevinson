---
ai_context:
  model_requirements:
    context_window: 16k_tokens
    memory_format: hierarchical
    reasoning_depth: required
    attention_focus: technical
  context_dependencies:
    - <previous_chat_summary_if_applicable>
  context_chain:
    previous: <previous_chat_summary_path>
    next: null
  metadata:
    created: 2025-05-24 10:20:41 AM CST
    updated: 2026-07-07 11:25:19 AM CDT
    version: v1.0.1
    category: chat_summary
    status: in_progress
    revision_id: "<chat-id>"
    parent_doc: "<previous_chat_summary_path>"
    abstract: "<brief_description_of_chat_purpose>"
---
# Chat Summary: {Title}

## Chat Details

- **Chat ID:** `{AREA-PREFIX}-{YYYYMMDD}-{NNN}`
- **Date:** `{YYYY-MM-DD HH:mm:ss AM/PM CST}`
- **Status:** In Progress

## Overview

{Brief description of the chat session's purpose and accomplishments}

## Current Progress Status

{Summary of progress made during this chat session}

## Implementation Details

{Key implementation details, decisions, and code changes made}

## Issues Encountered

{Description of any issues or challenges encountered}

## Next Steps

{Clear outline of what needs to be done next}

## Change Log

- `{YYYY-MM-DD HH:mm:ss AM/PM CST}`: Initial creation of chat summary
- `{YYYY-MM-DD HH:mm:ss AM/PM CST}`: {Description of update}

## Timestamp Management

Never hand-type a timestamp — always let the script write it. Use the **first available** method
(see `~/.claude/commands/rules/always/time.md` for the full detection hierarchy):

1. **If the project has a `package.json`** (pnpm scripts, `-f` already embedded — just append the path):

   ```bash
   pnpm time:created <path-to-this-file>   # initial creation (sets created + updated)
   pnpm time:updated <path-to-this-file>   # subsequent updates (updated only)
   ```

2. **Otherwise call the bash script directly** (path is `.scripts/`, `scripts/`, or `scripted/`
   depending on the project — this repo uses `.scripts/`):

   ```bash
   bash .scripts/cmd/bash/update-timestamp.sh -s created -f <path-to-this-file>   # creation
   bash .scripts/cmd/bash/update-timestamp.sh -f <path-to-this-file>              # update
   ```

3. **Fallback — get the current time only** (then paste its exact output; never guess):

   ```bash
   TZ=America/Chicago date +"%Y-%m-%d %I:%M:%S %p %Z"
   ```

Always update timestamps when making significant changes to the document.

