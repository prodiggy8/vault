---
tags:
  - algorithms
type:
author:
description:
aliases:
date created: Sunday, August 2nd 2026, 7:36:14 pm
date modified: Sunday, August 2nd 2026, 7:36:16 pm
---
```pseudo
Hanoi(n, src, dst, tmp):
	if n > 0
		Hanoi(n - 1, src, tmp, dst)
		move disk n from src to dst
		Hanoi(n - 1, tmp, dst, src)
```

> [!quote]
> For most recursions, unrolling the recursion is neither necessary nor helpful.

### Complexity

$$
\begin{gather}
T(0)=0 \\
T(n)=2T(n-1)+1 \\
T(n)\in O(2^n)
\end{gather}
$$
