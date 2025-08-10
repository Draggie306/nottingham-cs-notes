Networks are built in layers of abstraction.
- Physical layer is less CS but more physics, maths and electrical engineers. 
- As we go higher up, we build more layers of abstraction. 
- ARP converts IP addresses on L3, to 

Instead of directly connecting every computer, we use a shared medium. However, this  introduces some problems. We need to ensure that only one device is using the medium at a time, and that one device doesn't use it for an unreasonable length of time.

We use packets, 


to work out the start/end and to determine the size of the data payload, we can specify the length of data in the header, or use **packet/byte/bit stuffing**. This has a certain character to signify the stat and end of a packet, with another character in the middle to show that the data should not end prematurely.

In a star topology, they all connect to a central point (hub), and all communication travels to there