# Feedback loops and usual suspects by stack

Use the commands from the AGENTS.md profile when they exist. These are starting points.

## Flutter

| Bug type | Loop |
|---|---|
| Wrong UI state, overflow, missing widget | Widget test: `flutter test test/path_test.dart --plain-name "<name>"`; assert with finders, use `tester.pump` / `pumpAndSettle` |
| Logic or state bug | Unit test on the notifier / bloc / provider; override dependencies |
| Device-only or navigation bug | `integration_test/` driven by `flutter test integration_test -d <device>` |
| Static suspicion | `flutter analyze` (fast, deterministic) |
| Jank / slow frames | **Profile mode on a real device** (`flutter run --profile`) plus DevTools Performance. Debug-mode timing is not evidence |
| Build / plugin failure | `flutter clean && flutter pub get`; then Android `cd android && ./gradlew assembleDebug --stacktrace`, iOS `pod install --repo-update` |

Usual suspects: `setState` or `notifyListeners` during build; `BuildContext` used after an `await` (check `mounted`); unbounded constraints (`ListView` in `Column` without `Expanded`); missing `dispose()`; stale keys in lists; null from platform channels; async races in `initState`; text scale or small screens causing overflow; plugin version vs Gradle or Xcode version.

## Next.js

| Bug type | Loop |
|---|---|
| API route / server action | Scripted `curl` against `pnpm dev` (or the profile's dev command) asserting status and body |
| Rendering / hydration | Playwright script asserting DOM and console errors (hydration warnings show as console errors) |
| Works in dev, breaks in prod | `next build && next start`, then the same script. Dev and prod differ in caching, minification and static generation |
| Logic bug | Unit test on the function; mock the fetch boundary |

Usual suspects: hydration mismatch (`Date.now`, `Math.random`, `window` access, locale formatting during render); server vs client component boundary (`"use client"` missing, hooks in a server component); stale data from fetch or route caching (check revalidate, `dynamic`, `cache` settings for the installed Next version, since defaults changed between majors); env vars (`NEXT_PUBLIC_` prefix, build-time vs runtime); edge runtime missing a Node API; middleware matcher; image domain config; wrong `params` handling for the installed version.

## Laravel

| Bug type | Loop |
|---|---|
| HTTP behaviour | Feature test with Pest or PHPUnit: `php artisan test --filter=<name>` |
| Data / query bug | `php artisan tinker` for exploration, then encode in a test with factories |
| Queue / job | `php artisan queue:work --once` with `QUEUE_CONNECTION=sync` for a deterministic run |
| Slow request | Query log or Debugbar / Telescope to count queries and find N+1; compare before and after counts |

Usual suspects: stale config or route cache (`php artisan optimize:clear`); N+1 queries (`with()`); mass assignment (`$fillable`); validation vs authorisation (Form Request `authorize`); migration order or applied-migration edits; `.env` differences; queue worker running old code (restart it after deploys); timezone and casting; CSRF on non-GET calls. Logs: `storage/logs/laravel.log`.
