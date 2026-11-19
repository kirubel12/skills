# Stack detection

Check these files first. Read only what exists.

| Signal | Stack | Then read |
|---|---|---|
| `pubspec.yaml` | Flutter / Dart | SDK constraint, `flutter:` section, state management deps (riverpod, flutter_bloc, provider, get), `analysis_options.yaml`, `test/`, `integration_test/` |
| `package.json` with `next` | Next.js | `next` version, `app/` vs `pages/`, TypeScript, `scripts`, lockfile (pnpm, npm, yarn, bun), ORM (prisma, drizzle), auth, Tailwind |
| `composer.json` with `laravel/framework` | Laravel | Framework and PHP version, `artisan`, `phpunit.xml` or Pest, queue/cache drivers in `.env.example`, front-end stack (Inertia, Livewire, Blade) |
| `android/` + `ios/` | Flutter or React Native | Disambiguate by `pubspec.yaml` vs `package.json` |
| `.github/workflows`, `.gitlab-ci.yml`, `bitbucket-pipelines.yml` | CI | The exact lint/test/build commands CI runs. These are the most trustworthy commands |

## Git host from remote
Run `git remote get-url origin`.
- contains `github.com` -> `github`
- contains `gitlab` (including self-hosted) -> `gitlab`
- contains `bitbucket.org` -> `bitbucket`
- no remote -> ask once, default `github`

Default branch: `git symbolic-ref --short refs/remotes/origin/HEAD`, else `main`.

## Existing agent files
Look for `AGENTS.md`, `CLAUDE.md`, `.cursorrules`, `.cursor/rules`, `.github/copilot-instructions.md`. Merge their content rather than discarding it, and tell the user what you merged.

## Command sources (priority order)
1. CI workflow steps
2. `scripts` in `package.json`, `composer.json` scripts, `Makefile`
3. Stack defaults (`flutter analyze`, `flutter test`, `php artisan test`, `npm run lint`) marked `unverified` until run
