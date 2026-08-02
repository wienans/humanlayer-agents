---
name: grilling
description: Grill decisions as a whole frontier. Use when a workflow or user needs to expose and resolve every branch of a plan, design, or idea without asking the user for discoverable facts.
---

# Grilling

Map the subject as a **design tree**: each decision branches into the decisions that depend on it. The **frontier** is every unresolved decision whose prerequisites are settled.

Ask the whole frontier in one numbered round. Give a recommendation for every question, then wait for the human's answers before recomputing the frontier.

```text
Q1 - <question title>: <question, context, and choices>

Recommended: <answer and concise rationale>
```

Facts are agent work. Look up immediately discoverable environmental facts with read-only tools instead of asking the human. When a question requires scoped investigation or durable Evidence, return that factual need to the owning workflow as a neutral Research need; only explicit `research` authorizes that investigation. A pending fact blocks only the decisions that depend on it, so continue with the rest of the frontier. Decisions remain human work.

This is a primitive, not a workflow owner. Return resolved choices to the invoking concern. When a resolved choice introduces durable domain language or qualifies as an architectural decision, invoke `domain-modeling`; otherwise leave Domain Documentation unchanged.

Completion requires an empty frontier and human confirmation that the shared understanding is accurate. Stop after returning the resolved design tree to the caller; do not advance the workflow.
