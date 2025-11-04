

Recap:

- Monoprogramming alllows absolute addressing
- Multi-programming allows non-equal partitions to improve CPU use. This requires relocation and results in internal fragmentation: if we allocate 100mb per program but it only uses 1mb, we lose 

Overview: 
- Code relocation, protection
- Dynamic partitioning and swapping
- Segementation

## Relocation and protection

![](../../../Pasted%20image%2020251103150947.png)

The same address will be displayed if iVar is running twice simultaneously, but will have 2 values.

The principle:

There are two address spaces. The process has a logical address space between 0 and MAX, which is mapped to the physical address space. Sometimes, it will be identical “lucky”. Other times, it may be translated to another block of memory. The physical address space is the logical address *plus* the base - the addresses below.

![](../../../Pasted%20image%2020251103151254.png)

In the C code, both processes have the same logical address for iVar. Different offsets result in different physical addresses:

![](../../../Pasted%20image%2020251103151343.png)

There are three approaches to this:

- Static relocation at compile time: decide at compile time, code X will be linked to partition Y. 
	- *This is bad, as that area of memory could already be taken*
- Dynamic relocation at load time. When that piece of code is loaded, we add an offset to every logical address to get its physical address space location.
	- This will slow down the loading of a process
	- Doesn’t account for swapping: that process may not be there all the time; some processes may be taken out of memory as they may not be used for days, but cannot guarantee that it will be in the same location when reloaded into memory.
	- DLLs use this approach: they are kept in memory all the time, and this is where they are used to this day
- Dynamic allocation at runtime with hardware support: every time, we know the logical address, before we use the memory address bus, the CPU’s MMU adds the offset first.


A logical address is a memory address seen by the process: it is relative to zero, the compiler assigns them, and they are independent of the physical memory location (actual location in memory).

![](../../../Pasted%20image%2020251103151841.png)

### Protection

![](../../../Pasted%20image%2020251103152001.png)

Two special-purpose registers are maintained by the MMU, which contains a base address and bound: the base stores the start address, and bound holds the partition side. At runtime the base register is added to the logical address to generate the physical address, and this is compared against the bounds register



### Internal fragmentation

Instead of declaring partitions and sizes on startup, we allocate the exact amount of contiguous memory it needs, and a variable number of partitions. 

However, processes evolve over time. We can use swapping - this moves processes between the drive and main memory
- Some processes only run occasionally, some processes may use differening sizes of memory.

However, this leaves unusable chunks of memory distributed across physical memory:
![](../../../Pasted%20image%2020251103152639.png)

In one case, the gaps are too small to add a process, and other times the gaps are too big, which leaves small space: **external fragmentation**. Compaction (like defragging) takes a relatively long time. It is also complex to track free space and allocate memory to different locations.


Memory however is also “wasted” in physical memory within each process, in the area between the stack and the heap, due to the sparse address space.

The logical address does not have to be contiguous: it can be split into code, data, heap and the stack, stored anywhere in memory. Segmentation can be used to load only the relevant sections into memory, with each segment being contiguous. Each segment can have a base and bound pair, stored in a segmentation table, with part of the logical address used as an index for what segment it is. 

![](../../../Pasted%20image%2020251103153756.png)

This becomes simple: look at the 2 highest bits, to lookup into a table, which says the base and bound, and then read the offset. Segments can have protection bits (read/write/execute) and be shared between processes. If there is a read-only element then two processes can share the same variable.

The OS remains responsible for finding a large enough range of contiguous physical memory per-segment.






















