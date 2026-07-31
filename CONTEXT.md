# Engineering Workflow

This context defines the language used to move engineering work from initial orientation to evidence-backed design and implementation.

## Language

**Reconnaissance**:
A bounded orientation pass that identifies relevant surfaces, established facts, risks, and unknowns before classifying the work. It does not make design decisions.

**Research Questions**:
An objective query plan describing which existing behaviors and facts to investigate and where evidence may be found, without revealing the desired change.

**Research**:
A source-agnostic, objective synthesis of evidence that answers Research Questions about the current state. It documents facts and does not propose or choose changes.

**Domain Modeling**:
An event-driven design discipline that resolves canonical domain language and captures durable architectural decisions when they arise. It is active during decision-making, not a mandatory phase of every workflow.

**Domain Documentation**:
Committed codebase context containing canonical domain vocabulary, bounded-context relationships when needed, and qualifying architectural decisions. It does not own product requirements or work-specific technical and transition design.

**Context Map**:
The durable index of a multi-context domain model. It identifies each bounded context and distills the minimal semantic and technical relationships needed to understand how the contexts interact after task-specific design artifacts cease to be consulted.

**Decision Map**:
A Wayfinder tracker index that guides a large, uncertain body of work toward a defined destination. It links resolved Decision Tickets and exposes the remaining decision frontier without duplicating their answers.

**Decision Ticket**:
A child tracker record of a Decision Map that owns one decision or investigation and its resolution. _Avoid_: unqualified "ticket" when the distinction from a Delivery Ticket matters.

**Effort**:
The continuous identity of one desired outcome from an initial tracker record or direct prompt through delivery. It is a composable lifecycle role embodied by the starting record or first durable tracker artifact, not a mandatory wrapper record.

**Design Artifact**:
A tracker record that owns currently approved intent while open, qualified as Product Design, Technical Design, or Transition Design. It links relevant Domain Documentation and supporting Evidence rather than duplicating them; once closed, it is historical context.

**Product Design**:
A Design Artifact that owns the approved problem-and-behavior contract for an Effort while open. It synthesizes resolved decisions and asks only genuinely unresolved product questions; it is materialized as a separate tracker record or as concise Product intent on the Effort root per Adaptive Ceremony. _Avoid_: PRD as the canonical artifact.

**Product intent**:
The concise statement of an Effort's problem, success, and behavior kept on the Effort root when no separate Product Design record is materialized.

**Technical Design**:
A Design Artifact that owns the approved implementation intent for an Effort while open, composed of System Design, Program Design, and removable Transition Design layers and guided by a language-neutral core with progressively disclosed profile lenses.

**System Design**:
A Technical Design layer that owns the cross-component architecture: system context and boundaries, components with responsibilities and dependency direction, semantic and temporal contracts, quality-attribute scenarios, constraints and unknowns, alternatives and tradeoffs, and the current-to-target delta. It states the delta once; Transition Design owns the plan for traversing it.

**Program Design**:
A Technical Design layer that owns the in-code shape: module and type layout, call trees, dependency direction within components, testing seams and strategy, and patterns to follow. SOLID and CUPID are suggested quality guidance rather than enforced; testable design is a depth check.

**Transition Design**:
A removable Technical Design layer that owns the migration and cutover path when an Effort preserves or replaces existing behavior: baseline behavior-and-resources evidence, transition slices, platform seams, coexistence and compatibility, rollback and irreversible steps, and entry and exit evidence gates. It is omitted for greenfield efforts.

**Profile Lens**:
A progressively disclosed, additive Technical Design lens that injects domain-specific concerns, vocabulary, and views into the language-neutral core without forking it. Profile lenses compose; the default Embedded, Python, and TypeScript lenses are selected by the stack an Effort touches and overridable by the human.

**Delivery Ticket**:
A self-contained tracer bullet that condenses approved upstream intent into an implementation contract. Its implementation fits a single fresh context window and delivers a narrow, complete, independently verifiable path; an Effort may have multiple Delivery Tickets whose blocking graph forms incremental delivery phases. _Avoid_: implementation ticket, unqualified "ticket".

**Evidence**:
Research, prototype, test, or validation material that establishes facts supporting a decision or design. Evidence informs intent but does not own it.

**Adaptive Ceremony**:
A sizing principle that preserves authority boundaries while varying the number and depth of workflow steps and physical artifacts. Small, Medium, and Large work differ in ceremony, not in the meaning of their concerns.

**Tracker Adapter**:
Repository-specific instructions in `docs/agents/issue-tracker.md` that map tracker-neutral workflow operations and semantic roles to a configured tracker. Setup creates the adapter; workflow skills reach it through a context pointer rather than embedding tracker-specific commands or field names.

**Historical Tracker Record**:
A closed tracker record whose body preserves what was understood or approved at closure. Later corrections and supersession are annotations that link new work; they do not rewrite or reopen the record.

**Domain Impact**:
The completion record in a decision-producing tracker record that links any Domain Documentation changed by the design event, or states that no durable domain impact was found.

**Architectural Decision Record (ADR)**:
The durable record of an approved architectural choice and its rationale. A choice qualifies only when it is hard to reverse, surprising without context, and the result of a real trade-off.
