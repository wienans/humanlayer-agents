# Prototype: design artifacts at three scales

**This is a throwaway prototype — not production. It answers one wayfinder question, then gets archived on a throwaway branch.**

- **Ticket**: [Prototype design artifacts for representative projects](https://github.com/wienans/humanlayer-agents/issues/14) (#14) — a `wayfinder:prototype` child of the Decision Map [Design a unified architecture-first engineering workflow](https://github.com/wienans/humanlayer-agents/issues/1) (#1)
- **Branch**: `prototype/design-artifacts` (throwaway — do not merge)
- **Hosted copy**: https://ancient-crystal-rkwx.here.now/ — the single `index.html`. Openable by double-click (no build, no server); the Mermaid diagrams render from a CDN, so a fully-offline open shows their source text instead.

---

## 1. What is being prototyped

The **question** (verbatim from the ticket):

> Do the proposed problem/behavior and technical-design contracts produce concise but sufficiently deep tracker artifacts for a major Embedded C processor migration, a medium Python tooling change, and a smaller TypeScript/web change without irrelevant ceremony?

The two contracts under test are the **Product Design** contract ([issue #5, resolved](https://github.com/wienans/humanlayer-agents/issues/5)) and the **Technical Design** contract ([issue #15, resolved](https://github.com/wienans/humanlayer-agents/issues/15)), both recorded in:

- `CONTEXT.md` — Product Design, Product intent, Technical Design, System/Program/Transition Design, Profile Lens, Adaptive Ceremony, Design Artifact
- `docs/adr/0003-product-design-synthesizes-resolved-decisions.md`
- `docs/adr/0004-technical-design-layers-with-profiles.md`

The prototype renders, the way they'd actually appear on the tracker, the **artifact sets** for three fictional-but-realistic representative projects — one per ceremony level:

| # | Representative project | Scale | Records materialized |
|---|------------------------|-------|----------------------|
| 1 | Reactor-control firmware migration **STM32F103 → STM32H743** | Large | Effort root + **Design Discussion** + **Product Design (PRD)** + **Technical Design (TDD)**, full depth |
| 2 | Rework packaging/releases for the `hydrant` Python CLI (setuptools → hatchling) | Medium | Effort root (with **Product intent**) + **Design Discussion** + **Technical Design (TDD)**, medium depth |
| 3 | Add a session-export action to a web app's Settings page | Small | **One record** — Effort root carries Product intent + concise TDD, shallow |

## 2. Prototype shape decision

Per the `/prototype` skill, two branches exist: **UI** (what should it look like) and **Logic** (does the state/logic feel right). This ticket is closest to *"what should these artifacts look like"*, so it follows the UI branch — but the "radically different variants" being compared are the **artifact sets at the three ceremony levels**, not three layouts of one page. Each tab in `index.html` is one representative project; the structures differ structurally (1 vs 2 vs 3 records) by design. If this assumption is wrong, say so on the ticket and the prototype can be reshaped.

## 3. Design-doc template alignment (HumanLayer)

The design docs inside the prototype follow the HumanLayer design-doc family from `.opencode/skills/`, not free-form prose:

- **Design discussion** follows `create-design-discussion/SKILL.md` + `create-design-discussion/references/design_discussion_template.md`, materialized as a `design:discussion` record for Large and Medium (the two projects that actually hit decisions):
  - **Proposed End-State Architecture** with Before / After Mermaid diagrams side by side, plus a concise outline + pseudocode of the end state.
  - **Design Questions** — open ones rendered as titled options (Option A vs B, each with an optional snippet) + a `Recommendation:`.
  - **Resolved Design Questions** — titled, chosen option + rationale, and the options *not* chosen so the rejection is traceable.
  - **Patterns to Follow** in the precise form: subject line, `Pattern:` / `File:` fields, and an existing→proposed **before/after code pair** (or a single snippet for a brand-new pattern). These are the templates the skills themselves will emit from, so "do X" became "here is the existing code and here is the proposed shape".
- **Product side** follows `create-prd/SKILL.md` + `create-prd/references/prd_template.md`:
  `Problem to Solve` / `What does business success look like, and how can we measure it?` / `Proposed Solution` / `Alternative Solutions Considered` / `Out of Scope`. Materialized as a separate `design:product` record for Large, and as concise Product intent on the Effort root for Medium/Small.
- **Technical side** follows `create-tdd/SKILL.md` + `create-tdd/references/tdd_template.md`:
  - **System Design** — cross-component architecture with the current→target delta folded in as one coherent story (the TDD template explicitly forbids a separate "Current State / Desired End State" section). Takeaway-style headers (each header states its decision, like a slide title), Mermaid diagrams for flow, and type signatures / endpoint & message shapes / data schemas for the boundaries between components.
  - **Program Design** — in-code shape via call-stack trees, component trees, file-tree diffs, dependency-injection / seam maps, testing-seam maps, method signatures, and pseudocode.
  - **What We're Not Doing** — technical scope deliberately excluded.
  - **Patterns to Follow** — existing codebase patterns with file locations and snippets (the TDD side keeps the concise pattern-list form, while the design-discussion side carries the full before/after pairs).
- **Visual language** matches `create-tdd/references/artifact_template.html`: poimandres dark palette, square corners, IBM Plex Mono for code, system-ui for prose, badge / stat / before-after utility classes.

Note: HumanLayer has no separate "Transition Design" layer — migrations are told inside System Design as the delta story. Map contract #15 splits Technical Design into System/Program/Transition layers; this prototype's Large and Medium TDDs keep the migration plan (slices, gates, rollback) inside the System Design narrative, as the TDD template instructs. Whether the Transition layer should survive as a distinct section is one of the decisions this prototype is probing — call it out if you think it should.

**How the skills should be written later:** when the skill-topology ticket (#12) writes the design-doc skills for this workflow, it should **source the section shapes and snippets directly from these HumanLayer templates** (`create-prd`, `create-tdd`, `create-design-discussion`), rather than re-deriving them from this prototype or the contract docs. The prototype only shows *what the output looks like*; the templates are the canonical source for *how to produce it*. Where the prototype had to decide something the templates leave open (e.g. design-discussion materialized only when a project actually hits decisions), that decision is recorded on the relevant record and should be captured by the skill, not re-argued.

## 4. What to look at / judge

Open `index.html` (or the hosted URL) and flip through the three tabs. The feedback that matters:

1. **Conciseness** — is every section pulling weight, or does anything read as filler?
2. **Depth** — is each record deep enough to implement from without re-asking the questions (the contracts say approval is *implicit*: you start the next step when it's sufficient)? Do the System/Program sections actually reveal the architecture and design, or just describe it?
3. **Ceremony** — does Large feel appropriately heavier than Small, without ceremony for ceremony's sake? The "ceremony at a glance" strip exists to make this judgment one glance.
4. **Template fidelity** — does each TDD read like a HumanLayer TDD (takeaway headers, diagrams beside prose, seams and deltas made explicit)? Does the product side read like a HumanLayer PRD? Does each design-discussion read like a HumanLayer one (Before/After end-state architecture, titled design questions with recommendations, precise patterns)? Do the Before/After diagrams actually make the migration visible at a glance, and do the Pattern before/after pairs make the *new* code shape concrete rather than aspirational?

Domain details are fictional placeholders — judge shape, not engineering accuracy.

## 5. How to react

Reply on [issue #14](https://github.com/wienans/humanlayer-agents/issues/14) (or edit the HTML in this branch). The resolution of this ticket is the verdict — e.g. "the contracts produce concise-but-deep artifacts, with X too thin / Y too ceremonial" — which then feeds the skill-topology ticket ([#12](https://github.com/wienans/humanlayer-agents/issues/12)) and the workflow prototype ([#13](https://github.com/wienans/humanlayer-agents/issues/13)).

## 6. Files

- `index.html` — the prototype, plain HTML/CSS/JS, no framework, double-click to open. Mermaid diagrams load from jsDelivr CDN.
- `README.md` — this info pack.

## 7. How it was made / how to reproduce

- Contract sources: issues #5 and #15 (resolutions), `CONTEXT.md`, ADRs 0003/0004.
- Template sources: `.opencode/skills/create-design-discussion`, `.opencode/skills/create-prd` and `.opencode/skills/create-tdd` (SKILL.md + template + artifact-template references).
- Skill: `/wayfinder` (claim ticket #14 → `/prototype` → capture) + `/here-now` for hosting.
- Artifacts are rendered as "tracker records" matching the GitHub-issues tracker of this repo (`docs/agents/issue-tracker.md`).
