---
name: red-loop
description: >
  Debugging loop for anything broken, throwing, failing, flaky or slow in Flutter, Next.js, Laravel or other code.
  Builds a fast pass/fail feedback loop first, then ranks falsifiable hypotheses, fixes the root cause, and adds a
  regression test. Use whenever the user says debug, diagnose, "why is this failing", pastes an error or stack trace,
  or says it works locally but not in prod, even if they only ask for a quick fix.
---

# red-loop

The skill is the feedback loop. With a tight pass/fail signal you will find the cause; without one, reading code is guessing.
Read `AGENTS.md` (Profile block) for the stack and test commands. Style: terse, evidence over narrative.

## Redact first
Every command, log and artifact you show must have secrets replaced with `<REDACTED>`. Keep credentials in env vars, never inline. Quote only the log lines that carry signal.

## Phases

Skip a phase only when justified, and say which one and why. An error whose stack trace names the exact faulty line can go straight to Phase 5.

### 1. Build the loop
Create **one command** you have already run that fails on this exact bug. Use `references/loops-by-stack.md` for ready loops per stack. Preference order: failing test, scripted request, CLI with fixture, headless browser, replayed capture, throwaway harness, bisect or differential run, and last a human-in-the-loop script.

Done when the command is **red-capable** (asserts the user's real symptom, not "ran without crashing"), **deterministic**, **fast** (seconds) and **agent-runnable**. Show the command and its redacted output.
- Flaky bug: raise the reproduction rate (loop 100x, add stress, narrow timing) until it is debuggable.
- Slow bug: measure a baseline first (profiler, query plan, timer), then bisect.
- No loop possible: stop. List what you tried and ask for a reproducing environment, a redacted capture, or permission to add temporary instrumentation. Do not theorise without a loop.

### 2. Reproduce and minimise
Confirm the loop shows the **user's** failure, not a neighbouring one. Then cut inputs, config and steps one at a time, re-running after each cut. Stop when every remaining element is load-bearing.

### 3. Hypothesise
Write 3 to 5 ranked hypotheses before testing any. Each must predict something:
`If <X> is the cause, then changing <Y> makes the bug vanish / changing <Z> makes it worse.`
No prediction means it is a hunch, so sharpen or drop it. Show the ranked list to the user, since they often know what was just deployed. Do not block if they are away.

### 4. Instrument
One probe per prediction, one variable at a time. Prefer a debugger or REPL over logs. Tag every temporary log `[RL-xxxx]` so cleanup is one grep. Never "log everything and grep".

### 5. Fix and lock it
State the root cause in one sentence plus its evidence **before** editing. If the fix touches shared code or more than 3 files, pause for approval.
Write the regression test first when a correct seam exists, meaning a test that exercises the real bug pattern at the real call site. Watch it fail, fix, watch it pass, then re-run the Phase 1 loop on the original scenario.
No correct seam is itself a finding: say the architecture prevents locking this bug down.

### 6. Clean up
- [ ] Phase 1 loop is green on the original scenario
- [ ] Regression test passes, or the missing seam is noted
- [ ] `grep -r "RL-"` returns nothing
- [ ] Throwaway harnesses deleted
- [ ] Root cause written for the commit: `fix(scope): <what>` with a body line `Cause: <one sentence>`

## Why
A premature hypothesis anchors every later step. Ranked, falsifiable hypotheses and a red-capable loop remove that anchor and make "fixed" a measurement instead of a feeling.
