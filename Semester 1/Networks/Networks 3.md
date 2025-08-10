Book: Computer Networks and Internets

2 mechanisms for data transfer: parallel and serial.
- Parallel: use **many different wire**s to transfer data, reaching the destination at the same time
	- concurrent
- Serial: bit-by-bit, in order, sequentially, on one wire
	- Receiver needs to know how many its are being sent, bits in a character, how fast they are being sent (e.g. is 000100101 one? two? three? pieces? what is most/least significant?)
	- Some mechanism is needed to work out where one message begins and one ends

To identify the start and end of each character, we use start and stop bits, one to identify the start and end of each character. The start bit is always 0, and stop bit is always **1, which is then always transmitted and kept on the line until the next character is sent** and the start bit is 0. 0 is known to not be in the middle of a character 

If the line is read and there is a 1 to a 0, is 8 chars long but the tenth bit is 0, not 1, then although it started to look like it may have been a character, it is discarded as the stop bit was not 1.

This adds overhead: 25% extra bits (10 bits now for 8-bit input)

This is also known as full duplex: sending and receiving can be done at the same time, no need to wait for the other machine to finish transmitting. Half duplex: (original) Ethernet and WiFi. (Half duplex: like a wlkie-talkie, needs a mehanism to say that the conection is over and the other connection can be made)

Simplex: only send/only receive

## Data communication

RS232 - uses different voltages over a wire. Resistance and capacitance (??) in the cable means that it becomes less accurate to detect/more prone to interferene over a physical medium



Information source 1 -> source encoder -> encryptor (scrambler) -> channel encoder (encrypt) -> multiplexor -> modulator (modulates; converts to light in fibreoptics, electrical over copper, radio waves) -> physical medium -> demodulator (converts back to bits) -> demultiplexor (work out source heading to) -> channel decoder () -> decryptor -> source decoder -> destination 1

multiplexor: a switch that allows us to send multiple things over a medium. (i.e. image/audio goes to X/y, may be going/coming from different sources)


### Representing signals
RS232 uses +15V for a 0 and -15V for 1

Continuous oscillating signals go much farther (like a sine wave).









