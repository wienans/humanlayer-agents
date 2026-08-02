---
name: domain-modeling
description: Maintain Domain Documentation at decision-producing events. Use when canonical terminology, bounded-context relationships, or a qualifying architectural decision is resolved; other phases invoke it rather than editing Domain Documentation themselves.
---

# Domain Modeling

Domain Modeling is the sole writing primitive for Domain Documentation. Invoke it when a decision-producing workflow resolves durable language, context relationships, or architectural rationale. Research, prototyping as Evidence, implementation, and review consume Domain Documentation without changing it.

## Locate The Model

Read `CONTEXT-MAP.md` when present and follow it to the relevant context. Otherwise use root `CONTEXT.md`. Read applicable ADRs before changing either. Create files lazily only when there is resolved content to record.

## Resolve And Record

1. Challenge terms that conflict with existing canonical language.
2. Sharpen vague or overloaded language with concrete edge-case scenarios.
3. Check the code when a claim about current behavior affects the definition.
4. Write each resolved term immediately using [references/context-format.md](references/context-format.md).
5. Offer an ADR only when all three qualification tests in [references/adr-format.md](references/adr-format.md) pass and the human approves the choice.
6. Return links to changed Domain Documentation so the owning decision record can state its Domain Impact.

`CONTEXT.md` is a glossary, not a task specification. Keep product requirements and work-specific product, technical, transition, and implementation intent in their owning records.

Completion requires every newly resolved durable term to have one canonical definition, every qualifying approved architectural choice to have one ADR, and the caller to receive either the changed links or an explicit statement that no durable Domain Impact was found. Stop and return control to the invoking workflow.
