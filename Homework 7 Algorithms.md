### Problem 1

First we calculate the net balance $b_{i}$ (collectibles minus debt) for each person $i$. While some person has a non-zero balance, repeat:

- Pick some person $p$ with positive net balance and some other $q$ with negative
- Have $q$ transfer $\min(b_{p}, -b_{q})$ to $p$.
- Update their balances accordingly

### Problem 2

##### a)

**Variables:**

For each $s-t$ path $p \in P$, let $f_p$ be the amount of flow sent along $p$.

**Maximize**: $$\sum_{p \in P} f_{p}$$

**Subject to:**

$$
\begin{aligned}
\sum_{p \in P \\ e \in p} f_{p} \leq c(e) && \forall e \in E \\
f_{p} \geq 0 && \forall p \in P
\end{aligned}
$$

##### b)

**Variables:**

Define $y_{e}$ for each edge $e \in E$

**Minimize:**

$$\sum_{e \in E} c(e) \cdot y_{e}$$

**Subject to:**

$$
\begin{aligned}
\sum_{e \in p} y_{e} \geq 1 && \forall p \in P \\
y_{e} \geq 0 && \forall e \in E
\end{aligned}
$$

The variables $y_e$ represent fractional amounts of cutting each edge. Every $s-t$ path must receive a total cut of at least 1, and the objective minimizes $\sum_e c_e y_e$. Thus, the dual is a fractional version of minimum cut.

##### c)

Let $g$ be any feasible flow of value $v$. First, remove directed cycles of positive flow by subtracting the minimum flow on each cycle from all its edges. This preserves conservation and the flow's value, and each subtraction removes at least one positive-flow edge.

In the remaining acyclic flow, follow positive-flow edges from $s$. Conservation prevents stopping at an intermediate vertex, and acyclicity prevents revisiting a vertex, so the path reaches $t$. Subtract the minimum flow along this path and record that amount as path flow. Repeating this decomposes the flow into nonnegative path flows satisfying

$$
\sum_{p\in P}f_p=v,
\qquad
\sum_{p:e\in p}f_p\le g_e\le c_e.
$$

Thus $f$ is primal-feasible with objective value $v$.

Given an $s$-$t$ cut $(S,T)$, define

$$
y_e=
\begin{cases}
1,&e\text{ goes from }S\text{ to }T,\\
0,&\text{otherwise}.
\end{cases}
$$

Every $s$-$t$ path crosses from $S$ to $T$, so $\sum_{e\in p}y_e\ge1$ for every path $p$. Hence $y$ is dual-feasible, with objective value

$$
\sum_{e\in E}c_ey_e=\operatorname{cap}(S,T).
$$

By weak duality,

$$
v=\sum_{p\in P}f_p\le\sum_{e\in E}c_ey_e=\operatorname{cap}(S,T).
$$

Therefore, the value of any feasible flow is at most the capacity of any $s$-$t$ cut.

### Problem 3
##### a)

Let $k=\lfloor\log_2 n\rfloor$ and give every job size $1$. Use $2^k$ machines first. Each of the remaining $n-2^k$ jobs gets its own machine and is eligible only for that machine. Since $m\ge n$, there are enough machines for them.

Let $S_0$ be the set of all $2^k$ main machines. In each phase $i=1,\ldots,k$, partition $S_{i-1}$ into $2^{k-i}$ disjoint pairs. Introduce one job per pair, eligible only for the two machines in that pair.

Both machines in each pair have load $i-1$, so greedy may choose either. Let $S_i$ contain the chosen machine from each pair. Every machine in $S_i$ now has load $i$. After phase $k$, $S_k$ contains a single machine with load $k$. Introduce one final job eligible only for that machine, increasing its load to $k+1$.

The phases introduce $\sum_{i=1}^{k}2^{k-i}=2^k-1$ jobs, and the final job brings the total to $2^k$. Including the $r$ additional jobs gives exactly $n$ jobs.

Now consider an optimal schedule. Assign each phase-$i$ job to the machine in its pair that greedy did not choose. These machines form $S_{i-1}\setminus S_i$. Since the pairs within each phase are disjoint, and these sets are disjoint across phases, each machine receives at most one job. Assign the final job to the single machine in $S_k$, and each additional job to its own machine. Thus $\mathrm{OPT}=1$.

Greedy therefore has makespan $k+1=\lfloor\log_2 n\rfloor+1 \ge \log_2 n\cdot\mathrm{OPT}$.

##### b)

Take an optimal integral schedule, and let $x_{ij}=1$ if job $j$ runs on machine $i$ and $0$ otherwise. Second constraint holds because each job is on exactly one machine, and it is placed only on machines with $(i,j) \in E$. The left side of first constraint is the load of machine $i$, which is at most $OPT$. So $(x, OPT)$ is feasible for the LP, and the LP minimum satisfies $L* \leq OPT$.

##### c)

Suppose the support contains a cycle. Since the graph is bipartite, the cycle has even length. Alternately set $v_{ij}=\frac{\epsilon}{p_j}$ and $v_{ij}=\frac{-\epsilon}{p_j}$ on its edges, and set $v_{ij}=0$ elsewhere.

At each job $j$, the two changes cancel, preserving second constraint. At each machine, the changes in load are $\epsilon$ and $-\epsilon$, preserving first constraint. Then we choose:

$$
0<\epsilon<\min_{(i,j)\text{ in cycle}}p_jx^*_{ij}.
$$

Then both $x^*+v$ and $x^*-v$ remain nonnegative. Thus $(x^*,L^*)$ is the midpoint of two distinct feasible solutions, contradicting that it is a vertex. Therefore, the support has no cycles.

##### d)

A machine $i$ can receive jobs only from its parent job or its child jobs. A child job is assigned to $i$ only if it has no children itself. Such a job has only one edge in the support, so second constraint forces $x^*_{ij}=1$. Therefore, only the unique parent job of $i$ can be assigned to $i$ with $0<x^*_{ij}<1$, proving the claim.

##### e)

By part d, all jobs assigned to machine $i$ have $x^*_{ij}=1$, except possibly one job. The jobs with $x^*_{ij}=1$ contribute at most the LP load, which is at most $L^*$. The possible extra job contributes at most $\max_{j:x^*_{ij}>0}p_j$. Hence

$$
L_i
\le L^*+\max_{j:x^*_{ij}>0}p_j
\le L^*+\max_{j\in J}p_j
\le 2\,\mathrm{OPT}.
$$

The last inequality follows from $L^*\le\mathrm{OPT}$ and $\max_{j\in J}p_j\le\mathrm{OPT}$, since every job must run entirely on one machine. Machines with no support edges receive no jobs and have load $0$.
