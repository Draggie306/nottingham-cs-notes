

## Intro

CPUs are designed to execute instructions sequentially. A pipeline is made of fetching, decoding and executing data. Superscalar CPUs provide instruction-level parallelism, evaluating multiple instructions in parallel. 

CPUs employ many tricks to run faster. **Out-of-order execution** runs instructions the fastest for the CPU, not necessarily in the code's order. **Speculative evaluation** runs instructions in advance, based on what the CPU thinks will run next.

Registers are a small, fast part of memory located close to the CPU. There are specific registers: program counter holds which instruction should run next, program status word (PSW) holds flags for the CPU state, and general-purpose registers hold operands for CPU instructions. The compiler decides what to keep in registers. **Registers are part of the running program's state.**

### Memory Management Unit

The compiler assumes a program's logical address starts at `0` and ends at `MAX`. However, the physical location of memory cannot be known to the program beforehand - it is influenced by what other code is running, or multiple instances of the program requiring some unique space in memory. If the program does not run at physical address `0` but instead `100`, the MMU can add an offset of 100 to each compiled address. As the MMU is a register, its state is part of the overall program's state too.


### Kernel and user space

Code running by the user is executed in the CPU's user mode and is restricted - it cannot directly interact with hardware. Code running in kernel mode is referred to as the kernel - the core of the operating system, and can interact directly with the hardware. 


### Interrupts
Programs need to respond to events such as time passing, I/O events, peripherals, the network and erroneous instructions like dividing by 0. Interrupts are how these are handled. 

Interrupts are a mechanism for changing the normal flow of program execution. They can happen asynchronously (unpredictably, e.g. user input) or synchronously (directly triggered by the CPU; an exception). 

During execution of a task, an interrupt may be signalled (e.g. a previous I/O request is now available). The CPU then will store parts of its current state (registers) and runs a handler in kernel mode to service the interrupt, before switching back to the first task.

As they can occur at any time, handling them should not take a long time. This can be done by splitting handled work into a top and bottom component: the top is dealt with immediately (and is more urgent), and the bottom is scheduled to complete later on. They can also be nested - interrupted by higher priority interrupts. 

#### CPU utilisation
As I/O-bound processes are very slow, it is inefficient to naively wait for these devices to respond. Instead, interrupts can "call back" from the I/O device when an operation has finished, allowing the CPU to spend more time on useful calculations. This can be implemented by e.g. functions named `send_write` and `write_handler` that perform the corresponding actions.

### System calls
A system call is how a program requests a service (memory allocation, files, processes, etc.) from the OS. These are often done through APIs - a library of functions in user space. An API function called may make zero or many system calls. 

To execute a system call, its unique system call number is stored in a register, alongside its parameters. Then, a synchronous interrupt is triggered by an instruction called a **trap**. This interrupt is handled by kernel mode code, which calls a system call service routine, based on the call number and parameters in registers, continuing until the interrupt completes and returns to user mode code. 

There is no guarantee that the system call service routine will service the request immediately, and there is no guarantee that the caller will run after being serviced. This allows the OS to choose whether or not to run other programs instead.


### Use of C

C is used as it is performant, portable and predictable. There is no garbage collection (which is unpredictable) and it is compiled directly onto the hardware, for many different platforms.


# Processes

A process is (an abstraction of) a running program instance. A program is a passive file, a process has control structures associated with it, may be active and may have resources assigned. All data required to administer the process is stored by a process control block (PCB), a protected kernel data structure. The process table, to manage ALL processes, is simply an array of PCBs. Each process has a unique process identifier (PID).

The PCB contains **process identification** attributes (PID, parent PID), process **control information** (state, scheduling data), and **state information** (registers, program counter, program status word, files open).

A process may be **new** (just created, has PCB, waiting to be admitted), **ready** (waiting for CPU availability), **running** (currently on CPU), **blocked** (waiting) and **terminated** (no longer executable, finished/crashed).

These are typically stored as queues: a process can be admitted to the ready queue, dispatched to the CPU, and then added to an event queue first before being re-admitted to the ready queue.


![Pasted image 20251007115338](../../../Images/Pasted%20image%2020251007115338.png)

## Context switching

Modern devices are multiprogramming systems. The CPU is divided into time slices (quanta) and multiprogramming is achieved by interleaving process execution across these time quanta. Exchanging control between processes is done via context switching.

The response time of a process is the time from its creation to its first CPU access (new -> ready state). The effective CPU utilisation is the fraction of time the CPU is doing truly useful work (not context switching) - short time slices result in good CPU time but low effective utilisation, and vice versa.

To context switch, the kernel will save process state attributes to the PCB, then update the PCB's state (running -> ready/blocked/terminated). It will then add the PID to the relevant queue and run the scheduling algorithm to determine which new process to update from ready -> running before restoring its state and returning control to the new process. 

