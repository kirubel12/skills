# Output: diff-review

Path: `<notes_dir>/diff-review/<branch-slug>.md`. One file per review.

```markdown
---
skill: diff-review
date: <YYYY-MM-DD>
status: ready | ready-with-notes | fix-first
topic: <slug>
---

# Review: <branch> into <base>

Diff: <N files, +A -D>

## Checks
| Command | Result |
|---|---|

## Acceptance criteria
| Criterion | Met | Code | Test |
|---|---|---|---|

## Findings (introduced by this diff)
| Sev | Location | Issue | Evidence | Fix |
|---|---|---|---|---|

## Pre-existing (not blocking)
- <file:line> <one line>

## Verdict
<ready | ready with notes | fix first>: <one line reason>
```
