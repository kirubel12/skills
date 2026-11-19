# Output: peer-sync

Path: `<notes_dir>/peer-sync/<YYYY-MM-DD>.md`. If one exists for today, add a suffix: `-2`.
Use names, not email addresses.

```markdown
---
skill: peer-sync
date: <YYYY-MM-DD>
status: current
topic: <slug>
---

# Peer sync <date>

Anchor: <date and what it is>   Fetched: <time>   Base: <branch>
Visibility: pushed commits only. Local and uncommitted work on other machines is not visible.

## Activity
| Person | Branch | PR | Commits | Summary | Flags |
|---|---|---|---|---|---|

## Overlap with my work
| File | Mine | Theirs (person, branch) | Conflict probe |
|---|---|---|---|

## Suggested
- <one action per branch>
```
