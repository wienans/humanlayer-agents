---
name: wayfinder
description: Explicitly chart or advance uncertain work of any size as a tracker-backed Decision Map until it is ready for Product Design.
disable-model-invocation: true
---

An uncertain effort has arrived: the way from here to the **destination** isn't visible yet. Wayfinding is about finding that way, not charging at the destination. This skill charts the way as a tracker-backed **Decision Map**, then works its **Decision Tickets** — investigations or choices, not slices of a build to execute — one at a time until the route is clear. Uncertainty and decision structure determine its use; task size does not.

The destination varies per Effort, and naming it is the first act of charting — it shapes every Decision Ticket. It states the desired outcome whose problem and behavior `product-design` will specify once the consequential decisions are resolved.

## Plan, don't do

Wayfinder is **planning**: each Decision Ticket resolves an investigation or choice, and the Decision Map is ready to hand off when nothing consequential remains unresolved. Produce decisions, Evidence pointers, and qualifying Domain Documentation — not production deliverables. The pull to implement is the signal that the work has reached the edge of this phase.

## Refer by name

Every Decision Map and Decision Ticket is a tracker record with a **name** — its title. In everything the human reads — narration, the map's Decisions-so-far — refer to it by that name, never by a bare id, number, or slug. A wall of `#42, #43, #44` is illegible; names read at a glance. The id and URL don't vanish — a name wraps its link — but they ride _inside_ the name, never stand in for it.

## The Decision Map

The Decision Map is one tracker record for the Effort. Its Decision Tickets are child records whose semantic roles and dependencies expose the current frontier.

The map is an **index**, not a store. It lists the decisions made and points at the tickets that hold their detail; a decision lives in exactly one place — its ticket — so the map never restates it, only gists it and links.

Read `AGENTS.md` and follow its context pointer to the configured **Tracker Adapter**. Use the adapter's semantic operations to find or create the Decision Map, classify and create child Decision Tickets, wire blocking edges, query the frontier, claim work, resolve records, and annotate history. The adapter owns how those operations are represented.

Perform every Decision Map body change through the Tracker Adapter's serialized map-update operation. Reload the current body after acquiring the update, merge only this session's change without dropping other entries, then verify the change before releasing the update.

### The map body

The whole map at low resolution, loaded once per session. Open Decision Tickets are **not** listed — they are child records found by the Tracker Adapter's frontier query.

```markdown
## Destination

<what reaching the end of this map looks like — the spec, decision, or change this effort is finding its way to. One or two lines; every session orients to it before choosing a ticket.>

## Notes

<domain; skills every session should consult; standing preferences for this effort>

## Decisions so far

<!-- the index — one line per closed ticket: enough to judge relevance, then zoom the link for the detail the ticket holds -->

- [<closed ticket title>](link) — <one-line gist of the answer>

## Not yet specified

<!-- see "Fog of war": in-scope fog you can't ticket yet; graduates as the frontier advances -->

## Out of scope

<!-- see "Out of scope": work ruled beyond the destination; closed, never graduates -->
```

### Decision Tickets

Each Decision Ticket is a child tracker record of the Decision Map, sized to one agent session. A non-Research Decision Ticket's body is the question:

```markdown
## Question

<the decision or investigation this ticket resolves>
```

