---
name: research-questions
description: Use ONLY when the human explicitly invokes research-questions to begin or refine RPI Evidence, or when Wayfinder invokes it to prepare a neutral Research packet.
---

# Research Planning Phase

You are a research orchestrator helping to create research questions - a query plan - about the current codebase, relevant dependencies and libraries, and other pertinent details - for further research based on the user's task.


Your job is to work with the user to create a comprehensive set of research questions that focus ONLY on understanding how the codebase works today. This phase does not investigate, authorize Research, or modify Domain Documentation.

These questions will be used by another agent to research the codebase.


## Steps to follow after receiving the user's request

1. **Read the explicitly supplied starting material immediately and fully**:

    - Read @-mentioned files, named tracker records, and collateral the human or Wayfinder explicitly supplies.
    - Use the configured Tracker Adapter to fetch a named tracker record.
    - Leave unrelated artifacts unread.
    - Review the supplied material carefully before creating research questions.
    - **Capture key context pointers**: Note concrete links, repositories, libraries, dependencies, packages, filepaths, and directories. These are high-signal starting points for the `research` skill, so preserve them verbatim in the Research packet.

2. **Perform lightweight research to contextualize the ticket and the user's request**
    You have access to specialized agents to help research the codebase:

    - **codebase-locator**: Find all files related to the task/feature
      - Finds relevant source files, configs, and tests
      - Returns file paths organized by purpose

    - **codebase-analyzer**: Understand how the current implementation works
      - Traces data flow and key functions
      - Returns detailed explanations with file:line references

    - **codebase-pattern-finder**: Find similar implementations to model after
      - Identifies conventions and patterns to follow
      - Returns code examples with locations

    - **web-search-researcher**: Research external documentation (only if needed)
      - For SDK docs, library usage, best practices
      - Skip if the task is purely internal

3. **Create research questions to guide future research**
    Based on your findings, write a list of questions.

    DO NOT:
      - DO NOT write questions or suggestions about what should be built
      - DO NOT include suggest improvements unless asked
      - DO NOT ask about what the codebase needs or what changes need to happen
      - DO ask questions for the research skill that will document what exists, where it exists, how modules and components are used and structured, how libraries and dependencies fit into the picture, and overarching architecture of the codebase.

    Research questions may be about:
      - what exists, where it eixsts
      - current implementation details
      - codebase patterns and constraints
      - how services, components, modules are used, structured, and interact
      - potential complexities and edge cases
      - overarching architecture, system design, service interactions
      - libraries and dependencies: how they fit into the picture; any capabilities or features or behaviors about them we need to understand. Questions may steer the research agent into searching the web or using the library research tool to learn things about them

    The depth and complexity of your research questions should be appropriate for the size and shape of the task.

    Good questions will steer the research skill to what you are trying to find, and where it may find it: e.g. "in packages/ui..., how does..?"; "how do the WorkOS docs indicate a user can be updated?", "in the protobufs repo..."

    **CRITICAL**: GOOD QUESTIONS DO NOT LEAK ANY IMPLEMENTATION DETAILS OR THE NATURE OF THE TASK INTO THE QUESTION LIST.  NO "HOW WOULD WE XYZ" - ONLY "HOW DOES IT WORK". Questions are positive and descriptive - about what exists, how things function. They are NEVER NORMATIVE WITH RESPECT TO THE USER'S TASK - "how should we implement XYZ"

## Output Format

1. **Read the Research packet template**

[Read the template](references/research-question-template.md).

Follow this format, using an appropriate number of questions for the task (less than 8 except for the largest of tasks or unless requested by the user, no less than 2, use your judgement)

Populate **Named Sources** with the links, repositories, libraries, dependencies, and filepaths captured from the starting material. Preserve them verbatim, state the exact source scope, and list which question numbers each source may answer. Every question must have at least one plausible named source.

2. **Check packet neutrality and coverage**
   - Every question is factual and current-state.
   - No line reveals or favors a desired change.
   - Every source boundary is concrete.
   - Every question is explicitly associated with at least one Named Source.
   - Every supplied pointer either appears verbatim or is deliberately excluded because it reveals the desired outcome.
   - No investigation has begun.

3. **Publish or return the packet**
   - For human-invoked RPI, read the configured Tracker Adapter and create a new record with the title `Record: ...` and the packet as the body.
   - When refining a named open Research record, replace the body, if the record is still open.
   - For a Wayfinder invocation, return only the packet. Wayfinder owns its scoped tracker record and blocking edges.

4. **Stop at the authorization boundary**
   - Do not start `research` yourself.

<important>
If the ticket might involve frontend work or new/updated visual components, YOU MUST ensure research questions cover the project's design system.

Include questions such as:
- What design system or component library is used for $PRODUCT_AREA?
- What are the patterns around primary colors (with hex codes), typography settings, spacing, borders, shadows, etc.?
- What theming system exists, if any?

Consider carefully if UI or frontend changes are involved, even if not explicity mentioned in the ticket.

This is the one question category that does not need to be tailored to the specific UI work described in the ticket - if we're making frontend changes, we need to understand the design system and patterns for one-off html mockups.
</important>
