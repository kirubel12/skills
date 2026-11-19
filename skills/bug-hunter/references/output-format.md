# Output: bug-hunter

Path: `<notes_dir>/bug-hunter/<YYYY-MM-DD>-<slug>.md`.
Create the file when Phase 1 finishes and append after each phase, so another agent or session can resume from it.
Set `status: resolved` only when the Phase 6 checklist passes.

```markdown
---
skill: bug-hunter
date: <YYYY-MM-DD>
status: open | resolved
topic: <slug>
---

# <short symptom>

## Symptom
<exact error or wrong behavior, redacted>

## Loop
`<the one command>`  -> <redacted result>

## Minimal repro
<smallest scenario that still fails>

## Hypotheses
| # | Prediction ("if X then Y") | Result |
|---|---|---|

## Root cause
<one sentence> Evidence: <what proved it>

## Fix
<files changed, commit if any>

## Regression test
<path, or "no correct seam: <why>">

## Cleanup
- [ ] loop green  - [ ] no BH- tags left  - [ ] harness removed
```
