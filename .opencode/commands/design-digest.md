---
description: Digest an existing design document into individual tasks
---

# Digest Design Document

Parse an existing design document (UNIFIED_PLAN.md, PRD.md, or any markdown file) into individual tasks in the tasks/ directory structure.

**Document to digest:** $ARGUMENTS

## Process

### Step 1: Validate Prerequisites

1. Check for design.yaml (required for repo prefix)
2. Check for tasks/ directory
3. Check that the specified file exists

### Step 2: Load Configuration

Read repo configuration from design.yaml.

### Step 3: Read Document

Read the specified document and analyze its structure:
- Identify sections that could be individual tasks
- Look for existing task definitions
- Find dependencies between sections
- Note any cross-repo references

### Step 4: Analyze and Identify Tasks

For each potential task, extract:
- Title/summary
- Description
- Dependencies
- User stories or acceptance criteria
- Files to create/modify

### Step 5: Interactive Clarification

For each identified task, ask clarifying questions:
- Repo assignment (if submodules defined)
- Missing information
- Dependency validation
- Acceptance criteria

### Step 6: Create Task Directories

For each confirmed task:
- Generate task ID
- Create TASK.md, PROGRESS.md, REVIEW.md
- Update INDEX.md

### Step 7: Output Summary

```
═══════════════════════════════════════════════════════════════════
 DIGEST COMPLETE: {filename}
═══════════════════════════════════════════════════════════════════

Analyzed: {filename}
Tasks identified: {N}
Tasks created: {M}
Tasks skipped: {K}

## Tasks Created

- {PREFIX}-{NNN}: {Title}
- {PREFIX}-{NNN}: {Title}

## Dependencies Mapped

- {PREFIX}-{NNN} depends on {PREFIX}-{NNN}

## Next Steps

1. Review created tasks for completeness
2. Use /design-review to check task quality
3. Use /backlog-launch to start work

═══════════════════════════════════════════════════════════════════
```

## Error Handling

- **File not found:** Check path and try again
- **No tasks/ directory:** Run /design-init first
- **No design.yaml:** Run /design-init first
