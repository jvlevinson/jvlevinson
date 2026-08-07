---
ai_context:
  model_requirements:
    context_window: 8k_tokens
    memory_format: hierarchical
    reasoning_depth: required
    attention_focus: process
  context_dependencies:
    - /docs/01-project/98-ai_notes/00-templates/01-organization_process-001-v1.0.0.md
  context_chain:
    previous: /docs/01-project/98-ai_notes/00-templates/01-organization_process-001-v1.0.0.md
    next: /docs/01-project/98-ai_notes/00-templates/03-technical_specification-001-v1.0.0.md
  metadata:
    created: 2025-03-06 06:20:03 PM CST
    updated: 2026-02-16 12:00:00 PM CST
    version: v1.0.1
    category: process
    status: active
    revision_id: "cross-ref-guide-002"
    parent_doc: "/docs/01-project/98-ai_notes/00-templates/01-organization_process-001-v1.0.0.md"
    abstract: "Guide for implementing cross-references across the documentation system"
---
# Cross-Referencing Guide for Documentation System

## Overview

This guide establishes standards for cross-referencing between documents in the documentation system. Proper cross-referencing enables efficient navigation, ensures contextual completeness, and improves AI assistants' ability to access and relate information across the knowledge base.

## Cross-Reference Types

### 1. Dependency References

References that indicate a document depends on information in another document.

**Format:** `Depends on: Document Title -> relative/path/to/document.md` (example syntax)

**Example:**

```markdown
Depends on: [AI Notes Structure](../../NN-project_name/01-structure-001-v1.0.0.md)
```

**Usage Context:**

- In metadata sections under `context_dependencies`
- When introducing concepts defined elsewhere
- When extending functionality described in another document

### 2. Contextual References

References that provide additional context but aren't strict dependencies.

**Format:** `Related: Document Title -> relative/path/to/document.md (brief relevance)` (example syntax)

**Example:**

```markdown
Related: [Chunking Guidelines](../00-templates/01-chunking_guide.md) - Provides detailed guidance on optimal information organization
```

**Usage Context:**

- In "Related Documentation" sections
- When mentioning related but non-essential information
- When suggesting further reading

### 3. Implementation References

References to specific implementation details or examples.

**Format:** `Implementation: Document Title -> relative/path/to/document.md#section-anchor` (example syntax)

**Example:**

```markdown
Implementation: Optional tooling reference (not included in this repository)
```

**Usage Context:**

- When referring to code or technical implementations
- When linking to specific examples
- When connecting processes to tools

### 4. Historical References

References to previous versions or deprecated documents.

**Format:** `Historical: Document Title v1.0.0 -> ../../99-historical/path/to/document.md (Deprecated on YYYY-MM-DD)` (example syntax)

**Example:**

```markdown
Historical: [Previous Structure v1.0.0](../../99-historical/NN-project_name/00-structure-001-v1.0.0.md) (Deprecated on 2025-01-15)
```

**Usage Context:**

- When referring to previous approaches
- When documenting evolution of standards
- When explaining historical context

## Cross-Reference Locations


### Metadata Section

- Use `context_dependencies` for strict dependencies
- Use `context_chain` for sequential document relationships
- Use `parent_doc` for hierarchical relationships

### Document Body

- Include "Related Documentation" section at document end
- Use inline references when directly discussing related concepts
- Add "See Also" subsections at the end of relevant information chunks

### Special Sections

- "Source References" section for source materials
- "Implementation References" for technical implementations
- "Historical Context" for evolution and context

## Cross-Reference Best Practices


### 1. Relative Path Usage

- Always use relative paths from the current document
- Start paths with `../` to navigate up directory levels
- Check that paths resolve correctly before finalizing

### 2. Reference Bidirectionality

- When adding reference A → B, add corresponding reference B → A
- Match reference types when possible (dependency ↔ dependency)
- Note relationship direction when asymmetric

### 3. Reference Specificity

- Link to specific sections using markdown anchors when possible
- Target the most specific relevant document (not just general guides)
- Include version information for volatile references

### 4. Reference Maintenance

- Update references when documents move or are renamed
- Mark broken references with `BROKEN REF: description -> path/to/missing/document.md`
- Review all references during document updates

## Section Anchors


### Creating Anchors

- Anchors are automatically generated from headings
- Format: lowercase, spaces replaced with hyphens, punctuation removed
- Example: `## Implementation Details` → `#implementation-details`

### Custom Anchors

- Add custom anchors using HTML: `<a name="custom-anchor"></a>`
- Reference custom anchors with `#custom-anchor`
- Document custom anchors in a comment: `<!-- Custom anchor: custom-anchor -->`

## Cross-Reference Validation


### Manual Validation

1. Click each reference to ensure it resolves properly
2. Ensure bidirectional references exist
3. Verify reference types match the relationship

### Optional Validation (Not Implemented Here)

This repository does not currently ship an automated cross-reference validator. If you add tooling later, it can validate reference integrity (broken links, formatting consistency, bidirectional relationships) as part of CI.

## Common Cross-Reference Patterns


### Knowledge Graph Pattern

Connect conceptually related documents to create a navigable knowledge graph:

```text
A ↔ B ↔ C
↕       ↕
D ↔ E ↔ F
```

### Hierarchical Pattern

Create parent-child relationships between overview and detail documents:

```text
Parent
  ↓
Child1 ↔ Child2 ↔ Child3
```

### Sequential Pattern

Create chains of documents representing process steps or evolution:

```text
Step1 → Step2 → Step3 → Step4
```

## Change Log

- 2025-03-06 06:20:03 PM CST - Initial creation of cross-referencing guide
