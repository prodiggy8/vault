---
tags:
type:
author:
description:
aliases:
date created: Monday, November 9th 2026, 9:26:36 pm
date modified: Monday, November 9th 2026, 9:26:39 pm
---
Up until here is on paper.

#### General Method

- Set $p$ and $1-p$
- Find line of payoff for each column choice
	- If opponent picks A then $2p + 6(1-p)=6-4p$
	- If opponent picks B then $6p + 2(1-p)=4p + 2$
	- If opponent picks $C$ then $3p + 4(1-p) = 4-p$
- Plot, with $p$ ranging from $0$ to $1$

Whatever value of $p$ the opponent will pick the **lowest** of the lines. The lowest point among the three over all values of $p$ is called **lower envelope**.

- Find highest point in envelope: this is the lower bound.

___
Lower bounds: us coming up with algorithms and the adversary coming up with hard inputs

- Columns are all deterministic algorithms for sorting $n$ elements
	- This is finite if no redundancy
	- We must know the answer after ${n \choose 2}$ steps
- Rows are all possible inputs
- $R_{ij}$ is cost of algorithm $j$ on input $i$

- A deterministic algorithm with good worst-case is a column that performs well against all rows
- A randomized algorithm is a distribution $q$ over deterministic algorithms, such that the expected cost for each row is small. Mixed strategy for column player.


