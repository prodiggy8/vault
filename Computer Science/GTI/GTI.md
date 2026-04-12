Problem 1)
a)
$d$ should be the multiplicative inverse of $e \; mod \; \phi(n)$, where $n = pq$
- First, we find $\phi(n) = \phi(pq) = (p-1)(q-1)$
- Second, we use the Euclidian algorithm to calculate $gcd(e, \phi(n)) = 1$
- Third, using the reverse algorithm to express 1 as a linear combination of $e, \phi(n)$, giving us $d=4251$.
b)
Bob needs to send $(2014)^e \; mod \; n$

c)
Bob's original message is $(16648)^d \; mod \; n$


Problem 2) **Find all proper subgroups**

Since |K4|=4, the size of a proper subgroup can only be 1 or 2.
For size 1, the only possible is the identity, I.
For size 2, a subgroup must contain I and other element. The identity plus any of the other elements is a subgroup, since it's closed under o and under inverses.

Problem 3) **Breaking RSA**

Suppose they found $\phi(n)$, then they can find p and q as follows:

$n + 1 - \phi(n)=pq + 1 + (p - 1)(q - 1) = p + q$

From this, the difference can be computed:

$(p+q)^2=p^2+2pq+q^2$

Subtracting $4n = 4pq$

$p^2+2pq+q^2 - 4pq = p^2 - 2pq + q^2 = (p - q)^2$
$p-q=\sqrt{(p+q)^2-4n}$

Now we can just use sum and difference to isolate both:

$p=\frac{(p+q)+(p-q)}{2}$ and similarly for $q$.

If Ron and Adi had a quick way of finding phi, they could quickly factor n. It must be that finding phi is at least as hard as factoring n.

4)

Since A is a group, $|A| = |A^{-1}|$, as every element has an inverse
Pick arbitrary $x \in G$, $B = xA^{-1}$

$|A \cap B| = |A| + |B| - |A \cup B|$
Since $|A| = |B| > \frac{|G|}{2}$ and $|A \cup B| <= |G|$
We have that $|A \cap B|>0$

Notice that if we say that $|A| = \frac{|G|}{2}$
Then we reach $|A| + |B| = |G|$ and $|A| + |B| - |A \cup B|$ can be 0.

Z5 = {1, 2, 3, 4}
A = {1, 2}
x = 4
B = {3, 4}
AUB = {1, 2, 3, 4}
AIB = {}
