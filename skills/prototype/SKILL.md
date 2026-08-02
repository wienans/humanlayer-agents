---
name: prototype
description: Build throwaway Evidence for one design question. Use when a workflow or user needs to feel out a state model, logic, interaction, or visual direction before choosing it.
---

# Prototype

A prototype is throwaway code that answers one named design question. It produces Evidence; it does not approve intent, mutate Domain Documentation, or become an implementation workflow.

## Choose The Shape

- A business-logic, state-transition, or data-shape question uses [references/logic.md](references/logic.md).
- A visual or interaction question uses [references/ui.md](references/ui.md).

If the question is ambiguous, ask. When the human is unavailable, infer from the surrounding code and state the assumption visibly in the prototype.

## Shared Rules

1. Obtain the human's choice of a dedicated throwaway branch or worktree before editing. Stop if the active workspace could put prototype code on the production branch.
2. Mark the artifact as a prototype and place it near the relevant module or page.
3. Make it trivial to run using the project's existing conventions.
4. Keep state in memory unless persistence itself is the question.
5. Show the relevant state after every action or variant switch.
6. Spend no effort on production abstractions, exhaustive error handling, or automated tests.
7. Present the prototype and wait for the human's verdict.
8. Commit the complete artifact only to the approved throwaway branch. Publish that branch to the configured remote when one exists; otherwise retain the local branch and record the repository path, branch name, and full commit SHA as the durable pointer.
9. Use the Tracker Adapter's semantic **Record Prototype Evidence** operation on the invoking decision record with the question, verdict, and pointer.
10. Leave the production branch free of prototype artifacts. Production receives a separately implemented and tested version of the accepted decision.

Completion requires the human's verdict and a durable Evidence pointer. Return the answer to the invoking decision-producing workflow, which may invoke `domain-modeling` if the accepted decision has durable Domain Impact. Do not advance the workflow or implement production code.
