1)

Pseudo-palindrome is:
1. not a palindrome
2. when you delete one character it becomes one

Algorithm: longest pseudo-palindrome substring of a given binary string of length $\geq2$

Probability of failure is at most $\frac{1}{n}$
Cost must be better than quadratic and for full points must be the best cost you can achieve using techniques from this class.
Justify the cost with respect to the word RAM model.

[0101010101010101010101010101010]

```pseudo
PseudoPalindrome(S):
	
	
HasPseudoPalindrome(S, k):


IsPalindrome(S):
	return S[0..n/2] == S[n/2..n]
	
```