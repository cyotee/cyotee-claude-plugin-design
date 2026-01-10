# design - Task Design Plugin

Interactive design sessions for creating and refining tasks with user stories in UNIFIED_PLAN.md.

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
1. Reads existing UNIFIED_PLAN.md to understand context and patterns
2. Asks clarifying questions about scope, purpose, and technical approach
3. Gathers requirements through 2-4 focused questions at a time
4. Drafts user stories with testable acceptance criteria
5. Creates a complete task section with all required fields
6. Updates UNIFIED_PLAN.md with the new task
7. Commits the changes

**Example usage:**
```
/design Add a dark mode toggle to the settings page
```

**Interactive process:**
```
Round 1 - Scope & Purpose:
- What problem does this solve?
- What layer does this belong to?
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

**Output:** A complete task in UNIFIED_PLAN.md with:
- Task number and title
- Layer (Crane/daosys/product)
- Worktree branch name
- Description
- Dependencies
- User stories (US-N.1, US-N.2, etc.)
- Files to create/modify
- Inventory checks
- Completion criteria

---

### `/design:review`

Review all tasks in UNIFIED_PLAN.md for quality and completeness.

**What it does:**
1. Analyzes each task for completeness and clarity
2. Checks user story quality and testable criteria
3. Validates dependencies are up-to-date
4. Generates a review report with issues and recommendations
5. Asks which tasks to update
6. Makes refinements and commits

**Example output:**
```
# Task Review Report

## Summary
| Task | Title           | Issues Found    | Recommendation |
|------|-----------------|-----------------|----------------|
| 5    | Protocol DETF   | None            | Ready          |
| 7    | Slipstream Vault| Missing deps    | Needs update   |

## Detailed Findings

### Task 7: Slipstream Vault
- **Status:** Ready for Agent
- **Issues:**
  - Acceptance criteria vague for US-7.3
  - Missing error case coverage
- **Recommendations:**
  - Specify exact state transition behavior
  - Add revert tests for edge cases
```

---

### `/design:review <task-number>`

Review and refine a specific task.

**What it does:**
1. Finds the specified task in UNIFIED_PLAN.md
2. Analyzes all sections for quality
3. Asks clarifying questions to fill gaps
4. Updates the task with refinements
5. Commits changes

**Example usage:**
```
/design:review 7
```

**Review checklist:**
- Description explains "what" and "why"
- User stories follow proper format
- Acceptance criteria are testable
- Dependencies reference specific task numbers
- File paths are accurate
- Inventory checks are verifiable
- Completion criteria are measurable

---

## Task Template

Tasks created by `/design` follow this structure:

```markdown
## Task N: [Title]

**Layer:** [Crane | daosys | IndexedEx]
**Worktree:** `feature/[kebab-case-name]`
**Status:** Ready for Agent

### Description
[2-3 sentences explaining the feature]

### Dependencies
- Task X must complete first
- External system Y must be available

### User Stories

**US-N.1: [Story Title]**
As a [role], I want to [action] so that [benefit].

Acceptance Criteria:
- Specific, testable criterion 1
- Specific, testable criterion 2

### Files to Create/Modify

**New Files:**
- `path/to/NewFile.sol` - Description

**Tests:**
- `test/path/Test.t.sol` - Description

### Inventory Check (Agent must verify)
- [ ] Prerequisite 1 exists
- [ ] Prerequisite 2 works

### Completion Criteria
- All user stories implemented
- Tests pass
- Documentation updated
```

---

## User Story Format

Each user story follows this pattern:

```markdown
**US-N.Y: [Title]**
As a [user/system/keeper], I want to [action] so that [benefit].

Acceptance Criteria:
- Criterion must be specific and testable
- Include both success and failure cases
- Reference exact function names or behaviors
```

---

## Related Files

| File | Purpose |
|------|---------|
| `UNIFIED_PLAN.md` | Task backlog where tasks are created/updated |
| `CLAUDE.md` | Project context read during design |

## Workflow Integration

```
1. /up:plan           # See existing tasks
2. /design <feature>  # Create new task
3. /design:review     # Refine tasks
4. /backlog:launch    # Start working on a task
```

## License

MIT
