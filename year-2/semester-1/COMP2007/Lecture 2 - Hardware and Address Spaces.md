I/O, keyboard, disk etc. are all every slow relative to the CPU


Naively, the CPU executes a sequence of instructions one at a time. The basic cycle is fetch, decode and execute, in a pipeline.
A superscalar CPU provides instruction-level parallelism, and can fetch multiple instructions in batches and executing them. 

The CPU will shuffle the order of operations to keep the pipeline busy - not always the order given in the code. Speculative evaluation: the CPU will ”guess” which branch may be taken, and preemptively begin calculations along that branch.

> We must be very careful about the assumptions made about CPU behaviour. *Compiler optimisations and memory architecture complicate it further.* **Never make naïve assumptions about what the CPU is doing.**

### Registers
Registers are small fast amount of memory close to the CPU core. There are general-purpose (”scratch”/temp data storage) registers and specialised registers:
- the PC will count the current instruction being used
- program status word - flags configuring the CPU state
- general-purpose registers: storing operands for instructions

Registers and their content are part of the state of a program. 

### Moore’s law
Moore’s law (an observation) states that the number of transistors on an integrated circuit doubles roughly every 2 years. It is very closely linked to performance, so games and intensive applications would “double” in speed every 2 years.


### Multiple cores and threads
Modern CPUs have multiple threads of execution in each core and multiple cores in each CPU package.

Hardware evolution has implications on OS design

```c
#include <stdio.h>
#include <unistd.h>

int iVar = 0;

int main() {
	while(iVar++ < 10) {

	printf("Addr:%p; Val:%d\n", &iVar, iVar);

	sleep(1);
}
```

![Pasted image 20250930122623](../../../Images/Pasted%20image%2020250930122623.png)

We cannot know the exact physical address, so the compiler optimistically assumes that it its base address is address zero. If it is not, then an offset can be added - addresses cannot be fixed.

There are two address spaces: the **logical address** space, and **physical address** “where in memory at runtime”. When we compile, we do not know where it will be physically, so the logical address is used by the compiler.
The logical address consists of the physical address plus an offset.

![Pasted image 20250930123418](../../../Images/Pasted%20image%2020250930123418.png)
Given a memory range and two running programs.

This is important enough that modern hardware has specialist units (the **memory management unit**) to apply this offset. The state of the MMU is part of the state of the running program.


## Key Points

- OSes are very closely linked to hardware design and capabilities.
- Registers are part of the state of a running program.
- The MMU abstracts the real specifics of memory architecture
