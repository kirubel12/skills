# Host commands, tracker links, commit spec

Set `BODY_FILE=<notes_dir>/shipwright/<branch-slug>.body.md` (written at the plan gate, see `output-format.md`).

## Detect the host
`git remote get-url origin`: contains `github.com` means GitHub; contains `gitlab` (including self-hosted) means GitLab; contains `bitbucket.org` means Bitbucket. Anything else: ask once.
Base branch: `git symbolic-ref --short refs/remotes/origin/HEAD`, else the profile's `default_branch`.

## GitHub (`gh`)
```bash
git push -u origin "$BRANCH"
gh pr create --base "$BASE" --head "$BRANCH" --title "$TITLE" --body-file "$BODY_FILE"   # add --draft for drafts
gh pr view --web          # open it
```
If `gh pr create` fails because GraphQL is blocked (some restricted or cloud environments), use the REST API, which `gh api` supports. Add `-F draft=true` for a draft:
```bash
gh api repos/<owner>/<repo>/pulls -f title="$TITLE" -f head="$BRANCH" -f base="$BASE" -F body=@"$BODY_FILE" --jq '.html_url'
```
If `gh` is missing or unauthenticated, print the title and body and the compare URL `https://github.com/<owner>/<repo>/compare/<base>...<branch>?expand=1`.

## GitLab (`glab`)
Self-hosted: `glab` reads the host from the remote, or set `GITLAB_HOST`.
```bash
git push -u origin "$BRANCH"
glab mr create --source-branch "$BRANCH" --target-branch "$BASE" --title "$TITLE" --description "$(cat "$BODY_FILE")" --remove-source-branch   # add --draft for drafts
```
No `glab`: push with options, `git push -o merge_request.create -o merge_request.target="$BASE" origin "$BRANCH"`, then open the URL GitLab prints.

## Bitbucket Cloud (no official PR CLI)
Parse `<workspace>/<repo>` from the remote URL. Use the REST API; read credentials from environment variables, never write them in commands or files. Check Bitbucket's current docs for the supported auth method (app passwords are being retired in favor of API tokens), and use whichever the user has set up.
```bash
git push -u origin "$BRANCH"
curl -sS -X POST "https://api.bitbucket.org/2.0/repositories/$WORKSPACE/$REPO/pullrequests" \
  -u "$BITBUCKET_EMAIL:$BITBUCKET_API_TOKEN" -H "Content-Type: application/json" \
  -d "$(jq -n --arg t "$TITLE" --arg d "$(cat "$BODY_FILE")" --arg s "$BRANCH" --arg b "$BASE" \
      '{title:$t, description:$d, source:{branch:{name:$s}}, destination:{branch:{name:$b}}, close_source_branch:true}')"
```
Fallback with no credentials: print title and body and the URL `https://bitbucket.org/<workspace>/<repo>/pull-requests/new?source=<branch>&dest=<base>`.

## Branch naming
Use the profile's `branch_format`, default `<type>/<ticket-or-slug>`, for example `feat/ENG-123-login-flow` or `fix/cart-total-rounding`. Lowercase, hyphens, no spaces.

## Linking a ticket
| Tracker | Branch | Commit / PR |
|---|---|---|
| none | slug only | no ticket line |
| Linear | include the key (`eng-123`), or Linear's copied branch name | PR body line `Closes ENG-123` (or `Refs ENG-123` if it should not auto-close). Needs Linear's GitHub or GitLab integration enabled |
| Jira | include the key (`PROJ-123`) | key in the PR title or first commit line (`PROJ-123`) so Jira's dev panel links it; smart-commit commands only if the team uses them |

## Conventional commits
`<type>(<scope>): <subject>` with optional body and footers.
Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`.
Breaking change: `!` after the type or scope and a `BREAKING CHANGE:` footer.
Scope is a feature or module (`auth`, `cart`, `api`). Subject: imperative, lowercase start, no trailing period, 72 characters or fewer.
Body explains why. For fixes add a `Cause:` line with the root cause.
