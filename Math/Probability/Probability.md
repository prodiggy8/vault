**Counting**

Permutation $P(n, k) = \frac{n!}{(n-k)!}$
Combination $C(n, k) = {n \choose k} = \frac{n!}{(n-k)!k!}$
${n \choose k}={n \choose n-k}$

Stars and bars ${n + k - 1 \choose k - 1}$ where $k$ is the number of bars
$\#$ of solutions for $x_1+x_2+\dots+x_k=n$

$k {n \choose k} = n {n-1 \choose k - 1}$

**Multinomial Coefficients:** unique permutations of $n$ objects in $k$ groups of sizes $b_1,\dots,b_k$
$${n \choose b_1,b_2,\dots,b_k}=\frac{n!}{b_1! \cdot b_2!\dots b_k!}$$

**Probability Distributions**

$P(A_1 \cap A_2 \dots \cap A_n)=P(A_1)P(A_2|A_1)\dots P(A_n | A_1 \cap \dots \cap A_{n-1})$

$P(A \mid B)=\frac{P(A \cap B)}{P(B)}=\frac{P(B) P(A \mid B)}{P(B)}$

Independency $\Leftrightarrow P(A \cap B) = P(A)P(B) \Leftrightarrow P(A \mid B) = P(A)$

**Joint PMFs**

$P_X(x)=\sum_y P_{X,Y}(x, y)$

**Conditioning**

$P_{X|A}(x)=\frac{P(X=x \cap A)}{P(A)}$
$\mathbb{E}[X \mid A]=\sum_xxP_{X|A}(x)$
