---
description: Interactively create the global project PRD.md
---

# Create Project PRD (Product Requirements Document)

Use interactive Q&A to gather project requirements and generate the global PRD.md at the repository root.

## Instructions

### Step 1: Check for Existing PRD

If PRD.md exists, ask user if they want to update/replace or cancel.

### Step 2: Interactive Requirements Gathering

Ask 2-4 questions per round:

**Round 1 - Vision & Purpose:**
- What is the name of this project?
- In one sentence, what does this project do?
- What problem does it solve?
- Who are the target users?

**Round 2 - Scope & Goals:**
- What are the 3-5 key features?
- What is explicitly OUT of scope?
- What are the success metrics?

**Round 3 - Technical Context:**
- What are the key technical constraints?
- What external systems does this integrate with?
- What are the security requirements?

**Round 4 - Development Approach:**
- What is the repository structure?
- What are the key dependencies?
- What testing requirements exist?

### Step 3: Generate PRD.md

Create PRD.md with:
- Vision and Problem Statement
- Target Users
- Goals and Success Metrics
- Non-Goals
- Key Features
- Technical Requirements
- Development Approach
- Milestones

### Step 4: Confirm and Save

Show summary and confirm before writing.

### Step 5: Suggest Next Steps

```
PRD.md created successfully.

Would you like to initialize the task management structure?
Run: /design-init
```
