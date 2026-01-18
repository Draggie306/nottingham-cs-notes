

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

There is less overhead to adjust threads (all have the same shared, unprotected address space within a process) and some CPUs have hardware support for multithreading - true concurrency. As threads of a process share memory, communicating between threads is faster than interprocess communication. 

### Threading implementations

#### User threads
Many-to-one: one kernel process, but the process itself maintains a thread table and thread runtime system without the kernel's knowledge. 

This has the benefits of requiring no context switching or system calls, plus having full control over the scheduling within the application, and can be run on OSes that do not natively support threading. 

However, blocking system calls such as file accesses suspend the entire process, as the kernel sees all requests coming from one process. There is also no true concurrency as the kernel schedules the process to run on once CPU and it is non-preemptive with no interrupt mechanism.

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




# Memory Management




# File Systems