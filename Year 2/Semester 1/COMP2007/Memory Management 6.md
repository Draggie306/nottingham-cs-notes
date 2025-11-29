

Recap: paging with virual memory management underpins all memory management strategies today.

There are lots of challenges and policies required to make this work in practice today.

Today:

When deciding about using virtual memory, we should decide:
- when pages should be loaded into memory
- which pages are removed (using page replacement algorithms)
- How many pages and frames can be allocated to a process and if they are local or global
- When pages are removed from memory (using paging daemons)
- Problems that occur in virtual memory including thrashing

## Page replacement algorithms

1. Optimal page replacement
	- The best thing we can do but not practical in practice
2. FIFO page replacement
	- Second chance replacement 
		- Temporary ”changed” list - if it gets to the front, it is evicted
	- Clock replacement
		- Circular linked list is a bit more efficient
3. Not recently used
4. Least recently used


### Not recently used
In not recently used, we have a referenced and modified bit for each page in the page table. At the start, referenced bits are set to 0 and reset periodically (e.g. with interrupt signal). Referecned = “has this page been used in recent iterations”, modified = “have i written somethng to the page that hasn’t been synced to the hard drive”

### Page replacement
Thinking about needing a new piece of memory and if all memory is full, we need to decide what to replace it with.

If it has been modiefied, it must be written to the hard drive so it is not lost. With this i

There are 4 page types: 
- class 0: not referenced and not modified
	- This is the most preferred class: not used recenly and doesn’t need syncing to the hard drive
- class 1: not referenced and modified
	- Slightly worse: no longer used (so can free it) but should be written to the hard drive which will take some time.
- class 2: referenced and not modified
	- Even worse: page has been recently used (so it might need to be used again soon) but is on the hard drive as-is
- class 3: referenced and modified
	- Avoid: have to sync it to hdd before getting rid of it, and it has been recently accessed

Once determined, we can use the NRU easily:

Entries to the page table are inspected every page fault. Find one that meets class 0 on the first round. If nothing, re-search and find one that meets class 1 (but sync to the drive). If still nothing, set referenced bits to zero and retry. If still nothing, restart the first step - each element from class 2 and 3 is now in class 1 or 2. 

This is not perfect but is easy to understand and implement.

### Least recently used
Least recently used: keeps track with an ordered list. We use the past (what hasn’t been used for the longest time) and based on this, what is likely to not be accessed for a long time. 

![](Pasted%20image%2020251117151157.png)


> Resident set: pages in memory belonging to a process.

A small resident set means every process takes little memory, allowing more processes in memory, allowing higher CPU usage.

Ideally, every process has a small resident set. At the same time, we are increasing the chance there is something is not in memory but that is needed. A large resident set reduces page fault rate but lowers CPU use. Thus, there is a tradeoff between the resident set size and CPU utilisation.

The principle of working set (subset of resident set): all pages currently still using (referenced pages in the last working set window for the process). It is time-dependent: `W(t,k)` - k is the time/last memory references  

For a locality, once we move from one to another, generate lots of page faults at once, but then fast within the locality. 

The working set has 2 numbers. The number of pages will at least be 1 - there is always code associated with a process, 


k is a parameter that is set/tuned by the OS. If it is too small, not everything will be kept in memory, increasing page faults. Too large means there are too many unused pages are present, reducing CPU usage. Infinity just mend all pages are in the working set. 

Working sets can be used to guide the size of the resident set. If we notice that in the last 10 processes we are only using 2 pages, we can set the value to be 2.

> If the page fault frequency becomes too high: indicated the size of resident set is generally too small. 

If one process creates many main faults: a local or global page replacement policy can be used to that process A can take some memory from process B (which might not need all memory) and add it to its working set. 

Local: areas of the same process are reallocated. Every process has a fixed fraction of memory and the oldest page locally is not always the globally oldest one.


## Paging daemon

Most OS will have a background process running to proactively free pages for future page faults. If we need a new process NOW without one available, there is high overhead potential with writing to the drive. It thus makes sense to run something in the background to decide whether to proactively clean recently unused memory if load is not too heavy. 

It can be triggered by periodic intervals, when usage is too high, etc.

If can use a buffering list - if it is in the change it, reaches the front, and still hasn’t been used, only then remove it. 

> **The basic principles are easy but the fine-tuning is much harder.** 

## Thrashing
If all available pages are in active use and a new page needs to be loaded, the page will be evicted and reloaded very soon afterwards. “We recycle something that is needed again immediately.”

CPU usage becomes low, so the scheduler increases the amount of multiprogramming, to allocate frames 










