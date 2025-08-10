University of Nottingham - Networks (COMP1055)


## Packets
Packet switching is used: this means that communications are sent in small packets, which are interleaved with other packets along wires. This allows better network utilisation: instead of one device using a connection (like with telephone networks and circuit switching), multiple connections can be made over a single wire.

Packets are not just the data "payload" - they include a header with checksum, sequence number, ack number and more.

### The Network Layer Models

The OSI model has application, presentation, session, transport, network, data link and physical layers. However, most networks do not fit cleanly into this. For the internet and TCP/IP, only 5 layers are used.

It is still useful and used at different layers to determine by switches/routers where to forward packets to.

1. Application
2. Transport
3. Network
4. Data Link
5. Physical

The data link layer uses frames, whereas the network layer uses packets. 

At the network layer and above, we can consider the network connections and more abstracted away from physical connections - the two below do are not needed unless we are building the network infrastructure itself.

At the transport layer, multiplexing, reliability and flow control is managed. This is used by TCP/UDP, and is useful for ensuring data gets assembled correctly before being used in the application layer.


### Mechanisms for data transfer

A connection-oriented service requires the connection to be set up, data transferred and then the connection released.

To actually transfer data, we need the IP address (network/machine) at layer 3 of the sending/receiving computer, and the MAC address on layer 2 to allow machines on the same network to be uniquely identified. At layer 5 (application) these addresses can be human-readable and understandable like domain names. 

#### Address resolution protocol
When a device wants to send data to another on the same network, it broadcasts an ARP request to discover the MAC associated with the target IP. The device with the IP responds with the MAC. Then the communication can continue.
- The key here is the broadcast packet -- it cannot communicate directly so just send it to every device on the network.



### Serial and parallel transfer
There are two mechanisms for data transfer: parallel and serial.

Parallel: uses many wires to transfer data, concurrently, reaching the destination at the same time
Serial: uses less (one) wire and sends bits bit-by-bit


### Determining different bytes
So that the computer can correctly dertermine different bits from each other, there is a mechanism to handle this - start and stop bits. In serial:

- the start bit is always 0
- the stop bit is always 1 and the line is held at 1
- this process repeats - a 'character' or payload byte will always begin with 1 turning into 0, followed by 8 bits
> A framing error may occur if it does not return to 1 and resync is needed.


This is a layer of abstraction above the physical signals:

RS232 has a transmission/receive/ground wire where the sender and recipient are connected to opposite wires (makes sense). It uses +15v for 0 and -15v for 1 but can only be used for short distances. We can use more voltage levels for more bits but this can be noisy. Oscillating signals can go further. RS232 is a point to point connection: 1 sender, 1 recipient. By contrast, Ethernet and WiFi are multi-access connections.


## Topologies
Star, mesh -> simple (A Level)

Instead of connecting every computer, we can use a shared medium to transmit data across.
### Ring and token
(Token) Ring network - uses mechanisms like token passing to coordinate passign of packets around the network, the recipient reads the info as it passes by it, and goes back to the sender to verify no errors occurred. If the token is recieved, and a packet needs to be sent, send it, then pass the token.

### Bus
A bus network has all machines on the same wire. This is good as they can transmit at any time. If two or more transmit at the same time, garbage data is created. Access control protocols can be used:


## Collisions and avoidance



### TDM
Time division multiplexing: each machine gets a fixed amount of bandwidth on the whole medium. This is good but not effective use of the medium.

### Eventual packet delivery
No fixed time of packet getting sent successfully but it will get there in the end.


**Ack**nowledgement packets are an example of this. If there is no ack of a transmission, the client can resend after some (random) time, and keeps sending until it is ACK'd. This is an example of a reliable network. Eventually, the packet will definitely be received and acknoeledged. (this was improved later with slotted aloha - transmit at the start of allotted slots to reduce the risk of overlap).

### CSMA/CD
Carrier Sense Multiple Access with Collision Detection.

If there is nothing being transmitted on the bus, then send, else, wait until the line is clear and then immediately transmit. However, two+ devices immediately transmit then collision is likely.

Collision avoidance comes in by detecting if the signal transmitted matches the signal on the bus; if so, use **exponential back-off** to delay a random amount below the maximum delay, and transmit. Check for collision and if so double the delay until the packet is sent. 

