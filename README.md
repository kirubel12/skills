# Skills

Agent skills for everyday Flutter, Next.js and Laravel work. They follow the open `SKILL.md` format, so they work in Claude Code, Codex, Cursor and other agents that support skills.

## Skills

| Skill | Use it to | Trigger |
|---|---|---|
| `repo-scout` | Detect the stack and write `AGENTS.md` with a verified project profile. Run once per project | Manual |
| `bug-hunter` | Debug with a red/green feedback loop, ranked hypotheses and a regression test | Automatic |
| `branch-storm` | Brainstorm options or stress-test a plan, ending in a recommendation | Automatic |
| `pixel-audit` | Review a UI design or frontend code: hierarchy, accessibility, platform fit | Automatic |
| `frame-budget` | Audit Flutter and mobile apps: jank, rebuilds, accessibility, architecture | Automatic |
| `shipwright` | Commit, push and open a PR or MR on GitHub, GitLab or Bitbucket | Manual |
| `prompt-compiler` | Turn a rough prompt into a precise, checkable one | Automatic |

"Manual" skills have side effects, so they only run when you call them.

## Start a new project

1. Install the skills (below).
2. Run `repo-scout` once. It writes `AGENTS.md` (read by every agent) and a `CLAUDE.md` that points to it.
3. Every other skill reads the Profile block in `AGENTS.md`, so none of them re-interview you about stack, commands, git host, commit style or tracker.

```mermaid
flowchart LR
    A[Install skills] --> B[repo-scout]
    B --> C[(AGENTS.md profile)]
    C --> D[bug-hunter]
    C --> E[branch-storm]
    C --> F[pixel-audit / frame-budget]
    C --> G[prompt-compiler]
    C --> H[shipwright]
```

## Installation

All skills:

```bash
npx skills@latest add kirubel12/skills
```

One skill:

```bash
npx skills@latest add kirubel12/skills/bug-hunter
```

## Where output goes

Every skill saves its result as a markdown file in the project, in a folder named after the skill. A later session or another agent can read it and pick up where the last one stopped.

```text
AGENTS.md                      short profile, auto-read by every agent (repo-scout)
CLAUDE.md                      contains only: @AGENTS.md
.agent-notes/
  repo-scout/overview.md       stack, commands, architecture, hot spots (updated in place)
  bug-hunter/2026-11-19-cart-total.md
  branch-storm/offline-sync.md
  pixel-audit/checkout-2026-11-19.md
  frame-budget/product-list-2026-11-19.md
  shipwright/feat-cart-fix.md          run record
  shipwright/feat-cart-fix.body.md     exact PR body
  prompt-compiler/add-search-2026-11-19.md
docs/adr/0001-<slug>.md        only for hard-to-reverse decisions (branch-storm offers it)
```

- Folders are created on first write. One file per run; earlier runs are never overwritten (`overview.md` is the one exception, updated in place).
- Secrets are redacted before anything is written.
- Change the location with `notes_dir` in the `AGENTS.md` profile. `repo-scout` asks once whether to commit the notes or git-ignore them.
- Throwaway artifacts (prototypes, large logs, HTML reports) belong in the OS temp directory, not the repo.

## Working style

- Terse by default. Say "explain" or "go deep" for more.
- A skill asks at most one question at a time, and always offers a default you can accept with "ok".
- Heavy audits have a quick mode for narrow questions and a full mode for reviews, and the full mode stops for your decision before implementing.

## Evals

`evals/evals.json` has realistic prompts and expectations for each skill, plus prompts that should and should not trigger it. Run each prompt with and without the skill and compare.

## Credits

Built from ideas in public skill collections, including the lazy, per-purpose file conventions (`docs/adr/`, scratch folders, temp-dir artifacts): the feedback-loop-first debugging approach and the writing guidance in Matt Pocock's `mattpocock/skills`, the PR body format from Dex Horthy's show-me skill (HumanLayer), and the skill-writing guidance in Anthropic's `skill-creator`.

## License

MIT
