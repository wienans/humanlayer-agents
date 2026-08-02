---
name: product-design
description: Explicitly create, resume, or refine an Effort's approved problem-and-behavior contract from RPI Evidence or a sufficiently resolved Decision Map.
disable-model-invocation: true
---

# Product Design

Product Design turns an Effort, resolved choices, factual Evidence, and durable Domain Documentation into the contract a team can design and build from. It answers **what** the product must do and **why**: the problem, success, actors, flows, functionality, behavior, and edge cases. Leave schemas and implementation architecture to `technical-design`.

This is **synthesis**, not a fresh PRD interview. Preserve every settled choice, ask only genuinely open product questions, and keep the Product Design reading as one coherent current contract rather than a transcript or decision log.

## Concern-based authority

Authority comes from the concern a source owns, never from which document is newest:

- The **Effort** provides lifecycle identity and the starting outcome and scope context; it does not override current approved intent.
- **Decision Tickets** own choice history and rationale; Product Design owns the resulting current behavioral contract.
- **Evidence** owns established facts and evidentiary limits.
- **Domain Documentation** owns canonical terminology, context relationships, and qualifying architectural rationale.
- The open **Product Design** owns approved problem and behavior.

Link these sources instead of copying their contents. When sources that own the same concern conflict, surface the conflict for human resolution; chronology is not a tie-breaker.

## Working rules

**Draft before asking.** Synthesize everything authoritative into a cohesive draft first. Questions are only for gaps that remain after synthesis.

**Ask one frontier, not one question.** Use `grilling` for the canonical whole-frontier conversation. Product Design classifies the gaps and persists the resulting behavioral contract; `grilling` owns how the design tree is traversed.

**Rework; do not append.** Fold each resolution into the contract by rewriting, reordering, or removing content as needed. The artifact is a designed document, never a Q&A log or changelog.

**Show behavior.** Use Mermaid diagrams when they clarify actors, flows, states, or interactions. When a visual direction requires concrete exploration, invoke `prototype`; link the winning visual from its throwaway branch. During Product Design, fold the verdict into the contract and leave production code unchanged. Prototype HTML, routes, switchers, and losing variants stay out of production history.

**Write for humans.** A reader should understand the product by skimming the headers. Prefer takeaway headers, short paragraphs, and visuals beside the behavior they explain.

**Stay in product space.** Product states, interactions, rules, observable outcomes, and edge behavior belong here. Technical schemas, storage, module structure, dependency direction, migration mechanics, and implementation architecture belong to `technical-design`.

## 1. Establish The Entry Path

1. Require a named Effort, open Product Design, closed RPI Evidence record, or Decision Map. If the reference does not identify the Effort, ask for one and stop.
2. Read `AGENTS.md` and follow its context pointers to the configured Tracker Adapter and Domain Documentation rules.
3. Resolve the Effort and entry path:
   - **RPI:** require at least one closed Research record whose canonical Evidence bears on the Effort. The Research record may itself embody the Effort when it is the first durable tracker artifact. RPI has no required Decision Map.
   - **Wayfinder:** require a Decision Map with no open Decision Tickets, no completed Research awaiting reconciliation, and no consequential fog in **Not yet specified**. If the map is not ready, name the appropriate explicit `research` or `wayfinder` invocation and stop.
4. Find an existing open Product Design or Product intent for the Effort and resume it. One Effort has one current Product Design concern. If Product intent and an open Product Design coexist, or multiple open Product Design records exist, stop on an authority conflict rather than choosing one. A closed Design Artifact is historical: create its replacement, then annotate correction or supersession through the Tracker Adapter rather than editing or reopening it.

Entry-path differences end here. The remaining process behaves identically for RPI and Wayfinder.

## 2. Load The Authoritative Set

Read only the sources relevant to the contract, but account for every linked authority:

1. Read the Effort root and current Product Design or Product intent fully.
2. For a Decision Map, follow its resolution index and read the owning Decision Ticket resolutions needed for product behavior. Do not treat the map's one-line gists as canonical answers.
3. Read the canonical Evidence resolutions needed to establish current behavior, constraints, user needs, or prototype verdicts. Preserve unanswered questions and source limits; do not turn inference into fact.
4. Read the applicable Domain Documentation named by the repository's domain-doc pointer.
5. Build an internal coverage map from each source to the contract section it informs. Do not publish a requirement-level traceability matrix.

If two sources appear to disagree, identify which concern each owns. Apply the owner for that concern and preserve the other as a linked constraint or alternative where relevant. If equal authorities conflict or ownership is unclear, pause only the affected section and ask the human to resolve the authority conflict.

