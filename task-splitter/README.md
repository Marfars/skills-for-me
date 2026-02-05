# Task Splitter

A Claude Code skill that splits large coding tasks into ordered subtasks for cross-session execution.

## What It Does

When working on a complex feature that spans multiple modules, frontend/backend, or requires extensive implementation, this skill decomposes it into manageable subtasks — each designed to be completed in a single session.

## Usage

After discussing requirements and confirming a solution with Claude, invoke:

```
/task-splitter
```

## Output

The skill generates a structured planning directory in your project:

```
${projectRoot}/planning/${task_core}/
├── task_overview.md              # Overall task summary, progress tracking, Mermaid diagram
├── 01_database_schema.md         # Subtask 1
├── 02_api_endpoints.md           # Subtask 2
└── ...
```

### task_overview.md

Contains the full picture of the task:
- Overview and overall objectives
- Subtask progress table (Not Started / In Progress / Completed)
- Development order with rationale
- Comprehensive Mermaid diagram showing business flow, subtask dependencies, and their mapping
- Tech stack and notes

### Subtask Files

Each subtask file includes:
- Task overview and current status
- Upstream dependencies and downstream impact
- Business entry/exit points
- High-level design (architecture, interfaces, module breakdown)
- Core code (pseudocode initially, updated to actual code after implementation)
- Implementation details
- Acceptance criteria

## Skill Structure

```
task-splitter/
├── SKILL.md                                # Core instructions
└── references/
    ├── task_overview_template.md            # Template for task overview
    └── subtask_template.md                  # Template for subtask files
```

## Related Skills

- [find-task](../find-task/) — Find the next incomplete subtask and continue development in a new session
