# Output: repo-scout

Path: `<notes_dir>/repo-scout/overview.md`. Update in place on every run; set `date` to the scan date.
`AGENTS.md` keeps the short Profile that agents auto-read. This note holds the longer map that does not belong there.

```markdown
---
skill: repo-scout
date: <YYYY-MM-DD>
status: current
topic: <slug>
---

# Overview: <project>

## Stack
<framework, versions, package manager, state management>

## Commands
| Purpose | Command | Status |
|---|---|---|
| test | `<cmd>` | verified / unverified |

## Architecture
<= 15 lines: entry points, layers, data flow, where features live.

## Hot spots
<top paths by 90-day churn, with the commit count>

## Open gaps
<fields left as unknown, and what would resolve them>
```
