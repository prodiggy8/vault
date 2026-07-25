---
tags:
  - prep/fall2026
  - course/15-451
  - course/21-259
week: 4
dates: 2026-08-17 → 2026-08-23
hours: 10
status: not-started
---

# Week 4 — Greedy Proofs and Flow Modeling

Up: [[Fall 2026 Prep]] · Prev: [[Week 3 - Hashing and Probability]] · Next: [[Week 5 - Calibration]]

## 15-451 — Greedy + flows, 6h

Two genuinely separate skills. Don't blur them.

### Greedy is a *writing* skill

- [ ] Exchange arguments: 4 greedy correctness proofs, written out in full prose (1.5h) #course/15-451

"Prove your greedy algorithm is optimal" is a thing you rehearse cold, like a scale. The structure is nearly always the same — assume an optimal solution differing from greedy, find the first difference, swap, show you haven't made it worse. Write five of them and it stops costing you an hour on the exam.

### Flows is a *modeling* skill

- [ ] Max-flow / min-cut, Ford–Fulkerson, Edmonds–Karp (1h) #course/15-451
- [ ] Kleinberg & Tardos ch. 7 modeling problems: bipartite matching, disjoint paths, project selection, baseball elimination (3.5h) #course/15-451

> [!important] Weight modeling far above algorithms
> Nobody loses time *running* Edmonds–Karp. They lose it failing to see that the problem was a flow problem at all. The 3.5h on modeling matters more than everything else in this section combined.

## 21-259 — Bounds and regions, 4h

Stewart ch. 15. This is where [[Week 1 - DP to Reflex|Week 1's]] polar work pays off — protect that ordering.

- [ ] 15 problems in Cartesian: **set up the integral and stop.** Choose the order of integration deliberately (1.5h) #course/21-259
- [ ] 10 problems where the right move is polar. Practice *recognizing* it — circular boundary, or x² + y² in the integrand — not just executing it (1.5h) #course/21-259
- [ ] 5 stretch problems in cylindrical/spherical, worked solutions to hand. Exposure, not mastery (1h) #course/21-259

> [!tip] Why "set up and stop" is the right drill
> It isolates the skill that actually costs you time — sketch the region, choose the order, pick the coordinate system — from the grinding you already automated. Doing full problems here means spending 80% of your minutes rehearsing a skill you have.
>
> And per the [[21-259 Prep]] note: the failure mode in this course is a *wrong setup*, not bad arithmetic.

## Retro

- Hours actually spent:
- What was harder than expected:
- What to carry into Week 5:
