## Recap
Aloha (ack packets)
CSMA/CD (eternet originally)
CSMA/CA (wifi) - different natures of the medium require different algorithms of the access control protocols

centred around one key idea: the packet will be sent eventually. there may be issues, but there will be systems in place to eventually send it correctly.

## ethernet
we put data in packts to allow data to be multilexed across the network with data from other machines.

at the packet level (around level 2), it is connectionless

frame is made of different sections as it is transmitted. voltage chaneges 

### make up of a frame
There are three sections - the header, data, and error checking.

The header contains the destination address, source address and frame type. There is also a preamble (states number of bytes per section) and FSD (starter frame delimiter) 
.

- The preamble is 56 bits of alternating 1s and 0s. The preamble detects the signal is now there and allows the network card to "lock on" or synchronise with the data being received.
- This is due to Manchester Encoding - it defines the clock. 
- To transmit a 1, start with a low signal, and in one clock cycle, transition to 1. (and a 0 the other way.)
- After the preamble, there is the SFD which is 8 bits, of which the **final two are 1s**.

The 48-bit MAC of the destination is sent after this. it is sent first so that the NIC can decide more quickly to stop copying the data into memory if it is not intended for it (unless in *promiscuous* mode)
*A special MAC address can be used to designate a broadcast packet that's sent to all machines.*

It is then followed by the source address

THe frame type is a 16bit/2-byte standardised number to show the type of data.

To know the size of the packet (it's dynamic), we can determine if the carrier disappears and the line is empty. The standard shows the line must be idle for 96 bits

CRC enables us to chek for errors in transmission, 4 bytes (32bit) at the end that is generated from the packet's data. The sender and receiver generate the same number using the same algorithm to determine if a transmission at the end.
A simple checksum can add up all values in the data and check that - but burst errors are common on a network, causing various changes to the data around a single point. 


### Part 2 - Lecture 10 

A more advanced cyclical redundany check (CRC) uses the xor OPERATOR and the shift register.

Smallest valid Ethernet frame: 672 bits long
largest; 12304 bits
> this is based on: bit length




Packet size: too little and the network activity is mainly cattying packet headers, too large and latency increases significantly