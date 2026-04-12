Internetwork, or *internet* with lowercase i: arbitrary collection of networks interconnected to provide some sort of host-to-host packet delivery service.
![[Pasted image 20260205135148.png]]
The *Internet Protocol* allows for heterogeneous internetworks. It has two parts:
- An addressing scheme
- And a datagram (connectionless) model of data delivery

![[Pasted image 20260205140644.png]]
- HLEN since options are variable in size
- TTL (time to live) to kill packets that are looping in the network
- Protocol needed for demultiplexing (deliver to UDP or TCP?)
- TOS (type of service) defines packet's priority
- Version is at the beginning to allow for complete rework of fields in other versions
- Second word deals with **fragmentation and reassembly**

If no options, header size is 20 bytes (counted in number of 32-bit words)
Length counts in bytes instead

Maximum IP packet length is 65,535 bytes

**Fragmentation and Reassembly**

- Ethernet packets are only 1500 bytes long! Modern data link protocols allows for up 9000 bytes.
- **Either make them fit in the smallest data link packet or provide a way to divide them**

*Maximum transmission unit (MTU)* is the largest IP datagram a network can carry in a *payload* of a data link packet





Network layer
- Objective: end-to-end best effort delivery
- Problems
	- Addressing
	- Deliver data. how?
	- Routing