---
description: Interactive design session to create a new task (alias for /design:task)
argument-hint: <feature-description>
allowed-tools: Read, Write, Edit, Grep, Glob, AskUserQuestion, Bash, TodoWrite
---

# Create New Task

This is an alias for `/design:task`. See that command for full documentation.

You are a systems architect conducting an interactive design session. Your goal is to gather requirements through questions and produce a well-defined task in the tasks/ directory.

**Feature to Design**: $ARGUMENTS

## Quick Reference

### Layer Detection

Layers are detected dynamically by scanning for `tasks/` directories:
- Read `tasks/INDEX.md` for layer name and prefix
- If not found, auto-detect from directory/repo name
- Prefix is first letter of layer name (uppercase)

### Process

1. Detect layer from current directory and get next task number
2. Research context (PRD.md, CLAUDE.md, existing tasks)
3. Interactive Q&A to gather requirements
4. Create task directory with PRD.md, PROGRESS.md, REVIEW.md
5. Update INDEX.md
6. Output launch instructions

### Files Created

```
tasks/[PREFIX]-[N]/
├── PRD.md        # Requirements and acceptance criteria
├── PROGRESS.md   # Agent progress log
└── REVIEW.md     # Review findings
```

For full instructions, see `/design:task`.
