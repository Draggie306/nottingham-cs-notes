Taught by Geert De Maere. Researcher who contributed to Heathrow Airport’s scheduling algorithm. Nottingham has developed the best algorithm for runway scheduling in the world.

> Coursework: everything done so far is enough to complete the coursework.

Today’s goals: memory management, modelling efficiency of multiprogramming, and memory management based on fixed partitioning (used in 1970s and 80s).

## Memory management

There is a hierarchy of memory:
- Registers sit on the CPU, storing all data currently being worked on.
- They are incredibly fast and can be accessed at the same speed as a clock cycle. 
- Ideally, all memory is made of registers. However, it is very expensive.

 - Caches are thus used. Level 1/2/3 caches (1-4x slower than registers / 10-20x slower / 30-50x slower than a clock cycle, respectively)
 - Now there is an issue with cache coherency: updating data in the cache may not update it in another location (memory)
 - Most cache coherency issues are solved in the hardware and abstracted from the operating system.

- RAM is 100 to >1000x slower than a clock cycle

- Disks are 300k - 15m times slower than a clock cycle. This is a clear bottleneck. Minimising the impact of this is therefore essential


“**Higher memory**” is faster, more expensive and volatile. ”**Lower memory**” is slower and non-volatile. 

The OS provides an abstraction of memory: we do not provide the location (registers, ram location) when declaring a variable. There are complex internal mechanisms that support this. At a high level, memory can be seen as a linear array of bytes, starting at 0 and going to the limit.


### OS responsibilities
The OS must allocate/deallocate memory when requested. When we declare a variable, it is typically added to the stack. The compiler decides where it goes. A `malloc()` is more complicated: the OS finds a block of memory to allocate, and the OS’s standard library implements the malloc function and positions the finer malloc within this big block of memory. *This is all abstracted away.* The OS keeps track of which pieces of memory are still being used and by which process.

The OS also simulates “infinitely” large memory (compared to old computers) (this is 2^42 + number of address lines). It appears we can load as much as a process needs, but in reality the OS will give new chunks from discarded old chunks that are not needed any more.

The OS also controls access. We do not deal with protection - the OS checks if the process is allowed to access memory. 

It also moves data: whenever code is written, no code is written to load a file into memory from the disk first, but this still happens.

### Partitioning

Contiguous memory: each process is stored as one block in the physical memory in the computer. *We assume that the process is smaller than the physical block*.

Non-contiguous: the process is split into small blocks, each stored somewhere in the physical address space; the MAX(logical) may be adjacent to the OS, at the MIN(physical). This allows us to fill small gaps more easily.

Mono-programming is one single partition for user process.

Multi-programming can be with fixed equal- or non-equal sized partitions, or with dynamic partitions.

### Mono-programming

This has one single user process; no multi-programming. A fixed region of memory is allocated to the kernel, and the remaining memory is reserved for a single process. The process has direct access to physical memory. This is how MS-DOS worked.

There are 4 key components: machine code, data (constants declared), heap (dynamic memory), and the other side is the stack (e.g. stack frame). The heap and stack are placed on opposite sides of the address space: the heap grows up and the stack grows down with recursive calls. 


![Pasted image 20251028123129](../../../Images/Pasted%20image%2020251028123129.png)

> This used to be easy to work out: get the pointer of the main function (code), a pointer to an int (stack) and a malloc’d pointer (heap) and printing the memory address. However, the OS now applies memory address space randomisation to reduce security risks.

With mono-programming, there is no protection between the user processes and direct access to physical memory - so direct access to the OS is possible from the user code. The OS is also a process, so 2 processes must run anyway - defeating some logical reasons for its utility.

Multi-programming can be simulated by swapping: writing the process to the disk and loading a new one (which is very slow), or with threads within the same process. 

Mono-programming results in low CPU utilisation: if a process uses I/O 80% of the time, then it is not doing anything for 80% of the time as there is simply no other process available to do work. 

> Imagine a disk rotating at 7200 RPM, taking 4.2ms to rotate half a track
> Imagine a CPU running at 3.2 GHz (approx. 3.2 ×10^9 instructions per second) 
> I/O is slow, we are missing out on 3.2 × 4.2 × 10^6 instructions (13.44m)!

The more processes we have, the more chance there is that a process wants to actually use the CPU. If each process `n` has a chance `p` of using I/O then we can use `p^n` for the chance of using the CPU resources.    

![Pasted image 20251028124123](../../../Images/Pasted%20image%2020251028124123.png)

### Multi-programming

Multi-programming improves resource use. 







Issue: the compiler no longer knows in what partition code is located in, and therefore what addresses need to go in the machine code.










