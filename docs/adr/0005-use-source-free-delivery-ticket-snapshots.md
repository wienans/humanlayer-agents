---
status: accepted
---

# Use source-free Delivery Ticket snapshots

Source: [Define implementation tickets and architecture traceability](https://github.com/wienans/humanlayer-agents/issues/7)

Every Effort produces at least one separate Delivery Ticket whose body condenses all implementation-relevant Product and Technical Design into a self-contained snapshot. Delivery Tickets deliberately omit upstream source links, Design Anchors, and persistent coverage matrices: architecture is preserved through complete condensation, generator self-checking, and human approval rather than durable requirement-level traceability. This lets each fresh implementation context work from one authoritative contract without reconstructing design history, at the accepted cost of not being able to map an instruction back to an exact upstream statement later.
