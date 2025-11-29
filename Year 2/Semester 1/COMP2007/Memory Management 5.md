

The principle that we only use the memory in use by a process can be applied to page table. 

Page fetching and page replacement algorithms determine what to evict from memory/put into virtual memory.

The key principle of this is locality: groups of pages are used together, relating to a function. A stable locality: every bit of information is in memory, with no page faults. Page tables have become larger and more complex with present/absent bits + referenced/modified bits. 

### Inverted page table (hash table)
Multi-level page tables can become very big. An inverted page table has one table that contains one entry for every frame, proportional to memory size. 

Inverted page tables are indexed by the frame number and hash code

Physical address: has a virtual page number (e.g. 1) and offset. Based on the process ID and the page number, calculate the hash function. This is used as an index into the inverted page table (hash table). Each entry in this has a PID, page number, protection buts, and a link pointer to the next entry (as there can be collisions). 

The advantages are that the OS maintains a single inverted page table for all processes, which saves space for large virtual address spaces. 

Disadvantages include a slower/more difficult logical-physical address translation. Collisions still slow down address translation as they have to be handled. 

Hash tables reduce search time while TLBs improve performance. 

### Paging decisions

> Set of pages currently being used is the **working set.**
> It is a subset of the resident set: all memory with a frame associated 

Demand paging: process starts with no pages in memory. Usually, more than one page will be required for each process. Initially, this means until the entire locality of the process start has been brought into memory, page faults will be repeatedly generated, eventually stabilising. 

Pre-fetching involves bringing the working set into memory at once, reducing page faults. This requires the working set to be kept track of, with a tracker for which pages make up the working set using an aging algorithm.

### Page fetching

Avoiding unnecessary pages and page replacement is important. 
![](Pasted%20image%2020251111123307.png)

For a single page table with a memory access time of 100ns, and requiring two memory accesses (200ns), and a page fault time of 8ms… the page fault dominates
![](Pasted%20image%2020251111123415.png)

### Page replacements

Whenever a page is loaded, the OS needs to evict something. The page replacement algorithm decides what to remove. The algorithm checks when the page was last used/expected to be used again, and whether it has been modified (based on the table bit; if it has not been modified, it is the same as on the drive). 

This must be made intelligently, and there are a range of replacement algorithms. 

- Optimal page replacement
	- Every page is labelled with the number of instructions before it is used again.
	- Meaning, the page will not be referenced for the longest time, so is the optimal one to remove
	- This is infeasable in practice - can provide a lwer bound for page fault number and to compare with other algorithms
- First in, first out
	- Simple but performs quite poorly. 
	- The olfest page at the head of the list is evicted when the page fault occurs.
	- There is no way to discriminate different pages - a for loop is just as likely to be evicted as rarely-used pages
- Second-chance FIFO
	- If the page at the font has not been referenced, it is evicted. If the 

!!TODO: More stuff

For a very large 2d array, it is faster to access it row by row. This is because addresses are stored contiguously in …….


