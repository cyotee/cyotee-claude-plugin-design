---
description: Audit task definitions for quality and completeness (not code review)
---

# Task Definition Audit

Audit and refine task **definitions** (TASK.md files) for quality and completeness. This reviews task specifications, NOT implementation code.

**For code review**, use `/backlog-review` instead.

**Arguments:** $ARGUMENTS

## Command Dispatch

### If no arguments: Review All Tasks

1. Load configuration from design.yaml
2. Scan tasks/ directories and analyze each TASK.md for:
   - Completeness (all required sections present)
   - Clarity (unambiguous requirements)
   - User story quality (testable acceptance criteria)
   - Dependencies (correctly identified)
   - Status accuracy

3. Generate review report with summary and detailed findings

4. Ask user which tasks to address, then update TASK.md files

### If task ID provided: Review Specific Task

1. Find task directory
2. Read task files (TASK.md, PROGRESS.md, REVIEW.md)
3. Analyze the task for quality issues
4. Interactive refinement with user
5. Update TASK.md with refinements
6. Output summary of changes

## Review Checklist

### Structure
- [ ] Has Description section
- [ ] Has Dependencies section
- [ ] Has User Stories (at least one)
- [ ] Has Files to Create/Modify section
- [ ] Has Inventory Check section
- [ ] Has Completion Criteria section

### Quality
- [ ] Description explains "what" and "why"
- [ ] User stories follow "As a... I want... so that..." format
- [ ] Acceptance criteria are testable
- [ ] Dependencies reference specific task IDs
- [ ] File paths are accurate

### Consistency
- [ ] Task ID matches directory name
- [ ] Status reflects actual progress
- [ ] INDEX.md entry matches TASK.md

## Common Issues to Flag

1. **Vague acceptance criteria:** "Works correctly" should be specific
2. **Missing error cases:** Only happy path covered
3. **Stale dependencies:** Completed tasks still listed as blockers
4. **Incomplete file lists:** Tests or interfaces missing
5. **No inventory checks:** Agent won't verify prerequisites
6. **Status mismatch:** Marked "Ready" but has unmet dependencies
7. **Orphaned tasks:** Directory exists but not in INDEX.md

## Related Commands

- `/backlog-review <ID>` - Code review (implementation)
- `/backlog` - View task status
