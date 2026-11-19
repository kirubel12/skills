---
name: diff-review
description: >
  Reviews your own diff before it becomes a PR, on two axes: standards (project conventions, correctness, security,
  secrets, performance, error handling) and spec (does it meet the task's acceptance criteria). Use for "review my
  changes", "review before I merge", "is this ready for a PR", "check my diff", or automatically before shipwright.
---

# diff-review

Find what a reviewer would find, before they see it. Read the `AGENTS.md` Profile block (stack, default branch, commands), the newest note in `<notes_dir>/tdd-loop/` and the matching `task-graph` task for acceptance criteria. Use the stack pack in `references/stacks/`. Style: terse.

## Workflow

1. **Scope the diff.** `git diff <default_branch>...HEAD --stat`, then the full diff. Include uncommitted changes if there are any. Note generated or vendored files and skip reviewing them line by line.
2. **Run the checks** from the profile (lint, types, tests) and report the real results.
3. **Review on two axes:**
   - **Spec:** for each acceptance criterion, name the code and the test that satisfy it, or mark it unmet.
   - **Standards:** correctness and edge cases, error handling, security (injection, authz, secrets, unsafe deserialization), data and migration safety, performance (N+1, needless rebuilds, blocking calls), tests present for new behavior, breaking API changes, and consistency with `AGENTS.md` conventions.
4. **Verify each finding** by reading the surrounding code before reporting it. Drop anything you cannot ground in a `file:line`. Mark whether the diff **introduced** the problem or it **pre-existed** (report pre-existing ones separately and briefly).
5. **Report**, worst first:

| Sev | Location | Issue | Evidence | Fix |
|---|---|---|---|---|

   **P1** bug, security hole or data loss. **P2** likely problem or missing test. **P3** polish.
6. **Verdict:** `ready`, `ready with notes` or `fix first`, with the reason in one line.
7. **Fix only when asked.** Offer to apply the P1 and P2 fixes.

## Done when
- Every acceptance criterion is marked met or unmet.
- Every finding has a location and evidence, and the introduced and pre-existing ones are separated.
- Check results and the verdict are stated.

## Why verify first
An unverified finding wastes the author's time and trains them to ignore the reviewer. A short list of grounded findings beats a long list of guesses.

## Save output

Write the result to `<notes_dir>/diff-review/` (default `.agent-notes/`; `notes_dir` in the AGENTS.md Profile overrides it). Filename and template: `references/output-format.md`.
- One file per run. Never overwrite an earlier run's file.
- Create the folder on first write. Do not mention a missing folder.
- Redact secrets before writing.
- Finish with one line: `Saved: <path>`, then `Next: shipwright`.
