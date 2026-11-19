---
name: frame-budget
description: >
  Audits Flutter and mobile app code and screens against a frame budget (16ms at 60fps, 8ms at 120fps): jank,
  rebuilds, thumb reach, accessibility, platform adaptivity, state architecture and code debt, with file and line
  references and exact fixes. Use for "audit my app", "why is this janky", "review these screens", "is this
  architecture ready to scale", or when the user shares Flutter code or mobile screenshots, even for one narrow question.
---

# frame-budget

Flutter first. Native Android, iOS and React Native: apply the same lenses and verify against that platform's docs.
Read the `AGENTS.md` Profile block for stack and commands. Style: terse. Checks per lens are in `references/flutter-checks.md`.

## Rules that keep findings honest
- **Every finding has `file:line`.** A suggestion without a location cannot be acted on.
- **Measure performance in profile mode on a real device** (`flutter run --profile`, DevTools). Debug-mode numbers say nothing about release jank. If you cannot measure, label the finding "static, unmeasured".
- **Check APIs against current official docs** (flutter.dev, api.flutter.dev, pub.dev changelog) when web access exists. Otherwise label the suggestion "not verified against current docs". Read the `pubspec.yaml` SDK constraint first so suggestions match the installed version.
- **No hard-coded layout sizes.** Use `LayoutBuilder`, `MediaQuery.sizeOf`, `Flexible`, `Expanded`.
- **Shared-widget blast radius.** If a fix edits a widget used elsewhere, list every other usage (`grep`) before proposing it.
- **Touch only.** No hover-only or mouse-only patterns.

## Pick the mode
- **Quick** (one question): `Finding: <what>. Evidence: <file:line or measurement>. Fix: <code>. Risk: <low/med/high, who else is affected>.`
- **Full** (shared code or "audit"): workflow below.

## Full workflow
1. **Mirror.** State Flutter and Dart versions, state management (Riverpod, BLoC, Provider...), targets, and the device matrix you are assuming (for example "small Android and current iPhone"). Mark guesses "assumed".
2. **Audit** through nine lenses in order: thumb reach, platform adaptivity, hierarchy, interaction and gestures, accessibility, type and color, motion and state, performance, code debt and architecture.
3. **Report**, worst first:

| Lens | Location | Sev | Issue | Evidence | Fix | Risk and blast radius |
|---|---|---|---|---|---|---|

   **P1** crash, data loss or accessibility blocker. **P2** visible jank or friction. **P3** polish.
4. **Plan.** *Agile path*: low-risk fixes, no behavior change, say why it cannot regress (based on the usage scan). *Deep path*: architecture or motion overhaul, with the risk stated.
   **Stop here.** Ask for a path or "proceed".
5. **Implement** after approval. Prefer theme tokens (`ThemeData`, `ColorScheme`, `ThemeExtension`) over per-widget values. Run `flutter analyze` and `flutter test` after edits and report the result.
6. **Close** with three things: one *feel* win (a haptic or a motion tweak), three manual edge cases (text scale 150% on a small screen, slow or offline network, rotate or split-screen), and an offer to scan the rest of the project for the same pattern.

## Done when
- Every finding has a location, evidence and a fix.
- `flutter analyze` is clean after implemented changes.
- Shared-widget changes list their other usages.

## Save output

Write the result to `<notes_dir>/frame-budget/` (default `.agent-notes/`; `notes_dir` in the AGENTS.md Profile overrides it). Filename and template: `references/output-format.md`.
- One file per run. Never overwrite an earlier run's file.
- Create the folder on first write. Do not mention a missing folder.
- Redact secrets before writing.
- Finish with one line: `Saved: <path>`.