This does not mean Ethernet is reliable.

> A switch can simplify this and turn it into a star network by reducing the probability of collision by storing and forwarding all incoming and retransmitting them outgoing.


### CSMA/CD: the hidden node problem
In Wi-Fi, a device may be out of range of another but connected to the same basestation - so collision *detection* becomes impossible. It does not always know if there may be something transmitting on the network; if it does see something it will wait to transmit (Carrier Sense). To cope with this lack of visibility, it sends a short RTS (**Ready to Send**) packet. The basestation then sends a "clear to send" packet to all devices, so other ones know that it must wait for a transmission to finish first.


## Ethernet packets

Preamble, followed by 1 then MAC. Broadcast packets are all 1s for the MAC.

CRCs at the footer check for errors in transmission with electrical interference - burst errors affecting bits in a specific area of the packet. We use shift register and XOR to check for these.

Small packets - 55% data, large packets - 98% data. Inefficient to have small packets. However large packets increase latency. Packet sizes can be dynamic.


## Structure of ethernet
### Repeaters
Repeaters solve attenuation by amplifying/forwarding signal between areas e.g. different buses.

A backbone can have repeaters into parts e.g. of a building, which have more repeaters

> Similar to redstone!

A multiport repeater can be used to repeat a singal from one port onto all other ports.


### Bridges
Bridges are like repeaters but copy only complete frames to reduce risk of collisions, which only gets higher with repeaters. They are promiscuous - receiving all packets, and uses store and forward like switches.

They also filter packets to not forward packets from network 1 to 2, when it should just go to another machine in network 1 if sent from network 1.

