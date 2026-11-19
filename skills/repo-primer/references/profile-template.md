# AGENTS.md template

Fill every field. Write `unknown` instead of guessing. Delete sections with nothing project-specific to say.

````markdown
# <project name>

<one line: what this project is and who uses it>

## Profile

```yaml
stack: flutter | nextjs | laravel | other:<name>
package_manager: <pub | pnpm | npm | yarn | bun | composer>
git:
  host: github | gitlab | bitbucket
  default_branch: main
  commits: conventional
  branch_format: <type>/<ticket-or-slug>     # e.g. feat/ENG-123-login-flow
tracker: none | linear | jira
tracker_key: <ENG | PROJ | none>
commands:                                    # mark each: verified | unverified
  install: "<cmd>"   # verified
  dev:     "<cmd>"   # unverified
  test:    "<cmd>"   # verified
  lint:    "<cmd>"   # verified
  build:   "<cmd>"   # unverified
style: terse
```

## Architecture
<= 10 lines: entry points, state management, data flow, where features live.

## Hot spots
Top areas by 90-day commit churn (paths only).

## Do not touch
Generated files, vendored code, migrations already applied.

## Gotchas
Project-specific traps only. Example: "Run `dart run build_runner build` after editing models".

## Agent skills
Installed via the skills CLI. These skills read the Profile block above.
````
