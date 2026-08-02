# Issue tracker: GitHub

Issues and PRDs for this repo live as GitHub issues. Use the `gh` CLI for all operations.

## Conventions

- **Create an issue**: `gh issue create --title "..." --body "..."`. Use a heredoc for multi-line bodies.
- **Read an issue**: `gh issue view <number> --comments`, filtering comments by `jq` and also fetching labels.
- **List issues**: `gh issue list --state open --json number,title,body,labels,comments --jq '[.[] | {number, title, body, labels: [.labels[].name], comments: [.comments[].body]}]'` with appropriate `--label` and `--state` filters.
- **Comment on an issue**: `gh issue comment <number> --body "..."`
- **Apply / remove labels**: `gh issue edit <number> --add-label "..."` / `--remove-label "..."`
- **Close**: `gh issue close <number> --comment "..."`

Infer the repo from `git remote -v` - `gh` does this automatically when run inside a clone.

## Pull requests as a triage surface

**PRs as a request surface: no.** _(Set to `yes` if this repo treats external PRs as feature requests; `/triage` reads this flag.)_

When set to `yes`, PRs run through the same labels and states as issues, using the `gh pr` equivalents:

- **Read a PR**: `gh pr view <number> --comments` and `gh pr diff <number>` for the diff.
- **List external PRs for triage**: `gh pr list --state open --json number,title,body,labels,author,authorAssociation,comments` then keep only `authorAssociation` of `CONTRIBUTOR`, `FIRST_TIME_CONTRIBUTOR`, or `NONE` (drop `OWNER`/`MEMBER`/`COLLABORATOR`).
- **Comment / label / close**: `gh pr comment`, `gh pr edit --add-label`/`--remove-label`, `gh pr close`.

GitHub shares one number space across issues and PRs, so a bare `#42` may be either - resolve with `gh pr view 42` and fall back to `gh issue view 42`.

## Research record operations

Research workflows use these semantic operations. `Role: Research` in the body is the classification; do not add a triage-state label merely to represent that role.

- **Create Research record**: create an open issue titled `Research: <neutral current-state subject>` with the complete neutral Research packet as its body: `gh issue create --title "Research: ..." --body-file <packet-file>`.
- **Fetch Research record**: `gh issue view <number> --json number,title,body,state,assignees,comments,url`, plus `gh api repos/<owner>/<repo>/issues/<number> --jq .issue_dependencies_summary.blocked_by` for open native blockers. For fallback dependencies, inspect the body `Blocked by:` line and check each referenced issue. The body is the Research packet. A closed record is historical.
- **Revise open Research packet**: first fetch and verify that the record is open and has no Evidence resolution, then replace the body cohesively with `gh issue edit <number> --body-file <packet-file>`.
- **Claim Research record**: first verify that the record is open and has no open blocker. If unassigned, run `gh issue edit <number> --add-assignee @me`; if assigned to the current user, preserve that claim for resumption; if assigned to anyone else, stop. Re-fetch it and begin Research only when the current user is the assignee and its open blocker count remains zero.
- **Resolve Research record**: fetch comments and count top-level `## Evidence` resolution comments. If none exists, add the completed canonical Evidence as one comment with `gh issue comment <number> --body-file <evidence-file>` and re-fetch to verify exactly one exists. If exactly one already exists after a prior close failure, preserve it and do not comment again. Stop on multiple Evidence comments. Close without another comment using `gh issue close <number> --reason completed`. The packet body and this one resolution comment together are the canonical Research record.
- **Create linked Research record**: create the new neutral packet with **Create Research record**, adding `Related Research: #<closed-number>` below `Role: Research`. Then annotate the closed record with a `Follow-up: #<new-number>` comment. Neither operation changes the closed body or its Evidence.
- **Annotate correction**: leave a closed body and its Evidence comment unchanged. Add a comment beginning `Correction:` that states the corrected fact, cites its evidence, and links any replacement Research record.
- **Annotate supersession**: leave the closed record unchanged. Add a comment beginning `Superseded:` that links the newer Research record and explains which still-valid facts it replaces.

New investigation always gets a new open Research record. Never reopen or rewrite a closed Research record.

## Prototype Evidence operation

- **Record Prototype Evidence**: on the open Decision Ticket or Design Artifact that invoked the prototype, add one comment beginning `Prototype Evidence:` with the question, human verdict, and stable throwaway-branch pointer. Prefer a remote branch or commit URL; without a remote, record the repository path, retained branch name, and full commit SHA. Do not copy the prototype into the tracker or production branch. If there is no owning open decision record, return this Evidence packet to the caller and leave the prototype phase incomplete until the human names one.

## When a skill says "publish to the issue tracker"

Create a GitHub issue.

## When a skill says "fetch the relevant ticket"

Run `gh issue view <number> --comments`.

## Wayfinding operations

Used by `/wayfinder`. The **map** is a single issue with **child** issues as tickets.

- **Map**: a single issue labelled `wayfinder:map`, holding the Notes / Decisions-so-far / Fog body. `gh issue create --label wayfinder:map`.
- **Child ticket**: an issue linked to the map as a GitHub sub-issue (`gh api` on the sub-issues endpoint). Where sub-issues aren't enabled, add the child to a task list in the map body and put `Part of #<map>` at the top of the child body. Labels: `wayfinder:<type>` (`research`/`prototype`/`grilling`/`task`). Once claimed, the ticket is assigned to the driving dev.
- **Blocking**: GitHub's **native issue dependencies** - the canonical, UI-visible representation. Add an edge with `gh api --method POST repos/<owner>/<repo>/issues/<child>/dependencies/blocked_by -F issue_id=<blocker-db-id>`, where `<blocker-db-id>` is the blocker's numeric **database id** (`gh api repos/<owner>/<repo>/issues/<n> --jq .id`, _not_ the `#number` or `node_id`). GitHub reports `issue_dependencies_summary.blocked_by` (open blockers only - the live gate). Where dependencies aren't available, fall back to a `Blocked by: #<n>, #<n>` line at the top of the child body. A ticket is unblocked when every blocker is closed.
- **Frontier query**: list the map's open children (`gh issue list --state open`, scoped to the map's sub-issues / task list), drop any with an open blocker (`issue_dependencies_summary.blocked_by > 0`, or an open issue in the `Blocked by` line) or an assignee; first in map order wins.
- **Claim**: `gh issue edit <n> --add-assignee @me` - the session's first write.
- **Resolve**: `gh issue comment <n> --body "<answer>"`, then `gh issue close <n>`, then append a context pointer (gist + link) to the map's Decisions-so-far.