Classify each Decision Ticket through the Tracker Adapter as one of the semantic roles `Research`, `Prototype`, `Grilling`, or `Task` (see [Decision Ticket Types](#decision-ticket-types)). A Research Decision Ticket instead uses the neutral packet returned by `research-questions` as its body.

A Wayfinder session **claims** a Decision Ticket through the Tracker Adapter before resolving it, so concurrent sessions skip it. Open, unclaimed records are candidates for the frontier.

Wire only genuine prerequisites with the Tracker Adapter's blocking operation. A Decision Ticket is **unblocked** when every blocker is closed; the **frontier** is the open, unblocked, unclaimed children — the edge of the known. Research blocks only the Decision Tickets that consume its Evidence, so unrelated frontier work stays available.

The answer isn't part of the body — it is recorded on resolution (see [Work Through The Map](#work-through-the-map)). Assets created while resolving a Decision Ticket are linked from its tracker record, not pasted in.

## Decision Ticket Types

Every Decision Ticket is either **HITL** — human in the loop, worked _with_ a human who speaks for themselves — or **AFK**, driven by the agent alone. A HITL Decision Ticket only resolves through that live exchange; the agent never stands in for the human's side of it.

- **Research** (AFK, separately authorized): A neutral current-state investigation whose Evidence is needed before a decision can be made. Delegate packet creation to `research-questions` in a fresh isolated subagent, create the scoped Research Decision Ticket, and stop for the human to invoke `research` with that record. Wayfinder never starts or performs Research.
- **Prototype** (HITL): Raise the fidelity of the discussion by creating cheap, rough Evidence through `prototype` when "how should it look" or "how should it behave" is the key question. Keep the artifact on its throwaway branch, link it from the Decision Ticket, and leave production code unchanged during Wayfinder.
- **Grilling** (HITL): Conversation through `grilling`. This is the default when the unknown requires human judgment rather than factual Evidence.
- **Task** (HITL or AFK): Manual work that must happen before a _decision_ can be made — nothing to decide, prototype, or research, but the discussion is blocked until it's done. Signing up for a service so its API can be judged, provisioning access, moving data so its shape can be seen. This is the one type that _does_ rather than decides — and it earns its place by unblocking a decision, not by delivering the destination. The agent drives it alone where it can (AFK); otherwise it hands the human a precise checklist (HITL). Resolved when the work is done; the answer records what was done and any resulting facts (credentials location, new URLs, row counts) later tickets depend on.

When a resolution makes a design choice, invoke `domain-modeling` if it resolves durable terminology, context relationships, or qualifying architectural rationale. Every decision-producing resolution ends with:

```markdown
## Domain Impact

<links to changed Domain Documentation, or `No durable domain impact.`>
```

Research resolutions are factual Evidence, not design choices; do not manufacture a Domain Impact for them.

## Fog of war

The map is _deliberately_ incomplete: don't chart what you can't yet see. Beyond the live tickets lies the **fog of war** — the dim view of decisions and investigations you can tell are coming but can't yet pin down, because they hang on questions still open. Resolving a ticket clears the fog ahead of it, graduating whatever's now specifiable into fresh tickets — one at a time, until the way to the destination is clear and no tickets remain.

The map's **Not yet specified** section is where that dim view is written down: the suspected question, the area to revisit later. It's the undiscovered frontier _toward_ the destination — everything here is in scope, just not sharp enough to ticket. Write as loosely or as fully as the view allows; it doubles as a signpost for collaborators reading where the effort is headed.

**Fog or ticket?** The test is whether you can state the question precisely now — _not_ whether you can answer it now.

- **Ticket when** the question is already sharp — even if it's blocked and you can't act on it yet.
- **Not yet specified when** you can't yet phrase it that sharply. Don't pre-slice the fog into ticket-sized pieces: it's coarser than a ticket, and one patch may graduate into several tickets, or none, once the frontier reaches it.

**Not yet specified** excludes what's already decided (Decisions so far), what's already a live ticket, and what's out of scope (the next section).

## Out of scope

Fog only ever gathers _toward_ the destination. The destination fixes the scope, so work beyond it is **out of scope** — it isn't fog, and it doesn't belong in **Not yet specified**. It gets its own **Out of scope** section on the map: work you've consciously ruled out of _this_ effort. Scope, not sharpness, lands it here.

Out-of-scope work never graduates — the frontier stops at the destination — so it returns only if the destination is redrawn, and then as a fresh effort, not a resumption.

Ruling something out of scope is a scoping act, not a step on the route. When a ticket that already exists turns out to sit past the destination — mis-scoped in while charting, or exposed by a resolution — **close it** (a closed ticket is unambiguously off the frontier) and leave one line in the **Out of scope** section: the gist plus why it's out of scope, linking the closed ticket. It stays out of **Decisions so far**, which records the route actually walked — a scope boundary isn't a step on it.

## Invocation

Only explicit human invocation starts or resumes Wayfinder. It has two modes. Resolve or reconcile at most one Decision Ticket per session; Research is a separate explicitly invoked workflow, not an exception.

### Chart The Map

The human invokes Wayfinder with a loose idea or Effort.

1. **Find or name the Effort.** Query through the Tracker Adapter for an existing Decision Map for the Effort. Resume it when one exists; one Effort has one Decision Map.
2. **Name the destination.** Invoke `grilling` to pin down the desired outcome. Invoke `domain-modeling` when the exchange resolves durable domain language or architectural rationale. The destination fixes the scope, so settle it first.
3. **Map the whole frontier.** Grill breadth-first in one round: surface related unknowns together across the full destination rather than interviewing down one thread. Separate currently precise Decision Tickets from fog that is still too vague to ticket.
4. **Create or update the Decision Map.** Fill Destination and Notes, leave Decisions-so-far as the resolution index, and sketch remaining fog into **Not yet specified**. Create the map even when the route is already clear so the Effort has one durable entry artifact.
5. **Prepare the Decision Tickets.** For each factual gap, dispatch a fresh isolated subagent with only the neutral current-state subject and explicit source pointers; have it invoke `research-questions` and return only the packet. Do not expose the destination, desired outcome, proposed design, or unrelated planning context to that delegation. Use each returned packet as its Research Decision Ticket body. Draft other currently precise Decision Tickets with their questions.
6. **Create then wire.** Create the Decision Tickets through the Tracker Adapter, then add genuine blocking edges in a second pass. Keep unspecifiable work in **Not yet specified**. A Research edge points only to the decisions that require its Evidence.
7. **Stop at the phase boundary.** Charting resolves no Decision Ticket. Name the available next explicit invocation: `research` with a named frontier Research Decision Ticket, or `wayfinder` with the Decision Map for a frontier non-Research Decision Ticket. If no consequential Decision Ticket or fog remains, use the Product Design handoff below.

### Work Through The Map

The human invokes Wayfinder with a Decision Map and may name a Decision Ticket. Without one, choose the next frontier record in adapter order.

1. **Load the low-resolution map.** Read the Decision Map, query its frontier through the Tracker Adapter, and find closed Decision Tickets not linked from either **Decisions so far** or **Out of scope**. Do not load every child body.
2. **Reconcile one completed record first.** If the human named a closed unindexed record, or the query finds an unindexed resolution, read that record on demand. Append only a one-line gist and context pointer to **Decisions so far**, or to **Out of scope** when that is why it closed. For Research, read its Evidence resolution but leave the Research record as its sole owner. Graduate newly precise fog, create then wire any new Decision Tickets, and stop.
3. **Choose and check the frontier record.** Use the named open Decision Ticket or the first frontier record in adapter order. Before any mutation, verify it is open, unblocked, and unclaimed. If a named record is unavailable, report why and stop; otherwise skip unavailable records. If the selected record is Research, name `research` with that record as the next explicit invocation and stop without claiming or investigating it.
4. **Claim before work.** Claim a non-Research Decision Ticket through the Tracker Adapter as the session's first mutation, then refetch it. Continue only if it remains open and unblocked and the adapter confirms this session owns the claim.
5. **Resolve one Decision Ticket.** Zoom into related records only as needed and invoke skills named in Notes. Use `grilling` for human judgment and `prototype` for concrete Evidence. Apply the Domain Impact rule to every decision-producing resolution.
6. **Record the resolution.** Add the answer as a resolution comment, close the Decision Ticket, and append only its one-line gist and context pointer to Decisions-so-far.
7. **Advance the frontier.** Create then wire newly surfaced Decision Tickets. Graduate newly specifiable fog by removing it from **Not yet specified** so it lives only in its Decision Ticket. Rule records beyond the destination out of scope rather than resolving them on the route.
8. **Preserve history.** Open Decision Tickets may be revised or closed as out of scope. Closed tracker bodies are Historical Tracker Records: never edit, delete, or reopen them. Record later errors as correction annotations and changed valid decisions as supersession annotations that link the new Decision Ticket.

## Product Design Handoff

When the Decision Map has no open Decision Tickets, no completed Research awaiting reconciliation, and no consequential **Not yet specified** fog, report that the way to the destination is clear. Name `product-design` as the next explicit human invocation and stop without invoking it or producing Product Design. Keep the Decision Map available so a later design phase can return consequential gaps as new Decision Tickets.

The user may run unblocked tickets in parallel, so expect other sessions to be editing the tracker concurrently.
