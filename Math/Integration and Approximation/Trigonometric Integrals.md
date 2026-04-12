---
course: "[[Integration and Approximation]]"
note: 1
---
**Core identity:** $sin^2 x + cos^2 = 1$

$$I=\int{}{}{sin^mx \cdot cos^nx \;dx}$$

**Case 1: n is odd**

Save one cosine factor and substitute using the core identity.
$$I=\int{}{}{sin^mx\cdot(1-sin^2x)^k}\cdot cosx \; dx$$
Then substitute $u=sinx$

**Case 2: m is odd**
Save one sine factor and substitute using the core identity.
$$I=\int{}{}{(1-cos^2x)^k\cdot cos^nx \cdot sinx \; dx}$$
Then substitute $u=cosx$
**Notice that $du=-sinx$ in this case**

**Case 3: both m and n are even**
In this case, the half angle identities must be used.

$$sin^2x=\frac{1-cos^2x}{2}$$
$$cos^2x=\frac{1+cos^2x}{2}$$
$$sinx\cdot cosx=\frac{sin2x}{2}$$
---

**Core identity: $tan^2x+1=sec^2x$**

$$I=\int{}{tan^mx \cdot sec^nx \; dx}$$
**Case 1: n is even**
