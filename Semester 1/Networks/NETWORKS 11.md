


Limits of ethernet: practical limits to route around and in buildings.

Electrical limits
- resistance or capacitance. The further the signal, the more the degradation of it - voltage levels drop and sharp edges become less sharp and eventually undecodable.
- Time is also a problem: signal is not fully instant: at around 100m, it gets to the point where one machine and another machine may have already started even though carrier sense determined it was all okay. chance of collision increases as the distance increases

We use repeaters at level one to repeat on another network segment. generates a brand new signal.
There is a soft limit of 4 repeaters. There can be a backbone that is connected, with repeaters connected away from it, such as a backbone going up a building and separate repeaters connecting each room.
If anything, repeaters will increase the likelihood of collisions.

bridges are an alternative but similar. They operate on level 2. 
The bridge keeps a lookup table and because it operates on level 2, it can build a picture of where every machine on the network. It will only forward packets if and wen necessary, i.e. if the machine is on the other network connected to it. It is based on 2 simple rules:
- receiving each frame tells us what network the sending machine is on
- if we don't know which network a machine is on, forward the frame regardless.