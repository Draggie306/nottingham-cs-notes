### Recap

Aloha uses: Carrier sense multiple access with collision detection
WIFI uses CSMA/CD


Ethernet: no bother with acknowledgement due to wired nature of it.

Original Ethernet used the bus network. When nothing was being transmitted over the network, it would send (broadcast) the packet to all computers connected.


Carrier sense: detects bus usage, *senses* that data is being transmitted, and waits until immediately after this has finished and the line is clear.

Collisions can be detected through voltages being different. Computers send a jamming signal to ensure that the collision is detected by all machines, with no need for an ACK. 

> Eventual packet delivery does not guarantee the time at which a packet will be sent, just that it will be sent eventually. 


### Exponential back-off
We use exponential back-off to delay the packet resend to avoid further collision. The NIC will pick a random time at which to resend the packet, based on the maximum delay, *d*, and picks a value between 0 and *d*. If the packet collides again, d will be doubled. Eventually, the chance of collision will be so miniscule that the packet will be sent. 

Ethernet is a type of network but also includes protocol standard CSMA/CD too

Frame - use din lower level physical/data ink layer to term anything that encapsulates the data (packet)


### WiFi
based on ethernet
uses different collision detection system 

Hidden node problem: may not see devices outside its range.
This doesn't work with carrier sense, so no collision can be detected.

Uses Carrier Sense Multiple access with Collision Avoidance

Instead of detecting collision, we avoid it in the first place.
We send a small pilot packet to reserve the bus; if that doesn't collide, it can send its message.

A small packet called a Request to Send is sent, then the basestation sends a Clear to Send response to the RTS, removing the hidden node problem. All devices connected to the basestation receive this CTS and know not to send anything.


