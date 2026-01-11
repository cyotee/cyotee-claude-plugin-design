---
description: Interactive design session to create a new task
argument-hint: <feature-description>
allowed-tools: Read, Write, Edit, Grep, Glob, AskUserQuestion, Bash, TodoWrite
---

# Create New Task

You are a systems architect conducting an interactive design session. Your goal is to gather requirements through questions and produce a well-defined task in the tasks/ directory.

**Feature to Design**: $ARGUMENTS

## Process

### Step 1: Determine Layer and Location

Identify which layer this task belongs to:

| Layer | Task Directory | Prefix | Example |
|-------|---------------|--------|---------|
| **Crane** | `lib/daosys/lib/crane/tasks/` | C | C-1, C-2 |
| **daosys** | `lib/daosys/tasks/` | D | D-1, D-2 |
| **IndexedEx** | `tasks/` | I | I-1, I-2 |

If the tasks directory doesn't exist, inform user to run `/design:init` first.

### Step 2: Get Next Task Number

Scan existing task directories to find the next available number:

```bash
# For IndexedEx layer:
ls -d tasks/I-* 2>/dev/null | sed 's/.*I-//' | sort -n | tail -1
# Increment by 1 for new task
```

### Step 3: Research Context

Before asking questions, gather context:
1. Read PRD.md to understand project goals
2. Read CLAUDE.md to understand technical conventions
3. Read tasks/INDEX.md to see existing tasks
4. If the feature involves existing code, explore relevant files
5. Check for dependencies on other tasks

### Step 4: Interactive Requirements Gathering

Use AskUserQuestion to ask 2-4 focused questions at a time.

**Round 1 - Scope & Purpose:**
- What problem does this task solve?
- Which layer does it belong to?
- What are the key user actions or outcomes?
- What existing patterns should this follow?

**Round 2 - Dependencies & Constraints:**
- What other tasks must complete first?
- What external protocols/systems does this interact with?
- What are the key constraints or limitations?

**Round 3 - Acceptance Criteria:**
- What specific behaviors must be implemented?
- What tests are required?
- What are the edge cases to handle?

**Round 4 - Implementation Details:**
- What files need to be created or modified?
- What key design decisions need to be made?
- Any performance or gas requirements?

Continue until you have enough information for complete user stories.

### Step 5: Create Task Directory

Create the task directory with all files:

```
tasks/[PREFIX]-[N]/
├── PRD.md
├── PROGRESS.md
└── REVIEW.md
```

### Step 6: Write PRD.md

Use the template from tasks/0/PRD.md, filling in:

```markdown
---
task: [N]
title: [Title]
status: pending
layer: [Layer]
worktree: feature/[kebab-case-name]
created: [Today's date]
dependencies: [List of task IDs, e.g., ["I-1", "C-3"]]
---

# Task [PREFIX]-[N]: [Title]

## Description

[2-3 sentences from discussion]

## Dependencies

[From discussion - list task IDs and titles]

## Technical Details

[From discussion - architecture, interfaces, etc.]

## User Stories

### US-[N].1: [Story Title]

As a [role], I want to [action] so that [benefit].

**Acceptance Criteria:**
- [ ] [Criterion from discussion]
- [ ] [Criterion from discussion]

[Additional user stories...]

## Files to Create/Modify

[From discussion]

## Inventory Check

- [ ] [Prerequisites to verify]

## Completion Criteria

- [ ] All acceptance criteria met
- [ ] Tests pass
- [ ] Build succeeds
- [ ] Documentation updated

## Notes for Reviewer

[To be filled by implementing agent]

---

**When complete, output:** `<promise>TASK_COMPLETE</promise>`

**If blocked, output:** `<promise>TASK_BLOCKED: [reason]</promise>`
```

### Step 7: Initialize PROGRESS.md

```markdown
# Progress Log: Task [PREFIX]-[N]

## Current Checkpoint

**Last checkpoint:** Not started
**Next step:** Read PRD.md and begin implementation
**Build status:** ⏳ Not checked
**Test status:** ⏳ Not checked

---

## Session Log

### [Today's Date] - Task Created

- Task designed via /design:task
- PRD.md populated with requirements
- Ready for agent assignment
```

### Step 8: Initialize REVIEW.md

Copy template from tasks/0/REVIEW.md, updating task number.

### Step 9: Update INDEX.md

Add the new task to tasks/INDEX.md:

```markdown
| [PREFIX]-[N] | [Title] | 🆕 pending | `feature/[name]` | [Dependencies] | [Date] |
```

### Step 10: Check Dependencies

If this task depends on other tasks, check their status:
- If dependency is complete: ✅ OK
- If dependency is in_progress: Note in output
- If dependency is pending/blocked: Mark this task as blocked

### Step 11: Output Summary

```
# Task Created: [PREFIX]-[N]

**Title:** [Title]
**Layer:** [Layer]
**Status:** pending
**Dependencies:** [List or "None"]

## Files Created

- tasks/[PREFIX]-[N]/PRD.md
- tasks/[PREFIX]-[N]/PROGRESS.md
- tasks/[PREFIX]-[N]/REVIEW.md
- Updated tasks/INDEX.md

## Launch Agent

To start working on this task:

1. Create worktree:
   ```bash
   ./scripts/wt-create.sh feature/[name]
   ```

2. Launch agent:
   ```bash
   cd [worktree-path]
   claude --dangerously-skip-permissions
   ```

3. Start task:
   ```
   /ralph-loop:ralph-loop "Read tasks/[PREFIX]-[N]/PRD.md and execute the task." --completion-promise "TASK_COMPLETE"
   ```

Or use: /backlog:launch [PREFIX]-[N]
```

## Error Handling

- **No tasks/ directory:** Suggest running `/design:init`
- **No PRD.md in repo root:** Suggest running `/design:prd`
- **Dependency task doesn't exist:** Warn user, ask to continue anyway
- **Dependency task is blocked:** Ask if this task should also be marked blocked