## Scheduling

Process schedulers can be classified based on **time horizon**: long, medium and short-term. 
- Long-term schedulers (largely absent from modern OS) control the amount of multi-programming by mixing CPU and I/O-bound processes to keep many resources busy.
- Medium-term controls swapping and amount of multiprogramming (also largely absent)
- Short-term decides what process to run next. These manage the ready queue directly, and are frequently called by e.g. clock interrupts, blocking system calls and I/O interrupts.

Schedulers can also be classified based on approach.
- Non-pre-emptive (DOS): processes volunteer to yield their use of the CPU. This reduces scheduler's overhead but is very risky - if processes get stuck in an infinite loop, they will never terminate.
- Pre-emptive: processes can be forcefully (by e.g. clock signals) or voluntarily interrupted. This requires more context switches but prevents monopolisation.

The scheduler should ensure users are satisfied: have a low response time and turnaround, and to be predictable. For the system, it should also maximise the number of processed jobs, and to ensure processes are processed fairly (even wait time/no starvation).

- Average response time is calculated by adding the number of the first slice of each process's execution, and dividing by the number of processes.
- Average turnaround time is calculated by adding the number of the final slice of each process, and dividing by the number of processes. 

The CPU burst time (or execution time) is the amount of time the process needs to complete execution.

### First come, first served

+ Pros: Positional fairness - there first, so finish first.
- Cons: Favours long processes over short ones (e.g. shop checkout, does not affect long jobs but is mean to short ones); may compromise resource allocation (I/O favoured over CPU time)

### Shortest job first
+ Pros: always gives the optimal turn around time
- Cons: starvation for long jobs; compromises fairness and predictability (a "small" job may look long versus "tiny" jobs); processing times must be known beforehand

### Round Robin
Is a pre-emptive version of FCFS (runs in the order added), but which forcefully interrupts processes at a timer's interval. 
+ Pros: improves response times; effective for general-purpose systems
- Cons: increases overhead with context switches; favours CPU-bound process over I/O (may be allocated 100 slices when I/O only requires 1 CPU slice), can be reduced to FCFS with very short slices.

### Priority queue
A pre-emptive algorithm that schedules processes by high -> low priority. Within each queue, a round robin approach is used. The process priority is saved in the PCB.

+ Pros: can prioritise I/O-bound jobs
- Cons: low priorities may become starved if priorities are not updated.


### Multi-level feedback queues
Within each internal queue, a different scheduling algorithm can be used. Jobs can move between queues, commonly by moving lower priority queues if too much CPU time is used (to prioritise I/O-bound processes) and move to higher priorities to prevent starvation and *inversion of control*.

+ Pros: can temporarily promote processes and demote resource hoggers; are very configurable (queue count, migration policy, internal queue algorithm)
+ Cons: more difficult to implement

#### In Windows 7
The Windows 7 MLFQ algorithm uses a pre-emptive scheduler with dynamic priority levels. It has 2 priority classes with 16 total priority levels: **realtime processes** having a fixed level, and **variable processes**/threads can have their priorities boosted/changed temporarily.

Priorities are based on the process's base priority (between 0-16) and their thread's base priority. The thread's dynamic priority changes during execution, preventing starvation and priority inversion.


#### In Linux (CFS)
Linux uses the Completely Fair Scheduler. It has 2 types of tasks: real-time (broken down to FIFO and Round Robin) and pre-emptive, time sharing tasks (similar to variable processes/threads in Windows 7).

Realtime FIFO tasks have the highest priority and scheduled with FCFS, with pre-emption for even higher priority jobs should they enter the queue. Realtime Round Robin tasks are pre-empted by clock interrupts and have a time quanta associated. 

The ideal scheduler allows all N tasks to run simultaneously with 1/N of the CPU's power. To estimate this, we choose a **target latency** (time before every task gets CPU access; response time) with each task running for 1/N of this. There is also a **minimum granularity** of time to run on the CPU before being replaced, reducing context switching.

To be fair, the task's **virtual time** on the CPU is recorded, and **all tasks are ordered in ascending order** (in a red-black tree). The task with the lowest virtual time is considered to have been treated the most unfairly so will be run next. After that task spends 1/N of the target latency on the CPU, it is replaced by the next lowest task.

A weighting scheme is used to account for multiple priorities (we assume the weight is the task priority for simplicity). The recorded **virtual time** on the CPU is the **real time**, scaled up by the weight (virtual time runs at different speeds for different priorities). For example, after 100ms of real time, a priority 1 process may be considered to have used 100ms of CPU time, whilst a priority 2 process is at 200ms. This will mean that tasks are prioritised appropriately and allocated different future time slices. 

