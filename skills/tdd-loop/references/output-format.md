# Output: tdd-loop

Path: `<notes_dir>/tdd-loop/<task-slug>.md`. Create when the first test goes red and append per cycle.

```markdown
---
skill: tdd-loop
date: <YYYY-MM-DD>
status: open | done
topic: <slug>
---

# <task>

Task: <path to the task-graph file, or "ad hoc">

## Cycles
| # | Behavior | Test (file::name) | Red reason | Green |
|---|---|---|---|---|

## Suite
`<command>` -> <redacted result>

## Not tested
<behavior and why>

## Commits (if made)
<hash subject>
```
