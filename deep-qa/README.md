# Deep QA

A Claude Code skill that forces critical thinking and iterative questioning before providing any coding solution.

## What It Does

When working on any coding task, this skill reduces the understanding gap between you and Claude by combining targeted questions with codebase exploration. Instead of guessing and providing potentially inaccurate solutions, Claude iteratively asks questions and explores the codebase until all ambiguities are resolved.

## Usage

The skill triggers automatically when discussing implementation plans, requirements, or bug fixes. You can also invoke it manually:

```
/deep-qa
```

## Workflow

### 1. Initial Assessment

- Reads your request and identifies unknowns
- Explores the codebase for relevant context (files, patterns, dependencies)

### 2. Iterative Question-Explore Loop

- Asks targeted questions based on codebase findings and your requirements
- Explores more code as your answers reveal new areas to investigate
- Repeats until no understanding gaps remain

Question dimensions include: business intent, scope boundaries, technical context, edge cases, acceptance criteria, and ambiguity resolution.

### 3. Completion Signal

Once confident all gaps are resolved, outputs:

> 我已获得所有需要的信息 🐱

Then presents the solution adapted to the task type.

## Boundary Cases

- **Trivial tasks** → one quick confirmation, no forced multi-round questioning
- **User wants to stop** → respects immediately, states remaining assumptions

## Skill Structure

```
deep-qa/
├── SKILL.md                    # Core instructions
└── README.md                   # This file
```

## Related Skills

- [task-splitter](../task-splitter/) — Split a confirmed task into ordered subtasks (use after deep-qa has clarified requirements)
- [find-task](../find-task/) — Find the next incomplete subtask and continue development
