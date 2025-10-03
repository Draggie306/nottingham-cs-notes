
Key point: to record the state of the running program, we need to store the state of registers and also the state of the MMU. 


## Kernel and user space

Code in userspace reads in “user” mode or normal mode - which restricts the code’s priviliges. It cannot interact directly with hardware - it has to ask something to do it for it. It cannot just tell the hard drive to delete all data.

In kernel space, we can interact directly with hardware. The CPU operates in kernel mode. Things running in the kernel mode is the kernel - for this course, this is the operating system. 

> Things like the window manager, GUI, browser etc. even though part of the OS are not part of the kernel - which is the “real” operating system.


## Interrupts
The CPU need to interact with components like memory, respond and output to I/O, peripherals, and the network. To communicate with them and to receive events about something occurring, the CPU needs to know about this. 

The CPU also needs to know about the passing of time - how it knows how to sleep for 30 seconds, for example. The OS makes lots of decisions based on time. 

It also needs to know and handle “bad stuff” - e.g. dividing by zero, resulting in a bad state, or some panic state like hardware fault or cosmic ray.



Interrupts are the mechanism by which handling these events - changing the flow of execution - happens. Instead of going through each code line sequentially, an interrupt will stop the sequential execution and do something else. 
It can happen synchronously - an unpredictable event, such as a hard drive reporting that data has been written/read from a sector. 
It can also happen synchronously - directly triggered by the CPU, can be known known as an exception.

The interrupt mechanism is generally:
- the CPU is doing a task
- an interrupt is signalled by a hardware device, e.g. I/O data is available
- the CPU records aspects of its current state, **switches to kernel mode, and runs a handler to service the interrupt**.

Interrupts can happen at any time. This means handling them should not take too long - e.g. writing tons of data. Handlers can decide to split a top component to be dealt with “record that X has been written” and the bottom component scheduled for later “record full file in file system”.
Interrupts may be interrupted by higher priority interrupts, and can be nested. Eventually, critical code cannot be interrupted so must be disabled temporarily.

Blocking IO is ”naive” IO that wastes CPU cycles waiting for slow devices to respond.

Better CPU usage supports interrupts “calling back” from the IO device once it has finished - allowing the CPU to spend most time doing “useful” calculations


## System calls
System calls are how programs request services from the operating systems. This includes requesting memory, accessing files, running programs and accessing concurrency features.

An API is different to a system call:
- An API is a programming interface - library of functions/procedures that can be called, like `pthread` - a way of getting things done with threads
- The API will need to make zero, one or multiple system calls to the OS to get something done

A system call works by calling an interrupt:
1. When a system call is required, it is given a system call number, stored in a register.
2. Parameters, such as amount of memory, are stored as extra data in designated registers.
3. A synchronous interrupt is triggered, known as a **trap**. 
4. Kernel-mode code calls a system call service routine which implements the required code - looking at the system call number and its parameters.
5. The interrupt finishes and returns to user mode code.

The system call service routine may not service the system call immediately. The OS may not even continue to run the original system call - the OS has a choice as to what to run. System calls are the chance to allow other programs to work instead.

Details very by the OS: modern CPU designers may avoid these as it does involve overhead, but the general premise is the same.


## The C language
An OS must be fast enough for as many users as possible. A slow OS slows every programs that runs; energy efficiency is a concern (especially for mobile), so there is a bias towards performance over elegant and simple code, BUT it must be correct.

It should be written once as they are difficult to write, and thus simply recompiled for different  hardware. It should be predictable for user programs - it takes X for Y to happen. If there is e.g. a garbage collection system, this takes a while and risks the caller to be killed instead.

The 3 Ps:
- Performant
- Portable
- Predictable

