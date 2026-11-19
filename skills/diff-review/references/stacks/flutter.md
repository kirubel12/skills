# Flutter review checks

- `BuildContext` used after an `await` without a `mounted` check.
- Controllers, streams and subscriptions not disposed. `setState` after dispose.
- Work inside `build()` (parsing, sorting, creating controllers). Missing `const`. Rebuild scope too wide.
- `ListView` of unknown length without `.builder`. Unbounded constraints (`ListView` inside `Column`).
- Hard-coded sizes or colors instead of theme tokens. Text that overflows at 150% text scale.
- Secrets or API keys in source or `--dart-define` values committed.
- Null-safety escapes (`!`, `late` without initialization guarantees), platform-channel results used unchecked.
- New dependency: maintained, license, size. Run `flutter analyze`.
