Flow control - Don't overwhelm the receiver
Congestion control - Don't overwhelm the *network*

#### Goals:
- Efficiency
- Fairness

#### Solutions:
1. End-to-end congestion control
	- No feedback from network (this is transport layer)
	- Infer from loss and delay!

	
2. Network-assisted congestion control
	- Routers provide feedback to end systems
		- Single bit indicating congestion
	- Layer police! Routers are not supposed to talk to layer 3.
	- Makes router complicated

