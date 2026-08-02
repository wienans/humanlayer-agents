---
name: research
description: Use ONLY when the human explicitly invokes research by name with an open neutral Research record; investigates it in isolation and publishes canonical Evidence.
disable-model-invocation: true
---

# Research

Research turns one approved neutral packet into one canonical Evidence resolution. It documents current facts and evidentiary limits; it does not recommend, critique, choose, design, implement, or modify Domain Documentation.

## Authorize The Record

1. Require the human to name one open Research record. If none is named, ask for the record reference and stop.
2. Read only that record's packet and the configured Tracker Adapter. Do not read its parent Effort, Decision Map destination, desired outcome, proposed design, or unrelated planning artifacts.
3. Validate the packet against the `research-questions` neutrality and named-source contract. If it leaks a desired change or lacks usable source boundaries, stop and name `research-questions` as the corrective invocation.
4. Use the adapter's semantic **Claim Research record** operation before any source is investigated. An existing claim by the current user authorizes resumption; if the record is closed, blocked, or owned by someone else, stop without investigating.
5. Count canonical `## Evidence` resolution comments. If exactly one already exists after a prior close failure, use **Resolve Research record** to finish closing without dispatching a worker. Stop for human repair if more than one exists.

The explicit invocation plus successful claim is the authorization boundary. No other skill or worker may begin Research.

## Dispatch Isolated Research

Launch exactly one fresh `research-worker` subagent. Supply only:

- the neutral packet body;
- the exact Named Sources and their stated scope;
- the complete Evidence shape copied from [references/evidence.md](references/evidence.md) as format instructions.

Read that reference in the orchestrator and embed its contents; do not send the worker a relative path. Do not include conversation history, the parent record, desired outcomes, proposed changes, or other planning artifacts. The orchestrator performs tracker operations but does not investigate or synthesize facts itself.

Wait for the worker. If it marks a question unanswered and one targeted check of the existing Named Sources could resolve it, resume the same isolated worker once with that question. Supply no new planning context or source. After that single follow-up pass, retain every unresolved question as unanswered.

## Publish Evidence

Verify before publication that:

- every packet question is represented as established or unanswered;
- every established claim has a direct code reference or source citation;
- primary sources are preferred and secondary sources are identified;
- facts are separated from inference and unanswered questions;
- the text contains no recommendation, criticism, desired state, or design choice.

If the worker fails these checks, leave the record open and claimed, report the failure, and stop. Otherwise use the Tracker Adapter's semantic **Resolve Research record** operation to append the worker's completed Evidence as the record's single canonical resolution and close it. Create no separate Research document or duplicate Evidence artifact.

Closed Research records are Historical Tracker Records. Later errors use the adapter's **Annotate correction** operation; changed investigation needs the adapter's **Create linked Research record** operation and a new neutral packet. Never rewrite or reopen the closed body.

Completion requires a closed Research record whose canonical Evidence accounts for every question, including explicit unanswered questions after at most one follow-up pass. Report the record reference, name `product-design` as the next RPI invocation, mention `research-questions` only when a new factual packet is needed, and wait for the human.
