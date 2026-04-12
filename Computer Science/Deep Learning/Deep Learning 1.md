Plato, David Hume, Pavlov -> Humans learn through association (**associationism**)

Pairs of thoughts become associated based on organism's past experience -> Learning

Aristotle: four laws
- two events close together will be linked (contiguity)
- the more two events occur together, more powerful is the link (frequency)
- two things are similar, will be linked (similarity)
- seeing something may trigger the recollection of the opposite (contrast)

Associationist theory of mental processes: only one mental process, the ability to associate ideas
" theory of learning: cause, effect, contiguity, resemblance
Behaviorism: behavior comes from associations of actions with feedback

**Connectionism**

David Hartley's Observations on man (1749)
- Receive input through vibrations, brain is made of vibrations
- Connected ideas -> brain connects our memories to current senses

1800 - Brain is mass of **neurons**
Neurons are connected (in and out to others)

Alexander Bain: information is in the **connections**
1. **Neural Groupings**
- Neurons excite and stimulate one another
- Different combinations of inputs can generate different outputs
- Intensity of activation generate differences in propagation of activation

2. Making memories
- When two memories concur or closely succeed another, neurons find some bridge or place of continuity between them.
- Predicts Hebbian learning

~ 1 million neurons and 5 billion connections relating to 200k acquisitions.
He was concerned he didn't take into account the "partially formed associations" and the number of neurons responsible for recall/learning.

Connectionist machines: network of processing elements
Neural networks are connectionist machines!

Paradigms:

**Turing** (1948)

Learnable networks that can be trained to model any Boolean function.

A-type: random networks of NAND gates, no learning
B-type: connection between two units has a modifier whose behavior can be learned -> done by an A-type machine

**Parallel Distributed Processing**
Requires
- set of processing units, state of activation, output function for each unit, pattern of connectivity between units, propagation rules, activation rules to combine the inputs with the current state of the unit, a learning rule whereby patterns of connectivity are modified, environment in which the system must operate

**Connectionist System**
Requires
- connectivity of the units, activation function of the units, nature of the learning procedure that modifies the connections, how the network is interpreted semantically

**Individual elements**

Neurons: dendrites, soma, axon
Signal comes in through the dendrites into the soma, they exit from the axon to other neurons

**McCulloch and Pitts**
- Created mathematical model of a neuron
- Modeled neurons as performing propositional logic, where each neuron evaluates the truth value of its input

![[Pasted image 20250831192105.png]]

Such networks can model logic gates:

![[Pasted image 20250831192352.png]]

Hebb (1949)

Learning mechanism: as cell A repeatedly excites cell B, its ability to excite B improves
**Neurons that fire together, wire together**

Given neuron x and neuron y, an update formula:
$$w_{xy}=w_{xy}+nxy$$
 It's **unstable**
 - stronger connections will enforce themselves
 - no notion of competition
 - no reduction in weights
 - learning is unbounded
Improvement with forgetting: Sanger's rule

Rosenblatt**

Perceptron!
![[Pasted image 20250831193346.png]]
Association units combine sensory input with fixed weights
Response units combine associative units with learnable weights
- number of inputs combine linearly
- threshold logic: fire if combined input exceeds threshold

He also provided a learning algorithm!
w = w + n(d(x) - y(x))x
d(x) - desired outcome in response to input x
y(x) - actual output in response to x

- updated the weights whenever the perceptron output is wrong!
- **proved convergence** for linearly separable classes (data can be divided with a straight line)

Single neuron can't do XOR
- Two or gates (check if X or Y = 1 or = 0) connected by an AND gate.

Perceptron with real inputs
- Same threshold concept!
- threshold $\theta(z)$ activation function operating on weighted sum of inputs plus bias (affine function)

- can delimit very complex areas, reals build polygons, logic gates can add them up

Individual perceptrons -> boolean gate
MLP -> universal boolean functions
Individual perceptrons capture linear boundaries
Complex boundaries can be composed from them
MLPs can represent arbitrary decision boundaries
Can be used to classify data

To represent a hexagon -> 7 activation functions needed, 6 in hidden layer for the boundaries + output layer to AND them all

What about real outputs?

![[Pasted image 20250902164750.png]]
this outputs 1 iff input lies between T1 and T2, provided T2 > T1