When new tasks are added, their virtual time is set to the minimum virtual time across all tasks. Blocked tasks will also have their virtual time set to the minimum virtual run time minus an offset, or the task's old virtual run time, whichever is larger.


## Threads 
A process is made of two units: 
- **resources**: address space containing the process (data, heap, stack), plus files, I/O devices and channels.
- **execution trace**: instructions to run on the CPU

**Resources** can be shared by multiple execution traces, so we can make threads an abstraction of execution traces. Each thread has its own execution context - program counter, stack and registers (calculations should be done independently) - but all threads have access to the process's shared resources. 

Threads have the same states and transitions as processes, a thread control block, and thread table of TCBs and a thread ID.

![](../../../Images/Pasted%20image%2020251009151632.png)

### Why threads

There is less overhead to adjust threads (all have the same shared, unprotected address space within a process) and some CPUs have hardware support for multithreading - true concurrency. As threads of a process share memory, communicating between threads is faster than inter-process communication. 

### Threading implementations

#### User threads
Many-to-one: one kernel process, but the process itself maintains a thread table and thread runtime system without the kernel's knowledge. 

This has the benefits of requiring no context switching or system calls, plus having full control over the scheduling within the application, and can be run on OSes that do not natively support threading. 

However, blocking system calls such as file accesses suspend the entire process, as the kernel sees all requests coming from one process. There is also no true concurrency as the kernel schedules the process to run on once CPU and it is non-pre-emptive with no interrupt mechanism.

#### Kernel threads
The kernel manages threads through an API and system calls. By storing threads in the kernel's thread table, blocking threads can choose other threads from the same or different process. They are one-to-one.

This is pre-emptive, requires no thread runtime in user applications, and can achieve true parallelism. However, many mode switches occur which result in lower performance. 

#### Hybrid threading

User threads can be multiplexed onto kernel threads: the kernel sees and schedules a number of kernel threads, and the user application's threading library creates an unrestricted number of user threads from these. 

Thread libraries can be implemented in user space or based on system calls.

Although threads share the same process's address space, they must have unique stacks and program counters as otherwise function calls and return values would interleave, breaking each thread's control flow and causing incorrect behaviour. 

### Multiprocessor scheduling

#### Shared queues

To determine which thread to run and where to run it on a multi-core system, a shared queue can be used - a single or MLFQ shared between all CPUs, which all dequeue the next task.

+ Pros: automatic load balancing
+ Cons: queue contention, does not take advantage of the CPU state - cache and registers become invalid when moving to another CPU

#### Private queues

Private queues are a per-CPU queue, with each thread only running on once CPU. This allows better re-use of CPU state, such as the cache and translation lookaside buffer, and reduces contention. However, there is less load balancing: all processes may be placed on one CPU, so migration between CPUs is still possible. 

### Thread types

There are two types of thread: related and unrelated. 

- Related threads communicate and, ideally, run together, like a search algorithm. These cooperate, exchange messages and may share information between other threads, all in the "ready" state. 
- Unrelated threads are independent, from different programs or different users.

On a multiprocessor system, the goal is to get collaborating threads running at the same time across multiple CPUs. This can be done with two approaches:


#### Space sharing

This is when **processors** (space) are **partitioned between groups of related threads**/processes, rather than time sliced among many different, unrelated threads.

- *N* related threads are allocated to *N* dedicated CPUs, when these CPUs are available. 
- *M* related threads are kept waiting, until *M* dedicated CPUs are available. 
- As threads terminate, their CPUs are returned to the available CPUs list.
- The CPUs are not multiprogrammed to keep related threads running together, resulting in idle CPUs.

This has the potential for high efficiency with low overhead, but may result in low CPU utilisation and wasted cycles if tasks are not designed for this.

#### Gang sharing

Here, the scheduler groups related threads into gangs to run across available CPUs. It is pre-emptive with identical time slices across CPUs, allowing for tasks to be synchronised. 

However, because of this time slice synchronisation, if a thread blocks, the rest of the time slice will be wasted.

Space sharing does not use time slicing or pre-emption, resulting in lower CPU usage and idle CPUs. Gang scheduling does use them both, resulting in higher CPU usage but blocking calls waste time slices.


# Concurrency

Skip!


# Memory Management

There is a hierarchy of memory: registers (1 cycle) -> L1/L2/L3 caches (2-4, 10-20, 30-50 cycles) -> main memory (100/1000+ cycles) -> disks. (300k - 15m cycles) with faster, volatile, expensive "higher memory" and slower, cheaper, non-volatile "lower memory". The OS provides memory abstraction.

## Memory Models

### Contiguous & mono-programming

Contiguous memory allocates in one single block with no holes/gaps.

