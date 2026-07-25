---
tags:
  - prep/fall2026
  - course/15-451
  - course/21-259
week: 1
dates: 2026-07-27 → 2026-08-02
hours: 12
status: not-started
---

# Week 1 — DP to Reflex

> [!warning] Heaviest week, deliberately
> 12h. If something has to slip, **slip the 451 DP problems into Week 2 — never the polar repair.**

Up: [[Fall 2026 Prep]] · Prev: — · Next: [[Week 2 - Data Structures and Amortized]]

## 15-451 — Dynamic programming, 6h

Source: Erickson, *Algorithms*, ch. 3. See [[Resources]].

- [ ] Read Erickson ch. 3 (2h) #course/15-451
- [ ] 12–15 problems, deliberately hitting every shape the syllabus names — knapsack, DAG, subset, prefix, interval, tree (4h) #course/15-451
- [ ] Fill [[DP Problem Log]] as you go — fold this into the problem time, don't budget it separately #course/15-451

> [!important] The log is the deliverable, not the solutions
> You are not building a set of solved problems. You are building a mapping from *problem surface features* → *DP shape* → *state variable*. Six months from now you won't remember any individual problem; you will remember that "optimal way to split a sequence" means interval DP.

**Rules.** Twenty minutes minimum before you look at a solution — look earlier and you learn nothing but the illusion of understanding. When you do look, close it and re-derive from scratch before moving on.

**Exit condition.** Given a fresh problem, you can name the shape and the state variable in under 60 seconds. Not solve it. Name it.

## 21-259 — Polar and parametric repair, 6h

> [!danger] This is the most important block in the entire prep plan
> More important than anything on the 451 side. Not because it's hard — because it's a **prerequisite** gap. A missing unit costs you that unit. A missing prerequisite makes every later unit harder to absorb. Polar feeds ch. 15.3, cylindrical, spherical, and all of ch. 16.
>
> Fix it now and cylindrical costs you twenty minutes in October. Arrive with it shaky and you'll be learning three things at once under deadline.

### What 259 actually wants from polar

259 uses maybe a third of what 21-122 covered. Notably **absent**: graphing limaçons and roses. 259 regions are almost always disks, annuli, sectors, and the occasional cardioid.

- [ ] Conversion mechanics: x = r cos θ, y = r sin θ, r² = x² + y², and the quadrant trap in θ = arctan(y/x) (0.5h) #course/21-259
- [ ] The handful of curves that do show up: r = a, θ = c, r = 2a cos θ (circle *through the origin* — the one that trips everyone), cardioid r = a(1 + cos θ) (1h) #course/21-259
- [ ] **Region description drill — the money skill.** Given a shaded region, write θ-bounds *then* r-bounds. 15 regions: disk, off-center disk, annulus, sector, region between two circles, inside cardioid / outside circle (2h) #course/21-259
- [ ] Powers of sin and cos — these *are* the polar integrals. ∫cos²θ dθ over [0, 2π] until the half-angle identity is recall, not derivation (1h) #course/21-259

### What 259 actually wants from parametric

Given a geometric description, write **r**(t) and the t-range. That's nearly the whole ask for ch. 13 and most of ch. 16.

- [ ] 12 parametrizations: segment A → B, circle in a given plane, ellipse, helix, curve of intersection of two surfaces (1.5h) #course/21-259

> [!check] Exit conditions
> - Shaded plane region → θ-bounds and r-bounds in **under 90 seconds**, no hesitation
> - x² + y² in an integrand triggers "polar" before you finish reading the problem
> - "The segment from (1,0,2) to (3,4,1)" → **r**(t) and t-range without pausing
>
> Don't move to Week 2's calc block until these hold.

> [!note] Down-weighted on purpose
> **Trig substitution** and **partial fractions** — the two techniques 21-122's course description names by name — are the two least useful in 259. Polar, cylindrical, and spherical exist precisely to make √(a² − x²) disappear.
>
> Diagnostic: *if you're reaching for trig sub inside a multiple integral, you probably picked the wrong coordinate system.* Back out and re-set-up rather than grinding.

## Retro

- Hours actually spent:
- What was harder than expected:
- What to carry into Week 2:
