


## Rotational drives

Rotational hard drives are made of aluminium/glass platters in magnetised materil.

- Read/write heads fly just above the surface with an actuator to make sure the heads are on the correct tracks. 
- Data is stored on both sides of a platter.
- They rotate at a constant speed, so near the spindle (centre) is less fast than on the outside. 
- A disk controller abstracts the low level interface. *An additional level of indirection*. The detail of "go to track X on secotr Y" is hidden

These drives are 4 orders of magnitude slower than main memory.

### Format
Tracks are concentric circles on a side of a platter, organised in cylinders: all tracks in the same position relative to the spindle. Segments of a track are sectors.

In each sector, there is a preamble and error correcting code to prevent issues when reading. 

The time to move the read/write head from sector to sector will probably read a different sector. We can use **cylinder skew**: an offset (to go from one track to the next) added to sectors in adjacent tracks to account for the seek time, reducing rotational delays. 

The drive needs to make sure the sector to read is positioned below the R/W head immediately. The **seek time** is the time needed to move the arm to the cylinder. 

Sometimes, there will be bad luck: the sector will not be positioned below the head, requiring a full rotation, and sometimes it will be right there. On average, the delay is half a rotation of delay. This is **rotational latency**. 

Transfer times is given by N bytes take 1 revolution (16.7ms) b contiguous bytes takes b N revolutions `Tt = b/N × ms per revolution`

The access time is the access time + rotational delay + transfer time.

![[Pasted image 20251118121528.png]]

The estimated seek time `Ts` to move the arm from one track to another is approximated by: Ts = n× m +s (1)

- n the number of tracks to be crossed
- m the crossing time per track
- s any additional startup delay


To read a file of 256 sectors: 
- The average seek time is about 20ms, with 32 sectors/track
If the file is contiguously stored, the time to read the first track is 20 + 16.7/2 + 16.7 = 45ms (Seek time + rotational delay + transfer time)

### Disk Scheduling
When each process had a PCB, stored information would go in there as administrative overhead. Similarly, we have a file control block that keeps track of all information associated with a file.

The OS must position files strategically and optimise request to minimise overhead for seek time and rotational delays.

Thinking about requests over time by multiple processes: in a queue, the OS could re-sequence the items to minimise seek times. There is a table of requested sectors per cylinder.


### Disk scheduling 
Disk scheduling algorithms determine the order of disk requests being processed. They are heuristic, so not optimal but good enough. 

Given a disk with 36 cylinders, from 1-36:

- First come first served: processing the requests in the order they arrive. Travels too many tracks wastefully
- Shortest seek time first: selects the request closest to the current head position. This reduces tracks crossed by about 50%, but can cause starvation (continuous requests for the same location) and heavy movements towards the end of the list. 

SCAN:
- Keeps moving in the same direction until the end is reached.
- Service all pending requests as the head passes over them.
- At the final cylinder, it reversed direction, and this is repeated.
- The upper limit on waiting time is 2\*number of cylinders, so no starvation occurs. 

However, the middle cylinders are favoured under heavy use (max wait time is N tracks for middle but 2N for the edge). 


These algorithms work better when there is a high volume of read/write requests. 


### Driver caching
Nowadays the time to seek is longer than the rotational time, so it makes sense to read more sectors than required and cache them. It reads sectors during the rotational delay and can read multiple sectors when asked for the data from one sector.

## Solid state drives

SSDs are defined as being SLC, MLC and TLC (single level charge): number of bits in a transitor. The key problem is that they wear out: every time a bit is changed, a residual voltage is left. What used to be 1 becomes 0.9999999. Over time it becomes harder to distinguish between 0 and 1. To level the wear across the drive, the OS takes this into account.

Disturbance: if 1 is written is one place, 1 may be accidentally written in another place. 

SSDs are organised into pages (individual blocks), which are grouped into blocks, and these are located in banks. There is also a flash controller and memory used for caching.

![[Pasted image 20251118124457.png]]

If we want to write some information in one page within the block, we need to erase the entire block, before we can write data to one page. On modern blocks, they contain 1024 pages. 

Reading takes 10s of microseconds, but erasing takes a very long time (milliseconds). Writing takes 100s microseconds, but it is the erase operation that takes the longest.

This is write amplification: 1 page must be written, but all the remaining pages must be erased and re-written. 

![[Pasted image 20251118124830.png]]

