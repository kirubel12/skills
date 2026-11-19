# Output: branch-storm

Path: `<notes_dir>/branch-storm/<topic-slug>.md`.
Write it when the recommendation is final (Explore) or when the user confirms the decision list (Grill).

```markdown
---
skill: branch-storm
date: <YYYY-MM-DD>
status: open | decided
topic: <slug>
---

# <topic>

Mode: Explore | Grill

## Problem
<one sentence>

## Assumptions
| Assumption | Type (fact / assumption / opinion) |
|---|---|

## Options   (Explore)
| Option | <criterion 1> | <criterion 2> | <criterion 3> |
|---|---|---|---|

## Settled decisions   (Grill)
1. <decision> - <why>

## Recommendation
Recommendation: <option> because <reason>
Runner-up: <option> wins if <condition>
Cheapest test: <experiment>
What would change my mind: <observable>

## Open questions
```

## Promote to an ADR (only when asked or when all three hold)
Offer, never create unasked, a record at `docs/adr/NNNN-<slug>.md` when a decision is **hard to reverse**, **surprising without context** and the **result of a real trade-off**. Number = highest existing + 1. Body is a title and 1 to 3 sentences: context, decision, why. Skip easy-to-reverse or obvious decisions.