In mono-programming, there is a fixed region given to the OS whilst the remaining is given to a single process, which has direct access to memory. This was the case in MS-DOS. The stack grew down and heap up, with data and code too. This process always is located in the same physical memory location -- **absolute addressing**. 

However, as the process has direct memory access, it can access OS memory. Multi-programming is expected on modern machines, and this can be simulated through either writing the process to the disk and loading in a new one or with threads within the same process. This approach is common in embedded systems. 

### Multi-programming

The idea behind multi-programming is simple: the more processes there are, the greater the chance that one wants to use CPU, as opposed to waiting for I/O.  If each process `n` has a chance `p` of using I/O then we can use p<sup>n</sup> for the chance of using the CPU resources. CPU utilisation is 1 - p<sup>n</sup>. 

Given a computer with 1MB memory, with the OS using 200kb, we can fir 4x200kb processes on it. If each process has an I/O wait time of 80%, the overall system utilisation is around 60% (1 - 0.9<sup>4</sup>). Adding an extra 1MB memory (5 processes) increases utilisation to 87%. 

### Partition sizing

Multi-programming can be implemented by using static, equally-sixed contiguous partitions: allocation is easy and there is little overhead to calculate positions and which partitions are used/free by the OS. However, it results in low memory utilisation with excessive internal fragmentation. 

It can also be implemented to use static, non-equally sized contiguous partitions: this reduces internal fragmentation but requires extra consideration for process allocation: larger processes should not be given small partitions. This can be implemented with one private queue per partition (each process is given to the smallest partition it fits in, reducing internal fragmentation but can cause starvation with many small jobs not using all the available partitions), or a single shared queue that can allocate smaller jobs to large partitions, at the cost of increasing internal fragmentation.


## Relocation

A process running may have the same logical address for a variable, but different offsets result in different physical addresses - `physical = logical + base`.

This can be done in 3 ways:
- **Static relocation at compile time**:  during compilation, code X is in partition Y. This obviously won't work reliably as the partition may be occupied already.
- **Dynamic relocation at load time**: apply an offset to every logical address. This slows down process loading, doesn't account for swapping locations/frames in and out of memory, and is generally used by DLLs as they are kept in memory continually.
- **Dynamic relocation at runtime with hardware support**: before memory is accessed, the CPU's dedicated MMU adds the offset to the logical address first.

The principal of relocation is that the address/partition of a process is unknown at compile time. The logical address space must be mapped to the physical address space, once known. This must be done in any OS that allows processes to change physical memory locations. 

The MMU contains a base and bound register: the partition's start address and size, respectively. At runtime, the base register is added to the logical address to generate the physical address, and compared against the bound register. 

### Dynamic partitioning

Fixed partitioning results in internal fragmentation: an exact partition size for the process may not be available, so does not get fully used. Dynamic partitioning uses a variable number of partitions, and each process is allocated the exact amount of contiguous memory, fixing **internal fragmentation**. This improves overall memory utilisation. 

However, this creates **external fragmentation**: with **swapping** a process in and out (as memory requirements change, processes only need executing occasionally, or with memory pressure), a "hole" is created and new processes may be too small for it, or not use it wholly, leaving space remaining - fragmentation. Tracking free space becomes more complex. 

### Segmentation tables

Dynamic partitioning loads the whole logical address space into physical memory. Segmentation loads only rhe relevant sections as contiguous segments into memory, with each having an independent base and bound pair, stored in a **segmentation table**. The logical address is used as an index into the segmentation table.

