# Scope

A small, curated set of skills that cover the engineering workflow from idea to release. It stays small on purpose: every skill description sits in the agent's context all the time.

## The bar for changes
A change is accepted only if it clears both parts:
1. **Observed failure.** It describes something that went wrong in a real session: what you ran, what the skill did, what you expected. "It would be nicer if..." does not clear this.
2. **Fits the design.** It is not a one-person preference, a config option, or a branch for one tool. Those belong in your own `AGENTS.md` or a fork.

## New skills
A new skill is added only when the behavior cannot be composed from the existing ones. First try extending a skill or adding a stack pack.

## Stack packs
Stack knowledge lives in `references/stacks/<stack>.md` inside the skills that need it. A pack for a new stack (Python, Go, Rails, Java) is welcome: copy an existing pack as the template and keep it to checks that changed an outcome in a real session.
