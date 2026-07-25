---
tags:
  - prep/fall2026
  - course/15-451
  - course/21-259
week: 2
dates: 2026-08-03 → 2026-08-09
hours: 10
status: not-started
---

# Week 2 — Data Structures and Amortized

Up: [[Fall 2026 Prep]] · Prev: [[Week 1 - DP to Reflex]] · Next: [[Week 3 - Hashing and Probability]]

## 15-451 — Segment trees + amortized analysis, 6h

Source: cp-algorithms.com. See [[Resources]].

- [ ] Segment tree from scratch: point update, range query. **Write it, don't copy it** (1.5h) #course/15-451
- [ ] Lazy propagation (1.5h) #course/15-451
- [ ] 4–5 segment tree problems (1h) #course/15-451
- [ ] Amortized analysis: aggregate method, accounting method, potential method (1h) #course/15-451
- [ ] The classic set: binary counter, dynamic array doubling, stack with multipop, queue from two stacks (1h) #course/15-451

> [!warning] Potential functions are where people lose whole evenings
> Drill these until choosing Φ feels like a *choice between candidates* rather than a guess. The tell that you're not there yet: you can follow a potential-function proof but couldn't have produced the Φ yourself.

## 21-259 — Ch. 12–13, plus orientation on cylindrical/spherical, 4h

21-122 already covered vectors and the dot product, so only part of ch. 12 is new.

- [ ] Cross product — the actual new operation (0.5h) #course/21-259
- [ ] Lines and planes in 3D; quadric surfaces, recognize from equation and sketch (1h) #course/21-259
- [ ] Vector-valued functions, arc length, curvature (ch. 13) (1.5h) #course/21-259
- [ ] Cylindrical and spherical: **orientation only** (1h) #course/21-259

> [!note] Ch. 13 is 122's parametric curves with a z
> **r**(t) = ⟨x(t), y(t), z(t)⟩ is a parametric curve. Arc length ∫|**r**′(t)| dt is the 21-122 formula with one more term under the radical. If [[Week 1 - DP to Reflex|Week 1's]] parametrization drill went well, this chapter is mostly notation.

> [!important] Orientation, not mastery — this is deliberate
> You've never seen cylindrical or spherical, and that's **normal**. They're Stewart 15.7–15.8, taught around week 9 of the semester. Nobody arrives having done them.
>
> Spend one hour to see the structure, then stop:
> - Cylindrical **is** polar. Same r and θ, with z riding along untouched. That's the entire idea.
> - Spherical introduces ρ and φ, and the volume element ρ² sin φ dρ dφ dθ.
> - Note the φ-vs-θ convention trap now, so it isn't a surprise in October.
>
> Do **not** drill these. Pre-learning material you won't be taught for nine weeks decays. The drill happens in-semester, and it'll be cheap *because Week 1 made polar reflexive*.

> [!tip] Cheapest chapter in the course, and cheaper still for you
> Ch. 12 is near-pure mechanics with no conceptual overhead, and you've already seen vectors and the dot product in 122. Clear it fast and you buy effectively free weeks in September.

## Retro

- Hours actually spent:
- What was harder than expected:
- What to carry into Week 3:
