---
name: peer-sync
description: >
  Catches you up on what teammates did in a shared repo: what they committed and pushed to the main branch, which
  branches and PRs they published since your last commit, a summary per person, and which of their changes overlap or
  conflict with yours. Use for "what did my partner do", "what changed since my last commit", "did anyone push",
  "catch me up", or before starting work or pushing in a repo with more than one developer.
---

# peer-sync

Answer "what happened in this repo while I was working?" without pulling, merging or changing anything.
Read the `AGENTS.md` Profile block (default branch, git host). Style: terse. Commands and edge cases are in `references/commands.md`.

## What you can and cannot see
- **Visible:** commits that a teammate **pushed**, on any branch, plus PRs or MRs if the host CLI works.
- **Not visible:** commits that exist only on their machine, uncommitted work, and stashes. Never say a teammate "did nothing"; say "pushed nothing".
State this limit in the report.

## Workflow

1. **Find the anchor.** Identity from `git config user.email`. The anchor is the date of your last commit on any branch. If the user gives another anchor ("since Monday", "since commit abc", "what did Sam do"), use that and say so.
2. **Fetch.** `git fetch --all --prune` updates remote-tracking refs only. Say that it changes no branch, working tree or stash. Never run pull, merge or rebase here.
3. **Collect** teammates' pushed commits since the anchor, per remote branch (commands in the reference). Exclude your own, bots and merge commits, and group the rest by person, then by branch.
4. **Add PR state** when `gh`, `glab` or a Bitbucket token works: which are open, merged or closed, with reviewers. If not available, say "PR state unavailable" and continue.
5. **Summarize each person** in one to three lines by intent, using conventional-commit types and the areas touched (top directories). Flag these when present: breaking changes (`!`), migrations, lockfile or dependency changes, config or env changes, large deletions, changes to files in the hot spots list.
6. **Check overlap with your work.**
   - File overlap: your changed files (branch diff plus uncommitted) against theirs.
   - Conflict probe on committed state: `git merge-tree --write-tree --name-only HEAD <their-branch>`. Exit code 1 lists conflicting files. It does not touch the working tree.
   - Uncommitted overlap cannot be probed, so list the shared files and say so.
7. **Recommend** one action per branch: nothing to do, pull the base first, rebase later, or talk to a named person about a named file.

## Report shape

```
Since your last commit (<date>): <N> commits by <M> people. Pushed only, not local work.
<person>: <summary> [branch, PR state]
Overlap with your work: <files, conflict yes/no>
Suggested: <one action>
```

## Done when
- Anchor, fetch and the visibility limit are stated.
- Every teammate with pushed commits appears with a summary.
- Overlap is reported with the conflict-probe result, or the reason it could not run.
- Nothing was pulled, merged, rebased or modified.

## Privacy
Use names, not email addresses, in the saved note.

## Save output

Write the result to `<notes_dir>/peer-sync/` (default `.agent-notes/`; `notes_dir` in the AGENTS.md Profile overrides it). Filename and template: `references/output-format.md`.
- One file per run. Never overwrite an earlier run's file.
- Create the folder on first write. Do not mention a missing folder.
- Redact secrets before writing.
- Finish with one line: `Saved: <path>`, then `Next: tdd-loop` (or `bug-hunter` if the conflict needs fixing).
