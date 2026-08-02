---
name: research-questions
description: Use ONLY when the human explicitly invokes research-questions to begin or refine RPI Evidence, or when Wayfinder invokes it in an isolated worker to prepare a neutral Research packet.
---

# Research Questions

Create a neutral query plan about the current state. This skill identifies what Research must establish and where it may look; it does not investigate, answer the questions, authorize Research, advocate a change, or modify Domain Documentation.

## Build The Packet

1. Read only the starting material explicitly supplied by the human or Wayfinder. Extract the current-state subject and preserve concrete pointers verbatim.
2. Locate additional source paths only when needed to turn a vague pointer into a concrete one. Use filename and symbol location, not implementation analysis. Do not fetch external sources or answer any proposed question.
3. Write two to seven questions appropriate to the scope. Each question asks what exists, how it behaves, where responsibility lives, how components interact, or what constraints a named dependency establishes.
4. Remove desired behavior, proposed architecture, implementation hints, criticism, and rationale for making a change. A researcher reading the packet must not be able to infer which answer the requester hopes to find.
5. Name every allowed source using an exact file, directory, repository, dependency, documentation root, or URL. A directory or documentation root must state the permitted descendant scope.
6. Render the packet with [references/packet.md](references/packet.md). Every question must have at least one plausible named source, and every supplied pointer must either appear verbatim or be deliberately excluded as outcome-revealing.

## Publish Or Return

For a human-invoked RPI entry:

1. Read the configured Tracker Adapter through the repository context pointer.
2. Use its semantic **Create Research record** operation with the packet as the body. Create one record per coherent packet.
3. If refining a named open Research record, use **Revise open Research packet** instead. Rewrite it cohesively rather than appending notes.
4. Treat a closed Research record as Historical Tracker Record: leave its body unchanged and use **Create linked Research record** for new investigation.

For an isolated Wayfinder invocation, return only the packet to Wayfinder and stop. Wayfinder owns creation and blocking of its scoped Research Decision Ticket; this branch has no Research record reference or user-facing next-invocation response yet.

This phase is complete when the packet passes all of these checks:

- every question is factual and current-state;
- no line reveals or favors a desired change;
- every source boundary is concrete;
- the RPI Research record exists, or Wayfinder has received the packet;
- no investigation has begun.

For the human-invoked RPI branch, stop and wait for the human. Name `research` as the next invocation and include the Research record reference. Do not invoke it automatically.
