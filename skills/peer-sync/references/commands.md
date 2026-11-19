# peer-sync commands

Tested with git 2.43. `merge-tree --write-tree` needs git 2.38 or newer.

```bash
ME_NAME=$(git config user.name); ME_EMAIL=$(git config user.email)
BASE=$(git symbolic-ref --short refs/remotes/origin/HEAD 2>/dev/null | sed 's#^origin/##'); BASE=${BASE:-main}
ANCHOR_DATE=$(git log --all --author="$ME_EMAIL" -1 --format=%cI)   # or the user's own anchor
git fetch --all --prune
```

## Teammates' pushed commits since the anchor, per branch
On the base branch, take every commit since the anchor. On other branches, take only commits not yet on the base.
```bash
for b in $(git for-each-ref --format='%(refname:short)' refs/remotes/origin | grep -v '/HEAD$'); do
  if [ "$b" = "origin/$BASE" ]; then r="origin/$BASE"; else r="origin/$BASE..$b"; fi
  git log $r --since="$ANCHOR_DATE" --no-merges --format="$b|%h|%an|%ae|%cI|%s"
done | awk -F'|' -v me="$ME_EMAIL" '$4 != me'
```
Fields: branch, short hash, author name, author email, commit date, subject. Filter bots by name or email pattern (`[bot]`, `dependabot`, `renovate`).

## Files per person or branch
```bash
git diff --stat "origin/$BASE"..."origin/<branch>"            # size of a branch
git diff --name-only "origin/$BASE"..."origin/<branch>"       # files it touches
git log origin/<branch> --since="$ANCHOR_DATE" --author="<name>" --name-only --format= | sort -u
```

## My changes
```bash
{ git diff --name-only "origin/$BASE"...HEAD; git diff --name-only HEAD; } | sort -u   # committed on my branch + uncommitted
```

## Conflict probe (committed state only, read-only)
```bash
git merge-tree --write-tree --name-only HEAD origin/<branch>; echo "exit=$?"
```
Exit 0: merges cleanly. Exit 1: output ends with the conflicting file names and `CONFLICT` lines. The working tree and index are untouched.

## Pull request state
```bash
gh pr list --state all --search "updated:>=<YYYY-MM-DD>" --json number,title,author,state,headRefName,url
glab mr list --all --updated-after <ISO-date>
```
Bitbucket Cloud: `GET https://api.bitbucket.org/2.0/repositories/<workspace>/<repo>/pullrequests?state=OPEN` with credentials from environment variables. Check Bitbucket's current docs for the auth method.

## Edge cases
- **No commits by you yet:** ask for an anchor (date, commit or "last 7 days").
- **Several emails or names for one person:** group by name and mention the aliases.
- **Squash or rebase merges:** hashes differ from the branch commits, so match by subject and diff, not by hash.
- **Author date vs commit date:** `--since` uses the commit date, so rebased commits can look newer than they are.
- **Shallow clone:** history may be too short. Deepen with a bounded `git fetch --depth=<n>` and say so.
- **Large repos:** limit to `origin/$BASE` plus branches with commits in the window.
