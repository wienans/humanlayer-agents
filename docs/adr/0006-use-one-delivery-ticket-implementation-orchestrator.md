---
status: accepted
---

# Use one Delivery Ticket implementation orchestrator

Source: [Define implementation orchestration and human gates](https://github.com/wienans/humanlayer-agents/issues/8)

One `implement` workflow owns code-changing execution for a specific claimed Delivery Ticket. It delegates test-first implementation to a fresh Delivery Ticket worker, independently completes broad verification, pauses only for required manual verification or consequential contract mismatches, records verification once, and creates and pushes one cohesive commit per run. Workspace setup remains an optional human-controlled step, while PR description and code review remain separate non-implementation workflows; review findings return to `implement` only after the human selects them. This preserves one execution authority without coupling implementation to workspace policy or collapsing implementation, explanation, and review into one context.
