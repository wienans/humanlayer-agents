# Product Design Template

Use this as a concern checklist, not a demand for equal-length sections. Product intent on an Effort root may compress the same concerns; a separate Design Artifact should make them independently skimmable.

```markdown
# <Outcome-oriented Product Design title>

## <Takeaway header stating the problem>

<Who experiences what problem today, why it matters, and the relevant current behavior. Keep implementation detail out.>

## <Takeaway header stating what success changes>

<Observable outcomes and measures. State explicitly when no meaningful measure exists.>

## <Takeaway header naming the actors and end-to-end flow>

<Actors, goals, entry conditions, main flow, and meaningful alternate flows. Add a Mermaid flow or state diagram when it communicates the behavior faster than prose.>

## <Takeaway header summarizing the behavioral contract>

### <Product states and transitions>

<Observable states, transition triggers, and what each actor sees.>

### <Interactions and rules>

<Capabilities, decisions, validation behavior, permissions as users experience them, and other product rules.>

### <Edge behavior is explicit>

<Empty, partial, repeated, concurrent, unavailable, failed, cancelled, expired, and recovery behavior that is relevant to this Effort. Include only applicable cases.>

## Resolved choices preserve their alternatives and rationale

- [<Decision Ticket title>](link) - <chosen path, one-line product rationale, and relevant rejected alternative>
- <For an RPI choice without a Decision Ticket: chosen path, one-line product rationale, and relevant rejected alternative>

## Out of scope keeps the contract bounded

- <Excluded behavior or outcome and, when useful, why it is excluded>

## Design Anchors point to their authoritative owners

### Evidence

- [<Evidence record or prototype verdict>](link) - <fact or limit this contract relies on>

### Domain Documentation

- [<canonical context or ADR title>](link) - <terminology or durable rationale used here>

### Prototype visuals

- [<winning visual and verdict>](throwaway-branch-link) - <interaction or visual choice it demonstrates>

## Deferred to Technical Design

- <Only technical questions encountered while defining product behavior; omit this section when empty.>

## Domain Impact

<Links to changed Domain Documentation, or `No durable domain impact.`>
```

For concise Product intent on the Effort root, preserve at minimum the problem, success, actors/behavior, exclusions, Design Anchors, and `### Domain Impact` nested inside `## Product intent`. Add the remaining structure when omitting it would make approved behavior ambiguous.
