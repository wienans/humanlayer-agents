---
name: research
description: Use ONLY when the human explicitly invokes research by name with an open neutral Research record; investigates it and publishes canonical Evidence.
disable-model-invocation: true
---

# Research

You are tasked with conducting comprehensive research across the codebase to answer user questions by spawning parallel sub-agents and synthesizing one canonical Evidence resolution.

## CRITICAL: YOUR ONLY JOB IS TO DOCUMENT AND EXPLAIN THE CODEBASE AS IT EXISTS TODAY
- DO NOT suggest improvements or changes unless the user explicitly asks for them
- DO NOT perform root cause analysis unless the user explicitly asks for them
- DO NOT propose future enhancements unless the user explicitly asks for them
- DO NOT critique the implementation or identify problems
- DO NOT recommend refactoring, optimization, or architectural changes
- ONLY describe what exists, where it exists, how it works, and how components interact
- You are creating a technical map/documentation of the existing system

## Authorize The Record

1. Require the human to name one open Research record. If none is named, ask for the record reference and stop.
2. Read the configured Tracker Adapter, then fetch only that record's packet, state, assignees, blockers, and comments. Treat the packet as the complete research query; do not use its parent Effort, tickets, desired outcome, proposed design, or unrelated conversation context as evidence or scope.
3. Claim the research record. A current-user claim authorizes resumption; a closed, blocked, or differently owned record does not authorize investigation.

The explicit invocation plus successful claim is the authorization boundary.

## Investigate The Packet

1. **Read the packet and Evidence shape first:**
   - Read [references/evidence.md](references/evidence.md) fully before decomposing the work.
   - Account for every question and exact Named Source boundary.
   - Read directly named files fully before delegating related analysis.
   - Inspect only Named Sources and their stated descendant scope. Preserve insufficient answers as unanswered rather than expanding the scope.

2. **Analyze and decompose the research questions:**
   - Break the packet into composable areas while preserving question coverage.
   - Identify the components, patterns, dependencies, and current-state connections each area must establish.
   - Track every area and its supporting source boundary in a research plan.

3. **Spawn parallel sub-agent tasks for comprehensive research:**
   - Create multiple `task` subagents to research different aspects concurrently
   - We now have specialized agents that know how to do specific research tasks:

   **For codebase research:**
   - Use the **codebase-locator** agent to find WHERE files and components live
   - Use the **codebase-analyzer** agent to understand HOW specific code works
   - Use the **codebase-pattern-finder** agent to find examples of existing patterns

   **For web research and researching libraries & dependencies (if applicable):**
   - Use the **web-search-researcher** agent for external documentation and resources
    - IF you use web-research agents, instruct them to return LINKS with their findings, and please INCLUDE those links in your final report

   The key is to use these agents intelligently:
   - **Combine related questions**: Don't necessarily launch one subagent per research question. Group related questions that touch the same area of the codebase into a single subagent prompt. For example, if 3 questions are about how the daemon handles sessions, combine them into one codebase-analyzer call.
   - Aim for 2-6 well-scoped subagents rather than 1:1 question-to-agent mapping - this is not a hard rule, just guidance
   - Start with locator agents to find what exists
   - Then use analyzer agents on the most promising findings to document how they work
   - Run multiple agents in parallel when they're searching for **different areas** of the codebase
   - Each agent knows its job - just tell it what you're looking for
   - Don't write detailed prompts about HOW to search - the agents already know

4. **Wait for all sub-agents to complete and synthesize findings:**
   - IMPORTANT: Wait for ALL sub-agent tasks to complete before proceeding
   - Compile all sub-agent results
   - Prioritize live codebase findings as primary source of truth
   - Connect findings across different components
   - Include specific file paths and line numbers for reference
   - Verify all rpi/ paths are correct (task-specific files go in .humanlayer/tasks/)
   - Highlight patterns, connections, and architectural decisions
   - Answer the user's specific questions with concrete evidence

5. **Draft canonical Evidence:**
   - Follow [references/evidence.md](references/evidence.md).
   - Produce one cohesive Evidence resolution rather than a list of subagent reports or a separate Research document.
   - Include the current date, repository, revision, and branch where available so code citations retain their investigated context.

6. **Attempt to answer open questions**
   - if there are open questions in the doc you write, dispatch subagents to additional targeted research AFTER you write the doc
   - update the doc with your findings, removing and open questions that now have answers - don't append to the end,
   - do at most one additional pass to find more information, if your second group of subagents can't find all the answers, leave the remaining questions as open and proceed to the final answer

## Publish Evidence

Verify before publication that every question is accounted for, established claims have direct citations, primary sources are preferred, inference is labeled, and the text remains factual and non-normative. If the draft fails a check, leave the record open and claimed, report the failure, and stop.

Add your Evidence as a comment to the Tracker and close it. Closed Research records are Historical Tracker Records.

## Document Style and Format

The Evidence resolution should read as a **story about the codebase** — a technical explainer someone
wrote on purpose, told with diagrams, tables, code blocks, pseudocode, and takeaway headers in
between. It is **not a list of answers to the research questions**, and not a file index. A reader
should be able to understand how the system works from the Evidence alone — file citations support
the narrative, they don't replace it. Human readability is critical, but never at the expense of
technical depth and thoroughness.

