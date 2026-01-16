

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




# Processes



# Concurrency




# Memory Management




# File Systems