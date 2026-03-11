

Readers-Writers problem: many readers can concurrently read, writers only when there are no readers. However, readers overwhelm writers, starving them. Today, the goal is to favour the writers.

Solution 3 gives priority to writers.
- It uses iReadCount and iWriteCount to track of readers/writers
- Mutexes sRead and sWrite to synchronise the reader/writer critical sections, preventing race conditions
- Semaphore sReadTry coordinates stopping readers when there is a writer waiting
- Semaphore sResource to synchronise the resource for reading/writing.


![Pasted image 20251027151417](../../../Images/Pasted%20image%2020251027151417.png)

- Firstly, the readers would like to read. Checks capacity in the readTry semaphore (1 -> 0) and then locks the read semaphore to increment the count.
- First arrival: different behaviour.
- Release semaphores

There is a entry/exit section with a special case for the first/last reader/writer entering or exiting.

There is a shared resource and a waiting area. Readers are happy to go in to the waiting area if the light is off or the waiting area is on. Once a reader enters the waiting area, they turn the light on. If the light in the shared resource is on, readers enter. If the reader is the last one in the waiting area, then they turn the light off (exiting directly out of the shared resource). 



## Lock convoying

One thread enters the critical section. Two then is waiting “locked”, and the one in the critical section finishes, so two moves in the critical section. Then there is a load spike - threads 3-7 are waiting. Thread two leaves the critical section and three enters, but then thread 8 is waiting. Even though processes are running in equilibrium, we are now waiting 5 time slices instead of one. 

Locking occurs in two phases:
- a spinlock/busy wait for short time - cost increases over time.
- a system call - large one-off cost while OS adds to queues, etc.

Once we have a long enough queue, the lock will make system calls, slowing it down significantly. This delay will be much worse than the 5 time slices in the queue!

Modern CPUs have many cache levels, cache misses require slower memory access. If caches contain relevant data, performance improves. The MMU also assumes similar addresses are used, so context switches affect this. All these factors affect time slice length. Caches are going to be cold and will be required to be set up, and need to stay on the CPU long enough to get the benefits of faster speeds. 

Once we have a long queue, threads are blocked waiting for the lock, so do not use the full time slice. The kernel will run other threads to keep busy, but this means that when a thread reaches the critical section, the caches become cold. This means doing the same work is slower once there is a queue. 

Typically, the queue length is ballooned with e.g. a load spike. This means locking takes longer than expected, so system calls are used which increase overhead. Then context switches slow down CPU more, and the queue length increases, and the loop continues.

To get out of this situation, it is difficult. However:
- use less locks (usually only an issue )
- avoid doing work that does not need protection with a lock
	- e.g. do not lock during multiplication, only the counter afterwards
- avoid doing blocking operations (I/O, printf) when holding locks
- increase the number of locks, so the same block does not protect multiple pieces of data (deadlocks with multiple locks easier, but lock convoy harder)
- use less threads; more speed is not guaranteed
- modify wake-up strategy. FIFO maximises context switching. Once a queue has formed, all will have to wait for syscall overhead, so FIFO makes it mathematically worse. FILO may make it easier, so lock is handed to most recently queued process, avoiding a syscall…
- 














