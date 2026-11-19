# Output: frame-budget

Path: `<notes_dir>/frame-budget/<scope-slug>-<YYYY-MM-DD>.md`. Full mode only; Quick mode answers in chat unless the user asks to save it.
Write after the audit table, then append the chosen path, edits applied and the `flutter analyze` result.

```markdown
---
skill: frame-budget
date: <YYYY-MM-DD>
status: open | implemented
topic: <slug>
---

# <scope>

## Observed
Flutter and Dart versions, state management, targets, device matrix (mark guesses "assumed").

## Findings
| Lens | Location (file:line) | Sev | Issue | Evidence | Fix | Risk and blast radius |
|---|---|---|---|---|---|---|

## Measurements
<profile-mode numbers and device, or "static, unmeasured">

## Plan
Agile path: ...
Deep path: ...
Chosen: <path or pending>

## Applied
<edits, `flutter analyze` result>

## Manual checks
1. text scale 150% on a small screen  2. slow or offline network  3. rotate or split-screen
```
