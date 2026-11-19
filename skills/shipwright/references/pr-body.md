# PR body format

Use when the repository has no PR template. Skip preambles, keep prose short, use the project's own domain terms.

````markdown
## Summary

<smallest visual that makes the point: diff-sketch, call tree, file tree, or mermaid>

## Evidence

- **Before:** <failing test output / screenshot / measurement>
  **After:** <passing test output / screenshot / measurement>

## Merge danger

**Door:** one-way | two-way
**Blast radius:** <one phrase: who or what breaks if this is wrong>

Ticket: Closes ENG-123   <!-- only when tracker is linear or jira -->
````

## Summary: pick the smallest view
- Logic change: a few lines of pseudocode.
- Runtime flow: a call tree.
- UI structure: a component or widget tree.
- Refactor or layout: a shallow file tree.
- Components talking to each other: a mermaid sequence diagram (GitHub and GitLab render it; Bitbucket does not, so use a tree there).
- Small change in an existing shape: a `diff` block. Show the whole block only when most of it is new.

## Evidence
Real output beats claims. Visual change: screenshots before and after (best). Otherwise show the exact test that now fails then passes, or console or profiler output. Do not paste secrets.

## Merge danger
A **two-way door** can be rolled back cheaply. A **one-way door** cannot (destructive migration, deleted data, published API, store release). Name the blast radius so a reviewer knows where to look: layout shift, consumer breakage, query load, mobile responsiveness.

Format adapted from the show-me PR format by Dex Horthy (HumanLayer).
