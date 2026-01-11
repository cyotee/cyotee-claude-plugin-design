---
description: Initialize task management directory structure in a repository
allowed-tools: Read, Write, Bash, Glob, AskUserQuestion
---

# Initialize Task Management Structure

Create the tasks/ directory structure with template files for a new repository or layer.

## Instructions

### Step 1: Detect Layer Configuration

Dynamically determine layer name and prefix:

1. **Get repository/directory name:**
   ```bash
   # Get current repo name
   basename $(git rev-parse --show-toplevel 2>/dev/null || pwd)
   ```

2. **Check for existing tasks/ directories** (to avoid prefix collisions):
   ```bash
   # Find all tasks/ directories in the repo tree
   find . -type d -name "tasks" -not -path "*/node_modules/*" 2>/dev/null
   ```

3. **Generate prefix** from first letter of directory/repo name (uppercase)

4. **If prefix collision detected**, use AskUserQuestion to ask user for alternative prefix

5. **Check for config file** at `tasks/config.yaml` for existing layer definitions:
   ```yaml
   # Optional config file format
   layers:
     - name: "ProjectName"
       prefix: "P"
       path: "tasks/"
   ```

### Step 2: Create Directory Structure

Create the following structure in the appropriate location:

```
tasks/
├── 0/                    # Template directory
│   ├── PRD.md           # Task requirements template
│   ├── PROGRESS.md      # Progress log template
│   └── REVIEW.md        # Review findings template
├── archive/             # Completed tasks moved here
└── INDEX.md             # Task index/status overview
```

### Step 3: Create Template Files

**tasks/0/PRD.md:**

```markdown
---
task: 0
title: Task Template
status: template
layer: [LAYER_NAME]
worktree: feature/task-name
created: YYYY-MM-DD
dependencies: []
---

# Task [PREFIX]-N: [Title]

## Description

[2-3 sentences describing the task and its purpose]

## Dependencies

- [List prerequisite tasks: e.g., "[PREFIX]-1: Task Name"]
- [Or "None" if no dependencies]

## Technical Details

[Architecture diagrams, interface definitions, implementation notes]

## User Stories

### US-N.1: [Story Title]

As a [role], I want to [action] so that [benefit].

**Acceptance Criteria:**
- [ ] [Specific, testable criterion]
- [ ] [Specific, testable criterion]

### US-N.2: [Story Title]

...

## Files to Create/Modify

**New Files:**
- `path/to/NewFile.sol` - Description

**Modified Files:**
- `path/to/ExistingFile.sol` - What changes

**Tests:**
- `test/path/TestFile.t.sol` - Description

## Inventory Check

Before starting, verify:
- [ ] [Prerequisite exists/works]
- [ ] [Dependency is accessible]

## Completion Criteria

- [ ] All acceptance criteria met
- [ ] Tests pass (`forge test --match-path ...`)
- [ ] Build succeeds (`forge build`)
- [ ] No new compiler warnings

## Notes for Reviewer

[Agent adds notes here after implementation, before review]

---

**When complete, output:** `<promise>TASK_COMPLETE</promise>`

**If blocked, output:** `<promise>TASK_BLOCKED: [reason]</promise>`
```

**tasks/0/PROGRESS.md:**

```markdown
# Progress Log: Task [PREFIX]-N

## Current Checkpoint

**Last checkpoint:** [Not started]
**Next step:** [Read PRD.md and begin implementation]
**Build status:** ⏳ Not checked
**Test status:** ⏳ Not checked

---

## Session Log

<!-- Newest entries at top (reverse chronological) -->

### YYYY-MM-DD HH:MM - Session Start

- Initial session
- Reading PRD.md and CLAUDE.md

---

## Checkpoint Template

Use this format for checkpoint entries:

### YYYY-MM-DD HH:MM - [Checkpoint Name]

**Summary:** [Brief description of what was accomplished]

**Changes:**
- [File changed/created]
- [File changed/created]

**Decisions made:**
- [Design decision and rationale]

**Blockers/Issues:**
- [Any problems encountered]

**Next steps:**
- [What to do next]

**Build status:** ✅ Passing | ❌ Failing | ⏳ Not checked
**Test status:** ✅ Passing | ❌ Failing | ⏳ Not checked
```

**tasks/0/REVIEW.md:**

```markdown
---
reviewer: [pending]
date: [pending]
verdict: pending
---

# Review: Task [PREFIX]-N

## Acceptance Criteria Check

From PRD.md, verify each criterion:

| Criterion | Status | Notes |
|-----------|--------|-------|
| [Copy from PRD] | ⏳ | |

## Code Review Checklist

- [ ] Code follows project conventions (CLAUDE.md)
- [ ] No `new` deployments (uses CREATE3 factory)
- [ ] Tests cover success and failure paths
- [ ] No security vulnerabilities introduced
- [ ] Documentation updated where needed

## Findings

| ID | Severity | Summary | Status |
|----|----------|---------|--------|
| R-1 | | | |

**Severity levels:** Blocker | High | Medium | Low | Nit

## Build & Test Verification

```bash
# Commands run:
forge build
forge test --match-path [relevant tests]
```

**Build result:** ⏳
**Test result:** ⏳

## Follow-up Tasks

- [ ] [Any new tasks spawned from review findings]

## Verdict

**[PENDING]**

Options:
- **PASS** - Ready to merge
- **PASS WITH NOTES** - Ready to merge, minor items tracked
- **NEEDS WORK** - Must address findings before merge
- **BLOCKED** - Cannot proceed, requires [what]
```

**tasks/INDEX.md:**

```markdown
# Task Index

**Layer:** [LAYER_NAME]
**Prefix:** [PREFIX]

## Active Tasks

| # | Title | Status | Worktree | Dependencies | Created |
|---|-------|--------|----------|--------------|---------|
| | | | | | |

## Status Legend

- 🆕 **pending** - Task defined, not started
- 🚀 **in_progress** - Agent actively working
- 📋 **review** - Implementation complete, awaiting review
- ✅ **complete** - Reviewed and merged
- ❌ **blocked** - Cannot proceed (see task for reason)

## Quick Commands

```bash
# Launch agent for a task
cd <worktree-path>
claude --dangerously-skip-permissions

# In Claude, start the agent loop
/ralph-loop:ralph-loop "Read tasks/[N]/PRD.md and PROGRESS.md. Continue from last checkpoint." --completion-promise "TASK_COMPLETE"
```

## Archived Tasks

See `tasks/archive/` for completed tasks.
```

### Step 4: Confirm Creation

After creating all files, output:

```
✅ Task management structure initialized

Created:
- tasks/INDEX.md
- tasks/0/PRD.md (template)
- tasks/0/PROGRESS.md (template)
- tasks/0/REVIEW.md (template)
- tasks/archive/ (directory)

Next steps:
1. Run /design:prd to create the project's global PRD.md
2. Run /design:task to create your first task
```
