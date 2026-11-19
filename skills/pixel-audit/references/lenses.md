# Lens checklists

Audit in this order. Numbers are thresholds, flag anything below them.

## 1. Visual hierarchy
- One clear primary action per screen; one dominant focal point.
- At most 3 to 4 distinct text sizes per screen; size and weight carry rank, not color alone.
- Gestalt proximity: related items closer to each other than to unrelated items. Spacing on a 4 or 8pt grid.
- Scan path matches task order (F or Z pattern for content; top-to-bottom for forms).

## 2. Responsiveness
- Check narrow phone (360 wide), large phone, tablet, desktop. No horizontal scroll, no clipped text.
- Layout changes at breakpoints, not just scaling. No fixed widths on text containers.
- Flutter: `LayoutBuilder` / `MediaQuery.sizeOf`. Web: container queries or breakpoints, fluid type via `clamp()`.

## 3. Accessibility and hit targets (WCAG 2.2 AA)
- Text contrast 4.5:1 (large text 3:1). UI component and icon contrast 3:1.
- Touch targets: 44x44pt iOS, 48x48dp Material, never below 24x24 CSS px (WCAG 2.5.8) with spacing.
- Visible focus indicator; keyboard order matches visual order; status never conveyed by color alone.
- Labels for every control and image; error text says what to do. Support 200% text zoom without loss.

## 4. Platform consistency
- iOS: Human Interface Guidelines (large titles, tab bar, swipe-back, SF-style type). Android: Material 3 (top app bar, navigation bar, tonal surfaces). Web: platform conventions of the browser.
- Hold the design to the platform it ships on. Mixed idioms are a P2.

## 5. Interaction and feedback
- Every interactive element defines default, hover (pointer only), focus, pressed, disabled, loading, error and empty states.
- Response to input within about 100ms; show progress for waits over about 400ms.
- Destructive actions are confirmable or undoable. Gestures have a visible alternative.

## 6. Conversion logic (landing, checkout, signup only)
- One primary CTA above the fold, specific verb label. Remove competing links near it.
- Reduce fields; show price or cost before commitment; trust cues near the ask.
- Frame as a hypothesis with a metric, never as a promised lift.

## 7. Typography
- Body 16px / 1rem minimum on web, 14sp+ on mobile. Line height 1.4 to 1.6. Line length 45 to 75 characters.
- Consistent scale (for example 1.2 ratio). At most 2 families. Weight contrast of at least 200 between levels.

## 8. Color
- Semantic roles (primary, surface, on-surface, success, warning, error), not raw hex per component.
- Roughly 60/30/10 neutral/secondary/accent. Verify dark mode contrast separately.
- Do not rely on color alone to carry meaning.

## Principles to cite
Hick's Law (choices slow decisions), Fitts's Law (size and distance of targets), Gestalt proximity and similarity, Miller's 7+-2 (chunking), Jakob's Law (users expect familiar patterns), WCAG 2.2.
