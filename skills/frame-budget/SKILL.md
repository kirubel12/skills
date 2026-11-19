---
name: frame-budget
description: >
  Audits app UI performance and quality against a budget (16ms per frame at 60fps and 8ms at 120fps on mobile, Core
  Web Vitals on web): jank, rebuilds, reach, accessibility, platform fit, state architecture and code debt, with file
  and line references and exact fixes. Flutter and Next.js packs. Use for "audit my app", "why is this janky or slow",
  "review these screens", "is this architecture ready to scale", or when the user shares UI code or screenshots.
---

# frame-budget

Read the `AGENTS.md` Profile block (stack, commands) and pick the pack: `references/stacks/flutter.md` or `references/stacks/web.md`. No pack for the stack: use the lenses below with the platform's own docs. Style: terse.

## Rules that keep findings honest
- **Every finding has `file:line`.** A suggestion without a location cannot be acted on.
- **Measure before you judge.** Mobile: profile mode on a real device (`flutter run --profile`, DevTools). Web: Lighthouse or DevTools on a throttled profile. Debug or dev-mode numbers say nothing about release behavior. If you cannot measure, label the finding "static, unmeasured".
- **Check APIs against current official docs** when web access exists, using the installed version from the lockfile or `pubspec.yaml`. Otherwise label the suggestion "not verified against current docs".
- **No hard-coded layout sizes.** Use the platform's responsive primitives.
- **Shared-component blast radius.** If a fix edits a widget or component used elsewhere, list every other usage (`grep`) before proposing it.
- **Match the input model.** Touch-first on mobile. No hover-only patterns where touch is possible.

## Pick the mode
- **Quick** (one question): `Finding: <what>. Evidence: <file:line or measurement>. Fix: <code>. Risk: <low/med/high, who else is affected>.`
- **Full** (shared code or "audit"): workflow below.

## Full workflow
1. **Mirror.** State framework and version, state management, targets, and the device or browser matrix you assume. Mark guesses "assumed".
2. **Audit** through nine lenses in order: reach, platform fit, hierarchy, interaction and gestures, accessibility, type and color, motion and state, performance, code debt and architecture. The pack says what to check for each.
3. **Report**, worst first:

| Lens | Location | Sev | Issue | Evidence | Fix | Risk and blast radius |
|---|---|---|---|---|---|---|

   **P1** crash, data loss or accessibility blocker. **P2** visible jank or friction. **P3** polish.
4. **Plan.** *Agile path*: low-risk fixes, no behavior change, say why it cannot regress (based on the usage scan). *Deep path*: architecture or motion overhaul, with the risk stated.
   **Stop here.** Ask for a path or "proceed".
5. **Implement** after approval. Prefer theme tokens over per-component values. Run the profile's lint and test commands (for Flutter `flutter analyze` and `flutter test`) and report the result.
6. **Close** with one *feel* win (a haptic, a motion tweak, a perceived-speed fix), three manual edge cases (large text, slow or offline network, small screen or rotation), and an offer to scan the rest of the project for the same pattern.

## Done when
- Every finding has a location, evidence and a fix.
- Lint and tests are clean after implemented changes.
- Shared-component changes list their other usages.

## Save output

Write the result to `<notes_dir>/frame-budget/` (default `.agent-notes/`; `notes_dir` in the AGENTS.md Profile overrides it). Filename and template: `references/output-format.md`.
- One file per run. Never overwrite an earlier run's file.
- Create the folder on first write. Do not mention a missing folder.
- Redact secrets before writing.
- Finish with one line: `Saved: <path>`, then `Next: diff-review`.
