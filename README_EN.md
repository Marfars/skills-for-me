# skills-for-me

[中文](README.md)

A personal repository for maintaining Claude Code Skills.

## Introduction

This repository centralizes the development and maintenance of personal [Claude Code](https://docs.anthropic.com/en/docs/claude-code) Skills.

A Claude Code Skill is a modular extension package that enhances Claude's capabilities by providing specialized knowledge, workflows, and tool integrations. Each Skill can be triggered via commands in Claude Code.

## Skill Catalog

| Skill | Command | Description |
|-------|---------|-------------|
| [deep-qa](deep-qa/) | `/deep-qa` | Force critical thinking and iterative questioning before providing solutions |
| [task-splitter](task-splitter/) | `/task-splitter` | Split large coding tasks into ordered subtasks for cross-session execution |
| [find-task](find-task/) | `/find-task` | Find the next incomplete subtask, formulate an implementation plan, and assist with development |

## Repository Structure

```
skills-for-me/
├── archive/                        # Release artifacts (.skill packages)
│   ├── deep-qa.skill
│   ├── find-task.skill
│   └── task-splitter.skill
├── deep-qa/                        # deep-qa skill source
│   ├── SKILL.md
│   └── README.md
├── find-task/                      # find-task skill source
│   ├── SKILL.md
│   └── README.md
└── task-splitter/                  # task-splitter skill source
    ├── SKILL.md
    ├── README.md
    └── references/
        ├── task_overview_template.md
        └── subtask_template.md
```

## Installation

1. Get the corresponding `.skill` file from the `archive/` directory
2. Unzip the file:
   ```bash
   unzip task-splitter.skill
   ```
3. Move the extracted directory to Claude Code's skills directory:
   ```bash
   mv task-splitter ~/.claude/skills/
   ```
4. Restart Claude Code to take effect

## Usage

### deep-qa

When discussing implementation plans, requirements, or bug fixes, Claude automatically enters deep questioning mode — iteratively asking questions and exploring the codebase to fully understand requirements before providing solutions. You can also manually trigger it by typing `/deep-qa`.

See [deep-qa/README.md](deep-qa/README.md) for details.

### task-splitter

After discussing requirements and confirming a solution with Claude, type `/task-splitter` to split the task into multiple subtask files under the project's `planning/` directory.

See [task-splitter/README.md](task-splitter/README.md) for details.

### find-task

In a new session, type `/find-task` and Claude will automatically find the next incomplete subtask, formulate an implementation plan based on existing code, and assist with development.

See [find-task/README.md](find-task/README.md) for details.

## Adding New Skills

1. Create a new skill directory at the repository root containing a `SKILL.md` file
2. Add resource directories as needed: `references/`, `scripts/`, `assets/`
3. Write a `README.md` documentation file
4. After packaging, store the `.skill` file in the `archive/` directory
