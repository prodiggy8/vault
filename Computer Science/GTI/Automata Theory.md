A finite automaton is a 5-tuple $M=(Q, \Sigma, \delta, q_0, F)$ where $F \subset Q$ are accept states, $\delta: Q \times \Sigma \rightarrow Q$

$L(M)=\{w \in \Sigma^* \mid M \text{ accepts } w\}$ is the language of $M$

**Theorem:** any finite language is regular

$L=\{0^n1^n : n \in \mathbb{N}\}$ not regular

Proving a language is not regular
1. Assume for contradiction there is a DFA $M$ with $L(M)=L$
2. Argue (usually by Pigeonhole) there are two strings $x, y$ which reach the same state in M
3. Show there is a string $z$ such that $xz \in L$ but $yz \notin L$

**Non-deterministic finite automata**

**Theorem:** the class of regular languages is closed under all of the following operations:
1. Union, $A \cup B = \{w \mid w \in A \lor w \in B\}$
2. Intersection, $A \cap B = \{w \mid w \in A \land w \in B\}$
3. Complement, $A^C = \{w \mid w \notin A\}$
4. Reversal, $A^R = \{a_k\dots a_2a_1 \mid a_1a_2\dots a_k \in A\}$
5. Concatenation, $A \cdot B = \{vw \mid v \in A \land w \in B\}$
6. Star, $A^*=\{w_1\dots w_k \mid k \ge 0 \land w_i \in A\}$

To prove for the reversal, idea: flip transitions and swap start and accept states.
This might cause multiple start states or multiple ways to leave a state on the same symbol.

Such automata is **non-deterministic**
It accepts if **any** of the paths lead to an accept state

$M=(Q, \Sigma, \Delta, I, F)$, where $I$ is now a set of start states and $\Delta: Q \times \Sigma \rightarrow P(Q)$

**Theorem:** for every NFA there is an equivalent DFA

Regular operations: union, concatenation, and star
**Kleene's Theorem:** a language over $\Sigma$ is regular if and only if it can be constructed from $\emptyset, \{\epsilon\}, \{a\}$ for each $a \in \Sigma$


Cartesian product for multiple conditions: a DFA with two-tuple states
