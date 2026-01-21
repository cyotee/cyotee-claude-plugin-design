---
description: Create new tasks from code review suggestions
---

# Create Tasks from Review Suggestions

Parse a task's REVIEW.md file and create new tasks from accepted suggestions. This closes the review loop by turning actionable feedback into tracked work items.

**Task to process:** $ARGUMENTS

## Process

### Step 1: Validate Input

1. Check argument provided (task ID)
2. Find task directory
3. Check for REVIEW.md

### Step 2: Load Configuration

Read repo prefix and name from design.yaml.

### Step 3: Parse REVIEW.md

Extract suggestions with user responses:
- **Accepted** - Create a new task
- **Modified** - Create with user's modifications
- **Rejected** - Skip

### Step 4: Interactive Confirmation

For each accepted/modified suggestion, confirm:
- Create as task?
- Modify description?
- Skip?

### Step 5: Create New Tasks

For each confirmed suggestion:
1. Generate task ID
2. Create TASK.md with suggestion details
3. Set dependency on original task
4. Create PROGRESS.md and REVIEW.md

### Step 6: Update INDEX.md

Add new tasks to INDEX.md.

### Step 7: Update Original REVIEW.md

Mark suggestions as "Converted to task {PREFIX}-{NNN}".

### Step 8: Output Summary

```
═══════════════════════════════════════════════════════════════════
 TASKS CREATED FROM REVIEW: {ORIGINAL_TASK_ID}
═══════════════════════════════════════════════════════════════════

Source: tasks/{ORIGINAL_TASK_ID}-{name}/REVIEW.md

## Tasks Created

| New Task | Title | Priority |
|----------|-------|----------|
| {PREFIX}-{NNN} | Add Input Validation | High |

## Skipped Suggestions

| Suggestion | Reason |
|------------|--------|
| Suggestion 3 | Rejected by user |

## Next Steps

1. Review created tasks: /design-review {PREFIX}-{NNN}
2. Launch agent for task: /backlog-launch {PREFIX}-{NNN}

═══════════════════════════════════════════════════════════════════
```

## Error Handling

- **No task ID provided:** Show usage
- **Task not found:** Show available tasks
- **No REVIEW.md:** Run code review first
- **No accepted suggestions:** Mark suggestions as Accepted first
