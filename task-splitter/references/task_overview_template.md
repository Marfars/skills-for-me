# {Task Name}

## Overview

{Brief description of the overall task, including background, purpose, and scope. 1-3 paragraphs.}

## Overall Objectives

- {Objective 1}
- {Objective 2}
- {Objective 3}

## Subtask Progress

| # | Subtask | Filename | Status | Description |
|---|---------|----------|--------|-------------|
| 01 | {Subtask name} | {filename}.md | Not Started | {Brief description} |
| 02 | {Subtask name} | {filename}.md | Not Started | {Brief description} |

## Development Order

Develop in the following order. Later tasks may depend on outputs from earlier tasks:

1. **{Subtask 1}** — {Reason for this ordering}
2. **{Subtask 2}** — {Reason for this ordering}

## Business Flow & Subtask Dependencies

```mermaid
graph TD
    subgraph Business Flow
        B1["{Business Node 1}"] --> B2["{Business Node 2}"]
        B2 --> B3["{Business Node 3}"]
    end

    subgraph Subtask Dependencies
        T01["01_{Subtask 1}"] -.-> T02["02_{Subtask 2}"]
        T02 -.-> T03["03_{Subtask 3}"]
    end

    B1 -.- T01
    B2 -.- T02
    B3 -.- T03
```

> Legend: Solid arrows = business flow direction, Dashed arrows = subtask dependencies, Dotted lines = mapping between business nodes and subtasks.

## Tech Stack

- {Tech stack information, extracted from conversation context}

## Notes

{Other important notes, such as constraints, risks, or considerations}
