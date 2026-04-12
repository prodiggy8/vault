Web server:
- program that takes input from file descriptors
- that can be a network connection, a FIFO, a pipe, a terminal, a real file, or anything else
- processes the input according to an "agreed upon set of rules"
- writes output to a file descriptor

**Checkpoint 1**
- Takes input concurrently from FDs
- Copies the input string to an output string

1. Socket programming
2. IO multiplexing with select
3. Request parsing
4. ==Beej's Guide to Network Programming==

**Checkpoint 2**
- Takes input concurrently from FDs
- Parses input according to HTTP 1.1 protocol
- Potentially reading files if a client requested
- Writes output to a file descriptor

1. Persistent connection
2. Generate response for GET, HEAD, POST
3. ==Need to come up with system design before start==

**Checkpoint 3**
- Takes input concurrently from FDs
- Parses the input according to the HTTPS protocol via TLS
- Potentially reading/writing data
- Or invoking a program for processing client's data (CGI)
- Writes output to a file descriptor

1. HTTPS
2. CGI
3. Working flask blog
4. ==The better CP2 was designed, the easier CP3 will be==

**Sockets Intro**

Socket: endpoint <ip, port>
Connection: source endpoint <ip, port> + destination endpoint <ip, port>

**Client side**
- Create via socket()
- Connect to endpoint via connect()
- Write to socket via send()
- Read from socket via recv()

**Server side**
- Create via socket()
- Bind to an endpoint via bind()
- Listen for connections via listen()
- Accept connections via accept()]
- Read from socket via recv()
- Write to socket via send()

-> There will be random failures, need to be error prone (use Ctrl-C to test)

**Concurrency**
Need to be able to serve and accept at the same time!
- Multithreading
	- server gives each client its own thread
	- resource intensive, threads can't communicate between each other

- IO Multiplexing
	- watch a set of sockets (in main thread)
	- use select() to find sockets ready for IO

