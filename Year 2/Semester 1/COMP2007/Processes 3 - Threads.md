
Recap:
- Preemptive/non-preemptive schedulers - when processes are kicked off CPU time.
- Term-based scheduling: long vs short term - when different processes should be on the CPU
- Evaluation criteria including 
- Scheduling algorithm


> CPU Burst Time: the amount of time the process needs to complete execution. Just the time it needs to compute on the CPU.

![](Pasted%20image%2020251009150752.png)

## Threads

A process consists of two fundamental units: the resources and the execution trace. The resources included a chunk of memory, files, I/O devices, etc. The execution trace is the computation that exploits the resources.

A process can share its resources between multiple execution traces - we can share resources and work on different goals in parallel.

It thus makes sense to introduce an abstraction for an execution trace - threads.

A multi-threaded process will have duplicated registers and stack (to keep track of functions, arguments and ”working”/scratch space in registers), whereas a single-threaded process has one execution trace and shared code, data and files.

Every thread has its own execution context (PC, stack, registers) and all threads have access to the process’ shared resources: file handles, global variables, heap memory - *we can use these to communicate between threads*.

Similar to processes, threads have states and transitions (new, running, blocked, ready and terminated). There is a thread control block (TCB), a thread table of TCB, and each thread has a thread ID (TID) - can say in code “wait for ThreadTable\[id] to finish”.

![](Pasted%20image%2020251009151632.png)

It is considered practice to have a multiprocess (and/or fork()) AND multi-thread program.


- Threads incur less overhead to create/terminate/switch as address space remains the same for same-process threads. 
- Some vendor CPUs have direct hardware support for threads
- Inter-thread communication is easy, cheap and faster than interprocess communication as threads share memory by default. 
- There are no protection boundaries in the address space: threads are assumed to be cooperating towards a shared goal.
- Coordinating access to shared resources is very complex - synchronisation is required
- It is very common to have multiple blocking events at the same time: website threads can be spawned to load different images. Webservers can have many threads for each route. UI programs have one thread for the UI and others for the background app.



### Types of threads 

#### User threads
Here, thread management is carried out in user space with a user library. The process itself maintains a thread table, managed by a runtime system within the user process without the kernel’s knowledge.

The OS cannot help with waiting for system calls or I/O calls between threads, so blocking will occur. 

There is a many-to-one relationship between threads in the user and the process in kernel.

Advantages are:
- No context switching overhead
- No system call overhead - very cheap
- Full control over thread scheduling within your application
- OS-independent: can run threads on other OS that may not have kernel-level implementation of threads

Disadvantages:
- Blocking system calls (while (1) loops) suspend the entire process: user threads are mapped to a single process.
- There is no genuine concurrency as it will run on a single CPU
- Non-preemptive: no interrupts

In kernel space: the kernel is aware of the process able. Above, in user space, the thread table and runtime system lives in user space.

![](Pasted%20image%2020251009153146.png)

#### Kernel threads

The kernel manages threads through API and system calls. The thread table is in the kernel, which contains thread control blocks (a subset of process control blocks). If a thread blocks, the kernel is fully aware and can choose another thread from the same/different process.

This allows true parallelism, and be preemptive, with no management needed in user space. However, mode switches take place which can lower performance.

There is a one-to-one map between threads in kernel-space and user-space.

![](Pasted%20image%2020251009153555.png)

Null fork: overhead in creating, scheduling, running and terminating a null process/thread.
Signal wait: overhead in syncing threads.

#### Hybrid implementations
A hybrid threading model has some kernel threads which support multiple user threads. This multiplexes user threads onto kernel threads: the kernel sees and schedules a number of kernel threads while the user application sees and creates an unrestricted number of them. 

![](Pasted%20image%2020251009154014.png)

> Exam Q: In which situations would you favour user level threads? In which situation would you definitely favour kernel level threads?


### Thread Management

Thread libraries provide an API to manage threads entirely in user space or be based on system calls. POSIX’s PThreads can do both and is a standard.

![](Pasted%20image%2020251009154232.png)


Threads are of type `pthread_t`

```c
#include <pthread.h>
#include <stdio.h>
#define THREADS 10

void* hello(void* arg) {
	printf("Hello from thread %d\n", *((int*)arg));
	return 0;
}

int main() {
	int args[THREADS] = { 0 };
	pthread_t threads[THREADS];

	for(int i = 0; i < THREADS; i++) {
		args[i] = i;

		if(pthread_create(threads + i, NULL, hello, args + i)) {
			printf("Creating thread %d failed\n", i); return -1;
		}

}

for(int i = 0; i < THREADS; i++)
	pthread_join(threads[i], NULL);
}
```
























