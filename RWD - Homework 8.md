---
tags:
type:
author:
description:
aliases:
date created: Wednesday, November 18th 2026, 11:09:50 pm
date modified: Wednesday, November 18th 2026, 11:40:32 pm
---

### Problem 1

##### a) 

Wine A with mean 14.136.

##### b)

ANOVA, which stands for Analysis of Variance.

##### c)

With $\mu_{i}$ being the true mean of the grades for the $i$th wine, we define:

$$
\begin{align}
H_{0} &: \mu_{1} = \mu_{2} = \dots = \mu_{10} \\
H_{A} &: \text{At least one } \mu_{i} \text{ differs from the others} 
\end{align}
$$

##### d)

The largest is 4.208 for wine H, while the lowest is 1.601 for wine F. The ratio between both is $\approx 2.63$, which is reasonably close to 2, so we can consider the condition met.

##### e)

$$\begin{align}
F=3.9734 && \text{(test statistic)}\\ 
p=0.0002
\end{align}$$

##### f)
Since the p value is $0.0002 < 0.05$, we reject the null hypothesis, i.e., there is sufficient evidence to conclude at least one wine's true mean rating differs from the others.

### Problem 2

##### a)
55 students picked pink as favorite color in 2006, out of 364 respondents to the survey that year. That’s $\frac{55}{364}\approx15.1\%$ of respondents.

##### b)
$$

\begin{align}

H_{0}: \text{there is no association between survey year and favorite color among Pitt students} \\

H_{A} : \text{there is an association between survey year and favorite color among Pitt students}

\end{align}

$$

##### c)
The smallest observed cell counts is the amount of students who picked yellow in 2006. 7 in total, which is greater than 5.

##### d)
The resulting $p$ is $0.0001$.

##### e)
$$

E = \frac{\text{row total} \cdot \text{column total}}{total} = \frac{75 \cdot 364}{676} \approx 40.38\%

$$

##### f)
The observed count for pink in 2006 is 55 and from previous part, the expected count is $\approx 40.3846$.

$$\text{Contribution} = \frac{(O - E)^2}{E} = \frac{(55 - 40.3846)^2}{40.3846} = \frac{(14.6154)^2}{40.3846} = \frac{213.6095}{40.3846} \approx 5.29$$

##### g)
Since the $p$-value ($0.0001$) is less than $0.05$, we reject the null hypothesis, i.e., there is strong statistical evidence of an association between survey year and favorite color among Pitt students.