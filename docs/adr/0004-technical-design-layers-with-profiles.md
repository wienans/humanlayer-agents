---
status: accepted
---

# Technical Design layers with progressively disclosed profiles

Source: [Define the technical design contract and profiles](https://github.com/wienans/humanlayer-agents/issues/15)

Technical Design is a Design Artifact that owns the approved implementation intent for an Effort, split into System Design, Program Design, and removable Transition Design layers. System Design owns the cross-component architecture and a single current-to-target delta; Program Design owns the in-code shape, carrying SOLID and CUPID as suggested quality guidance (not enforced) and testable design as a depth check; Transition Design owns the migration and cutover path and exists only when an Effort preserves or replaces existing behavior. The design is driven by whole-frontier grilling over a draft synthesized from resolved Wayfinder decisions and Product Design, so settled questions are never re-asked, and approval is implicit in the human starting the next workflow step rather than explicit per-phase sign-off. A language-neutral core plus Embedded, Python, and TypeScript profile lenses guide the record; each profile is an additive lens that composes with the others rather than forking the core. This replaces the HumanLayer TDD two-phase approval with a no-repeat synthesis model and adds the Transition layer for behavior-preserving work.
