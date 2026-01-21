
Recap:
- Jobs can have different priority levels, with multiple queues (one for each priority level, e.g. from 0 to 3).
- Jobs of the same priority run using Round Robin

- Threads are an abstraction of a thread of execution: lighter weight vs processes (as processes have address spaces and file handles)
- Hybrid/user/kernel threads have different advantages and different advantages (genuine/emulated concurrency)
 
> PThreads are important for coursework: they are the library upon which everything will be built.

## Multi-level feedback queues
Feedback queues allow priorities to change dynamically. Jobs can move between queues: if too much CPU time, it can be demoted to a lower priority queue (to prioritise I/O/interactive processes - making better use of the hardware) or promoted (preventing starvation and avoid **inversion of control**).


> Exam 2013-2014: Explain how you would prevent starvation in a priority queue algorithm

### Inversion of control


![](../../../Images/Pasted%20image%2020251013151223.png)
Having 3 processes:
- Even though the first process A is low priority, it runs first and holds the resource. 
- Process B has high priority, so it starts running. However it wants the same resource as Process A, so it is blocked. 
	- At this point, if it was the only process running, A would carry on until it has finished with the resource.
- Process C (medium priority) runs. It doesn’t need the resource, just calculations on the CPU (for hours). 
- This means that this situation has a high priority process is doing nothing whilst a lower priority process has full control over the system.

> Higher priority processes have lower numbers. 


![](../../../Images/Pasted%20image%2020251013151421.png)

To prevent starvation, MLFQs can temporarily promote processes, and demote resource hogs to lower levels.

Feedback queues are very highly configurable, but with great power comes great responsibility. There can be:
- A large number of queues - up to the implementation to decide.
- Promotion/demotion policies can vary lots
- Different scheduling algorithms used for the individual queues
- Changeable access to the queues


## Scheduling in Windows 7 and Linux

### Windows 7 scheduler

- There are 16 levels of priority, starting with the process priority.
- Each thread has a base priority (highest/lowest, above/below normal, and normal).
- Each thread has a dynamic priority that can be boosted up or down depending on goals - e.g. browser image fetch low but word writing high.

Processes may have their priorities dynamically changed during execution between the base and tis maximum class priority:
- I/O: boost priority until there is an I/O request and then immediately yields the CPU to something else. 
- Boosting prevents starvation and priority inversion


### Linux: The Completely Fair Scheduler

Scheduling has changed to make better use of multiple processors. 

Linux has 2 types of tasks/job:
- Realtime tasks (due to POSIX compliant standards), divided into:
	- realtime FIFO tasks: the highest priority and scheduled with FCFS. Preemption can occur if there is a higher-priority process
	- realtime Round Robin tasks, preemptable by clock interrupts with an associated time slice.
	Neither guarantee hard ”realtime” deadlines/guarantees
- Time-sharing tasks (similar to Windows’ variable tasks) which are preemptive.

The ideal fair scheduler:
- has a CPU that allows all N tasks to run simultaneiously with each receiving 1/N CPU powers (5 tasks, each gets 20%)
- Real CPUs though cannot run arbitrary tasks in parallel

To divide up CPU time, we choose a target latency: the amount of time before each task gets the CPU, and measures how far we are from being fair. To achieve this, all tasks N are allowed to run for 1/N of the target latency.
We also choose a minimum granularity - minimum time to run before considered to switch, to reduce excessive context switching.

To be fair:
- Virtual time is recorded - total CPU time
- Tasks are ordered in ascending order of virtual time used (in a red-black tree)
- The task with the lowest virtual time is considered to have been treated the least fairly, so will run the next. 
- After a task has had 1/N of the target latency, it will be replaced with the next lowest virtual run time.
- System calls may lead to less than allocated time, getting back on the CPU more quickly.

The recorded virtual time on the CPU is the realtime scaled by the weight of the priority (**VERY SIMPLIFIED**). E.g. of both 100ms actual CPU time, a priority 1 has 100ms virtual time, whereas a priority 2 has 200ms virtual time. 

> **Virtual time runs at different speeds for different process priorities.**

Unlike time slicing, tasks will be given different time windows to run in.

![](../../../Images/Pasted%20image%2020251013153357.png)

To avoid ”pathological” behaviours:
- new tasks will have their virtual run time set to the current minimum virtual tun time - else it would start at zero, and would run for a *very* long time
- blocked tasks have their virtual run time set to the greater of:
	- the current minimal run time, minus a small offset (to allow it to run next)
	- its old virtual run time (if already getting lots of CPU access)

### Multiprocessor scheduling

Shared queues are a single or multi-level queue that is shared between all CPUs. This allows automatic load balancing by arbitrary CPUs:
- does not take advantage of CPU state: cache becomes invalid when moving to a different CPU, so loses efficiency
- Translation look-aside buffers (TLBs, part of the MMU) are invalidated

Private queues are a per-CPU queue. Each thread only runs on once CPU. This allows better re-use of CPU state (cache, TLB) and reduces contention, but there is less load-balancing - all processes could be placed in one CPU even with 4 total system CPUs. Thus, migration between CPUs is possible, perhaps for those at the end of the queue.

## Scheduling related threads

Related threads: those that communicate with one another and run together (e.g. searching algorithm)

Unrelated threads: independent processes - different users/programs

![](../../../Images/Pasted%20image%2020251013154255.png)


**Space** and **gang** sharing are approaches to get collaborating threads running at the same time across multiple CPUs.

### Space sharing
N related threads are allocated to *N* CPUs (when *N* CPUs are availble). 

Gang scheduling groups related threads into chunks on the CPU and uses time slicing.





