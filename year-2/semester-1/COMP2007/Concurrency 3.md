

### Coursework
- There are instructions on how to compile/run the code in the project: **do not change the Makefile**. It is assumed to be used.
- Can I compile on a different Linux machine? Yes, broadly it will work, but still check and test on the students2024 SSH machine.
- Don’t use things that don’t get taught: if it hasn’t been taught by next Monday, it probably will not be needed. 
- Can I use pthreads condition variables? No. All questions can be solved cleanly and elegantly without these.

- Do not have any compile warnings!

### Recap

Mutexes are one way to lock and enable concurrency, without causing chaos in our programs.

Software approaches to mutual exclusion: Peterson’s solution. It is a historical/educational solution that makes naive assumptions about the hardware. 

Modern texhniques: spinning around and waiting (teat_and_set, compare_and_swap) that are atomic and mean we can enter critical sections. 

Operating system: queue until the lock becomes available, using a system call. Can be expensive: with context switching etc., but straight forward.

- Modern implementaiton: one is slow (longterm waits), other is cpu-intense “busy waiting”/spinlocks -> do this one first for a few cycles, but then defer to the slower but more suited with syscalls.


Mutex usage:
- Somewhere, a `pthread_mutex_t lock` is created.
- Then, it is initialised with `pthread_mutex_init(&lock, 0)` - this turns the empty memory into something useful.
- Then acquire the lock with `pthread_mutex_lock(&lock)` - either acquired or blocked for now.
- Then do the critical section `counter++`
- Then unlock the pthread with `pthread_mutex_unlock(&lock)`
- Finally, destroy/free the memory with `pthread_mutex_destroy(&lock)`


## Semaphores

These are synchronisation abstractions. They have a capacity  (natural number) which changes during their use.
We can distinguish between binary semaphores (2 values, 0 and 1) and counting semaphores (unbounded, 1 -> any number)

They have two functions to manipulate them:
- `wait()`, which decrements the capacity (blocking if the capacity is 0).
- `post()`, which increments the capacity. **Any thread can do this**, compared to with mutexes.

### Pseudocode

There is some structure that:
- has an integer capacity
- has a structure that has a list of process

with a `wait()` function that:
- takes in the semaphore pointer
- decrements the counter
- if the counter is below 0, then block() with a system call

and a `post()` function that:
- takes in the semaphore
- increments the counter
- wakes up the process from the list with a system call
	- This can be any process, do not make assumptions as to which thread will be picked up.

### Examples

![Pasted image 20251020152033](../../../Images/Pasted%20image%2020251020152033.png)

This wait and post operations must behave atomically, naively this can be done with a mutex `lock` and `unlock` when called.

There are different strategies used to wake up processes, so do not assume (e.g. might not be the first one blocked, might have more I/O processes, etc)

Communication within the same process can be defined as type `sem_t` - an anonymous semaphore. (don’t fork a process with this…)

- sem_init() initialises the value of the semaphore
- sem_wait() decrements the value of the semaphore
- sem_post() increments the values of the semaphore

`man` pages can be used for these: man `sem_init`

### Real-word issues

- Never ignore compiler warnings.
- Always check return values - slide examples don’t for space reasons.
	- Especially for pthreads, exit the code or blow up if it’s not right! 
- Test code thoroughly - implicit assumption Mac would work like Linux was wrong!
- Be aware of platform specific issues such as sem_unlink behaviour on Mac.
- Use the appropriate concurrency primitives - the example really needed a mutex
	- If there is a choice between a really powerful thing (semaphores) or a lowly specific thing (mutex) then use the mutex, as there is less scope for bugs or issues to appear.

## Producer/consumer problem

Producers are making something that we want to share with something else. 
A consumer is taking the produced things and doing things with them, e.g. coordinating activity between threads.

There is a buffer between them; crucially, if we add to this and it is full, then we get blocked. This might not be the case (but often, the size is bounded). The consumer wants to do something with the things being produces; if there is nothing produced in the buffer, it gets blocked.

The simplest version is one producer and consumer, and an unbounded buffer size. To have this:
- we use a counter (index) to keep track of buffer items, producer increments, consumer decrements.
- This buffer uses 2 binary semaphores:
	- `sync` to synchronise buffer access, initialised to 1 (similar to a mutex)
	- `delay_consumer` ensures that the consumer blocks when there are no items available, initialised to 0

The consumer (launched, at some point, by a pthread_create) is constantly consuming. Simulaneously we have a producer “busy-waiting” to produce something.

The consumer does a sem_wait (equivalent to a mutex aquire, locking the buffer/item counter) and stops, as the delay_consumer is 0.

Then, the producer drops in to the sem_wait(sync), which is 1, and enters the rest of the code. It does its job and then runs `sem_post(&delay_consumer)`, which wakes up the other thread, then `sem_post(&sync)`

[… more notes]

![Pasted image 20251020153933](../../../Images/Pasted%20image%2020251020153933.png)

Any manipulation of items must be synchronised. However, it is not safe.

- When the consumer has exhausted the buffer, it should be blocked, but the producer increments items before it is checked by the consumer.

























