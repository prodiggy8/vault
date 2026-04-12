Other activation functions
"soft" perceptron (logistic) -> a squashing function $\frac{1}{1 + exp(-\sum_i{w_i x_i + b})}$

Depth of graph: **longest path** from a source (only outgoing edge) to sink (only incoming edges)

"Deep": Depth of output neurons > 2

Layer: group of neurons at the same depth

How many layers for a Boolean MLP?
- Truth table in DNF with an or at the output

Karnaugh map can be used to "group" inputs and find a reduced version of the DNF.

Checkerboard Karnaugh map: largest irreducible one, number of neurons requires is $2^{n-1}$

In a deep network can be modeled as $X \oplus Y \oplus W \oplus Z$
Since XOR takes 3 gates, we have $3 \cdot \text{\#vars}$

MLPs can compute **any boolean function** -> since they can compute any individual gate





DL & Cloud lectures