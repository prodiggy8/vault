---
tags:
  - computer-science
  - algorithms
  - graph-theory
type: note
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Sunday, May 31st 2026, 4:08:02 pm
date modified: Sunday, May 31st 2026, 4:14:05 pm
---

A **spanning tree** of an undirected graph $G$ is a subgraph that is a tree and contains every vertex of $G$.

Given a connected, undirected, *weighted* graph with a function $w: E \rightarrow \mathbb{R}$, a **minimum spanning tree** is a spanning tree $T$ that minimizes:

$$w(T):=\sum_{e \in T} w(e)$$

sa