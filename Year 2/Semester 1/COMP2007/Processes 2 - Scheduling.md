The OS’ big job is to decide what to run and when to run them. New processes have to be admitted from new to ready, and when it gets to run (ready -> run). It also decides when to interrupt certain processes (running -> ready).

The scheduler (or dispatcher) decides what process to run, and uses a scheduling algorithm to do this.

## Process Scheduling & Schedulers
There are 3 scales of scheduling to consider:
1. Long-term scheduling: a good balance of processes wanting to run: a mixture of I/O-bound (waiting) processes and CPU-intensive processes. A mixture of both lets us make good use of the hardware.
	- This is largely absent on most modern operating systems
2. Medium-term: controls swapping and the amount of multi-programming (number of processes using the CPU). 
3. Short-term: decides what processes to run next
	- Manages the **ready queue**, is invoked very frequently, usually after a certain number of CPU clock interrupts, I/O interrupts or blocking system calls.

Non-preemptive scheduling strategies rely on processes voluntarily giving away “yielding” on the CPU. Implicit strategies like I/O operations can also be used. *Risks: no way to get out of bad situations e.g. infinite loop.*

Modern OS use preemprive: when a process is running, it may be interrupted forcefully, regardless of whether it wants to. It prevents CPU monopolisation, but requires context switching overhead. Most OS are of this type.

To assess the performance: users want a fast response time, turnaround time and predictability, while the system wants to maximise the number of jobs per unit time and being fair - an equal distribution of processing and waiting time, and reducing starvation.

Improving response time requires more context switches, worsening the throughput and increasing turnaround time - there are tradeoffs for each.


In 20 time slices:
- Average response time measures the start point for each process, adding all start points and dividing by the number of jobs.
- Average turnaround time: measures the end point for each, adding them and dividing by the total.

## Scheduling Algorithms


### First Come, First Served
 + Pros: Positional fairness: there first, finish first.
 + Cons: Favours long processes over short ones (e.g. shop checkout, do not affect long jobs but are mean to short ones), may compromise resource allocation

### Shortest job first
- Pros: always gives the optimal turn around time
- Cons: starvation for long jobs, compromises fairness and predictability (a small job may look long in comparison to tiny jobs), processing times must be known beforehand

### Round Robin
- A pre-emptive version of FCFS, which forcefully interrupts processes at a timer interval. 
- Pros: improves response times, effective for general-purpose systems
- Cons: increases overhead with context switches, favours CPU bound process over I/O (may be allocated 100 slices when I/O only requires 1 CPU slice), can be reduced to FCFS with very short slices.

### Priority queues
 A pre-emptive algorithm that schedules processes by priority. The priority is saved in the PCB. Within each priority level, round-robin is used.
- Pros: can prioritise I/O-bound jobs
- Cons: low priorities may become starved

**Exam question calculation example**

![](Pasted%20image%2020251007124038.png)




Generally, the average response time and average turnaround time are the most used metrics.
