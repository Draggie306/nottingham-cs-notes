Week 2 - new topic Processes.

Recap:
- Interrupts change the normal flow of computation, switching from user to kernel mode. 
- System calls allow to run kernel code to access services of the OS, and are implemented with interrupt triggering. 

## Processes

A process is an abstraction of a running instance of a program.
A program is passive - a file. A process has a state and is dynamic: it has control structures, may be active, and may have resources assigned to it.

All information required to administer a process in the kernel is in a process control block (PCB) - usually just a struct in C. All process control blocks are recorded in the process table - an array of PCBs. Each process has a unique process identifier (PID) associating it with its PCB (usually the index in the process table).

A process’ memory image contains the program code (shared or not), a data segement, a stack and heap. The stack and heap are placed on opposite sides of the memory image, so they can grow down and up, respectively.

### Process states and transitions
- **New** - it has just been created, with a PCB and is waiting to be admitted, and may not be in memory.
- **Ready** - process is waiting for CPU to become available
- **Running** - is currently having instructions executed.
- **Blocked** - cannot continue, e.g. waiting for I/O keypress (“yes” or “no” buttons)
- **Terminated** - no longer executable (has finished/crashed). The PCB might be preserved

**State transitions:**
- **New -> ready**: admit the process and commit it to execution. *The OS may be too busy so may be left in new for a while.*
- **Running -> blocked**: process is waiting for input, or ran a system call
- **Ready -> running**: process has been selected to use CPU by the (process) scheduler
- **Running -> ready**: process stops using the CPU, e.g. is paused, or interrupt is called
- **Running -> terminated**: process has returned from `main()` in C, has called `exit()` or has written outside of array memory bounds.

Interrupts and system calls control these transitions. When a system call is made, it may run something differently.

The operating system’s central data structure are queues. Admitted processes in the ready queue may be dispatched for the CPU to run. Then, different events e.g. I/O can be waited and processes added to these queues, and/or processes time out if they occupy too much CPU time.

![Pasted image 20251007115338](../../../Images/Pasted%20image%2020251007115338.png)

### Context switching

CPU access must be shared in modern, multiprogramming,  single-processor systems. **Time slicing** is used by interleaving the execution of processes. Control is given and passed between processes using context switching. There is a tradeoff between the time slice length and context switch time.

> Slicing time fast enough that gives the impression that different processes are using the CPU at the same time is only an emulation of parallelism: hardware support is required for true concurrency and parallel processing.


When a context switch takes place, the system saves the state of old processes and loads the state of the new process. Saving **updates/writes** the process control block, restarting them **reads** from the PCB.

- The response time of a process is the time taken from creation to its first CPU access
- Effective utilisation is the fraction of the time the CPU is doing useful work. Useful work = not context switching.

Short time slices result in good response times but low effective CPU usage. If context switching and time slices are 1ms each, the CPU is only doing useful work 50% of the time. If there are 100 processes, it will take 198ms for the final process to run after the first. (99 x 1+1ms)

Long time slices result in poor response times but better effective usage. If a context switch takes 1ms and time slices are 100ms, the CPU is useful 99% of the time. However, for 100 processes, it will take 9999ms (99 x 100 + 1) to run the final process.


A PCB contains 3 attribute types:
- Process identification (PID)
- Control information (state, scheduler info)
- State information (registers, stack pointer, program counter, status word, files)

The PCB is a kernel structure, so is protected - else could raise own priority, interfere with other programs, etc.


To switch between process, the kernel:
1. Saves process state to PCB (includes PC, registers, MMU)
2. Updates PCB state (running -> blocked/ready)
3. PID placed in the appropriate queue (ready/blocked queue)
4. Runs the scheduler to select the next PID from the “Ready” queue
5. Updates PCB state (ready -> running)
6. The new PID’s state is restored from the PCB (PC, registers, MMU)
7. Returns control to the new process



### Process implementation
An OS maintains info about the status of resources in tables:
- process tables (PCBs)
- memory tables (memory allocation blocks, )
- I/O tables
- file tables

When a process is allocated, it is given a PCB for each process, which is allocated in the process table. Tables are maintained by the kernel and are cross-referenced: this allows fast access, no linear searches needed.

### System calls
System calls are wrapped in OS libraries. On a Unix-like OS, `fork()` creates a process copy. The underlying syscall to implement `fork` is `clone`.

Syscalls with exit/abort can be used to tell the OS to be killed. Resources will be deallocated, output flushed, memory freed. Other processes can be terminated with `kill()` or, on Windows, `TerminateProcess()`.

Waiting for a process and recovering information about how it is terminated can be done with the `waitpid(PID)` syscall. The OS must then retain information about terminated processes to service wait calls - once these calls have been serviced, the control data can then be cleaned.

#### In Linux
In Linux, fork() creates an exact copy of the current process. It returns the PID of the child process to the parent, and returns 0 to the child process.

The typical pattern is to creae a different process:
1. Call fork() to create an exact copy
2. Call an exec() function to replace the current process with a nwe program.
	- e.g. replacing myself with the current process, `execl(“/bin/ls”, “ls”, “l”, 0)` will replace the bash process with the `ls` function

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
	pid_t const pid = fork();
	if(pid < 0){
		printf("Fork failure\n");
		return -1;
	} else if(pid == 0) {
		printf("Child process\n");
		execl("/bin/ls", "ls", "-l", 0);
	} else {
		int status = 0;
		waitpid(pid, &status, 0);
		printf("Child %d returned %d\n", pid, status);
	}
}
```
> It is a good idea to understand this as it is a hotbed for exam questions, and is fundamental to other




