---
name: deep-qa
description: "Force critical thinking and iterative questioning before providing any coding solution. Reduce the understanding gap between user and Claude through targeted questions combined with codebase exploration. Automatically triggers when: (1) user invokes /deep-qa (2) discussing implementation plans, requirements, or solution design (3) debugging or fixing bugs (4) making architecture decisions (5) any coding task where context is not fully clear. Use BEFORE /task-splitter to ensure requirements are fully understood."
---

# Deep QA

Iteratively question the user and explore the codebase to eliminate understanding gaps before providing any solution.

## Core Principle

Never guess. Never assume. When uncertain about any aspect of the task, **ask** the user or **explore** the codebase before proceeding. The cost of one more question is always lower than the cost of a wrong solution.

## Workflow

### Step 1: Initial Assessment

Upon receiving a coding task:

1. Read the user's request carefully
2. Identify what is known vs. unknown
3. Explore the codebase proactively — scan relevant files, directory structure, existing patterns, dependencies, and conventions
4. Formulate the first round of questions based on both the request and codebase findings

### Step 2: Iterative Question-Explore Loop

Repeat until no understanding gaps remain:

1. **Ask** targeted questions to the user — batch related questions, focus on what would most change the solution direction
2. **Explore** the codebase in parallel — read files, trace call paths, check configs, examine tests
3. **Synthesize** the user's answers with codebase findings
4. **Re-evaluate** remaining gaps — if any exist, prepare the next round

Question dimensions (select relevant ones per task):

- **Business intent**: What problem does this solve? What does success look like?
- **Scope boundaries**: What is explicitly out of scope? What are the constraints?
- **Technical context**: What existing code/patterns must be respected? What dependencies exist?
- **Edge cases**: What happens when inputs are invalid, services fail, or data is missing?
- **Acceptance criteria**: How will correctness be verified? What tests are expected?
- **Non-functional requirements**: Performance targets? Security concerns? Compatibility needs?
- **Ambiguity resolution**: When requirements conflict or are vague, surface them explicitly

Guidelines for each round:

- Lead with codebase findings: "I found X in the codebase, which suggests Y. Is that correct?"
- Prioritize questions that would most change the solution direction
- Group related questions; do not scatter unrelated ones
- Show what you have learned so far to build shared understanding
- Quality over quantity — one precise question beats five vague ones

### Step 3: Completion Signal

When confident that all understanding gaps are resolved, output:

```
我已获得所有需要的信息 🐱
```

Then present the solution, adapted to the task type:

- **Implementation plan** → structured approach with steps
- **Bug fix** → root cause analysis and fix
- **Architecture decision** → options with trade-offs and recommendation
- **Feature request** → design and implementation outline

For complex tasks, suggest using `/task-splitter` to decompose into ordered subtasks.

## Boundary Conditions

**Trivial tasks** (e.g., rename a variable, add a log line):
- One quick confirmation round is sufficient
- If the task is unambiguous after reading the code, proceed directly with the completion signal

**User signals to stop questioning** (e.g., "just do it", "enough questions"):
- Respect the user's decision immediately
- State remaining assumptions explicitly before proceeding
- Mark unresolved gaps as assumptions in the output

## Anti-Patterns

- **Guessing**: Filling unknowns with plausible-sounding assumptions
- **Premature solution**: Jumping to implementation before understanding the problem
- **Interrogation fatigue**: Asking too many low-value questions in a single round
- **Echo questioning**: Rephrasing what the user already said as a question
- **Ignoring codebase signals**: Asking the user questions that the codebase already answers
