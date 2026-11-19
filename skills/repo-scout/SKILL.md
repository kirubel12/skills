---
name: repo-scout
description: >
  Project kickoff. Detects the stack (Flutter, Next.js, Laravel, other) and writes AGENTS.md with a verified project
  profile (commands, git host, commit style, tracker, hot spots) that every skill here reads. Run when starting a
  project, opening an unfamiliar repo, or when AGENTS.md is missing or stale. Also use when the user says "set up this
  repo for agents", "onboard me to this codebase", or "map this codebase".
disable-model-invocation: true
---

# repo-scout

Write the project profile once so no other skill has to interview the user again.

Style: terse, no emoji, no praise. Expand only if the user says "explain".
Questions: ask only for what cannot be detected, one at a time, each with a recommended default the user can accept with "ok".

## Workflow

1. **Explore.** Follow `references/stack-detection.md`. Also read existing `AGENTS.md`, `CLAUDE.md`, `.cursorrules`, `README.md`.
   For an existing repo, find hot spots: `git log --since=90.days --name-only --pretty=format: | sort | uniq -c | sort -rn | head -15`. Recent churn shows where the work is.
2. **Mirror.** Print what you found in under 10 lines: stack, commands, host, branch, hot spots, gaps. This is the confirmation step.
3. **Fill gaps.** Ask one question per unknown field, with a default. Fields: one-line purpose, tracker (`none` | `linear` | `jira` and key prefix), git host if there is no remote, paths agents must not touch.
4. **Draft.** Fill `references/profile-template.md`. Show the draft and let the user edit it before anything is written.
5. **Write.**
   - `AGENTS.md` holds the content (Claude Code, Codex, Cursor and others all read it).
   - `CLAUDE.md` contains only `@AGENTS.md`.
   - If `CLAUDE.md` already has real content, offer to move it into `AGENTS.md` (ask once). If `AGENTS.md` exists, update the profile block in place and leave the user's other sections alone.
   - New empty project: propose the minimal folder layout for the stack, scaffold nothing without a yes.
6. **Verify.** Run each detected install, lint and test command in its fastest form. Mark it `verified` or `unverified`. A command nobody has seen work is a guess, so label it.
7. **Report** in three lines: files written, commands verified, open gaps.

## Done when
- `AGENTS.md` has no placeholders (unknowns say `unknown`).
- `CLAUDE.md` points to it.
- Every command carries a verified or unverified mark.
- The profile is under about 80 lines. Link to docs instead of copying them.

## Why these rules
- Only project-specific facts belong in the profile. Generic advice costs context on every turn and the agent already knows it.
- Hot spots come from git history because architecture diagrams go stale and commit churn does not.
