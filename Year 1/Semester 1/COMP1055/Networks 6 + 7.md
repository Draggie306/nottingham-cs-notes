Recap:

We use layers of abstraction, and protocols connect these layers.

#### Types of nets
Point-to-point: connects 2 computers only (RS232)
Multi-access networks; can connect multiple computers over the shared medium. 


#### network topology
There are multiple wyas computers can be connected over a shared medium. This can be classified by their shape or topology. This represents the logical way they are connected, not the physical way.

Star network: all computers connected via a central hub.

Ring network: a closed loop. Packets are passed to the next computer in sequence until they reach the intended destination. 

- A small "token" can be passed around the ring. Each computer waits for the token to arrive, and sends a packet if it needs to (to not monopolise the resource). Then it must send the token on,

Bus network: all devices connected to a central wire. As data is sent, all computers on the same wire receive the data.
We need to prevent data collision: if 2 machines transmit at the same time, packets will collide, resulting in corrupted data.

#### TDM
We can use time division multiplexing, where a controller synchronizes machines to each have a fixed time slot at which to send information. It cycles through different fixed time-sots 
Logically a star but implemented as a bus.
It is great for multi-tenancy networks bu poor for utilitsation of bandwidth, i.e.

### Eventual packet delivery
We relax the restriction that the packet will get there on the first time. Accepts that there will be collisions and corruptions, it not reaching the destination the first time.

## random access protocols
We use random access protocols as it uses randomisation to prevent al computers accessing the shared medium at the same time. It is called random because access *only occurs when a machine has a packet to attend*. 

### Aloha
hawaii uni wanted ro provide access to the expensive mainframe computer. 
due to layout of the islands, used radio waves instead at 24k baud at 100khz.

it had a central computer, which passed info to the "Menehune", not a problem for outgoing packets as this computer is the only one transmitting. 

however, when receiving from clients, there is an issue. usually, the data received will be random, and therefore able to be received. however sometimes it may collide. to solve this, the menehune sends a reply to the client when is successfully receives a packet - an **ack**nowledgement packet. if there is no ack, the client resends the packet after a period of time - a random period of time (in the random access protocol.)

Slotted aloha - create slots to reduce collisions - only transmit at the start of the slots (reduce chance of overlaps)
Is a reliable network as the client (sender)is fully aware that the packet was received correctly.


### Ethernet

CSMA/CD
bus/ether has no electrical signals when no frame being transmitted. if we need to transmit, we wait until the line is free/nothing is being transmitted and immediately transmit. this is ***c**arrier **s**ense*.
/CD: if the signal on the wire and what was transmitted from the network card don't mach, there must have beena  collision. there is no need to wait for an acknowledgement. it sends a jamming signal.




