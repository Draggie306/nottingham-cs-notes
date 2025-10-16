

Summary:
- Threads and processes exec in parallel with shared resources
- This lets the system be kept busy, but requires additional coordination for correctness
- What is run, when and where, is unpredictable. The outcome of programs may be dependent on arbitrary choices by the scheduler and hardware

> Assume bad stuff will happen and you’ll be in a good place….

![](../../../Pasted%20image%2020251014121104.png)

`counter++` does three things: read it from memory into a register, adds one to the value in register, and stores the value back into memory. This is not atomic.

In more detail:
- Thread 1 reads into the register, adds one, stores it into the register.
- Context switches: Thread 2 reads the counter, adds one, and stores it  back

Or:
- Thread 1 reads the counter from memory into the register (= 1).
- Context switch: thread 2 reads `counter` into the register (= 1).
- Context switch: thread 1 adds 1 to the value (= 2), and then stores it into `counter`.
- Context switch: thread 1 adds 1 to the `register` and stores it in counter (= 2). 
This means that there were 2 additions by 1, but `counter` is still 2, not 3.

Equally:

![](../../../Pasted%20image%2020251014122018.png)
This results in e.g. `b` being inputted, but `bb` being displayed the user.


### Race conditions
Code has a race condition if its correctness is dependent on the order in which computation is performed.

It typically occurs when there are **multiple threads**, which access **shared data**, and the **result depends on when** different code runs.

The kernel is equally vulnerable to race conditions, so the OS must be designed to cope with these issues.

Race conditions can lead to unpredictable and wrong behaviour. Thus, we want software 

A critical section is a software feature, a section of code that can be run by only 1 thread at a time (e.g. incrementing a counter). This is known as **mutual exclusion**. However, to enforce this, we can:
- use the OS/compiler to provide direct support for critical sections as a primitive
- the OS/compiler provides locks which can be only be held by one thread at a time

An implementation of critical sections shouls provide:
- mutual exclusion: only one process can be in its critical section at a point in time
- progress
	- processes/threads in the remaining code do not influence access to critical sections
	- deciding when competing processes get access to the critical section cannot be indefinitely postponed
- bounded waiting: fairly distributed waiting times for non-indefinite waiting
These have to be independent of the order in which computations are executed.

### Enforcing mutual exclusion
A standard approach is to use mutexes (locks). 
- only one thread can acquire the mutex
- other threads attempt to acquire the mutex lock
- once the thread has finished, it releases the lock.


Mutexes and other concurrency primitives - semaphores - introduce deadlocks.

> Race conditions are a “beginner” mistake; deadlocks are difficult to analyse and resolve 

![](../../../Pasted%20image%2020251014123837.png)
Typically, CPU usage will drop to zero and neither process/thread will make any progress.

> a set of threads is deadlocked if each thread in the set is waiting for an event that only another thread in the set can use.


There are four minimum conditions for deadlocks to occur:

- mutual exclusion: a resource can be assigned to at most one process.
- hold and wait condition: a resource can be held whilst requesting new resources
- no preemption: resources cannot be taken away forcefully from a process
- circular wait: there is a circular chain of two or more process, waiting for a resource held by the other process.

No deadlocks can occur if one condition is not satisfied.

> This is likely to occur in coursework. If so, check the order in which order of resources are requested.














