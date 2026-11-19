# Output: release-gate

Path: `<notes_dir>/release-gate/<version-or-date>.md`.

```markdown
---
skill: release-gate
date: <YYYY-MM-DD>
status: go | go-with-risks | no-go
topic: <slug>
---

# Release <version>

Target: <store | web | package | backend>
Previous: <tag>    Commits since: <N>
Suggested bump: <major | minor | patch>

## Checklist
| Item | Status (pass / fail / unknown) | Evidence |
|---|---|---|

## Changelog (draft)
### Features
### Fixes
### Breaking

## One-way doors
- <item> (owner)

## Rollback
<steps and estimated time>

## Verdict
<GO | GO with risks | NO-GO>: <one line>
```
