---
tags:
  - statistics
type:
author:
description:
aliases:
date created: Wednesday, October 7th 2026, 9:51:19 pm
date modified: Wednesday, October 7th 2026, 9:51:24 pm
---
##### 1) a.
| **room_disinfectant \ patient_outcome** | **lived** | **died** | **Row Totals** |
| --------------------------------------- | --------- | -------- | -------------- |
| used                                | 34        | 6        | 40             |
| not_used                            | 19        | 16       | 35             |
| **Column Totals**                       | 53        | 22       | 75             |
##### 1) b.
| **room_disinfectant \ patient_outcome** | **lived** | **died** | **Row Totals** |
| --------------------------------------- | --------- | -------- | -------------- |
| used                                    | 0.45      | 0.08     | 0.53           |
| not_used                                | 0.25      | 0.21     | 0.47           |
| **Column Totals**                       | 0.71      | 0.29     | 1              |
##### 1) c.
$P(\text{lived})=71 \%$, a marginal probability.
##### 1) d.
$P(\text{used} \cap \text{lived} )=45\%$, a joint probability.
##### 1) e.
$$\begin{aligned}
P(\text{used} \cup \text{lived})&=P(\text{used}) + P(\text{lived}) - P(\text{used} \cap \text{lived} ) \\
&=0.53 + 0.71 - 0.45 = 0.79
\end{aligned}$$
##### 1) f.
$P(\text{lived} | \text{used})=\frac{P(\text{lived} \cap \text{used})}{P(\text{used})}=\frac{0.45}{0.53}=0.85$, a conditional probability.
##### 1) g.
$P(\text{lived} | \text{not used})=\frac{P(\text{lived} \cap \text{not used})}{P(\text{not used})}=\frac{0.25}{0.47} \approx 0.54$, a conditional probability.
##### 1) h.
A higher probability as seen in the previous two questions results.
##### 1) i.
It is not independent, since independent events have the property $P(A|B)=P(A)$. If $A$ is living and $B$ is using disinfectant we have $P(A|B)=0.85 \neq P(A) = 0.71$.
##### 1) j.
Yes. The events are not independent, which means one event depends on the other, i.e., they’re associated.
##### 1) k.
It would be $P(\text{lived} \cap \text{used})=P(\text{lived})P(\text{used})=0.71 \cdot 0.53 \approx 0.38$.

##### 2) a.
It would be $p=\frac{1}{10}$.
##### 2) b.
We’re dealing with 11 prices, i.e., $n=11$ trials, all with probability $p=0.1$ (from previous part).
##### 2) c.
$P(X=5)={11 \choose 5}(0.1)^5(1 - 0.1)^{11-5}=462 \cdot 0.1^5 \cdot 0.9^6 \approx 0.0025$
##### 2) d.
Yes, very surprising. It’s an incredibly low probability.