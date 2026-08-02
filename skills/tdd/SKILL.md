---
name: tdd
description: Drive implementation through vertical red-green slices at an approved testing seam. Use when a workflow or user requests test-first work, red-green-refactor, behavioral tests, or integration tests.
---

# Test-Driven Development

TDD is a tight red-green loop through a public testing seam. It is execution guidance, not a workflow owner: consume approved intent and Domain Documentation, change neither, and return verification to the invoking implementation workflow.

Run code-changing cycles only when the owning implementation workflow has invoked this primitive. Otherwise return seam and test-strategy guidance without editing code.

## Establish The Seam

Use the Testing Seam already approved by the Delivery Ticket or design. When it is absent or cannot exercise the Desired End State, stop and report the missing obligation to the owning implementation workflow; TDD does not choose or approve a seam during execution. Tests and callers should cross the same seam.

Read [references/tests.md](references/tests.md) for test quality and [references/mocking.md](references/mocking.md) before introducing a test double.

## Red-Green Slices

For each observable behavior:

1. **Red**: write one behavioral test with expected values from an independent source, run it, and confirm it fails for the intended reason.
2. **Green**: add only enough production behavior to pass that test, then rerun it.
3. **Check**: run the focused surrounding tests before starting the next slice.
4. **Repeat**: let the completed slice inform the next test rather than writing a horizontal batch in advance.

Keep refactoring separate from proving new behavior. Refactor only while green and without changing the approved interface or Desired End State.

If a change cannot produce a meaningful behavioral test, record the concrete reason and the alternative runnable verification instead of adding a ceremonial test. The invoking implementation workflow decides whether that exception satisfies the Delivery Ticket.

Completion requires every implemented behavior to have a witnessed red state and green state, or one documented exception with runnable verification. Return focused command results and changed behavior to the caller; do not commit, change tracker state, invoke review, or advance the workflow.
