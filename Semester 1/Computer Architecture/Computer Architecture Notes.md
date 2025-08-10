Computer Architecture - COMP1056 - University of Nottingham - Year 1, Autumn Semester, School of Computer Science. Taught by Dr Steven Bagley: C55, Computer Science building


Taught through a) synchronous online lessons through demonstrations and theory, b) pre-recorded videos and c) other things on Moodle

![[Pasted image 20241030091527.png]]

#### Definitions
von Neumann:  data and instruction in memory.

von Neumann bottleneck: CPU can either fetch an instruction or modify/access data, not both.


### Buses
To communicate with the CPU, we use the data bus and address bus. 
#### Data Bus
In the data bus, the CPU will fetch 16-bit/32-bit chunks using it. It is transmitted in parallel. The size of the Bits of the bus is not the same as the data bus bits.

It is **bidirectional**: data can be read from/written to at the same time.
#### Address Bus
The address bus is used to carry the address for the piece of memory to access (read/write from/to).

> CPU bit length or word size may not be equal to the data bus width.

#### Control Bus
The control bus is used for control signals to tell the rest of the system what the CPU is doing.
- Read/write line
- Address Strobe (AS) - checks validity of address on address bus
- Data strobe (DS - checks validity of data bus

### Processing Information
Computers used to be analogue, but it was difficult to distinguish (heat may change value)

We use binary as it is easier to determine the difference between just two values. This enables us to use logic.

Combinatorial logic: output depends only on the current value of the inputs.
Sequential logic: output depends on the current and previous values of the input.

### Decimal to Binary

1. Initial number: 211
2. Divide by 2.
3. Result is:             105 r1
4. Divide by 2 again. 52 r1
5. Divide by 2 again. 26 r0
6. Divide by 2 again. 13 r0
7. Divide by 2 again. 6 r1
8. Divide by 2 again. 3 r0
9. Divide by 2 again. 1 r1
10. Divide by 2 again. 0 r1

Enumerate the remainders from latest operation to first
= 11010011

### Boolean arithmetic
All Boolean functions can be expressed in terms of just AND, OR and NOT applied to the inputs. This is known as the *canonical representation*.

These have their own symbols that can be used to write down logic equations.
This is similar to how to write mathematical equations (i.e. `x` for multiplication).

![[Pasted image 20241101120639.png]]

XOR can be defined as:
`NOT A AND B OR A AND NOT B.`

After writing an expression and producing a working logic circuit, it may work - but it not necessarily be the simplest solution.

Thus, the aim is to use as few gates as possible. This saves money and also reduces propagation delay - of which, there is such a delay of ~10ns for each logic gate.

![[Pasted image 20241106092308.png]]
A ripple carry adder is known as such as each result "ripples" through into the next full adder. In this case (4\*30ns), the propagation delay will be around 120ns.

A carry occurs when there is a result larger than e.g. 4-bits. This bit is preserved by the CPU with the carry flag.


#### Representing negative numbers
To subtract, instead of building a separate circuit for handling negative numbers, we can simply add a negative number. To do this, we need to have a way to represent negative numbers.

- Sign and magnitude
	- uses the first bit to denote positive or negative
	- simple to implement, but makes it harder for addition
- Excess-n
	- where `n` represents the offset, e.g. Excess-3 would have `0` being `0011`.
- One's complement
	- leave all positive bits as-is
	- for negative, invert the bits of the equivalent positive number
	- addition can be performed, but leads to two zeroes (a + and a -) and results need tweaking with the carry bit after an adder
- Two's complement - ***This is the standard used on all CPUs.***
	- Invert the bits (i.e. perform one's complement) and add `1` to the result.
> **Note: two's complement is NOT the same as inverting all the bits apart from the least significant. A binary `1` needs to be added to the inverted number.** 

Both Sign & Magnitude and Two's Complement can both quickly be used to determine positive/negative by the most significant bit being 1 or 0, respectively.


### Logic and circuits
**Combinatorial logic** refers to the fact that **the output is a combination of the input values**, vs sequential logic which also has a time component. **Logic circuits always do the same thing if the same signal(s) are transmitted, and have a fixed functionality**.

The CPU's heart is the ALU - the CPU is built from combinatorial logic.

The ALU is considered to have two outputs usually and one output. They usually take in multiple bits (e.g. 16-bits in both inputs, and outputs)
The ALU's functionality is dynamic - it can change. Therefore, it needs a mechanism to select what function it performs. This is done by having control pins.

The ALU should be able to perform many functions. To do this, we can reduce the number of operations needed to perform internally by using e.g. de Morgan's to simplify OR to AND, etc.. 

Minimising the circuit complexity requires fewer transistors and smaller silicon, resulting cheaper prices, less propagation delay and thus faster processors.

The ALU takes in various signals:
- `zx`
	- Set `x = 0`
- `nx`
	- Set x to `not(x)`
- `zy`
	- Set `y = 0`
- `ny`
	- Set y to `not(y)`
- `f`
	- If is true, out `A + B`, else out `A AND B`
	- Uses a multiplexor
- `no`
	- Invert output
... and returns (outputs) the result of these operations.

Sequential logic refers to logic circuits that depend on the *sequence* of previous inputs and outputs.

#### FLIPFLOPS
Multiple (D-type) flip-flops can be connected to the same clock - this is common in memory and RAM. Flip-flops store (and output) their current state, until a signal tells it to switch to the opposite state!


## State Machines

### Finite state automata
> A machine that can be in exactly one of a finite number of states at a given time.

Its characteristics are that one:
- has exactly 1 start state, but can have many finish/ending states;
- can have many transitions from one state into another state (or can be the same);
- can be drawn pictorially.

Once we work out all possible states, we can then design the hardware to accommodate the machine.

We can build state machines from discrete logic components, but more states will make the logic more and more complex. Therefore, we use programmable logic elements to implement the combinatorial logic. 

We also need to provide logic for unused states that, if the output accidentally transitions into one of these states, it does something sensible - e.g. triggers a stop signal until someone resets the system. *Therefore, we also need some reset logic - to force the system into a known state.*

State machines allow us to develop logic circuits.

**Moore state machine: output depends on the *current state only*** - purely the state we are in. Know exactly when clock changes and the flipflop updates to change the state.

**Mealy state machine - output depends on the *current state and any of the inputs*** - can happen at any point in time. They respond more quickly to change but not as predictable.

### Registers
The von Neumann bottleneck refers to the fact that the CPU can only access data or instructions, not both, at the same time.

Registers are used for 2 purposes in the CPU:
- some are part of programming and accessible via software
- others used to help sequence the moving around the data path - controlling how data is moved in the CPU (temporarily storing a value in it, using others too)

The program counter stores the address of the current instruction being executed, incrementing after each instruction completes (except branch instructions/changes to R15).

- Data path: series of functional units (ALU etc.)
- MAR: similar to writing down address on paper so we don't forget it later
- Control logic enables and disables functional units to control the data path.

## Sequential Logic
### Gates
#### SR Latch
There are 2 inputs: R and S. They both go into one NOR gate each. The output of the NOR gate is used as another input to the other NOR gate, and also the outputs Q and not Q.

The use of this gate is that it can be used to store the state of bits!

![[30-SR-flipflop-circuit.png]]

#### 1-bit register
It has a multiplexer with a flipflop, with the output of the flipflop going into the multiplexor.
#### Flip-flops

(D-latch)
![[d-type-latch.png]]


### Half and full adders

![[half-full-adder.png]]
## An example - The 6502

It is a simple 8bit CPU released ~50 years ago.

- A - the Accumulator.
	- The main register - all arithmetic and logic operations affect and go into the accumulator
- X and Y
	- Temporary storage and pointer-arithmetic-type operations

Despite being very simple, it can run on *any* program

> **Turing** showed there was a very small number of instructions - around 8 - that a CPU needed to run *any* program; if it implements them, it is Turing complete

There are 2 parts of machine code: the set of instructions (what the CPU can do) and a binary encoding of those instructions. 
The set of instructions varies between CPUs but usually they offer similar sorts of instructions. The 6502 offered ~56 instructions. 
Several instructions support various different addressing modes (way to access memory) giving ~150 unique instructions

The 6502 is generally a one-address instruction set - each instruction takes one address. An *address* may be a memory location, register or immediate value.
A two-address instruction may be source and destination (ADD a,1)
A three-address (like in ARM) may be destination, source and second source (ADD r0, r0, #1)


When building machine code, we can encode and decode instructions in a simple way for logic. Instead of checking all the bits in an instruction, we can just use a pattern matching example but on a lower level. For instance, the top 8 bits in a 32-bit instruction size being 1 may define an instruction to read from ROM. Therefore, we can check for this, and **any** instruction that has these `1`s in the first 8 bits independent of the rest are known to be reading from ROM. The lower and upper bounds are therefore:

`0xFF000000` - equivalent to `1111 1111 0000 0000 0000 0000 0000 0000`
and
`0xFFFFFFFF` - equivalent to `1111 1111 1111 1111 1111 1111 1111 1111`

(for instructions where there is a bit lower than the most significant used to specify an instructions, we fill all bits to the left of it with `0`, and the range of matched bits to the right of it between all `0` and all `1`.)

More detail about this further down!

# Optimisations
There are many tricks used by modern computers to make them go faster.

### The FDE Cycle
#### Fetch
Get from memory (involves setting bus lanes, signals, etc...)
#### Decode
CPU hardware analyses the opcode and decides which part of the CPU needs to be engaged process the instruction and their order.
#### Execute
Runs the steps needed for the specific instruction. This could be more than 1 step and may require accessing memory again - for instance, `LDRB` means load byte in memory at a given operand.

In this cycle, each step is synchronised to the clock. This means there are 3 cycles per instruction.

### Pipeline hazards 
A **pipeline bubble** is a stage when some parts of the CPU are not doing anything because a hazard forced the delay of an earlier stage, slowing execution times.

For instance, LDR will fetch data (and cannot also fetch the next instruction as it must be decoded first). As looking up data in memory is very slow, the decode and execute sections in the cycle will already have been completed for a time before 

#### Data hazard
One of these occurs when an instruction requires a value calculated by a previous function.
This is a hazard as we may try to execute before the value is actually available.

We can bypass this problem by using **data forwarding** - the result of one instruction is sent directly to where else it is required in the pipeline without rewriting to registers - this is provided by CPUs.

> When writing this out in rows/columns, there will be nothing in the Fetch column if the row's Execute column will interact with memory, such as with LDR or STR.

The longest step of a pipeline stage will define the length of a clock cycle.


## Superscalars

There are still ways to make the CPU faster - although we are still limited to the clock speed.

Superscalar - CPU fetches, decodes, executes two (or more) instructions in one clock cycle, by e.g. having multiple ALUs. The result is that each instruction takes 0.5 cycles (or less)

> assuming that they do not require the output of one in the next instruction or depend on each other.

CPUs are considered to be **in-order**. This means they are executed in the same order they appear in memory - so instructions will be sequentially executed, line-by-line.
However, the program needs to be designed to do this - generally it is up to the programmer or compiler to decide how to implement it. 

Some CPUs use **out-of-order execution**, which automatically reorders instructions to execute them in the fastest way for the specific CPU's design. Although it may sound *crazy* it will reorder instructions as they come into the CPU to be in the best order -- but not change the results or how the program works.

## Limitations of optimisations

These optimisations have all happened at the instruction level, without change from the code.
This only go so far - clock speed or tweaking clock speed and architecture. And also requires a lot of logic to implement.

Rather than making CPUs faster, we can have multiple separate CPU cores that run the same code in parallel. However, we need to change how the program is written.

> The reason why clock speeds have stagnated is because of power. With higher clocks, the power requirement increases and is dissipated as heat - which we need to take away from the CPU else it will melt. This limit is known as the **power wall** - the limit of heat we can easily dissipate from it.
 
CPUs are built using a technology called Complimentary Metal-Oxide Semiconductor (CMOS). This means that energy is required when transistors switch state. As we increase the clock speed, we increase the rate of switching and the power used.

We have combated this by reducing the CPU voltages but this has reached a limit now - especially in phones and handheld devices that could not have a fan/cooler.



## Multiple processors
We can increase the amount of data that can be processed in each step by reducing the execution time required to complete a program.

> Multi-**processor** system: multiple pieces of silicon (e.g. 2 CPU sockets) in 1 system.

> Multi-**core** system: multiple processors on the same socket.

### Flynn's taxonomy

A processor can have a single or multiple instruction stream, and a single or multiple data stream.

**SISD**
Single instruction/single data stream: the processor goes through each instruction sequentially and executes them on the data, producing a singular output (e.g. ADD). *This works fine, but there is no parallelism.*

**SIMD**
Each instruction (e.g. ADD) will act on multiple different values at the same time, executing on multiple data items. Each data item will be updated at the same time. This is on data-level parallelism. 

> *This works well for certain tasks, such as GPUs, e.g. completing the same transformation on world coordinates into the screen coordinates.*

It allows us to perform the same operation on many data items.

In `x86`, the `addps` instruction given two registers adds all the values at each array index (e.g. `xmm0[0]` gets added to `xmm1[0]`, etc.) all at once

**MISD**
Multiple instructions act on a single piece of data - very uncommon

**MIMD**
Different instructions act on different pieces of data at the same time - required in a multicore system.



# Addressing the system
Address space is the number of bits on the address bus (the number of bytes, the total range of addresses the CPU can access).

The address space is part of designing the system: although we do not need to use all of it, we can partition it however we want.
It is divided between RAM, ROM (e.g. between address 0 and 4, this tells the computer where to boot from, so must be the same) and I/O.

These chips all have various address lines . The address is a binary number. To be aligned, these addresses are multiples of powers of two.

> Address spaces do not have to be completely full - there can be spaces unaddressed.

## Decode logic
Whenever we want to look up an address and decode it, we can look at the prefix of the lowest and highest possible address in the address range (if it is a power of 0).

For instance:
$$
A_{19} \cdot A_{18} \cdot \overline{A_{17}} \cdot A_{16} \cdot A_{15} \cdot A_{14} \cdot \overline{A_{13}} \cdot \overline{A_{12}}
$$
The maximum addressable addresses here are 20 bits wide (upper is 19). This specific format means that the bits at positions 19-12 must be: `11011100`. The bits between `11-0` can be *any value*; it doesn't matter, to determine what this is decoding. To write this address as hex, go from the bottom 4 bits up in 4-bit increments and convert the binary into hex, for both a lower and upper.

This would be:
$$
11011100\space000000000000\space(lower)
$$

$$
11011100\space111111111111\space(upper)
$$
and, as hex:
$$
0xDC000\space(lower)
$$
$$
0xDCFFF\space(lower)
$$


If there is a number specified as `0` but outside of the main block of "prefixes", e.g. A16 is `0` but A4 is `0`, then the maximum number would be filled with `1`s all after A4, e.g. if A4 is the most significant byte, the higher limit would be: `01111`.


## Parallel execution

Modern systems employ so many tricks under the hood (rewrite registers etc., see above) that machine code is an abstraction of the chip implementation. 

MIMD systems can be more efficient: in merge sort, one CPU can execute multiple instructions on different data values.

> Enables us to break the program down into independent chunks to reduce the time it takes to execute.

Both multiprocessor and multicore systems have multiple cores (complete processing units).
- Multicore have them all on the same chip, often sharing L3 cache between all cores (but separate L1 and L2 caches per core). They appear to the system as e.g. 8 separate processors.
- Multiprocessor has each processor as its own standalone chip, individually on a motherboard with multiple sockets. Each has its own L1, L2, L3 cache. *These can also be multi-core systems.*



## Cache
CPU runs far faster than RAM today. It has to wait a relatively very long time for the RAM to return the value. Although CPU speeds were increasing, RAM would bottleneck the speed, so would appear the same speed. 
To make things run faster, the CPU has a cache between the CPU and (dynamic) memory. It is a small amount of high-speed RAM.

Why?
> A program only needs a small amount of instructions on the same amount of data over and over (**locality; spatially and temporally**), so it decides to keep a local copy of it in the fast cache RAM. 
> Instead of waiting to fetch from RAM it will just go to the cache instead.

## Hardware Multithreading

![[Pasted image 20241129122901.png]]

We can also use hardware multithreaded processors. This is one CPU, but it presents as two cores to the system. Both of those cores have their own program counters and registers, but share L1/L2 caches, register banks and ALUs. 

There are also big security risks with this: the way multithreading works, programs may be able to measure and time how long it takes to execute/read data from a cache, and 

> Symmetric multiprocessor - tasks are distributed uniformly across all processors. 

### Shared memory
Most systems today use a shared memory mode: this means that there are many CPU cores, however, they are all connected to the same block of memory with the same memory addresses. *meaning, if accessing address 2, all CPUs will get the same data at this memory address.*

To do this they are all connected to the same system bus. On this bus, memory, I/O devices etc. are connected to it. The **bus arbiter** controls this - to say that only one CPU can access the bus at the same time, although they can have different virtual address spaces.

Processors can communicate with each other by setting values in memory which other processors can read. For instance, once one merge sort is completed by one CPU, it can set some memory to say this was completed and then other CPUs can detect this. However, this brings another issue with corruption.


#### Bus snooping
To prevent cache invalidation, we can use a bus snooper that monitors bus transactions. As there may be multiple instances of caches, when one processor changes the value in one cache, the change should be propagated to the other instances of it, to ensure there is no corruption and uphold *cache coherency*. If the snooper detects that another cache has a copy, it may invalidate or flush it, requiring a full fetch from the correct, up-to-date location.

### NUMA
With more and more cores accessing memory, the **bus arbiter** will have more and more chance of already accessing the memory that another core is also accessing. As core count increases, the likelihood of waiting for another core to finish with it than not.

The solution is to change the model to have a NUMA (**n**on-**u**niform **m**emory **a**ccess) system.
Some parts of the memory can be accessed faster than other parts; the latency is more for some memory addresses.

e.g. split some cores to access one block of memory, and others have another block. For a core to access the other block, it has to go over a shared memory network (DSM network).

However, this is a hard(er) programming model - as we want to ensure as many requests as possible are on the "local" memory segment.

> Uniform access system: one that cannot access memory at same time as other CPU core.
## Parallel programming

How to make use of multiple processors? We split programs into separate pieces that run at the same time!

### Forking
Split a program into two, with one side executing one block of code and the other completing a different set.

When we fork, the OS creates a completely new process & different ID. However, it will keep e.g. the same resources open, such as files and network connections. The programs have independent scheduling and can call other programs or be killed individually without affecting the other.

In C - fork() function
- returns twice. A value of 0 to the child process, and a value of the child process ID to the parent

```c
if (!(fork() != 0))
{
     /* The parent process */
}
else
{
     /* The child process */
}
```


Forks are heavy for the operating system to manager increasing its load and uses up a process ID which there may only be a limited number of. 

### Threading
Threads are an alternative approach. We don't need to make a complete new process. 


A thread is a path of execution within a process - with its own registers, program counter, and stack frame. All processes have at least 1 thread. Threads, rather than processes, can be switched to more simply, and can be scheduled to be run by the OS.

In C, we can use `pthread_create`, passing in a pointer to the function to execute

When the threaded function finishes, the thread will end and be cleaned up automatically.

As soon as the main thread finishes, all the other threads created will be killed. They are bound by the process. To prevent this, we can use `pthread_join` which will allow the thread passed in to finish before moving to the second.

We cannot control how the instructions are interleaved at the machine code level. This may lead to problems with seeing different values for the same variable - memory can be different to the value in register (see below, memory hierarchy). We can use `volatile unsigned int x;` in C to tell the compiler to always use the memory value rather than the cached value in cache.

We can use a mutex (mutual exclusion) to control execution - locking and unlocking code to control which thread can run code and modify the data.

```c
pthread_mutex_lock(&lock);
/* code that adds variables */
pthread_mutex_unlock(&lock);
```


# Is a fast CPU needed?

We assume that, during the Fetch-Decode-Execute cycle, that each instruction will take 1 clock cycle to execute; however, this is not true (see below). There is no way to overcome this - the length of the motherboard track from CPU to RAM would take longer than 1 clock cycle, just for the electrical signal to travel.

Furthermore, accessing RAM isn't instant. It's fast, but not particularly fast. It will take between 10-20ns to access data (the memory latency), once it receives the signal to begin reading.

![[Pasted image 20241209131217.png]]
*Expectations vs. reality.*

It used to be much more symmetrical, but as CPUs have become considerably faster over time (and RAM hasn't), there is this gap. During this fetch, the CPU is in a **wait state** - and reduces the amount of operations that can be carried out significantly. 

There are different ways of making memory, with each having a different price and different characteristics, including access latency.

Recap:
- When the CPU wants to read, it sends the address of the memory location along the address bus.
- It then sets the read/write signal to read (control bus)
- It then enables the output enable signal on the RAM to generate the signal
- The RAM will provide the value back to the CPU along the data bus.

## Memory types

#### Static RAM
- Set it to have a value, and this value will be remembered until system is turned off/changed.
- Fastest to access data
- Very expensive
- Made from 6 transistors
#### Dynamic RAM
- Constantly have to refresh each value in memory
- Designed for data density, so relatively cheap for lots of it
- Made from a transistor and capacitor (so must be powered)
#### Flash RAM
- SD card, SSD drives, USB sticks included
- Can store data when power is lost
#### Hard disks
- Temporarily copies unused data to the disk until it is needed again

We could use some fast static RAM to hold the program's instructions and some slower dynamic RAM to hold the data.

### Code path optimisations
Thinking about programs and how they run - if an instruction executes, there is a high chance that the next instruction will also be executed. In fact, if the instruction is not a branch, it's almost guaranteed that the next instruction will be executed.

As most states of programs running are inside loops, there is a good chance that these will get executed again. We can copy an instruction, and maybe also a few instructions around it in the **program's spatial/temporal locality**, into faster static RAM (or cache) to allow it to execute faster.

- Spatial locality: if memory location is accessed, nearby memory locations are likely to be referenced toon
- Temporal locality: if an instruction is executed, it is likely that it will be executed again.

This can be implemented by having a memory hierarchy: there is a cache (of SRAM) between the CPU and main memory. We can only access the slow DRAM when necessary to get the best of both worlds, whilst having fast access from SRAM and having lots of slower but cheaper memory in DRAM.

Instead of waiting for 100 cycles for DRAM to be accessed, the cache can be accessed in 10 cycles, allowing for ~10x more cycles to be completed!

## Memory hierarchy
Firstly, look in the small fast static RAM cache, if not, look into DRAM and make a copy of the whole line (spatial locality) to copy surrounding values into the cache.

To measure cache performance, we use:
- hit rate
- miss rate
- hit time (time required to access the cache and determining if it is a hit or miss)
- miss penalty
	- time required to access and fetch a cache line from memory, transmit it and insert into the cache, pass data back to CPU

There are multiple cache levels: L1 is closest to the CPU and very fast, L2 is bigger but slower, L3 is bigger but slower too, etc.. The miss penalty when not in L1 but still in L2 is still less than fetching from DRAM.

Separate caches are used for the instructions and the data - in the same cache would reduce performance of access to both (von Neumann bottleneck).

## Updating values

With data, we write data too. A write-through cache approach means that data is written immediately to a memory location, it is also updated in the cache. This may be a waste of time as often in a loop there may be an increment counter, so updating the memory once the value has finished being updated is more efficient.

A write-back cache writes the updated value into the cache, and writes to memory once it's finished being changed. However, there may be inconsistencies with e.g. multiple CPUs and I/O devices not accessing them.