The segment has a binary code, and an offset (relative to segment's start) alongside protection bits and the base/bound to be used by the MMU


## Managing free space


### Bitmaps

A bitmap can be set up so that each bit is `0` if its corresponding block of memory is free and `1` if it is used. Memory is split into blocks of e.g. 4KB, so 8192 bits represent 32MB of memory but the bitmap occupies just 1KB of storage.  A trade-off exists between the bitmap size and block size: larger blocks increase internal fragmentation but smaller blocks make searching the bitmap longer.

### Linked lists
A linked list allows the OS to record a variable number of free and used partitions. Each element contains data, such as the start address, size, and if it is free or allocated, with a pointer to the next partition. 

#### First fit
The first fit scans from the start until a sufficiently large gap is found: if the space is the exact size, allocate it, otherwise, mark the first entry with the size requested and allocate and the second to the remaining size. 

#### Next fit
This is the same as first fit, but the algorithm keeps track of where the allocation stopped next time. This gives all memory an even change of allocation. However, this performs worse than first fit. 

#### Best fit
Best fit searches the entire linked list for the smallest free section large enough to allocate to the request. This creates many tiny "holes".

#### Worst fit
This finds the largest available partition and splits it. The leftover part is still very large (and perhaps more useful) but it is generally not good in practice. 

#### Quick fit
This maintains multiple lists of various commonly-used sizes, such as 4K, 8K, 16K. It is much faster as it uses secondary, more specific lists, but creates many tiny "holes".


### Coalescing & compacting
When two adjacent entries in the linked list become free, they can be combined, and the linked list reordered. Typically this occurs by examining the next/previous entries on every free, and adjusting the links as appropriate.

Compacting can be used to analyse free blocks distributed across all memory, but requires swapping in/out of memory, moving and coalescing to truly optimise memory allocation. 

## Paging

Paging breaks the assumption that memory must be contiguous. It uses fixed partitioning and relocation. Memory is split into very small blocks (e.g. 4KB), processes are allocated some of these, and are **perceived to be contiguous** by the process. It reduces internal fragmentation to a few remaining blocks, and there is no external fragmentation (gaps between blocks).

A **page** is a small block of contiguous memory in the logical address space. 

A **frame** is a small block of contiguous memory in the physical address space. 

### Address translation

Pages are mapped onto frames of typically the same size using address translation.

The leftmost `n` bits represent the page number: 4 bits = 16 pages. The rightmost `m` bits represent the offset within the page: 12 bits = 4KB pages. A logical address of `0001 000000000000` means page the start of page 1.

Translation occurs in the page table. The page number is translated/mapped to a frame number, and the offset is simply copied (as the page/frame sizes are equal). The MMU uses a page table for devices with hardware support. 


### Virtual memory

The principle of locality means that code and references to it are usually clustered close to each other, and code/data manipulation are only usually a small subset of all pages of the program. Therefore, not all pages have to be in memory at any given time; desired blocks can be loaded on-demand. 



#### Page faults 

When the CPU accesses a page not in memory, a page fault is generated:
- trap the OS (save registers, execute interrupt service routine to determine frame and issue I/O)
- Context switch to another program
- Interrupt received for I/O completion: save registers, update page table, wait for original process to be scheduled
- Context switch to original process

This improves CPU utilisation as more processes can be in memory at any given time. The logical address can be now larger than the physical address space. 

### Page tables

In the page table, the physical address mapping may be marked with an **absent** bit flag.

To keep values synchronised, there may also be a **modified** bit flag used to only write modified bits to the disk, and also a **referenced** bit flag to not evict a frame from memory if it is currently in use.

The **resident set** of a process are all the pages with an associated physical frame, "residing" in memory.

Now, for 32-bit machines, the address space is 2<sup>32</sup>  with pages of 2<sup>12</sup> bytes (4KB), 20 bits can be used to number pages, equal to 4MB at 4 bytes per page table entry.


### Multi-level page tables
As page tables increase in size with memory size, they cannot be stored into registers. Increasing page size reduces page table size but increases fragmentation.

To combat speed and size constraints, MLPTs are used. The page number is divided into an index into the root page table (which is always kept in memory) and an index into the second-level page table (which may be in virtual memory) containing the page <-> frame mapping. However, with 2 levels, memory referencing becomes 3x slower (much worse if virtual memory is hit) and there may be up to 5 levels, creating a bottleneck.

### Translation look-aside buffers
TLBs are located inside the MMU and are used to cache the most frequently-accessed page table entries. They can be searched in parallel and work due to the principle of locality - a large number of references to a small number of pages is likely. 


### Inverted page tables

These are directly proportional to the size of main memory. It contains one entry per page, indexed by frame number. It is searched by hashing the page number and Process ID as an index.

Entries in inverted page tables have a PID, page number, protection bits and a link pointer to the next entry, as collisions are possible.

Hash tables reduce search time versus multi-level page tables, and translation lookaside buffers help to improve performance by reducing the frequency of searches.


### Paging decisions

**Page fetching policies** are used to determine what and when pages should be **loaded**, and **page replacement algorithms** are used to determine what and when pages should be **removed** from memory.

#### Page fetching policies

**Demand paging** only loads pages when needed. It starts the process with no pages in memory: the first instruction will immediately cause a page fault. More page faults will be repeatedly generated, until the entire locality is brought into memory, and then page faults will stabilise. 

Pre-paging brings the entire working set into memory at once. This reduces the rate of page faults, but requires tracking the working set and an aging algorithm. It aims to load pages before page faults are generated. 

#### Page replacement algorithms

If all pages are in use, the OS must choose which to remove to load a new one. This takes into account when the page was last used, expected to be re-used and whether it has been modified (only modified pages need to be written to the disk). 


##### Optimal page replacement
Ideally, every page is labelled with the number of instructions that will be executed before it is used again, and the page with the greatest number of this will be evicted. In practice, this is infeasible but useful for comparison with other algorithms.


##### First in, first out
This maintains a linked list, with new pages added at the end of the list. The oldest page - the one at the head - is evicted when a page fault occurs.

It is easy to implement but there is no way to discriminate frequently-accessed pages with rarely-used pages.


##### Second-chance FIFO
If a page is at the front of the list AND it has not been referenced, it is removed. Otherwise, it is placed at the **end** of the list and the **reference bit is reset**. This works better than FIFO, but can degrade to FIFO if all pages are referenced, and it also requires much overhead as the list changes constantly with popping and pushing.

##### Clock replacement
Second-chance FIFO can be improved by maintaining a circular list. A pointer "clock hand" points to the last page visited, advancing through the elements, setting their reference bit from 1 to 0, until it meets an element with 0, which replaces its page. It may still be slow for long lists due to linear array access.

##### Not recently used
This tracks **referenced and modified** bits in the page table (reset periodically).

There are 4 classes: not referenced and not modified 0 -> not referenced and modified 1 -> referenced and not modified 2 -> referenced and modified 3. 

It can be implemented by scanning through all pages in class 0, and removing that one. If there are none, scan again for class 1, but set the reference bit to 0 for each visited page. If still none, then start this process again - all pages in 2 and 3 are now 0 or 1.

##### Least recently used
The OS keeps track of when a page was last used in the page table. This is costly to order, but can be implemented in hardware with a counter that increments after each instruction. This is very close to the optimal, but difficult to track.


### Working set

The resident set is **all pages of a process residing in memory**. The working set is the **set of referenced pages in the last working set window** (measured in memory references OR process time) for that process.

Working sets can be used to tune the size of resident sets, optimising memory utilisation. Pages can be removed from the resident set if they are not in the working set - if only 2 pages are used over the last 10 processes, the resident set size can be set to 2.

Setting the working set's window value to small will result in missing pages, but too large will cause too many unused pages to be present. (Infinite means all pages are in the working set).

As the working set is costly to calculate, we can use the page fault frequency instead to approximate whether to increase/decrease the resident set's size.

### Resident set

Small resident sets can store more processes in memory, improving CPU utilisation but creating more page faults. Large resident set sizes may not reduce page fault rate and cause diminishing returns, so a trade-off exists.

Replacement policies can be local (same process has a page replaced) or global (another process has a page taken away), for variably-sized resident sets. 

### Paging daemon
A daemon run by the OS at periodic intervals, most often during low CPU/user usage, that selects pages to evict if too few frames are free. It is often more efficient to keep a number of pages free for future page faults, otherwise finding, evicting and writing to the drive will increase page fault times.


### Thrashing
This occurs when pages are swapped out and immediately loaded again. This happens when all available pages are in active use and a new page needs to be loaded: the evicted page will have to be reloaded soon, as it is still active.

When the scheduler sees low CPU utilisation, it may increase the degree of multi-programming. Frames will then be reallocated from existing to new processes, creating an I/O backlog with page faults. The CPU's usage then continues to drop so the degree of multi-programming keeps increasing. 

This can be prevented by using better page replacement policies, ensuring processes do not have too few pages, and detecting if the page fault frequency is over a thrashing threshold and stopping the degree of multi-processing.


# File Systems


At the low level, there are shared layers and file-system specific layers.

Shared layers include interacting with the device's controller/drivers/interrupt handlers, and also include the basic file system - instructing device drivers to read/write blocks.

File-system specific layers have different implementations. A bitmap or linked list can be used to model logical blocks for files and free space, and the local file system manages metadata, directory structures, and protection. 

The application programs on the system define the structure of their files.

## Rotational hard drives
R/W heads fly above the surface (0.2-0.07mm) of aluminium/glass platters, connected to a single disk arm controlled by an actuator. Data is stored on both sides of the platter. The platter rotates at a constant speed - near the central spindle is slower than the outside. A controller abstracts the low level interface. Rotational HDDs are ~4 orders of magnitude slower than memory.

Disks are organised into tracks (a circle of a side of a platter), sectors (segments of a track) and cylinders (tracks of the same position, relative to the spindle). Sectors usually have equal numbers of bytes, containing a preamble, data and ECC - actual disk capacity is slightly lower because of this low-level formatting.

### Access times
Cylinder skew is an offset added to sectors in adjacent tracks, to account for seek time. 

**Access time** is **seek time** (required to move the arm to the cylinder) + **rotational latency** (time before the sector appears under the head, on average half a rotation) + **transfer time** (from start to end of data being under the head).

As requests may happen concurrently, access time can be added to a **queuing time**. This allows the order of operations to be optimised. 

The estimated seek time to move the arm from one track to another can be approximated by: `number of tracks to cross` x `crossing time per track` + `startup delay`. 


The OS/hardware must position/organise files and sectors strategically to minimise overhead from seek times and rotational delays. I/O requests that happen and go through system calls can be kept in a **table of requested sectors** per cylinder, allowing the OS to re-sequence them optimally.


### Disk scheduling
To determine the order to process disk requests for minimal overhead, heuristic algorithms are used (none are optimal). 


#### First come first served
Processes the requests in the order they arrive. 

Given access to cylinder locations:
11 1 36 16 34 9 12
In the order of arrival (FCFS) the total length is:
|11-1|+|1-36|+|36-16|+|16-34|+|34-9|+|9-12|=111


#### Shortest seek time first
This selects the next request that is closest to the current head position. This reduces travel distance by about 50% versus FCFS. However, continually arriving requests for the same location could starve other regions. 


#### SCAN algorithms
This algorithm keeps moving in the same direction until the end cylinder is reached. It continues in one direction, servicing all requests as it passes over the cylinder, and then reverses the direction at the end. The maximum waiting time is `2 * (number of cylinders)`.  

*Look-SCAN slightly optimises this by only moving to the last cylinder with a request, versus the whole disk.*

SCAN favours the middle cylinders for heavy use. Further, as seeks are cylinder-by-cylinder, the arm can stick to one cylinder if it has many requests on the same track.

C-SCAN is an improvement by moving one-way until the last cylinder is reached, when it then reverses direction but does not service requests. Once at the first cylinder again, it reverses direction but services. It is fairer and equalises response times. 

N-step-SCAN divides the queue into segments of N requests, each handled with SCAN.

Optimal algorithms are very difficult to achieve, as requests arrive over time and algorithms need perfect knowledge of information beforehand. 

### Driver caching
The time required to seek to a new cylinder is often more than rotational time. Therefore, it makes sense to read more sectors than required, during the **rotational delay**. Modern controllers can read multiple sectors at a time.


## Solid state drives
SSDs suffer from wear out and disturbance. They are organised into banks, blocks and pages, and some have volatile cache memory. 

The Flash Translation Layer maps logical blocks to physical pages. To read data, it is uniform for any page of any location (microseconds). Erasing requires erasing blocks of multiple pages (milliseconds). Writing to a page requires erasing the block first. 

Data can be directly mapped: logical pages as seen by the OS can be put on to physical pages. 

Writing is bad on SSDs due to write amplification increasing wear - some blocks are used more than others. Wear levelling is used to prevent this.

## Drive Layout
A drive is divided into blocks, with the logical file system superimposed on the physical device. 

### Partitions

At the start of the drive, the Master Boot Record is located. It is read and executed by the BIOS and contains the partition table. One partition is marked as active, and contains the OS's boot block. Drives are split into multiple partitions. 

Each partition has:
- Space reserved for a boot block
- A super block (master file table) for meta stats about the partition.
- Free space (data structures used to indicate free metadata/data blocks like linked lists)
- Metadata (i-nodes)
- Data blocks (root directory)

### Boot Sequence
The BIOS loads the MBR from the first physical drive. Then, the MBR reads the partition table, and locates the primary partition marked as active. The MBR then loads the boot block from the active partition, a program to load the rest of the OS's starter files.

## Logical filesystem
### Directories
These are just special files that group other files together, as defined by the FS. A bit is set to indicate they are directories, and they can be given human-readable names.

In NTFS, all attributes are stored in the directory file: file names, disk addresses, etc. This reduces inefficiencies by not having to seek/read other data.

In Unix, the directory contains a pointer to the data structure (i-nodes) that contains the file attributes. This keeps directories minimal and separates concern of the directory's file data.

### Files
Every file has a system-wide AND process-specific file control block, kernel data structures. It contains permissions, dates, sizes and data blocks/pointers to data blocks. 

The process file table contains process-specific information: all files open to it, file handles, read/write pointers, and a reference to the system-wide file table.

The system-wide filetable contains general information: location on disk, access times and **reference count**. 

The `open()` systemcall maps the logical filesystem's name to the low level name, with the file metadata. It then retrieves the file metadata into a file control block. It then adds it to the **process and system (open) file tables** (incrementing the global's reference count) and returns a **process-specific file handle** (an index into the process's file table). The close call decrements the reference count, updates the disk content, and removes the FCB from all file tables when no longer referenced.


## File system implementations

Contiguous file systems are easy to implement and result in the optimal read/write performance: blocks are clustered close to other files, reducing seek times. However, the exact size of a file is not always known and, similar to memory management, needs an algorithm to decide which blocks to allocate. Deleting a file results in external fragmentation (needing slow defragmentation).

It is appropriate on DVDs as they are write-once and store sequential data e.g. films.


### Linked lists
Files can be stored discontiguously in separate but linked blocks. Only the address of the first node is stored in the file metadata, with each block also containing a data pointer to the next block. 

These are easy to maintain, can grow dynamically, have no external fragmentation. However, internal fragmentation is an issue as the block may not always be used, and random disk access will be slow with many seek operations required. Larger blocks improve speed but increase internal fragmentation. Also, if one block is corrupted, then the rest of the file is lost. For simplicity, the block contains data and pointer - only one or the other should ideally be stored.


### File allocation tables
Linked list pointers can instead be stored in an index table, called a FAT (in-memory). However, the FAT grows with number of blocks and can occupy significant space in memory for large disks, growing linearly. 


### i-nodes

Index nodes contain that file's attributes and block pointers. They are only loaded when the file is open, stored in the system-wide file table. Only the size of an i-node `n` multiplied by number of files open at any point `k` of memory is required.

i-nodes are composed of direct block pointers (usually 12), (single/double) indirect block pointers or multiple, similar to multi-level page tables.

In Unix, all metadata is stored in an i-node. Directories are thus only composed of the file name and a pointer to the i-node. They are a special type of file.

To open a file, we start at the i-node for the root `/`, getting the contents. We ten get the i-node for the next directory, and the contents recursively, until the target file is looked up. 


#### Hard and soft links
A hard link means that 2 directories reference the same i-node. A counter within the i-node will ensure that the reference counter is 2. This is fast, but has the disadvantage of that if the i-node is deleted, hard links will point to an invalid i-node or worse, the wrong file. The i-node must therefore be left if the reference count is greater than 0.

A soft/symbolic link means the owner maintains a reference to the target i-node, but the referencer maintains a small file with its own i-node containing the location and name of the shared file. This requires an extra lookup for the link file. There are no problems deleting the original file, and they can link to files across different machines. 


## Log-structured file systems

In a traditional Unix file system, an i-node is allocated, initialised and written usually at the start of the disk. Then, the directory entry is updated and written. The i-nodes, directories and data are scattered across the file, slowing down random disk access particularly on rotational drives. 

A log structured file system is treated as a circular log. Read and write operations are buffered and, once full, flushed to the disk as one contiguous segment. All data, directories and i-nodes are written to the same segment. 

It also has a cleaner thread, positioned at the tail of the log, running "compacting" operations by reclaiming free space caused by files and directories being deleted. This also prevents fragmentation.

(Rotational) disk performance is greatly increased, but the cleaner thread required additional CPU overhead. Writes are also more "robust" as they are performed all at once.


#### On SSDs

SSDs suffer from write amplification - the entire block must be erased to update a page's data. There may be 1024 pages per block. This expensive operation can be deferred by marking a page as dirty in the FAT, and the cleaner thread can do this when there is lower levels of activity. 

As these file systems are implemented in the controller, the SSD may change addresses, as it does not care about metadata. A mapping table is used to prevent this: it is inspected whenever a logical address needs mapping to a physical address, known as re-mapping.


## Journaling

Deleting a file involves three actions: removing the directory entry, adding the i-node to the free i-node pool, and adding the data blocks to the free list. If a crash occurs between any of these, blocks can become inaccessible. 

Journaling file systems log events before they take place. Actions are written to a log file, then executed, then the entries are removed once completed. After a crash, we can examine the log and execute the remaining actions. This is used by NTFS, ext3 and ext4.

#### Recovery

Journaling does not completely avoid inconsistencies. i-nodes, directories and free lists must be kept consistent as they are structural: system utilities like `scandisk` check for block and i-node consistency. 

##### Block consistency

Block consistency checks typically build two tables, counting how often a block is present in a file (based on i-nodes) and the free list. A consistent file system has 1 in either. A missing block is resolved by adding it to the free list, double-counted blocks cause the free list to be rebuilt. If a block is present in multiple files, a **deep copy** is made.

##### i-node consistency

i-node or directories can be made consistent by going through a directory, and incrementing file-specific counters, such that one file is associated with one counter. If a file present in multiple directories, compare the file and i-node counters and correct if necessary. 


## Virtual file systems

Different file systems usually co-exist, but are abstracted by the OS's virtual file system which relies on standard OO principles like polymorphism. File-system specific code to implement e.g. POSIX standards like `open()` and `opendir()`. The VFS maps/translates the POSIX call to the native file system call through VFS function table entries, for a specific file system.


## Free space management

Similarly to memory management, bitmaps and linked lists can be used for free space management.

Linked lists can be modified by tracking the number of consecutive free blocks for each entry, do not waste disk space (as they use empty space). Bitmaps are the most commonly used today, however.


## Defragmentation
Removing and creating files over time results in fragmentation. Defrag utilities makes file blocks contiguous, combining free space into a large contiguous region. ext* file systems suffer less from fragmentation with **block groups**.

## Linux file systems

ext2 added larger files, names and better performance.

ext3 and 4 added journaling and improvements to it.











