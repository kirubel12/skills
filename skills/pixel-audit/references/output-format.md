# Output: pixel-audit

Path: `<notes_dir>/pixel-audit/<screen-slug>-<YYYY-MM-DD>.md`. Full mode only; Quick mode answers in chat unless the user asks to save it.
Write after the audit table, then append the chosen path and the edits actually applied.

```markdown
---
skill: pixel-audit
date: <YYYY-MM-DD>
status: open | implemented
topic: <slug>
---

# <screen>

## Observed
Platform, stack, grid, palette, type scale (mark guesses "assumed").

## Context
Purpose, goal, audience.

## Findings
| Lens | Sev | Issue (observed value) | Principle | Fix |
|---|---|---|---|---|

## Plan
Fast path: ...
Deep path: ...
Chosen: <path or pending>

## Applied
<tokens changed, files edited>

## Quick win
<the 10-minute fix>
```
