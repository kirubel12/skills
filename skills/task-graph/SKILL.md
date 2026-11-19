---
name: task-graph
description: >
  Turns a settled decision or idea into a short spec and an ordered set of thin end-to-end tasks with blocking edges
  and checkable acceptance criteria, as local markdown files or draft Linear/Jira tickets. Use for "write a spec",
  "break this down", "plan this feature", "create tickets", or right after a branch-storm decision, before any code is written.
---

# task-graph

Turn "we decided X" into work an agent or a teammate can pick up cold. Read the `AGENTS.md` Profile block (stack, `tracker`, `tracker_key`) and the newest note in `<notes_dir>/branch-storm/` first. Style: terse.

## Workflow

1. **Anchor.** State the goal in one sentence and list the open questions. Ask only a question that blocks the spec, one at a time, with a default.
2. **Spec.** Keep it short: problem, goals, non-goals, acceptance criteria for the whole feature, risks. Skip sections with nothing to say.
3. **Slice into tracer bullets.** Each task is a **thin vertical slice** that runs end to end (UI to data, or request to response) and can be demonstrated alone. Avoid layer-by-layer tasks ("build the whole database", then "build the whole UI"), because nothing works until the last one lands. Task 1 is the thinnest working path.
4. **Per task:** title, acceptance criteria written as pass or fail statements, test approach (which seam, which test type), estimated size (fits one session or split it), and `Blocked by`.
5. **Check the graph.** No cycles. List the **frontier**: tasks with no open blockers. Mark risky or one-way-door tasks.
6. **Gate.** Show the spec and task table. Wait for a yes or edits.
7. **Write.** Tracker `none`: files under the notes folder (see the reference). Tracker `linear` or `jira`: put draft tickets in the note, and create real tickets only if a tracker tool is available and the user confirms. Use `tracker_key` for ids.

## Done when
- Every task has acceptance criteria a test or a command can verify.
- The graph has no cycles and task 1 is an end-to-end slice.
- The frontier is listed, so the next agent knows where to start.

## Why thin slices
Early end-to-end feedback exposes wrong assumptions while they are cheap. Horizontal tasks hide integration failures until the end.

## Save output

Write the result to `<notes_dir>/task-graph/` (default `.agent-notes/`; `notes_dir` in the AGENTS.md Profile overrides it). Filename and template: `references/output-format.md`.
- One file per run. Never overwrite an earlier run's file.
- Create the folder on first write. Do not mention a missing folder.
- Redact secrets before writing.
- Finish with one line: `Saved: <path>`, then `Next: tdd-loop`.
