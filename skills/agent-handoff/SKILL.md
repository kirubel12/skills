---
name: agent-handoff
description: >
  Compacts the current session into a short handoff note so a fresh agent (Claude Code, Codex, Cursor, a new session)
  can continue the work: goal, state, decisions, files, working commands, blockers, next steps and which skills to run.
  Use when switching agents or sessions, before a context reset, or when the user says "hand this off", "save progress",
  "I'll continue tomorrow".
disable-model-invocation: true
---

# agent-handoff

Write the note a new agent needs to resume without asking you anything. If the user passed a focus ("next session is
about X"), tailor the note to it. Style: terse. Under about 60 lines.

## Workflow

1. **Collect** from the conversation and the repo: `git status`, the branch, recent commits, and the newest notes in `<notes_dir>/*/`.
2. **Do not duplicate** what other artifacts already hold (specs, task files, ADRs, notes, issues, commits, diffs). Link them by path or URL.
3. **Write the note** using the template in `references/output-format.md`. Capture what is not written down anywhere else: decisions and the reasons for them, what was tried and failed, and what is half done.
4. **Verify the note is resumable.** Every command in it must be one you saw work, every path must exist, and the next step must be doable without more context. Fix any that fail.
5. **Redact** secrets, tokens, personal data and internal hostnames.
6. **Hand over** a one-line starter prompt the user can paste into the next session: `Read <path> and continue from "Next steps".`

## Done when
- A new agent could start from "Next steps" using only the note and the files it links.
- Nothing in the note duplicates another artifact, and nothing sensitive is in it.

## Prompts that work

Name the skill and include what the next session will do and which agent will do it.
- "Use agent-handoff. The next session in Codex will finish the tests for task 02."
- "Use agent-handoff. I am stopping for today, save everything I need to resume."

## Save output

Write the result to `<notes_dir>/agent-handoff/` (default `.agent-notes/`; `notes_dir` in the AGENTS.md Profile overrides it). Filename and template: `references/output-format.md`.
- One file per run. Never overwrite an earlier run's file.
- Create the folder on first write. Do not mention a missing folder.
- Redact secrets before writing.
- Finish with one line: `Saved: <path>`, then the starter prompt.
