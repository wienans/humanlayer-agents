# Domain Context Format

## Single Context

Use one root `CONTEXT.md`:

```markdown
# {Context Name}

{One or two sentences describing the context.}

## Language

**Order**:
The customer's committed request for fulfillment.
_Avoid_: Purchase, transaction
```

Definitions state what a domain-specific concept is in one or two sentences. Pick one canonical term and list misleading synonyms under `_Avoid_`. General programming terms and implementation details do not belong.

## Multiple Contexts

When root `CONTEXT-MAP.md` exists, it indexes context-specific `CONTEXT.md` files and records only the durable semantic and technical relationships between contexts:

```markdown
# Context Map

## Contexts

- [Ordering](./src/ordering/CONTEXT.md) - receives and tracks orders
- [Billing](./src/billing/CONTEXT.md) - invoices fulfilled orders

## Relationships

- **Ordering -> Billing**: Ordering emits `OrderFulfilled`; Billing consumes it.
```

Infer the relevant context from the decision. Ask when ownership is genuinely ambiguous.
