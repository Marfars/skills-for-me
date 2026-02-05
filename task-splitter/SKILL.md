---
name: task-splitter
description: "Split large coding tasks into ordered subtasks for cross-session execution. After discussing requirements and confirming the solution with Claude, invoke this skill to decompose the task into ordered subtask files under the project's planning/ directory. Use when: (1) user invokes /task-splitter command (2) a complex feature needs to be split into multiple development phases."
---

# Task Splitter

Split a confirmed large coding task from the current conversation into ordered subtask documents for cross-session execution.

## Workflow

### Step 1: Analyze Conversation Context

Extract from the current conversation:
- User requirements and business objectives
- Confirmed technical solution and architectural decisions
- Involved modules, classes, and interfaces

### Step 2: Determine Task Core Name

- Generate a short English identifier (snake_case), e.g. `user_authentication`, `order_management`
- Confirm the name with the user

### Step 3: Split into Subtasks

- Determine development order based on business dependencies
- Each subtask should be an independently deliverable functional unit
- Consider functional modules, frontend/backend separation, business flow, etc.

### Step 4: Generate Files

Determine the project root path (prefer `git rev-parse --show-toplevel`, fallback to current working directory), then:

1. Create directory `${projectRootPath}/planning/${task_core}/`
2. Read [references/task_overview_template.md](references/task_overview_template.md), generate `task_overview.md`
3. For each subtask, read [references/subtask_template.md](references/subtask_template.md), generate `{two-digit-order}_{english_summary_snake_case}.md`

**Idempotency**: If the target directory already exists, ask the user whether to overwrite or append.

### Step 5: Present Results

Output the list of generated files with a brief explanation of the development order and dependencies.

## Output Specifications

### File Naming

- Task overview: `task_overview.md`
- Subtask files: `{two-digit-order}_{summary}.md` (e.g. `01_database_schema.md`, `02_api_endpoints.md`)

### Status Values

- **Not Started**
- **In Progress**
- **Completed**

### Mermaid Diagram

Draw a single comprehensive Mermaid diagram in task_overview.md that includes:
- Business flow (solid arrows `-->`)
- Subtask dependencies (dashed arrows `-.->`)
- Mapping between business nodes and subtasks (dotted lines `-.-`)

## Template Files

Read the following templates when generating files:

- Task overview template: [references/task_overview_template.md](references/task_overview_template.md)
- Subtask template: [references/subtask_template.md](references/subtask_template.md)
