---
tags:
type:
author:
description:
aliases:
date created: Tuesday, September 29th 2026, 8:19:30 pm
date modified: Tuesday, September 29th 2026, 8:19:35 pm
---
# Problem 3

## a)
We create a union-find structure that will be used to keep track of the new edges to be added, with both path compression and union-by-size. We add a variable to the structure keeping the number of sets. We also keep the original spanning tree to track distances between two nodes.

## b)
`AddRoads(u, v)` will do the following:
- `Union(u, v)`
- Go up in the tree with two pointers starting at  `u, v` until they both meet. Keep track of the nodes we passed by.
- For each node `w` we passed by we do `Union(x, w)`

`NumBridges()` just returns the value of the variable we set in the beginning in $O(1)$.

**Correctness:**
- Notice that by definition an edge $(u,v)$ is not a bridge if there is another path from $u$ to $v$ that does not include such edge. Hence there is a cycle containing edge $(u,v)$ and every edge in this cycle is not a bridge.
- When adding an edge to the spanning tree, we create a cycle and hence destroy bridges.
- By traversing the tree we find all edges contained in such cycle, say $k$ of them. We union all of their nodes in the union-find structure, hence decreasing the number of connected components by exactly $k$.

**Complexity:**
- 

## c)

