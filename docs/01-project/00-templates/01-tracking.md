---
ai_context:
  model_requirements:
    context_window: 8k_tokens
    memory_format: tabular
    reasoning_depth: optional
    attention_focus: analysis
  context_dependencies: []
  context_chain:
    previous: <file_path>
    next: <file_path>
  metadata:
    created: <YYYY-MM-DD HH:mm:ss A/PM CST>
    updated: 2026-02-04 11:48:14 AM CST
    version: <vX.Y.Z>
    category: tracking
    status: <active|archived>
    revision_id: "<commit-hash>"   # New field: unique revision identifier
    parent_doc: "<file_path>"  # New field: hierarchical relationship
    abstract: "<High-level summary>"  # New field for quick context
---
# [Document Title]
- **Path:** `/docs/01-project/00-templates/01-tracking.md`
- **Last Updated:** (template; see YAML `metadata.updated` when instantiated)
- **Purpose:** Template for progress/status tracking docs (issues, progress logs, audits).
- **Suggested related folders (docs-only):**
  - Issues: `/docs/01-project/01-analysis/00-tracking/00-issues/`
  - Progress: `/docs/01-project/01-analysis/00-tracking/01-progress/`
  - Completed: `/docs/01-project/01-analysis/00-tracking/99-completed/`


## Current Status
- Overall status: [In Progress/Complete/Blocked]
- Priority: [High/Medium/Low]
- Target completion: [Date]

## Progress Summary
### Completed Items
- [x] Item 1 (completed [Date])
  - Details
  - Impact
- [x] Item 2 (completed [Date])
  - Details
  - Impact

### In Progress
- [ ] Item 3 (started [Date])
  - Current status
  - Blockers
  - Next steps
- [ ] Item 4 (started [Date])
  - Current status
  - Blockers
  - Next steps

### Pending
- [ ] Item 5
- [ ] Item 6

## Metrics
### Timeline
- Start date: [Date]
- Current milestone: [Milestone]
- Next milestone: [Milestone]

### Statistics
- Total items: [Number]
- Completed: [Number]
- In progress: [Number]
- Pending: [Number]
- Completion rate: [Percentage]

## Issues and Risks
### Current Issues
1. Issue 1
   - Impact
   - Mitigation
   - Owner

### Potential Risks
1. Risk 1
   - Probability
   - Impact
   - Mitigation strategy

## Next Steps
1. Immediate actions
2. Short-term goals
3. Long-term planning

## Related Documents
- Link to related doc 1
- Link to related doc 2

## Change Log
- [Date] - Initial creation
  - Added section 1
  - Added section 2 

---

## Template Notes
- Replace all `<...>` YAML placeholders.
- Keep the visible “Last Updated” line aligned to YAML `metadata.updated` in real docs.