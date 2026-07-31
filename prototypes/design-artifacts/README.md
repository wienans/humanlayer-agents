# Prototype: design artifacts at three scales

**This is a throwaway prototype — not production. It answers one wayfinder question, then gets archived on a throwaway branch.**

- **Ticket**: [Prototype design artifacts for representative projects](https://github.com/wienans/humanlayer-agents/issues/14) (#14) — a `wayfinder:prototype` child of the Decision Map [Design a unified architecture-first engineering workflow](https://github.com/wienans/humanlayer-agents/issues/1) (#1)
- **Branch**: `prototype/design-artifacts` (throwaway — do not merge)
- **Hosted copy**: https://ancient-crystal-rkwx.here.now/ — the single self-contained `index.html`, also openable by double-click (no build, no server)

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
| 1 | Reactor-control firmware migration **STM32F103 → STM32H743** | Large | Effort root + **Product Design** + **Technical Design** (System/Program/**Transition**, Embedded lens) |
| 2 | Rework packaging/releases for the `hydrant` Python CLI (setuptools → hatchling) | Medium | Effort root (with **Product intent**) + **Technical Design** (System/Program + thin Transition, Python lens) |
| 3 | Add a session-export action to a web app's Settings page | Small | **One record** — Effort root carries Product intent + concise System/Program (TS/Web lens, shallow) |

## 2. Prototype shape decision

Per the `/prototype` skill, two branches exist: **UI** (what should it look like) and **Logic** (does the state/logic feel right). This ticket is closest to *"what should these artifacts look like"*, so it follows the UI branch — but the "radically different variants" being compared are the **artifact sets at the three ceremony levels**, not three layouts of one page. Each tab in `index.html` is one representative project; the structures differ structurally (1 vs 2 vs 3 records) by design. If this assumption is wrong, say so on the ticket and the prototype can be reshaped.

## 3. What to look at / judge

Open `index.html` (or the hosted URL) and flip through the three tabs. The feedback that matters:

1. **Conciseness** — is every section pulling weight, or does anything read as filler?
2. **Depth** — is each record deep enough to implement from without re-asking the questions (the contracts say approval is *implicit*: you start the next step when it's sufficient)?
3. **Ceremony** — does Large feel appropriately heavier than Small, without ceremony for ceremony's sake? The "ceremony at a glance" strip exists to make this judgment one glance.
4. **Contract fidelity** — does each record contain what the contracts prescribe (e.g. Product Design's problem/success/actors/behavioral-contract/out-of-scope/alternatives-traceability; Technical Design's System components+delta, Program shape, Transition slices+gates, profile lens, "What We're Not Doing")?

Domain details are fictional placeholders — judge shape, not engineering accuracy.

## 4. How to react

Reply on [issue #14](https://github.com/wienans/humanlayer-agents/issues/14) (or edit the HTML in this branch). The resolution of this ticket is the verdict — e.g. "the contracts produce concise-but-deep artifacts, with X too thin / Y too ceremonial" — which then feeds the skill-topology ticket ([#12](https://github.com/wienans/humanlayer-agents/issues/12)) and the workflow prototype ([#13](https://github.com/wienans/humanlayer-agents/issues/13)).

## 5. Files

- `index.html` — the prototype, self-contained (plain HTML/CSS/JS, no framework, double-click to open).
- `README.md` — this info pack.

## 6. How it was made / how to reproduce

- Contract sources: issues #5 and #15 (resolutions), `CONTEXT.md`, ADRs 0003/0004.
- Skill: `/wayfinder` (claim ticket #14 → `/prototype` → capture) + `/here-now` for hosting.
- Artifacts are rendered as "tracker records" matching the GitHub-issues tracker of this repo (`docs/agents/issue-tracker.md`).
