# design - Task Design Plugin

Interactive design sessions for creating and refining tasks with user stories in the tasks/ directory structure.

## Installation

```bash
/plugin marketplace add cyotee/cyotee-claude-plugins
/plugin install design@cyotee
```

## Commands

### `/design <feature-description>`

Start an interactive design session to create a new task.

**Aliases:** `/design:task <feature-description>`

**What it does:**
1. Detects the current layer by scanning for tasks/ directories
2. Auto-generates layer name and prefix from directory/repo name
3. Asks clarifying questions about scope, purpose, and technical approach
4. Gathers requirements through 2-4 focused questions at a time
5. Drafts user stories with testable acceptance criteria
6. Creates task directory with PRD.md, PROGRESS.md, REVIEW.md
7. Updates tasks/INDEX.md with the new task

**Example usage:**
```
/design Add a dark mode toggle to the settings page
```

**Interactive process:**
```
Round 1 - Scope & Purpose:
- What problem does this solve?
- Which layer does this belong to?
- What are the key user actions?

Round 2 - Technical Approach:
- What existing patterns should this follow?
- What dependencies does this have?
- What external systems does this interact with?

Round 3 - Implementation Details:
- What are the key design decisions?
- What are the acceptance criteria?
- What tests are needed?
```

**Output:** A task directory with:
- `tasks/[PREFIX]-[N]/PRD.md` - Requirements and acceptance criteria
- `tasks/[PREFIX]-[N]/PROGRESS.md` - Agent progress log
- `tasks/[PREFIX]-[N]/REVIEW.md` - Review findings
- Updated `tasks/INDEX.md`

---

### `/design:init`

Initialize the tasks/ directory structure in a repository.

**What it does:**
1. Detects layer from repository/directory name
2. Generates prefix from first letter of layer name
3. Creates tasks/ directory with templates
4. Creates tasks/INDEX.md with layer info

**Created structure:**
```
tasks/
├── 0/                    # Template directory
│   ├── PRD.md           # Task requirements template
│   ├── PROGRESS.md      # Progress log template
│   └── REVIEW.md        # Review findings template
├── archive/             # Completed tasks moved here
└── INDEX.md             # Task index/status overview
```

---

### `/design:prd`

Interactive PRD creation for project-level requirements.

**What it does:**
1. Asks questions about project vision, goals, and constraints
2. Gathers target users and success metrics
3. Creates PRD.md at repository root

---

### `/design:review`

Review all tasks for quality and completeness.

**What it does:**
1. Scans all task directories in tasks/
2. Analyzes each PRD.md for completeness and clarity
3. Checks user story quality and testable criteria
4. Validates dependencies are up-to-date
5. Generates a review report with issues and recommendations
6. Asks which tasks to update

---

### `/design:review <task-id>`

Review and refine a specific task.

**Example usage:**
```
/design:review P-7
```

**Review checklist:**
- Description explains "what" and "why"
- User stories follow proper format
- Acceptance criteria are testable
- Dependencies reference specific task IDs
- File paths are accurate
- Inventory checks are verifiable
- Completion criteria are measurable

---

## Layer Detection

Layers are detected dynamically:
1. Scan for tasks/ directories in the repository
2. Read `tasks/INDEX.md` for layer name and prefix
3. If not found, auto-detect from directory/repo name
4. Prefix is first letter of layer name (uppercase)

## Task Template

Tasks created by `/design` follow this structure:

```markdown
---
task: N
title: [Title]
status: pending
layer: [Layer Name]
worktree: feature/[kebab-case-name]
created: YYYY-MM-DD
dependencies: []
---

# Task [PREFIX]-N: [Title]

## Description
[2-3 sentences explaining the feature]

## Dependencies
- [PREFIX]-X must complete first
- External system Y must be available

## User Stories

### US-N.1: [Story Title]
As a [role], I want to [action] so that [benefit].

**Acceptance Criteria:**
- [ ] Specific, testable criterion 1
- [ ] Specific, testable criterion 2

## Files to Create/Modify

**New Files:**
- `path/to/NewFile.sol` - Description

**Tests:**
- `test/path/Test.t.sol` - Description

## Inventory Check
- [ ] Prerequisite 1 exists
- [ ] Prerequisite 2 works

## Completion Criteria
- [ ] All user stories implemented
- [ ] Tests pass
- [ ] Documentation updated
```

---

## Related Files

| File | Purpose |
|------|---------|
| `tasks/INDEX.md` | Task index with status table |
| `tasks/[ID]/PRD.md` | Task requirements |
| `PRD.md` | Global project requirements |
| `CLAUDE.md` | Project context |

## Workflow Integration

```
1. /up:plan           # See existing tasks
2. /design:init       # Initialize tasks/ (first time)
3. /design <feature>  # Create new task
4. /design:review     # Refine tasks
5. /backlog:launch    # Start working on a task
```

## License

MIT
