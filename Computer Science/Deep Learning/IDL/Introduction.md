McCulloch and Pitts model: mathematical model of a neuron, with excitatory and inhibitory gates.
- Can build boolean gates with them.

Hebb: proposed learning mechanism
- Neurons that fire together, wire together

Rosenblatt: Perceptron
- Inputs combined linearly, fire if input exceeds a threshold
- Learning algorithm: $w=w + \eta(d(x) - y(x))x$
- $d(x)$ is desired output, $y(x)$ is actual output
- Single neuron can't emulate XOR

![[IDL_perception.png]]

- Can be extended with **real valued** inputs and thresholds
- An activation $\theta(z)$ operates on the weighted sum plus a bias
- **Universal classifiers** for any decision boundary

$z=\sum_i w_ix_i + b$
Sigmoid function: $\frac{1}{1+\exp(-z)}$

**Depth:** longest path from a source to a sink
**Layer:** set of neurons that are at same depth with respect to the input

