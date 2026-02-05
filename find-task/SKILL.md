---
name: find-task
description: "Find the next incomplete subtask in the project's planning/ directory, formulate an implementation plan based on existing code, and assist with development. Use when: (1) user invokes /find-task (2) starting a new session to continue unfinished tasks (3) needing to update planning documents after completing a subtask."
---

# Find Task

Find the next incomplete subtask in the planning/ directory, formulate an implementation plan, and assist with development.

## File Structure Convention

planning/ directory structure:

```
${projectRootPath}/planning/${task_core}/
├── task_overview.md                    # Task overview
├── 01_${summary}.md                    # Subtask files
├── 02_${summary}.md
└── ...
```

Subtask status values: **Not Started** / **In Progress** / **Completed**

Key section headings (used for locating and updating content):
- `## Current Status` — Status field in subtask files
- `## Core Code` — Code section in subtask files
- `Subtask Progress` table — Progress table in task_overview.md

## Workflow

### Phase 1: Find Task

1. Determine project root path (prefer `git rev-parse --show-toplevel`, fallback to current working directory)
2. Scan all subdirectories under `${projectRootPath}/planning/`
3. Read the Subtask Progress table in each subdirectory's `task_overview.md`
4. Determine the next target subtask:
   - **Priority**: Subtasks with "In Progress" status (unfinished work from previous session)
   - **Then**: First subtask with "Not Started" status, in order
5. If multiple task_core directories exist, list all and let the user choose
6. If all subtasks are completed, notify the user and suggest overall acceptance review

**Edge cases**:
- planning/ directory does not exist → prompt user to use `/task-splitter` to create a task plan
- Target subtask has incomplete upstream dependencies → warn user and confirm whether to proceed

### Phase 2: Formulate Implementation Plan

1. Read the target subtask file (high-level design, implementation details, acceptance criteria, etc.)
2. Read upstream subtask files (understand completed dependency outputs)
3. Scan existing relevant code files in the project
4. Synthesize the above to generate a concrete implementation plan
5. Ask the user for clarification on any ambiguities

Display format:

```
Task Group: {task_core}
Current Task: {order} - {subtask name}
Status: {current status} → In Progress
Upstream Dependencies: {status description}

Implementation Plan:
1. {Step 1}
2. {Step 2}
...

Proceed with implementation?
```

### Phase 3: Assist Implementation

Assist the user in writing code according to the implementation plan.

### Phase 4: Update Documents

After code implementation is complete, **proactively ask** the user whether to update the following:

1. **Subtask file** `## Current Status`
   - Update to "Completed" (or "In Progress" if partially done)

2. **Subtask file** `## Core Code`
   - Replace pseudocode with the actual implementation code

3. **task_overview.md** Subtask Progress table
   - Update the status column for the corresponding subtask

Execute updates only after user confirmation.
