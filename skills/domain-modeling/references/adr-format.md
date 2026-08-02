# ADR Format

Create an ADR only when the approved choice is all three:

1. **Hard to reverse**: changing it later has meaningful cost.
2. **Surprising without context**: a future reader would reasonably question it.
3. **A real trade-off**: credible alternatives existed and were rejected for stated reasons.

ADRs live in the applicable `docs/adr/` directory and use the next sequential `NNNN-slug.md` filename.

```markdown
---
status: accepted
---

# {Short decision title}

{One to three sentences stating the context, approved choice, and rationale.}
```

Add considered options or consequences only when they preserve non-obvious rationale. Approval and ADR creation are one event; do not write an ADR for an unapproved proposal.
