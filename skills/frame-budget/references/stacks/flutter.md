# Flutter checks per lens

## 1. Thumb reach
- Primary actions in the bottom third on large phones; avoid top-corner-only critical actions.
- Targets at least 48x48dp with spacing. Use `kMinInteractiveDimension`.

## 2. Platform adaptivity
- `.adaptive` constructors (`Switch.adaptive`, `CircularProgressIndicator.adaptive`), platform back gesture (iOS swipe-back, Android predictive back), safe areas (`SafeArea`, view insets), `Theme.of(context).platform` for idiom switches.
- Material 3 on Android, Cupertino conventions where the iOS feel matters.

## 3. Hierarchy
- One primary action per screen; typography from `TextTheme`, not ad-hoc `TextStyle`.

## 4. Interaction and gestures
- Every tappable shows pressed feedback (`InkWell`, `Ink`, or `Material`). Gestures have a visible alternative.
- Debounce repeated taps on network actions; disable buttons while loading.

## 5. Accessibility
- `Semantics` labels on icon buttons and images; `ExcludeSemantics` for decoration.
- Text scale: test at 150 to 200% (`MediaQuery.textScalerOf`). No fixed-height text containers.
- Contrast 4.5:1; never color alone for state. Test with TalkBack and VoiceOver.

## 6. Type and color
- Colors from `ColorScheme`; dark theme supported; no raw `Color(0x...)` scattered in widgets.

## 7. Motion and state
- Implicit animations (`AnimatedContainer`, `AnimatedSwitcher`) before explicit controllers; dispose every controller.
- Loading, empty, error and success states exist for every async screen. Haptics via `HapticFeedback` for key confirmations.

## 8. Performance (measure in profile mode)
- Rebuild scope: push `setState` down, split widgets, use `const` constructors, `select` on providers, `BlocSelector`.
- Lists: `ListView.builder` or `SliverList` for long lists, stable `key`s, `itemExtent` when fixed height.
- Avoid work in `build()`: parsing, sorting, creating controllers. Cache with providers or `late final`.
- Costly effects: `Opacity` on large trees (prefer `AnimatedOpacity` or `FadeTransition`), `saveLayer` triggers (clips, shadows on many items), unbounded `Image` decode (`cacheWidth` / `cacheHeight`).
- `RepaintBoundary` only where the profiler shows repaint cost. Heavy compute: `compute()` or an isolate.
- Startup: lazy init, defer plugins, avoid awaiting everything in `main()`.

## 9. Code debt and architecture
- Business logic out of widgets; one source of truth per piece of state; repository layer between UI and data.
- Async hygiene: no `BuildContext` use after `await` without `mounted`; cancel streams in `dispose`.
- Dependency health: outdated or discontinued packages (`flutter pub outdated`), analyzer lints enabled (`analysis_options.yaml`), tests cover the state layer.
