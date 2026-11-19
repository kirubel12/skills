# Web checks (Next.js and React)

Measure first. Lab: Lighthouse or DevTools Performance on a throttled mid-range device profile, plus `next build` output for bundle sizes. Field: real-user data if the project has it. Targets (good): LCP 2.5s or less, INP 200ms or less, CLS 0.1 or less. If you cannot measure, label the finding "static, unmeasured".

## 1. Reach and ergonomics
Targets 44px+ on touch, primary actions reachable on small screens, no hover-only controls.

## 2. Platform fit
Respect system dark mode, reduced motion (`prefers-reduced-motion`), and native form controls where they work.

## 3. Hierarchy, 4. interaction, 6. type and color
Same as the UI checklist: one primary action, defined states, a type scale, theme tokens.

## 5. Accessibility
Semantic HTML before ARIA, labels on inputs, visible focus, contrast 4.5:1, keyboard order, alt text, 200% zoom.

## 7. Motion and state
Loading, empty, error states for every async view. Animate `transform` and `opacity`, not layout properties.

## 8. Performance
- **LCP:** the hero image uses `next/image` with `priority` and correct `sizes`. Fonts via `next/font`. No render-blocking third-party scripts (`next/script` with a strategy).
- **JS cost:** keep `"use client"` at the leaves, not at layout roots. Check the bundle analyzer for large imports, dynamic-import heavy widgets, and avoid shipping server-only libraries to the client.
- **INP:** split long tasks, defer non-urgent state updates (`useTransition`, `useDeferredValue`), debounce expensive handlers, virtualize long lists.
- **Re-renders:** find them with the React Profiler before adding `memo`. Fix state placement first.
- **CLS:** reserve dimensions for images, embeds and ads. No content injected above existing content.
- **Data:** avoid request waterfalls (fetch in parallel), cache with intent, stream with Suspense where it helps.

## 9. Code debt and architecture
Server and client boundary is deliberate, one source of truth per piece of state, no duplicated fetch logic, types without `any`.
