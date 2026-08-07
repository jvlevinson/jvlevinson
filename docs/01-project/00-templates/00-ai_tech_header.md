---
ai_context:
  model_requirements:
    context_window: <8k|16k|32k>_tokens  # Select based on document complexity and context needs
    memory_format: <sequential|tabular|hierarchical|graph|relational>  # Choose based on content structure and relationships
    reasoning_depth: <required|optional|none|deep|shallow>  # Determines AI analysis depth and reasoning requirements
    attention_focus: <technical|process|analysis|infrastructure|security|documentation>  # Sets primary document purpose
  context_dependencies:
    - <file_path>  # List of required documents for full context
    - <related_issue_path>  # Related issue documents
    - <reference_doc_path>  # Reference documentation
  context_chain:
    previous: <file_path>  # Previous document in logical flow
    next: <file_path>  # Next document in logical flow
    related: []  # List of related documents not in direct chain
  metadata:
    created: <YYYY-MM-DD HH:mm:ss A/PM CST>  # Initial document creation time
    updated: <YYYY-MM-DD HH:mm:ss A/PM CST>  # Last modification time
    version: <vX.Y.Z>  # Semantic versioning
    category: <issues|technical|guide|analysis|infrastructure|security>  # Document category
    status: <draft|review|active|archived|deprecated>  # Current document state
    revision_id: "<ISSUE-XXX-000>"  # Unique identifier for the document
    issue_type: "<bug|feature|enhancement|infrastructure|security>"  # Type of issue being tracked
    severity: "<critical|high|medium|low>"  # Impact level of the issue
    owner: "<username|team_name>"  # Person or team responsible
    parent_doc: "<file_path>"  # Parent document in hierarchy
    abstract: "<High-level summary>"  # Brief document description
    tags:  # Relevant keywords for searching and categorization
      - <tag1>
      - <tag2>
    environment:  # Technical environment details
      os: "<os_name>"  # Operating system requirements
      docker_version: "<version>"  # Docker version requirements
      node_version: "<version>"  # Node.js version requirements
      dependencies: []  # List of other technical dependencies
    impact_analysis:  # Impact assessment
      scope: "<system_wide|component_specific>"  # Scope of impact
      affected_systems: []  # List of affected systems
      description: "<impact_description>"  # Detailed impact description
    resolution:  # Resolution tracking
      status: "<not_started|in_progress|blocked|resolved>"  # Current resolution status
      priority: "<urgent|high|medium|low>"  # Priority level
      assigned_to: "<username>"  # Person assigned to resolve
      expected_completion: "<YYYY-MM-DD>"  # Expected completion date
      blockers: []  # List of blocking issues
    external_references:  # External documentation links
      - name: "<reference_name>"
        url: "<url>"
        type: "<documentation|github|ticket>"
    review_status:  # Review tracking
      reviewed_by: "<username>"  # Reviewer
      review_date: "<YYYY-MM-DD>"  # Review date
      comments: "<review_comments>"  # Review comments
    change_history:  # Document change tracking
      - date: "<YYYY-MM-DD>"
        author: "<username>"
        description: "<change_description>"
---