### Headers state the takeaway, not the topic or the question

Make it read like a document a human wrote for other humans: a reader should be able to skim the
headers alone and come away with how the system actually works. Give every section and sub-point a
header that asserts its *takeaway* — the way a good slide title states its message ("Sessions
persist to Postgres before the daemon acks the write"), not a generic topic label ("Sessions") and
**not the research question restated** ("How are sessions persisted?"). Lead with the point, then
support it with prose, citations, and visuals.

- BAD (topic label): `### Session storage`
- BAD (question as header): `### How does the daemon persist sessions?`
- GOOD (takeaway): `### Sessions persist to Postgres before the daemon acks the write`

Keep paragraphs short, and place each diagram, signature, table, or snippet immediately beside the
prose it illustrates — never let the text become a wall with all the visuals piled at the end.

### Writing and citation style
- Write each findings section as a **cohesive explanation** of how something works, with file/line
  citations woven in parenthetically
- **Concept-first, not location-first**: describe what something does, then cite where it lives —
  not the other way around
- Bullets are fine for listing fields, flags, or options, but each bullet should describe a concept,
  not just point at a file
- When multiple facts come from adjacent lines in the same file, use a **range** (e.g.
  `file.ts:45-67`) rather than citing each line individually
- Be thorough — include enough citations that a developer can trace every claim back to code
- BAD: `- \`src/app.ts:57\` creates WorkosService` / `- \`src/app.ts:58\` creates S3Service` / `- \`src/app.ts:59\` creates JiraService`
- GOOD: "Services are module-level singletons created at startup in `src/app.ts:57-80`: WorkosService, S3Service, JiraService, LinearService, StripeService, and two Drizzle database handles."

### Visual structure — show the shape of the code, don't just describe it

Reach for a high-bandwidth visual whenever it conveys structure faster than prose would. Don't rely
solely on bullet lists — mix prose, tables, diagrams, and code. Technical depth and thoroughness
must not be sacrificed for readability — do both.

Pick the views that make each part of the story clearest:

- **Tables** for comparisons, capability matrices, config matrices, and other structured data.

- **Mermaid diagrams** for object graphs, data flows, sequence/control flow, and architectural
  relationships between components.

- **Call-stack tree** for how control actually flows through a service, CLI, worker, or request
  handler today. Show the important calls, not every frame.
  ```text
  handleRequest
    authenticate(token)
    SessionService.load(sessionId)
      sessionStore.fetch(sessionId)
    SessionService.append(event)
      eventStore.write(event)
  ```

- **File tree** for how responsibility is split across files and directories. Format like `tree`
  output so depth is easy to scan; annotate what each file is responsible for.
  ```text
  src/session
  ├── session-service.ts   # loads/appends sessions, owns the write path
  ├── session-store.ts     # Postgres queries behind the service
  └── session-route.ts     # HTTP handler that calls the service
  ```

- **Component tree** for frontend areas — production components, their state/local data, and
  module/package boundaries (the example below is React/TSX; adapt to whatever UI framework the
  codebase uses).
  ```tsx
  <SessionPage> (apps/example/src/routes/session.tsx)
    useSessionData()
    <SessionToolbar>
      <SessionList> (packages/ui)
        useVirtualizer()
  ```

- **Type signatures, endpoint shapes, and data contracts** for the boundaries between components as
  they exist — function signatures, routes, message shapes, or the schema behind a store (use the
  codebase's language).
  ```text
  PUT /api/sessions/:id
    request:  { event: SessionEvent }
    response: { session: Session }
  ```

- **Pseudocode** for complex algorithms or logic — english-y, not a programming language — to show
  how something currently behaves without reproducing the whole function.
  ```text
  on(sessionEvent)
    load session from store
    if session.closed
      reject event
    else
      append event and persist
      return updated session
  ```

### Code References section
- Should be **very comprehensive** — a developer should be able to navigate the entire researched
  area from this list
- It is okay to reference **directories** in addition to individual files
- **Indicate coverage**: note when the list is exhaustive for a given area vs. when it covers
  key files but others in the directory may also be relevant
- Group related files together

### Testing patterns
- Document under each findings section how that component is currently tested
- Include **test file locations**, testing approach (unit/integration/e2e), mocking patterns,
  test fixtures and utilities used
- If there are no tests, say so explicitly — that's a finding

<guidance>
## Important notes:
- Focus on concrete source paths, line ranges, stable links, and current behavior.
- Make the canonical Evidence self-contained; helper task reports are inputs, not additional artifacts.
- Document cross-component connections, examples, usage patterns, and testing patterns as they exist.
- Read directly named files fully before delegating related analysis, and wait for all helper tasks before synthesis.
- Follow the authorization, investigation, follow-up, and publication order exactly.
- Preserve unresolved questions in Evidence after the one permitted targeted follow-up pass.

## Markdown Formatting

When Evidence contains code blocks showing other Markdown, use four backticks for the outer fence so inner three-backtick blocks remain intact:

````markdown
# Example README
## Installation
```bash
npm install example
```
````
</guidance>
