---
description: Initialize task management directory structure in a repository
---

# Initialize Task Management Structure

Create the tasks/ directory structure with template files for a new repository.

## Instructions

### Step 1: Detect or Create Configuration

1. Check for existing design.yaml
2. If no design.yaml exists, ask user for:
   - Repo prefix (2-6 uppercase chars, e.g., CRANE, DAO, IDX)
   - Repo name (human-readable)

3. Create design.yaml:
   ```yaml
   repo_prefix: <PREFIX>
   repo_name: <REPO_NAME>
   ```

### Step 2: Create Directory Structure

```
tasks/
├── TEMPLATE.md          # Task template
├── INDEX.md             # Task index/status overview
└── archive/             # Completed tasks moved here
```

### Step 3: Create Template Files

**tasks/TEMPLATE.md:** Standard task template with all required sections

**tasks/INDEX.md:** Task index with status table and legend

### Step 4: Confirm Creation

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
1. Run /design-prd to create the project's PRD.md (optional)
2. Run /design to create your first task
3. Or run /design-digest <file> to import tasks from existing document
```

## Error Handling

- **tasks/ already exists:** Ask if user wants to reinitialize
- **design.yaml already exists:** Show current config, ask to update
- **Not in a git repo:** Warn but continue
