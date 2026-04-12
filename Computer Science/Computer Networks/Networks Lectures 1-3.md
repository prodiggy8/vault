- 4 homework assignments (10%)
- 3 projects (45%)
- Midterm (15%) and Final (20%)
- Quizzes and participation (10%)

Projects are supposed to run forever
- robust and handles all errors
- concurrency
- needs testing


**Network:** collection of nodes and links

Two methods of data transfer:
- **Circuit switching:** establishing a dedicated connection (circuit) before data is sent.
- **Packet switching:** sends information as self-contained packets that have an address.
	- Each one traves independently
	- Messages can be broken down in multiple packets
	- Switches arbitrate between inputs

Requirements for packets:
- header information: addresses and more
- data
- How to reach destination: routing.
- How to choose the routes?
	- Human
	- Centralized (until 1980s)
	- Distributed (Internet) -> uses a **routing protocol**
		- Many different protocols at play! 

**An inter-net:** a network of networks
**The Internet:** set of networks of the Internet Service Providers (ISP), about 20k different networks
- Enables communication of diverse applications: web, P2P, video streaming, gaming, file transfers, and more.
- 100M hosts
- Adversarial environments: delays, packet loss, security challenges, etc.

**Layered Network Model: Open Systems Interconnection (OSI)**

7 - Application (1 -1)  everything else
6 - Presentation (1 -1) byte ordering, security
5 - Session (1 -1) How to tie flows together
4 - Transport (1 -1) How to send packets end2end
3 - Network (1 - n - 1) How to route packets
2 - Data link (1 - n - 1) How to transmit frames
1 - Physical (1 - n - 1) How to transmit bits



- OSI is a standard way of breaking a system in a set of components, provides isolation
- Each layer provisions a higher layer
- "Peer" layers on different systems (computers) communicate via protocol
- OSI is more of a **conceptual model** successful at shaping thought, while most of the internet is built on higher level protocols (TCP/IP, Appletalk)
- TCP/IP is where most of the Internet has been built

![[Pasted image 20260120105830.png]]
For **Local Area Networks**, the IEEE 802 standards "refine" the OSI data layer into two distinct layers for more detail.
2 - Data link:
	3 - Logical Link Layer (LLC)
	Interface between hardware and the network layer
	Allows for protocol multiplexing (IPv4, IPv6, etc)
	2 - Media Access Control (MAC)
	Manages how multiple devices "take turns" to transmit data without interfering with each other

**A TCP/IP/802.3 Packet**

Ethernet preamble
MAC header
LLC / SNAP header
IP header
TCP header
Data