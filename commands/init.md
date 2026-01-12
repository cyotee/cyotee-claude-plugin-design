---
description: Initialize task management directory structure in a repository
allowed-tools: Read, Write, Bash, Glob, AskUserQuestion
---

# Initialize Task Management Structure

Create the tasks/ directory structure with template files for a new repository.

## Instructions

### Step 1: Detect or Create Configuration

1. **Check for existing configuration:**
   ```bash
   # Check for design.yaml in repo root
   if [ -f "design.yaml" ]; then
     echo "Found design.yaml"
     cat design.yaml
   fi

   # Check for local overrides
   if [ -f ".claude/design.local.md" ]; then
     echo "Found local overrides"
   fi
   ```

2. **If no design.yaml exists**, ask user for configuration:
   - Use AskUserQuestion to get:
     - Repo prefix (2-6 uppercase chars, e.g., CRANE, DAO, IDX)
     - Repo name (human-readable name for the repo)

3. **Create design.yaml** in repo root:
   ```yaml
   # design.yaml - Task management configuration
   # This file is shared with the team (checked into git)

   repo_prefix: <PREFIX>
   repo_name: <REPO_NAME>

   # Optional: define submodules for root repos
   # submodules:
   #   - prefix: DAO
   #     path: lib/daosys
   #     name: DAOsys
   ```

4. **Note about local overrides** (optional, user can create later):
   - `.claude/design.local.md` - gitignored, per-developer overrides
   - Can override any setting from design.yaml

### Step 2: Create Directory Structure

Create the following structure:

```
tasks/
├── TEMPLATE.md          # Task template
├── INDEX.md             # Task index/status overview
└── archive/             # Completed tasks moved here
```

### Step 3: Create Template Files

**tasks/TEMPLATE.md:**

```markdown
# Task {PREFIX}-{NNN}: {Title}

**Repo:** {REPO_NAME}
**Status:** Ready
**Created:** {DATE}
**Dependencies:** None
**Worktree:** `feature/{kebab-name}`

---

## Description

[2-3 sentences explaining the feature and its purpose]

## Dependencies

- [List prerequisite tasks: e.g., "{PREFIX}-001: Task Name"]
- Or "None" if no dependencies

## User Stories

### US-{PREFIX}-{NNN}.1: [Story Title]

As a [role], I want to [action] so that [benefit].

**Acceptance Criteria:**
- [ ] [Specific, testable criterion]
- [ ] [Specific, testable criterion]

### US-{PREFIX}-{NNN}.2: [Story Title]

...

## Technical Details

[Architecture diagrams, interface definitions, implementation notes]

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
- [ ] Tests pass
- [ ] Build succeeds
- [ ] No new compiler warnings

---

**When complete, output:** `<promise>TASK_COMPLETE</promise>`

**If blocked, output:** `<promise>TASK_BLOCKED: [reason]</promise>`
```

**tasks/INDEX.md:**

```markdown
# Task Index: {REPO_NAME}

**Repo:** {PREFIX}
**Last Updated:** {DATE}

## Active Tasks

| ID | Title | Status | Dependencies | Worktree |
|----|-------|--------|--------------|----------|
| | | | | |

## Status Legend

- **Ready** - All dependencies met, can be launched with `/backlog:launch`
- **In Progress** - Implementation agent working (has worktree)
- **In Review** - Implementation complete, awaiting code review
- **Changes Requested** - Review found issues, needs fixes
- **Complete** - Review passed, ready to archive with `/backlog:prune`
- **Blocked** - Waiting on dependencies

## Quick Filters

### Ready for Agent
(Tasks with all dependencies met)

### Blocked
(Tasks waiting on dependencies)

## Cross-Repo Dependencies

Tasks in other repos that depend on this repo's tasks:
- (none yet)
```

### Step 4: Confirm Creation

After creating all files, output:

```
✅ Task management structure initialized

Created:
- design.yaml (repo configuration)
- tasks/INDEX.md (task index)
- tasks/TEMPLATE.md (task template)
- tasks/archive/ (archive directory)

Configuration:
- Repo Prefix: {PREFIX}
- Repo Name: {REPO_NAME}

Next steps:
1. Run /design:prd to create the project's PRD.md (optional)
2. Run /design to create your first task
3. Or run /design:digest <file> to import tasks from an existing design document
```

## Error Handling

- **tasks/ already exists:** Ask user if they want to reinitialize (will not overwrite existing tasks)
- **design.yaml already exists:** Show current config, ask if user wants to update it
- **Not in a git repo:** Warn but continue (some features may not work)
