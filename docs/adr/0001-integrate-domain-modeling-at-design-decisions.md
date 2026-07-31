---
status: accepted
---

# Integrate domain modeling at design decisions

Source: [Define domain modeling and ADR integration](https://github.com/wienans/humanlayer-agents/issues/4)

Decision-producing workflows explicitly invoke Domain Modeling when design choices are resolved; factual and execution phases only consume Domain Documentation, while review may suggest but not write glossary entries. Domain Documentation owns canonical language, context relationships, and qualifying architectural rationale, while Tracker Design Artifacts own work-specific product, technical, and transition design. This split keeps durable codebase context current without duplicating task design or imposing domain-document ceremony on every phase.
