# Find Task

A Claude Code skill that finds the next incomplete subtask from the planning directory, formulates an implementation plan, and assists with development.

## What It Does

When starting a new session on a previously split task, this skill automatically locates the next subtask to work on, reads the existing codebase for context, and presents a concrete implementation plan. After implementation, it helps keep planning documents up to date.

## Usage

```
/find-task
```

## Workflow

### 1. Find Next Task

- Scans `${projectRoot}/planning/` for task directories
- Reads `task_overview.md` to check subtask progress
- Prioritizes "In Progress" tasks (unfinished from last session), then picks the first "Not Started" task
- If multiple task groups exist, lets you choose

### 2. Formulate Implementation Plan

- Reads the target subtask file and upstream dependencies
- Scans existing project code for context
- Generates a step-by-step implementation plan
- Asks clarifying questions if needed

### 3. Assist Implementation

Helps write code according to the implementation plan.

### 4. Update Documents

After implementation, proactively asks whether to update:
- Subtask status → "Completed" or "In Progress"
- Core code section → replace pseudocode with actual implementation
- Task overview progress table → sync status

## Edge Cases

- **No planning directory** → suggests using `/task-splitter` first
- **All tasks completed** → notifies and suggests overall acceptance review
- **Upstream dependencies incomplete** → warns and asks for confirmation before proceeding

## Skill Structure

```
find-task/
└── SKILL.md                    # Core instructions
```

## Related Skills

- [task-splitter](../task-splitter/) — Split a large task into ordered subtasks
