---
type: algorithm
aliases: ["Bellman-Ford", "Bellman Ford", "BF"]
solves: "[[Single-source shortest paths]]"
techniques: ["[[Dynamic programming]]", "[[Relaxation]]"]
requires: ["no negative cycles"]
handles: ["negative edge weights", "directed", "detects negative cycles"]
fails_on: ["negative cycles (reports instead of solving)"]
time: "O(VE)"
space: "O(V)"
correctness: "[[Induction on path length]]"
source: "[[Erickson Ch08 Shortest Paths]]"
status: can-derive # reference | implemented | can-derive
---
