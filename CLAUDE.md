# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a personal Claude Code Skills maintenance repository. Each subdirectory contains a standalone skill with its own `SKILL.md` (required) and optional resources (`references/`, `scripts/`, `assets/`).

## Skills in This Repository

| Skill | Command | Description |
|-------|---------|-------------|
| task-splitter | `/task-splitter` | Splits large coding tasks into ordered subtasks for cross-session execution |
| find-task | `/find-task` | Finds next incomplete subtask, formulates implementation plan, assists development |

These two skills work together: **task-splitter** creates the plan, **find-task** picks up where the last session left off.

## Packaging and Validation

Skills are packaged using the skill-creator toolchain at `~/.claude/skills/skill-creator/scripts/`:

```bash
# Validate a skill
python3 ~/.claude/skills/skill-creator/scripts/quick_validate.py <skill-directory>

# Package a skill into .skill file (auto-validates first)
python3 ~/.claude/skills/skill-creator/scripts/package_skill.py <skill-directory>

# Initialize a new skill from template
python3 ~/.claude/skills/skill-creator/scripts/init_skill.py <skill-name> --path <output-directory>
```

Packaged `.skill` files go into `archive/`.

## Key Conventions

- **SKILL.md frontmatter**: YAML `description` values containing colons must be quoted
- **Shared contract between task-splitter and find-task**: find-task locates content in planning files by these section headings: `## Current Status`, `## Core Code`, `Subtask Progress` table. Changing these headings in task-splitter's templates requires syncing find-task's SKILL.md
- **Status values**: `Not Started` / `In Progress` / `Completed`
- **Bilingual docs**: Root README.md is Chinese, README_EN.md is English; skill source files (SKILL.md, templates) are English
