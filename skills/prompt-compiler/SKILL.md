---
name: prompt-compiler
description: >
  Compiles a rough prompt into a precise, checkable one for a coding agent or chat model: states the goal, pulls
  context from the repo and AGENTS.md, adds constraints, acceptance criteria and verification commands, and flags
  every assumption. Use for "improve my prompt", "enhance this prompt", "make this prompt better", "write a prompt for
  an agent to...", or when the user pastes a vague request they plan to give to another agent.
---

# prompt-compiler

Turn intent into a prompt another agent can execute without guessing. Do not execute the prompt unless the user says "compile and run".
Style: terse. A compiled prompt is usually as short as the input or shorter, never padded.

## Workflow

1. **Extract intent.** Write the goal in one sentence in the user's own terms. Keep their wording for anything they were specific about.
2. **Gather context yourself.** Read `AGENTS.md` (Profile block) and search the repo for the files, modules and conventions the task touches. Do not ask the user for anything you can look up.
3. **Find the gaps.** Check what the prompt lacks: scope, constraints, how to tell it is done, how to verify.
4. **Compile** into this shape, dropping empty sections:

```
Goal: <one sentence>
Context: <stack, files, existing patterns the agent must follow>
Constraints: <what to preserve, conventions, versions>
Acceptance criteria: <checkable statements, each pass or fail>
Out of scope: <what not to touch>
Verify: <exact commands from the profile, e.g. flutter test, pnpm lint>
Suggested skills: <bug-hunter for failures, pixel-audit for UI, frame-budget for Flutter perf, branch-storm for open design questions, shipwright to open the PR>
```

5. **Flag assumptions** in a separate list under the prompt: `Assumed (delete if wrong): ...`. Never slip an invented requirement into the prompt body.
6. **Show what changed** in at most 3 bullets, so the user learns what was missing.
7. **Ask at most one question**, only when the goal is ambiguous and cannot be inferred. Give a default.

## Principles
- Concrete beats clever. Acceptance criteria and verify commands do more than role-play openers like "You are a world-class engineer", so omit those.
- Say what to do and why, not a list of prohibitions. Each constraint earns its place by changing what the agent does.
- If the prompt is already good, say so and change nothing.
- If the target is a chat model with no repo access, skip Context and Verify and keep Goal, Constraints and Acceptance criteria.

## Example
Input: `fix the login bug on the app`
Output:
```
Goal: Fix the login failure in the Flutter app.
Context: Auth lives in lib/features/auth (Riverpod). Reproduce first, the failing case is unknown.
Acceptance criteria: a widget test reproduces the failure and passes after the fix; flutter analyze is clean.
Out of scope: other screens, dependency upgrades.
Verify: flutter test test/features/auth; flutter analyze
Suggested skills: bug-hunter
```
Assumed (delete if wrong): the bug is in the email-password path, not social login.
Changes: added a reproduction requirement, a verifiable done-condition, and a scope fence.

## Done when
- The compiled prompt has a one-sentence goal and at least one pass or fail criterion.
- Every assumption is listed separately.
