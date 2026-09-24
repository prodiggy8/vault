**1. Where the deleted character has to be**

Let s = s[0..L−1] be a non-palindrome and let i be the first mismatch from the outside, i.e. s[j] = s[L−1−j] for j < i and s[i] ≠ s[L−1−i].

_Lemma._ If deleting some character of s gives a palindrome, then deleting s[i] or deleting s[L−1−i] gives a palindrome.

_Proof._ Say the deletion is at position k and the result t is a palindrome.

- k strictly inside the mismatched pair (i < k < L−1−i): for every j ≤ i we have j < k and L−1−j > k, so t[j] = s[j] and t[L−2−j] = s[L−1−j]. The pair (i, L−1−i) is still a mismatched pair of t, contradiction.
- k < i (the case k > L−1−i is the mirror image): for k ≤ j < i, t[j] = s[j+1] and t[L−2−j] = s[L−1−j] (one checks L−2−j ≥ k), and t is a palindrome, so s[j+1] = s[L−1−j] = s[j]. Hence s[k] = s[k+1] = ⋯ = s[i], and deleting s[k] produces exactly the same string as deleting s[i]. □

So a pseudo-palindrome is a string that is not a palindrome but becomes one when you delete one endpoint of its first mismatched pair. Unrolling this, a pseudo-palindrome occurring in T is exactly a substring of the form (writing the "delete left" type; "delete right" is the mirror image)

T[a−1−i .. b+i] where T[a..b] is a palindrome (b ≥ a), T[a−1] ≠ T[b], and T[a−1−j] = T[b+j] for j = 1..i.

Deleting T[a−1] leaves i matched layers around the palindrome T[a..b], so it is a palindrome; the pair (a−1, b) is a mismatch, so the string itself is not one. Its length is (b−a+1) + 1 + 2i.

**2. Reducing to O(1) queries per center**

Fix the center c of the inner palindrome (there are 2n−1 centers, integer and half-integer) and the side, say "delete left". As the inner length ρ = b−a+1 runs over values of the right parity, the pairs (a−1, b) are the successive pairs at distance 1, 2, 3, … around the center c − ½. Call ρ _eligible_ if 1 ≤ ρ ≤ P(c), where P(c) is the length of the longest palindrome centered at c, and its pair (a−1, b) mismatches.

_Claim._ For a fixed (c, side), the best candidate uses the largest eligible ρ.

If ρ′ < ρ are both eligible, then the pair belonging to ρ is a mismatch sitting (ρ−ρ′)/2 layers outside the pair belonging to ρ′, so the extension from ρ′ can reach at most (ρ−ρ′)/2 − 1 layers, giving length ≤ ρ′ + 1 + (ρ − ρ′) − 2 = ρ − 1 < ρ + 1 ≤ length obtained from ρ. □

So for each (c, side) we need three things:

1. P(c): palindromes centered at c are nested, so binary-search the length.
2. The largest eligible ρ: start at the pair for ρ = P(c) and walk inward until the first mismatch. Walking inward k layers without a mismatch means T[a−1 .. a−2+k] equals the reverse of T[b−k+1 .. b] (with a, b the endpoints for ρ = P(c)), so the walk length is again found by binary search; the largest eligible ρ is P(c) − 2k, and if that is < 1 there is no candidate on this side.
3. The extension i: the largest i with T[a−1−i .. a−2] equal to the reverse of T[b+1 .. b+i], capped by the ends of T; binary search once more.

Output the maximum of ρ + 1 + 2i over all (c, side); if no center yields a candidate, T is a constant string and has no pseudo-palindrome (any two adjacent distinct characters would already give one of length 2).

Correctness: every candidate we output is a pseudo-palindrome by the unrolled form in §1, and every pseudo-palindrome in T has that form for some (c, side) with an eligible ρ and some i no larger than the maximal extension, so it is no longer than what we return for that (c, side).

**3. Answering the queries with fingerprints**

Every query above is "is T[x .. x+ℓ−1] equal to the reverse of T[y−ℓ+1 .. y]?" (a palindrome test T[x..y] is the special case with the two blocks meeting in the middle). Pick a random prime p and precompute prefix fingerprints h(T[0..j]) mod p of T and of T reversed, together with the powers 2^j mod p, in O(n). The fingerprint of any substring of T or of the reverse of any substring of T is then a constant number of mod-p operations, so a query is O(1) and each binary search is O(log n).

Total: O(n) preprocessing + (2n−1) centers × 2 sides × 3 binary searches × O(log n) = **O(n log n)**.

**4. Word RAM justification.** Each fingerprint comparison is a string-equality test between two strings of length ≤ n, which by the analysis in the notes fails with probability at most n/π(M) when p is drawn from {1..M} (a difference of two n-bit numbers has at most n prime factors). We make Q = O(n log n) comparisons and want total failure ≤ 1/n, so by the union bound it suffices that each fails with probability ≤ 1/(nQ), i.e. π(M) ≥ n²Q = O(n³ log n). By Corollary 5.1 this holds for M = 2·n²Q·log₂(n²Q) = O(n³ log² n), so p has O(log n) bits. Since the input has n cells the model gives w ≥ log n, so p, every residue, and every product of two residues fit in O(1) words, and each mod-p operation is O(1). Prime selection costs O(polylog n), dominated by the rest. Fingerprint errors are one-sided (equal strings never look unequal), and if none of the Q comparisons errs the binary searches and the final answer are exactly correct, so the algorithm is correct with probability ≥ 1 − 1/n in O(n log n) time.

**Why not better.** The only tool from the course that gives fast general equality tests is fingerprinting, and it turns each "how far do these match" question into a binary search; that log factor is what stands between this and linear time. (Deterministic O(n) is possible with suffix-array/LCP machinery, which is outside the course.)