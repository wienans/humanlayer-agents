# Architecture-First Engineering Workflows

The independent OpenCode distribution lives directly under [`skills/`](skills/). Existing skills under `.opencode/`, `.agents/`, and `matt-skills/` are unchanged source material, not runtime dependencies of the independent suite.

The delivered RPI path through Product Design is:

```mermaid
flowchart TD
    A[research-questions] -->|explicit human invocation| B[research]
    B -->|explicit human invocation| C[product-design]
    D[wayfinder] -->|sufficiently resolved; explicit human invocation| C
```

`research-questions` creates a neutral Research packet and stops. Only `research` authorizes investigation; it publishes canonical Evidence and stops. `product-design` then converges that Evidence or a sufficiently resolved Wayfinder Decision Map into the approved problem-and-behavior contract and stops before `technical-design`.

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
