Can use different voltages to show different bits. Four voltage levels could give 2 bits of data at a time

Modulation schemes...


Transmission rate is detemined on the 
- Baud Rate (*pronounced board rate*), which is the number of signal changes per seconds
- Number of symbols that can be sent (number of different symbols that can be transmitted)
bits per second = baud rate x floor(log2 \#symbols)

> floor() always rounds down,, i.e. floor(2.99) gives 2; likewise ciel(2.0001) gives 3

Increasing the baud rate requires faster responses, and increasing the symbol count requires the computer to still be able to distinguish the difference between symbols in the same time.

Each computer will need to communicate with every other computer at once. However, this results in a full mesh network and becomes quickly unscalable, with `n-1` ports and `(n-1)!` cables. 

But - this is an assumption. Each computer does not need to connect with any other computer at the same time. To do this, we use a **shared medium**, like a cable or radio wave. Each computer connects to a shared medium. If data is sent over it, all machines that are connected to it receive that data 

To distinguish where data is intended to go, we need addressing. Control also needs to happen to ensure that only one computer/device is transmitting at a same time on the shared medium to reduce the chance of data corrupting. 
Access control is also needed to ensure that one device does not **monopolise** the shared medium resource. To solve this, we use packets. This allows other devices to send their packets without waiting for one monopolising device to completely finish.

Packet switiching is sending each chunk of data (packets) individually, in-turn, across a shared medium



