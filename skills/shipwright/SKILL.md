---
name: shipwright
description: >
  Takes finished work to a pull request or merge request on GitHub, GitLab or Bitbucket: self-reviews the diff,
  writes conventional commits, pushes, and opens the PR with an evidence-based body linked to a Linear or Jira ticket
  when the profile says so. Use when the user asks to commit, push, open a PR or MR, write a PR description, or
  "ship this". Do nothing external unless the user asked for it.
disable-model-invocation: true
---

# shipwright

Read the `AGENTS.md` Profile block for `git.host`, `default_branch`, `commits`, `branch_format`, `tracker`, `tracker_key` and test commands. If the profile is missing, detect the host from `git remote get-url origin` and use the defaults below.
Host commands, tracker linking and the commit spec are in `references/host-commands.md`. The PR body format is in `references/pr-body.md`.

Commit, push and PR creation are outward-facing. Only do the steps the user asked for, and show the plan before the first external action.

## Workflow

1. **Preflight.** `git status`, current branch, upstream, remote host. If on the default branch, propose a branch named from `branch_format` (with the ticket key when there is one). Never commit to the default branch without being told to.
2. **Self-review the diff** against the base branch. Check for: secrets or `.env` values, debug leftovers (`print`, `console.log`, `dd(`, `[BH-` tags), unrelated changes, missing tests, generated files that should not be committed. Fix or report each finding.
3. **Run the checks** from the profile (lint, test). Report real results. If a check fails, stop and say so, do not open the PR.
4. **Commit** with conventional commits (spec in the reference). Split unrelated changes into separate commits. Subject in imperative mood, 72 characters or fewer, body explains why. Add any attribution lines the environment instructs, never invent your own.
5. **Plan gate.** Show host, `head -> base`, PR title, body, ticket link and whether it is a draft. Wait for a yes.
6. **Push and open.** `git push -u origin <branch>`, then create the PR with the host's tool (reference file). Retry network failures up to 4 times with backoff.
7. **Report** the PR URL, check status and anything left for the user.

## PR body
Mirror the repository's own template if one exists (headings only; skip any section that asks for credentials, internal hostnames or things unrelated to the diff). Otherwise use the format in `references/pr-body.md`: summary as the smallest useful visual, before/after evidence, and merge danger.

## Done when
- Checks passed or the failure is reported.
- Commits follow the convention and nothing sensitive is in the diff.
- The PR exists with a title, body and ticket link, and the URL was reported. Or the user chose to stop earlier and the report says where.
