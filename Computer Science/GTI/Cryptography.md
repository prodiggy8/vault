One-Time Pads:
1. Encode using the code book
2. XOR it with the next unused random bits

Given prime $p$, generator $g$ of $\mathbb{Z}_p^*$ and $a \in \mathbb{Z}_p^*$, find exponent $k$ such that $a \equiv_p g^k$
Such $k$ is the discrete logarithm of a

**Diffie-Hellman Key Exchange**

$p$ and generator $g \in \mathbb{Z}_p^*$ public

1. Alice chooses $a \in \mathbb{Z}_p^*$ and computes $x=g^a \mod p$ and sends to Bob
2. Bob chooses $b \in \mathbb{Z}_p^*$ and computes $y = g^b \mod p$ and sends to Alice
3. Alice computes $y^a \mod p = g^{ab} \mod p$
4. Bob computes $x^b \mod p = g^{ab} \mod p$

This is a secret for Diffie-Hellman

**RSA**

1. Pick large primes $p$ and $q$ and publish $n=pq$
2. Publish random $e \in \mathbb{Z}_{\phi(n)}^*$
3. Private key will be $d$ inverse of $e$
4. Sender computes $m^e \mod n$ with $m$ being the message
5. Using $d$, the received can read the message since $(m^e)^d \mod n=m$