## 3. Materialize And Draft

Use the lightest materialization that keeps Product Design ownership and approval clear:

- Keep concise **Product intent** on the open Effort root when the problem, success, and behavior remain easy to review there.
- Create a separate child Design Artifact qualified `design:product` when multiple actors, flows, product states, UI interactions, alternatives, or distinct product approval would make Product intent unclear.

Adaptive Ceremony changes depth and materialization, not the workflow path or authority boundary. Do not classify the Effort as Small, Medium, or Large, and do not create a separate design-discussion record.

Read [the Product Design template](references/product-design-template.md), then create or rewrite the complete draft through the Tracker Adapter. Fit the depth to the Effort while accounting for every template concern. In particular:

- State success in observable terms. Use a product metric, adoption signal, benchmark, reliability target, or qualitative read that lets the team judge whether the Effort worked. If no meaningful measure exists, state that explicitly rather than inventing one.
- Describe actors and end-to-end flows from their point of view.
- Specify states, interactions, rules, and edge behavior precisely enough to review without prescribing implementation.
- For Wayfinder, trace alternatives to the Decision Tickets that chose among them without restating the deliberation. For RPI choices resolved inside Product Design, record the chosen path and concise rationale directly.
- Link relevant Decision Tickets, Evidence, Domain Documentation, and prototype branches as Design Anchors rather than duplicating them.

Use takeaway subheadings inside the template sections when the contract needs more structure.

## 4. Resolve Only The Open Frontier

Classify each apparent gap before asking anything:

- **Settled:** incorporate the authoritative answer without asking it again.
- **Missing fact:** do not ask the human for a fact that needs Evidence. If the fact could change the affected behavior, mark that section blocked. With a Decision Map, return the factual gap to Wayfinder so it can prepare a neutral Research Decision Ticket; in RPI, name `research-questions` for the affected Evidence gap. Stop after preserving the rest of the draft. A clearly labeled, non-blocking assumption may remain in the contract.
- **Consequential Wayfinder choice:** when a choice could change the destination, scope, key behavior, quality target, or downstream architecture or transition strategy, create a focused Decision Ticket on the existing Decision Map through the Tracker Adapter, wire only genuine blockers, and link it from a blocked note in the affected Product Design section. Name `wayfinder` with that Decision Ticket and stop; leave every unaffected section intact.
- **Local product choice:** add it to the current Product Design frontier.
- **Technical choice:** defer it to `technical-design`; do not disguise it as a product question.

An RPI Effort does not gain a Decision Map silently. Resolve its bounded product choices in the frontier. If the uncertainty has become broad enough to require decision mapping, report that change and name `wayfinder` as an optional explicit human invocation.

For the local product frontier, invoke `grilling` and follow its whole-frontier rounds until the human confirms shared understanding. As each round resolves choices, persist those answers in the draft; this keeps the current contract coherent and does not advance to a downstream phase. After each round:

1. Rework every affected Product Design section so the answer reads as part of the contract.
2. Invoke `domain-modeling` immediately when a resolution introduces or sharpens canonical terminology, context relationships, or qualifying architectural rationale.
3. Use `prototype` when interaction or visual Evidence is the cheapest way to resolve a remaining choice, then link the winning branch and verdict while leaving production code unchanged.
4. Recompute the frontier. Ask the next round only when new choices become unblocked.

The frontier is complete when every product branch is resolved, deferred to its proper authority, or linked to a focused blocking record.

## 5. Complete The Contract

Before completion, verify the current materialization:

- The problem, success measures, actors, flows, behavioral rules, states, interactions, and edge behavior are clear at the depth this Effort needs.
- Alternatives and exclusions are explicit.
- Every product-relevant settled Decision Ticket is preserved and no settled question was re-asked.
- Every factual claim is supported by linked Evidence or clearly marked as a non-blocking assumption; no blocking Evidence need remains.
- Relevant Domain Documentation and prototype branches are linked, not copied.
- Technical schemas and implementation architecture are absent or explicitly deferred.
- No affected section remains blocked by an unresolved authority conflict or open frontier choice.

Run `domain-modeling` for any approved durable terminology or qualifying architectural choice not yet captured. Populate the template's Domain Impact in the Product Design's owning tracker record: use `### Domain Impact` within Product intent or `## Domain Impact` in a separate Product Design. Link changed Domain Documentation or state `No durable domain impact.`

Leave the current Product Design open as the owner of approved product intent. Report its name and link, state that invoking the next phase constitutes human approval, name `technical-design` as the valid next explicit invocation, and stop without invoking it. There is no separate review gate.
