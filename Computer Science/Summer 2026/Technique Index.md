---
tags:
  - prep/fall2026
  - course/15-451
  - living
---

# Technique Index

Up: [[15-451 Prep]]

The whole point of 15-451 prep in one table. **Add a row every week during the semester.** By finals this is your cheat sheet, already written, in your own words, with no cramming.

The middle column is the one that matters. Anyone can list techniques; the skill is recognizing which surface features of a problem statement point where.

| Technique | Trigger — what in the statement points here | Canonical example | Notes |
|---|---|---|---|
| Interval DP | "optimal way to split / merge / parenthesize a sequence" | matrix chain multiplication | state is `(i, j)` over subintervals |
| Tree DP | structure is a tree, answer at a node depends on children | maximum weight independent set on a tree | usually two states per node: included / excluded |
| Subset DP | small `n` (≤ ~20), answer depends on *which* items chosen | TSP over subsets | `2^n` states, watch the exponent |
| Exchange argument | "prove this greedy is optimal" | interval scheduling by earliest finish | find first difference from OPT, swap, show no worse |
| Potential method | amortized cost over a *sequence* of operations | dynamic array doubling | pick Φ so expensive ops are pre-paid |
| Indicator RVs | "expected number of X" | expected collisions under universal hashing | linearity works *without* independence |
| Min-cut | "minimum removal to separate", bottleneck, partition into two sides | image segmentation, project selection | dual of max-flow — check both directions |
| Bipartite matching | assign each A to at most one B, no conflicts | job assignment | unit capacities, source → A → B → sink |

## Rules for this file

1. One row per technique, never per problem.
2. The trigger column is written in *problem language*, not technique language. "Small n and you're choosing a subset" — not "use bitmask DP."
3. If you had to look a technique up twice, it belongs here.
4. Review the whole table before each quiz. It takes four minutes.
