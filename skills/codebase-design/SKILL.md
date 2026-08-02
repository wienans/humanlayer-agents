---
name: codebase-design
description: Design deep modules and testing seams. Use when a workflow or user needs to place an interface, simplify caller knowledge, improve locality, compare module shapes, or make code testable through public behavior.
---

# Codebase Design

Design **deep modules**: substantial behavior behind a small interface at a clean seam. This is shared design guidance, not a workflow owner. Return designs and trade-offs to the invoking concern; do not approve them or modify Domain Documentation directly.

## Vocabulary

**Module**: anything with one interface and an implementation, at any scale.

**Interface**: everything a caller must know, including signatures, invariants, ordering, errors, configuration, and performance characteristics.

**Implementation**: behavior hidden inside a module.

**Depth**: leverage at the interface; how much behavior callers can use per unit of interface they must learn.

**Seam**: a place where behavior can vary without editing the caller.

**Adapter**: a concrete implementation satisfying an interface at a seam.

**Leverage**: capability gained by callers from one interface.

**Locality**: concentration of knowledge, change, bugs, and verification in one place.

## Design Tests

- Reduce methods, parameters, required ordering, and exposed configuration while preserving capability.
- Apply the deletion test: deleting a useful deep module should spread its hidden complexity back across callers.
- Make callers and tests use the same interface.
- Accept dependencies rather than constructing them inside behavior.
- Introduce a seam only when at least two adapters are justified, commonly production and test.
- Keep internal test seams out of the external interface.

For dependency-specific seam placement, read [references/deepening.md](references/deepening.md). When the interface choice is consequential or the first design looks obvious, use [references/design-it-twice.md](references/design-it-twice.md).

Completion requires an explicit interface, hidden responsibilities, seam and adapter strategy, testing surface, and trade-offs. If a human-approved design changes durable vocabulary or qualifies for an ADR, invoke `domain-modeling`; otherwise return it to the owning design workflow unchanged.
