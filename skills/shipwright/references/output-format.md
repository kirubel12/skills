# Output: shipwright

Two files per branch, in `<notes_dir>/shipwright/`:
- `<branch-slug>.body.md`: the exact PR body, nothing else. Pass it to the host with `--body-file` or the API.
- `<branch-slug>.md`: the record of the run.

Write both at the plan gate, before anything external happens, so the user reviews real files. Update the record with the PR URL after creation.

```markdown
---
skill: shipwright
date: <YYYY-MM-DD>
status: planned | opened
topic: <slug>
---

# <PR title>

Host: github | gitlab | bitbucket
Base <- head: <base> <- <branch>
Ticket: <KEY or none>
Draft: yes | no

## Checks
| Command | Result |
|---|---|

## Commits
<hash subject, one per line>

## Self-review
<findings and what was done about each>

## Result
URL: <PR or MR URL, once opened>
```
