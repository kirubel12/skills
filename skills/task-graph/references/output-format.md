# Output: task-graph

Path: `<notes_dir>/task-graph/<feature-slug>/`
- `spec.md`: the spec.
- `tasks/NN-<slug>.md`: one file per task, numbered from `01`. Never one combined file.
- Local files are the source of truth when the tracker is `none`. For Linear or Jira, the same files hold the drafts and record the ticket ids.

Update `Status:` in place as work proceeds (`open`, `claimed`, `done`). Append answers or comments at the bottom under `## Notes`.

## spec.md
```markdown
---
skill: task-graph
date: <YYYY-MM-DD>
status: draft | approved
topic: <slug>
---

# <feature>

## Problem
## Goals
## Non-goals
## Acceptance criteria
- [ ] ...
## Risks
## Open questions
## Task graph
| # | Task | Blocked by | Size | One-way door |
|---|---|---|---|---|
```

## tasks/NN-slug.md
```markdown
Status: open | claimed | done
Blocked by: 01, 02        (or "none")
Ticket: <ENG-123 or none>

# <task title>

## Acceptance criteria
- [ ] <pass or fail statement>

## Test approach
<seam, test type, first failing test to write>

## Notes
```
