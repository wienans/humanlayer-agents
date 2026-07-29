# RPI Workflows

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
