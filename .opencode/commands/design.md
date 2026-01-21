---
description: Interactive design session to create a new task
---

# Create New Task

You are a systems architect conducting an interactive design session. Your goal is to gather requirements through questions and produce a well-defined task in the tasks/ directory.

**Feature to Design**: $ARGUMENTS

## Process

### Step 1: Load Configuration

Read repo configuration from design.yaml:
- `repo_prefix` - The prefix for task IDs (e.g., CRANE, DAO, IDX)
- `repo_name` - Human-readable repo name

If no design.yaml exists, inform user to run `/design-init` first.

### Step 2: Get Next Task Number

Scan existing task directories to find the next available number.

### Step 3: Research Context

Before asking questions, gather context:
1. Read PRD.md if it exists
2. Read CLAUDE.md/AGENTS.md if it exists
3. Read tasks/INDEX.md to see existing tasks
4. Explore relevant files if the feature involves existing code
5. Check for dependencies on other tasks

### Step 4: Interactive Requirements Gathering

Ask 2-4 focused questions at a time:

**Round 1 - Scope & Purpose:**
- What problem does this task solve?
- What are the key user actions or outcomes?

**Round 2 - Dependencies & Constraints:**
- What other tasks must complete first?
- What are the key constraints?

**Round 3 - Acceptance Criteria:**
- What specific behaviors must be implemented?
- What tests are required?

**Round 4 - Implementation Details:**
- What files need to be created or modified?
- What key design decisions need to be made?

### Step 5: Generate Task ID and Directory

```
Task ID: {PREFIX}-{NNN}
Directory: tasks/{PREFIX}-{NNN}-{kebab-case-title}/
```

### Step 6: Create Task Directory

Create:
- `tasks/{PREFIX}-{NNN}-{kebab-name}/TASK.md` - Requirements
- `tasks/{PREFIX}-{NNN}-{kebab-name}/PROGRESS.md` - Progress log
- `tasks/{PREFIX}-{NNN}-{kebab-name}/REVIEW.md` - Review template

### Step 7: Update INDEX.md

Add the new task to tasks/INDEX.md with appropriate status.

### Step 8: Validate Dependencies

- Verify all listed dependencies exist
- Check for circular dependencies
- Determine initial status (Ready or Blocked)

### Step 9: Output Summary

```
═══════════════════════════════════════════════════════════════════
 TASK CREATED: {PREFIX}-{NNN}
═══════════════════════════════════════════════════════════════════

Title: {Title}
Status: {Ready | Blocked}
Dependencies: {List or "None"}

## Files Created

- tasks/{PREFIX}-{NNN}-{kebab-name}/TASK.md
- tasks/{PREFIX}-{NNN}-{kebab-name}/PROGRESS.md
- tasks/{PREFIX}-{NNN}-{kebab-name}/REVIEW.md

## Launch Agent

/backlog-launch {PREFIX}-{NNN}

═══════════════════════════════════════════════════════════════════
```

## Error Handling

- **No tasks/ directory:** Run `/design-init` first
- **No design.yaml:** Run `/design-init` first
- **Circular dependency detected:** Show cycle path and abort
