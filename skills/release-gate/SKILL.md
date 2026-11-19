---
name: release-gate
description: >
  Go or no-go check before a release: version bump, changelog drafted from commits, CI status, migrations, env and
  config changes, dependency and secret scan, one-way doors and a rollback plan, for mobile stores, web deploys and
  backends. Use for "are we ready to release", "pre-release checklist", "ship to production", "cut a release", or
  after shipwright merges. Never tags, publishes or deploys unless the user asks.
---

# release-gate

A release is the point where mistakes get expensive and hard to undo. Read the `AGENTS.md` Profile block (stack, default branch, commands) and the latest `diff-review` note. Use the stack pack in `references/stacks/`. Style: terse.

## Workflow

1. **Define the release.** Target (store build, web deploy, package, backend), the previous version (`git describe --tags --abbrev=0`) and the commits since it.
2. **Gather evidence** and fill the checklist. Mark each item `pass`, `fail` or `unknown`, never assumed:

| Item | How to check |
|---|---|
| CI green on the release commit | Host UI or CLI (`gh run list`, `glab ci status`); report real status |
| Tests, lint, types, build | Profile commands, run them |
| Version and changelog | Suggest the bump from commit types: `feat` is minor, `fix` is patch, `!` or `BREAKING CHANGE` is major. Draft the changelog from the commit subjects, grouped by type |
| Migrations and data changes | List them. Say whether each is reversible and safe on large tables |
| Config and env | New or changed variables, and whether production has them |
| Dependencies and secrets | The stack's audit command, plus a scan of the diff for keys and tokens |
| Review status | Latest `diff-review` verdict |
| Rollback | State the exact steps, and how long they take |

3. **Flag one-way doors:** destructive migrations, deleted data, published APIs, store submissions. Each needs a named owner's yes.
4. **Verdict:** `GO`, `GO with risks` (list them) or `NO-GO` (list blockers). State the reason in one line.
5. **Stop.** Offer the next actions (bump version, create tag, trigger deploy) and do them only on an explicit yes.

## Done when
- Every checklist item is pass, fail or unknown with its evidence.
- One-way doors and the rollback plan are written down.
- A verdict is stated, and nothing was tagged, published or deployed unasked.

## Why unknown is allowed
A confident "pass" nobody verified is how bad releases ship. Say `unknown` and make it a blocker or an accepted risk.

## Save output

Write the result to `<notes_dir>/release-gate/` (default `.agent-notes/`; `notes_dir` in the AGENTS.md Profile overrides it). Filename and template: `references/output-format.md`.
- One file per run. Never overwrite an earlier run's file.
- Create the folder on first write. Do not mention a missing folder.
- Redact secrets before writing.
- Finish with one line: `Saved: <path>`, then `Next: peer-sync` or the next feature in task-graph.
