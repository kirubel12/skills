---
name: tdd-loop
description: >
  Builds a feature or task test-first in small red-green-refactor slices, choosing the seam and test type for the
  stack (Flutter, Next.js, Laravel, others). Use for "implement this", "add this feature", "write tests for", "TDD
  this", or when starting a task from task-graph. Prefer it over writing code first and tests afterwards.
---

# tdd-loop

Read the `AGENTS.md` Profile block (stack, test command) and the newest note in `<notes_dir>/task-graph/`. Pick the stack pack in `references/stacks/`. Style: terse.

## Workflow

1. **Pick the task.** The next unblocked task from `task-graph`, or restate the user's request as a task. List its acceptance criteria as **behaviors** (what a user or caller observes), not implementation steps. Order them from simplest to richest.
2. **Choose the seam.** Test through the public interface where the behavior is visible (a widget, a route, a service method). The stack pack lists the usual test types. If the project has no test setup, stop and ask once whether to add the minimum.
3. **Run the loop, one behavior at a time:**
   1. **Red.** Write one failing test. Run it and show that it fails **for the expected reason** (not a typo or missing import).
   2. **Green.** Write the least code that passes. Run the test.
   3. **Refactor.** Clean up with the suite green. Run the suite again.
4. **Do not write all the tests first.** Writing every test up front tests imagined behavior and locks in structure before you have learned anything. One test, then one implementation, then the next.
5. **Mock only at system boundaries** (network, clock, filesystem, payments). Never mock the code under test or its private collaborators.
6. **Finish.** Run lint, types and the full suite from the profile. Report real results. Update the task `Status:`. Offer a conventional commit per green slice, and do not commit unasked.

## Rules and reasons
- A test that has never been seen failing proves nothing, so always show the red run.
- Assert on observable behavior. Tests tied to private internals break on every refactor and stop protecting you.
- If a behavior cannot be tested at any reasonable seam, say so. That is an architecture finding worth recording.

## Done when
- Every acceptance criterion has a test that was seen failing and is now passing.
- Lint, types and the full suite are green, or the failures are reported.
- The note lists the tests added and anything left untested, with the reason.

## Save output

Write the result to `<notes_dir>/tdd-loop/` (default `.agent-notes/`; `notes_dir` in the AGENTS.md Profile overrides it). Filename and template: `references/output-format.md`.
- One file per run. Never overwrite an earlier run's file.
- Create the folder on first write. Do not mention a missing folder.
- Redact secrets before writing.
- Finish with one line: `Saved: <path>`, then `Next: diff-review`.
