---
name: pixel-audit
description: >
  Lints a UI design the way a linter checks code: reviews screenshots, mockups, Figma exports or frontend code
  (Flutter, Next.js/React/Tailwind, Blade) for hierarchy, accessibility, platform fit, interaction states and
  typography, with P1-P3 severity and exact fixes. Use for "review this design", "critique my UI", "make this look
  professional", "is this color okay?", or whenever the user shares a screen image or UI code, even for one narrow question.
---

# pixel-audit

Read the `AGENTS.md` Profile block for the stack so fixes use the right token system. Style: terse, specific, no praise.
Lens checklists with numbers are in `references/lenses.md`. Read it before auditing.

## Pick the mode
- **Quick** (a specific question, e.g. "is this contrast okay?"): answer in this shape, then add up to 2 other P1 issues you noticed.
  `Verdict: <ok / not ok>. Why: <principle or WCAG criterion>. Fix: <exact value or code>.`
- **Full** (screenshot or code with no narrow question, or the user asks for an audit): run the workflow below.

## Full workflow

1. **Mirror.** In 4 lines state what you observe: platform (web, iOS, Android, dashboard), stack, grid (4/8pt?), palette, type scale. Anything unclear is labelled "assumed". Never assume the grid or stack silently.
2. **Context.** Screen purpose, user goal and audience. Take them from the prompt or the profile. Ask one question only if the answer would change a verdict, with a default.
3. **Audit** through the lenses in order: hierarchy, responsiveness, accessibility and hit targets, platform consistency, interaction states and feedback, typography, color. Add conversion logic only for landing, checkout or signup screens.
4. **Report** as a table, worst first:

| Lens | Sev | Issue (observed, with value) | Principle | Fix (exact value or code) |
|---|---|---|---|---|

   Severity: **P1** breaks usability or accessibility, **P2** visible friction or unprofessional feel, **P3** polish.
5. **Plan.** Two paths: *Fast* (low-risk fixes that ship today) and *Deep* (structural changes for long-term quality). Group tasks as visual polish, flow, and (if relevant) conversion.
   **Stop here.** Ask which path, or "proceed".
6. **Implement** after approval. Convert fixes into the project's tokens (Flutter: `ColorScheme`, `TextTheme`, a `ThemeExtension` for spacing; web: Tailwind theme or CSS variables). Apply precise edits to the files when you have code access, otherwise give copy-paste edits with exact values (`padding: 12px 24px`, weight 600). Tie each edit to the issue it fixes.
7. **Close** with one 10-minute fix worth 80% of the impact. For conversion screens add one A/B hypothesis with a measurable metric.

## Done when
- Every issue cites an observed value and a principle (WCAG 2.2, HIG, Material 3, Gestalt, Fitts, Hick).
- No finding uses a vague adjective. "Cluttered" becomes "6 competing 16px+ text styles above the fold".

## Why
Vague critique cannot be acted on or verified. Observed value plus principle plus exact fix can be checked by the next person.
