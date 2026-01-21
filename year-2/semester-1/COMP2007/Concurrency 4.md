

### Recap:

Semaphores:
- Have a capacity
- Less restrictive than mutexes.

Other:
- Producer and consumer problems
- Even though locking is happening, race conditions still occur



## Unbounded single producer-consumer problem

There is a delay consumer semaphore that is used like a thread to wake up the consumer thread when there is something available.

There is also a producer thread that locks the buffer (this case, a counter). If it is the first thing in the items, it notifies the other side, waking up the consumer, and releases the lock.

![](../../../Images/Pasted%20image%2020251021121217.png)

The issue here is there is an implicit relationship between `items` and the semaphore `delay_consumer`. 

> In coursework, there may be 2 arrays and a counter - the things that need to be atomic may not be individual reads and writes, but the whole operation

Solving this with unlocks can result in deadlocks.

![](../../../Images/Pasted%20image%2020251021121501.png)


To solve the problem, we can use a temporary variable, to store the value of items inside the critical section, and decrement delay_consumer semaphore for consistency.

![](../../../Images/Pasted%20image%2020251021121707.png)

Instead of testing `items`, we are testing “temp” - an earlier source of truth, which can be referred to after 

The number we want is “how many items were left when we decremented”.

> Coursework: do not refer to variables as “temp” - all variables are temporary. 

Correctness: is the solution above obviously correct? No, it doesn‘t look guaranteed to be correct, and more “ad-hoc”.


### Bounded buffer

The previous code works by storing the number of items.

A different problem has n consumers, m producers and a buffer size N, based on 3 semaphores:


- sync - keeps mutual exclusion of the buffer
- empty - counting semaphore, the number of empty buffers, set to N
- full - counting semaphore, the number of full buffers, set to 0


![](../../../Images/Pasted%20image%2020251021122528.png)

Producer: waits for some capacity in the empty slot. It then waits for the lock, put things in to it, and frees the lock. Repeats, as there is space in the semaphore left, until its capacity is zero.








## The Dining Philosophers problem

Defined as:
- 5 philosophers sitting on a round table
- Each philisopher has a plate of spaghetti
- The spaghetti is too slippery, so each philisopher needs 2 forks to eat.
- When hungry (and not thinking about life), they try to acquire the forks on the left and right.
This is a limited set of resources (forks) and processes (philosophers)

Forks are represented by semaphores, initialised to 1. 1 if the fork is available and 0 if not; and the philosopher goes to sleep. The approach: each philosopher picks up a fork and waits for the second one to become available (without putting the first down).

![](../../../Images/Pasted%20image%2020251021123426.png)

This means that every process is waiting for other process, causing deadlock. We can attempt to prevent deadlocks by:
- Putting the forks down and waiting at a random time - back off for a while if can’t pick up the second. 
	- Depending on how long we wait, it can cause ”livelock” (both processes back away at the same time, causing CPU to go high: e.g. person gets in way, moves to left, other moves to left, moves back, etc…)
	- Can cause starvation: outside scope of the scheduler, that means the philosopher (and process) keeps getting starved.
	> DO NOT have this backoff design in coursework
- Putting an extra fork on the table - cheating!
- Lock the whole table “global mutex” - set by one philosopher at a time.

![](../../../Images/Pasted%20image%2020251021124131.png)

This is a ”big” lock: locking the whole table (don’t really need the other semaphores). Only one philosopher can use the table at a time, so there is no real issue/nothing complex can happen.

Can the value of `eating` semaphore be 2 (the optimal solution) for more parallelism? No, because the next person will be unable to get a fork. And because the limit is 2, it will not just cycle to the 3rd philosopher…. 


