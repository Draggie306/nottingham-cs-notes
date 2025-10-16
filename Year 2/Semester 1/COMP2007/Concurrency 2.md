
Locks and critical sections in more detail.

> Coursework released
## Mutual Exclusion
There are some ways to implement locks and critical sections:

- software-based: Peterson’s solution
- hardware-based: test_and_set(), compare_and_swap()
	- These are required to be atomic
- OS-based: kernel blocking


### Peterson’s solution
Is a software based solutions, just requiring a C compiler. Works, if naive assumtions are made about what you see is what you get (nothing to do with caches, memory etc.)


It uses 2 shared variables:
- `turn`: indicates which process can access the critical section
- `bool flag[2]`: indicates in slot `i` that the `i`th process is ready to enter the critical section (can be made bigger/generalised, usually 2 processes).
- The algorithm satisfies all the critical section requirements (mutual exclusion, progress, fairness)

![](../../../Pasted%20image%2020251016151208.png)

The program is polite: it waits for permission to get into the critical section. Process `i` does the same thing as process `j`.

- Initialises flag to false
- Updates flag to be true, indicating other process can access
- While the other program is using it, drop out
- Enter the critical section
- Exit the critical section by setting the process flag to false
- Repeat.

Mutual exclusion:
- The variable `turn` can have only one value at a time. Every process agrees on this value.
- Both `flag[i]` and `flag[j]` are `true` when they want to enter the critical sections, so at most one while condition in `flag[i] && turn == i` is false, so one process can enter the critical section  

Progress
- Threads in the remaining code does not influence access to the critical sections. The thread that makes progress is decided in finite time.
	- If no thread wants to enter, nothing happens
	- Only thread i wants to enter the critical section in which case flag[j] && turn == j is false, as flag[j] is, and it may proceed.
	- Only thread j wants to enter the critical section in which case flag[i] && turn == i is false, as flag[i] is, and it may proceed.
	- Both threads want to enter the critical section, then at least one of flag[i] && turn == i or flag[j] && turn == j is false, depending on the value of turn, and somebody can make progress


Fairness/bounded waiting:
- It is fairly distributed, process cannot be made to wait indefinitely

![](../../../Pasted%20image%2020251016152440.png)


## Hardware approaches

> Do not write Peterson’s solution in code, as it is theoretical.


Providing hardware operations that generally do more than one thing at once is common. There are specialist funcitons that cannot be split into two and are therefore atomic: test_and_set() or compare_and_swap(). We combine these with a variable to indicate the lock is in use. We also use a repeated checking strategy, known as a spinlock/busy waiting.


Pseudocode for `test_and_set()`
- Takes in memory address
- Reads the old value
- Sets value to true
- Returns old value

To use:
`while test_and_set(&bIslocked)`
- As the old value will be returned, 


![](../../../Pasted%20image%2020251016153203.png)




![](../../../Pasted%20image%2020251016153406.png)

If the value returned is false, the lock was just obtained. Else something else has it, so it infinitely loops.


Spinlocks can waste lots of CPU cycles; alternatively, locking can be made using system calls - waiting for the lock in a queue in the kernel.

Realistic locks use hybrid strategies: briefly spinlock, but (as this is expensive for long locks), fall back to system calls.

## Mutexes

Are an abstraction for providing mutual exclusion. They give two functions:
- `acquire(&mutex)` - before entering the critical section, returns when nobody else is holding the lock
- `release(&mutex)` - after exiting the critical section, allowing other threads to acquire it. 
Only the thread that acquired the lock can release the mutex. 

This can be implemented in any way, as an abstraction.

![](../../../Pasted%20image%2020251016154317.png)

`pthread_mutex_init` - common in coursework

> Run `man pthread x` - if there is trouble with the coursework

`pthread_mutex_lock` and `pthread_mutex_unlock`





### Questions:

> If it is “waiting for an event” -> observer pattern, then why is there something continuously checking and effectively using a spinlock? 


