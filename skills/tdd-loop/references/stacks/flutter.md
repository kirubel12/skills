# Flutter test seams

| Behavior lives in | Test type | Notes |
|---|---|---|
| Pure logic, notifiers, blocs | Unit test (`test`), `flutter test` | Override providers or inject repositories. Use `mocktail` or fakes at the data boundary |
| A screen or widget | Widget test (`flutter_test`) | `pumpWidget`, find by text, key or semantics, `tester.tap`, `pump` / `pumpAndSettle`. Wrap with the app's theme and providers |
| A full user journey on a device | `integration_test/` | `flutter test integration_test -d <device>`. Keep few, slow |
| Visual regressions | Golden tests | Sparingly, on stable components only |

Run: `flutter test --plain-name "<name>"` for one test, `flutter analyze` for static checks.
Traps: forgetting `await tester.pump()` after state changes, real timers in tests (use `fakeAsync`), network in widget tests (inject a fake client).
