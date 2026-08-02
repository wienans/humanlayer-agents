# Canonical Evidence Resolution

The `research` skill publishes this shape as the Research record's single resolution comment.

```markdown
## Evidence

### Research Context

**Date**: [Current date and time with timezone]
**Git Commit**: [Investigated commit hash]
**Branch**: [Investigated branch name]
**Repository**: [Repository name]

### Research Questions

[List of original research questions from the Research packet.
Present as a numbered list if multiple questions were provided.]

### Scope And Method

[Named Sources inspected, versions or revisions when available, and source limitations. State any use of secondary sources.]

### Question Status

| Question | Status | Basis |
| --- | --- | --- |
| 1 | Established | [Direct citations] |
| 2 | Unanswered | [Where the Named Sources were insufficient] |

### Summary

[2-4 focused paragraphs synthesizing what was found. Cover key architectural patterns, data flows,
and relationships. Synthesize, don't compress every detail.]

### Detailed Findings

[Organize by concept/feature, not by file location. Number top-level sections. Write as a story
about the codebase with citations woven in, not a file index and not a list of answers to the
research questions. Use tables, mermaid diagrams, call-stack trees, file trees, component trees,
type signatures, and pseudocode where they convey structure faster than prose. Keep every view
objective — describe current state, never use `diff` blocks or `+`/`-` change markers.]

#### 1. [Takeaway about this concept — the header asserts what's true, not the topic or the question]

[Prose explanation of what this is and how it works. Cite file locations inline using ranges
for adjacent lines — e.g. (`src/app.ts:57-80`). Reach for the right view: tables for comparisons,
code blocks for key type signatures, mermaid for architectural relationships, call-stack/file/
component trees for structure, pseudocode for complex logic. Place each visual beside the prose it
illustrates.]

##### Testing patterns

[Test file locations, testing approach (unit/integration/e2e), mocking patterns, fixtures
and utilities. If no tests exist, say so explicitly.]

#### 2. [Takeaway about the next concept]
...

### Code References

[Very comprehensive list of key files and directories, grouped by area. Indicate when the list
is exhaustive for a given area vs. when it covers key files but others may exist.]

#### [Group name]
- `path/to/file.ts:28-36` — Description of what's there
- `path/to/directory/` — Description of directory contents (key files listed, others exist)

### Architecture Documentation

[Narrative paragraphs describing architectural patterns, conventions, and design decisions.
How components compose, how data flows, what conventions are followed.]

### Unanswered Questions

[Genuine investigative questions about things not fully traced or understood. Focus on
"How does X reach Y?" not "Should Z be refactored?" If truly none, say "None."]
```

Use direct repository files, official documentation, specifications, standards, or upstream source as primary evidence. Cite precise lines, anchors, pages, or sections. Label secondary sources and inference explicitly.

Keep the resolution factual and non-normative. It contains no recommendations, preferred alternatives, criticism, implementation steps, or claims beyond the Named Sources.