Bridges contain a MAC table for each side of the bridge. Receiving a packet allows the bridge to build up what network that machine is on; if it receives a packet with unknown destination network (i.e. it hasn't discovered it yet), it will forward it to the other network.


# Berkeley Sockets API

Berkeley Sockets standard is the main way to transfer data over a network. IT was developed as part of BSD unix and thus treats everything as a file - using the same I/O instructions as accessing a file (cannot seek, just read/write to the bytes in it). It aims to be network-agnostic, generally following the client-server model.

## Background

The UNIX file I/O is similar to C’s file I/O. We open a file first (which returns an (integer) descriptor), then read/write bytes from it using the descriptor, and close the file when finished.

The integer descriptor is used to refer to that specific socket as we may have multiple open concurrently, making it easier to close/read from a specifc socket.  

> In reality, C wraps the UNIX i/o functions and routines to cache disk data into memory for faster access, but this is abstracted.

### TCP Introduction
TCP gives a reliable, stream-oriented connection to another computer.
Can work out if a connection doesn't work or gets dropped.

- One machine needs to be listening for a connection (on a specific port)
- Second machine need to connect to that open port.
Once this connection is open, the connection is bi-directional.

> A **protocol** describes exactly and precisely how the communication should happen (e.g. order of bits, meaning of bits). Not always complexity 

The stability allows the API to be built on top of it.

## Implementing Berkeley sockets

Berkeley sockets use recv()/send()/close() instead of read/write/close.

Instead of open()ing a connection, we create a socket() first.

To do this, we:
- create a socket using `socket()` 
```c
#include <sys/socket.h> 
sockFD = socket(PF_INET, SOCK_STREAM, IPPROTO_TCP);

/* udp:
	sockFD = socket(PF_INET, SOCK_DGRAM, IPPROTO_UCP);

For ipv6:
	simply change PF_INET to PF_INET6
*/

if (sockFD — -1){
	/* some error occurred */
	fprintf(stderr, “Socket creation failed\n”);
	exit(1);
}

close(sockFD);
```
Here, PF_INET is the protocol domain (i.e. the internet protocol.), sock_stream is the connection type, and ipproto_tcp is the protocol type (i.e transmission control/user datagram).


After, we need to connect to the server listening with connect(). We provide the (IP) address of the destination and the port to connect to, which uses a struct sockaddr_in. 

### Connecting
```c
connect(sockFD, (struct sockaddr *)&sad, sizeof(sad));

/* returns 0 if everything is fine, can wrap in e.g. if(connect() != 0) {..err..} */
```
where:
- sockFD is the socket descriptor int from initialising socket()
- sad is the struct containing the IP address and port
- sizeof(sad) is the size of the struct 

> To be network-agnostic, we may have different sized structures for different addresses - e.g. IPv6 is 4x the size of IPv4. Thus, the size of the struct will change accordingly - and we need to use sizeof(the_struct) to correctly allocate this

## Addressing
Whilst socket() and connect() will work to connect to any computer, the problem is working out which computer to connect to. 

```c
struct sockaddr_in sa;

memset(&sa, 0, sizeof(sa));
server.sin_family = AF_INET; /* internet protocol */

server.sin_port = htons(4444);

server.sin_addr.s_addr = INADDR_ANY;
```

### Endianness
Computers have different orders for the way they represent different bits. Whilst most chips use little endian - where the least significant byte is in the lowest address, the internet standardised on using big endian - where the most significant byte is in the lowest address (typically 0).

- Host to network (setting value on net): `htonX()` functions.
- Network to host (getting from net): `ntohX()` functions are used.

To set the port: we use `htons(16_bit_number)` - this means “translate from how the host encodes data to how the network encodes data, for a short integer”.
Similarly, we would use `htonl(32_bit_number)` to set an IP address.


### DNS Lookups
We need to use the `getaddrinfo()` function to let the computer look up an IP and port for us, so we don’t need to remember it. This returns a linked list of multiple addresses with multiple data types.

We can use a template structure `struct addrinfo hints;` to provide hints to the function to not return us things that are not relevant, instead of manually searching through the linked list.

```c
struct addrinfo hints;
int ret;

memset(&hints, 0, sizeof(hints));

hints.ai_family = AF_UNSPEC; /* any IPv4 or IPv6; we can iterate over it */
hints.ai_socktype = SOCK_STREAM;
hints.ai_protocol = IPPROTO_TCP;


if (!(ret = getaddrinfo(argv[1], “80”, &hints)))
{
	/* returns 0 if everything was successful; invert to be True if succeed */
}

freeadrinfo();
``` 
where, when calling `getaddrinfo()`:
- the first parameter, `argv[1]`, is a string containing the address of the machine we want to connect to
- the second param, `“80”`, is a string containing the service to connect to - can be a port, or a string service like `“http”`
- a pointer to the hints
- a pointer to a pointer of an `addrinfo` struct that points to the beginning of a linked list of all the addresses to connect to.

- to send it, we use `send()`


- transfer data using `send()`/`recv()`


- close using `close()`

## Full Client Boilerplate

```c

int main(int argc, const char * argv[])
{
	char buf[256];
	char line[256];
	int sd;
	char c;
	size_t n;
	int ret;
	struct addrinfo hints;
	struct sockaddr_in sa;
	struct addrinfo *ip;
	int quit = 0;
	
	/* Set up socket address */

	memset(&hints, 0, sizeof(hints));
	hints.ai_family = AF_UNSPEC;
	hints.ai_socktype = SOCK_STREAM;
	hints.ai_protocol = IPPROTO_TCP;

	if(!(ret = getaddrinfo(argv[1], "http", &hints, &ip)))
	{
		/* If getaddrinfo was successful */
	
		/* Returns a pointer to the first element in the linked list, traverse through to find an address that works */
		struct addrinfo *p = ip;

		while(p)
		{
			/* Create a socket, taking the family, socktype and protocol out of the returned structure as it may be IPv4/v6 */
			sd = socket(p->ai_family, p->ai_socktype, p->ai_protocol);

			/* if it’s able to make that socket, then try to connect to it */
			if(sd != -1)
			{
				/* Connect */
				if(connect(sd, p->ai_addr, p->ai_addrlen) == 0)
				{
					break;
				}
				else
				{
					close(sd);
					sd = -1;
				}
			}
			else
			{
				fprintf(stderr, "Failed to create socket\n");
			}
			p = p->ai_next;
		}
	}
	else
	{
		fprintf(stderr, "Failed to resolve %s: %d\n", argv[1], ret);
		exit(1);
	}
	
	freeaddrinfo(ip);
	if(sd == -1)
	{
		fprintf(stderr, "Failed to connect to %s\n", argv[1]);
		exit(1);
	}

	/* Communicate */

	sprintf(buf,"GET %s\r\n", argv[2]);
	send(sd, buf, strlen(buf), 0);

	do
	{
		n = recv(sd, &c, 1, 0);
		if(n == 1)
		{
			printf("%c", c);
		}
	} while(n == 1);

	/* Close */
	close(sd);
	
    return 0;
}
```


### Server

pass in a pointer to an integer that is set up with the amount of memory

```c
alen = sizeof(client);
clientConnection = accept(serverSocket, (struct sockaddr*)&client, &alen);
```
where `alen` is the size of the structure.

This is a blocking function, so will stall and not return a `clientConnection` until one is made


convert network byte ordering to host byte ordering (else the bytes will be in the wrong order):

```c
ntohl(client.sin_addr.s_addr);

/* --- or --- */

printf("connecton made on %d")
```


> Port numbers are 16-bits (short) and IP addresses will be 32-bits



To read a line from a network:
```c
do {
n = recv(sd, &c, 1, 0);
buf[i] = c;

if (i > 0 && buf[i] == '\n' && buf[i-1] == '\r')
{
	
}
}
```



# Network modeling

connection-oriented: arrives in order

> Layers 5 and 6 on the OSI model are not really used on the internet.

connectionless: send and it. (no need to be a connection, e.g. light to turn off doesn't need to send back)

Layer 3 is the IP protocol. It is designed to be routed across multiple heterogenous networks (different types of network protocol). Sits on top, regardless of the underlying network type.

Needed to implement 2 basic functions:
- addressing (and routing) - specifies each machine to identify its network and where a specific machine was, and allowing to get packets from one network to another
- fragmentation (different networks may need different size packets)

Every IP packet is a connectionless protocol - treats different packets individually even if going to the same address. Sends *datagrams* to another machine. No guarantee the order they will arrive in, or if they will arrive.


IP needs addresses that:
- uniquely identifies the machine
- identify what network the machine is on
> (more unique than ethernet address; the ethernet address just needs to be unique on *that* network)

To do this, the IP address is split up. The first two sections identify the network (e.g. 128.243 identifies the University of Nottingham) and then the last two identify the machine.


### IP address classes

![[Pasted image 20241127122822.png]]

CIDR allows us to use blocks to slow down exhaustion of addresses


A packet with headers can be up to 65535 bytes, but IP packets can be carried inside other packets like Ethernet, which usually has 1500 bytes.

Time to live: mechanism to stop the chance of packets ending up in a (permanent) loop by decrementing the TTL by 1 for each time the IP datagram "hops" between network routers - if it hits zero, it is discarded and a special packet is sent back to the source, informing that it wasn't reached.


When fragmented, the data in an IP packet is split into chunks, sent as ip packets across the other network. The identification field is used to uniquely identify the packet, and the fragment offset field comes within the larger packet that was being sent.

With IPv6, it finds out the largest packet size allowed between two machines, and uses this as its MTU for sending packets, as opposed to fragmenting them.


Store and forward: router receives the packet before sending it out on the destination network

> The home router receives the packet and realises "it's not for the home network" so then sends it to the ISP's network


Router needs memory to buffer the packets as they arrive before sending them out

Because routers rewrap packets into level 2 packets

CIRR /32: point-to-point link (on its own network) - can only transmit to and from one other machine
### Routing tables

A routing table has several properties:
- source independence - the next hop does not depend on the packet source, only the destination.
- hierarchical - needs to only know how to reach a network, not a machine. *Once it reaches a network, the routers internally can decide where to forward it to internal smaller networks or a machine.*
- universal routing - there is a next hop for every possible destination
- optimal routes - the next hop should be the optimal/shortest path to the destination
- default route: there is a catch-all route for anything not specified for a specific route.

A routing table may be static - does not change (until reboot). Useful for devices that don't change e.g. home device or router, as it is only connected to ISP and home devices. 

If a link goes down, this would not work for a static routing table, and a dynamic routing table is used on larger (internet) scales. Routers send information to each other when there are changes and a program updates the routing table as the machine is running.

> A routes fail, the system will route around them.

A default route would be represented by a \* (catch-all) so the router knows that, if it cannot forward a packet directly, it can instead send it to the catch-all/default router on the next hop.


### Next hop routing

Very simple.

Each machine looks up what the next hop is in a routing table and send it to it via a network connection. If the next machine is on the same network, then 

>Maps a destination address to the next hop - the address of the next machine to send to,

![[Pasted image 20241203115528.png]]

Computer would take the l3 packet, wrap it to a L2 packet (ethernet) and sets the frame header to say it will came from machine A and go to machine B, for example.

If the receiving machine isn't the destination, it looks up in its routing table what the next hop is for the destination.

> Source independence: the next hop only depends on the destination, not the source nor the route it took to get there.

Instead of having records in the routing table for all 4 billion addresses, we simplify it as much as possible. In the example above, we can 

Hierarchical addressing: real networks made of lots of small networks

 

The routing table should guarantee 
- universal routing - a hop is speicifed for each possible destination
- optimal routes - the next hop should give the shortest path
It is typvally construvtd automatically by the router as it connects and talks to other networks and computers

Netmask: used to separate IP between network and machine part.

![[Pasted image 20241204124402.png]]


Dynamic routing table; program on router builds an initial routing table at boot, as network conditions change, it gets updated. Routers can talk to each other informing them of changes, making it fully autonomous. The sytem will route around breaks and interruptions on the network

![[Pasted image 20241210111233.png]]


The static routing table (construted when the router boots) fills in the table at boot and doesn't change - good but if there is a change
Dynamic routing table - can change, built by a program continuously running


to build outing tables: 
- we can use a graph, with nodes being networks, and each edge being a link with a weight (score) to work out the optimal route


### Distributed routing algorithms

![[Pasted image 20241210115032.png]]


# DNS
A distributed hierarchical system used to map plaintext names to IP addresses.
Lots of small DNS servers have records for a specific set of machines. 

To start, there are 13 root servers. `a.root-servers.net`.  This will give the IP of top-level domains, which then can be queried by IP to the domain, then again to any subdomains until finally the IP of the machine is accessed.

## Types of DNS servers
There are 3 types of DNS servers:
- authoritative name servers: hold the answer to a query - like the above example
- recursive name server: will perform the search on behalf of the user to get the final IP
- caching name server: store the answer to a query to respond faster.




# TCP

## Problems with the Internet Protocol
The underlying network that uses IP is **unreliable** - we cannot guarantee that a sent data packet will be received by the intended machine. This is known as a best-effort protocol - it will do its best to get the network to the destination but it cannot guarantee it will, and if it does, with any order or timeliness.

There will also be no quality of service assurances, e.g. always take 3ms for a 512byte packet.

## Solving IP's unreliability problems with TCP
TCP solves the unreliability by using a sequence number. This is a 32-bit number used to identify the byte. The TCP header stores the sequence number of the first byte in the packet (there are some rules for this).

Out-of-order packets, due to routers choosing a different "optimal path", can be reorganised and put in the right order, with this sequence number.

To account for packet loss, **ack** packets are sent back with each received packet. After the retransmission timer expires, the sender can simply send it again, knowing the recipient hasn't received it.

> If an ack packet gets lost, the sender will send it again, but can be discarded by the recipient as it will have an already-existing sequence number.


## Ports
We don't just connect IP addresses to other IP addresses, we use ports as well.

Within the TCP packet, there is a source and destination port in the header. When the data goes back, these will be swapped. This allows for multiple distinct applications or other machines to connect at the same time.

## Windowing
If there was just one stream of SYN/SEND/ACK, then there would be lots of idle time on the network. The sender can send multiple packets with different data ranges to combat this; as ACKS also state the sequence number, we can almost continuously be receiving data without much waiting - making the best use of the available bandwidth.

The window field in the TCP header can adjust this to handle more/less data dependent on conditions at any point. The receiver can say to stop sending if e.g. there is no space left on it.


## SYN
A connection is first established by agreeing sequence numbers on both ends with a SYNchronise packet.

### Three-way handshake
Sender: send SYN with SN of XXXX
Recipient: receive SYN, send SYN + ACK with ack'd SYN and recipient SYN
Sender: receive SYN and ACK recipient's SYN
Recipient: receive ACK

### TCP close
Sender sends FIN+ACK, recipient gets FIN+ACK, sender receives FIN+ACK and sends ACK, which recipient receives and closes the connection

