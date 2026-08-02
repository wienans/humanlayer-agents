# Architecture-First Engineering Workflows

The independent OpenCode distribution lives directly under [`skills/`](skills/) and [`agents/`](agents/). Existing skills under `.opencode/`, `.agents/`, and `matt-skills/` are unchanged source material, not runtime dependencies of the independent suite.

The delivered RPI Evidence entry path is:

```mermaid
flowchart TD
    A[research-questions] -->|explicit human invocation| B[research]
```

`research-questions` creates a neutral Research packet and stops. Only `research` authorizes the isolated `research-worker`, publishes canonical Evidence, names `product-design` as the downstream suite phase, and stops. The downstream skill is delivered by a separate slice.

Shared model-invoked primitives are `grilling`, `domain-modeling`, `prototype`, `codebase-design`, and `tdd`.

## Source Workflows

Each step names the skill to run. Complete one skill before starting the next.

[Guide Skills-Workflosw](https://docs.humanlayer.com/guide/skills-workflows)
[Reference Skills-Workflosw](https://docs.humanlayer.com/reference/skills-workflows)

## Design Discussion Workflow

```mermaid
flowchart TD
    A[create-research-questions] --> B[create-research]
    B --> C[create-design-discussion]
    C --> D[create-structure-outline]
    D --> E[setup-worktree]
    E --> F[implement-outline]
    F --> G[describe-pr]
```

## PRD and TDD Workflow

```mermaid
flowchart TD
    A[create-research-questions] --> B[create-research]
    B --> C[create-prd]
    C --> D[create-tdd]
    D --> E[create-structure-outline]
    E --> F[setup-worktree]
    F --> G[implement-outline]
    G --> H[describe-pr]
```
