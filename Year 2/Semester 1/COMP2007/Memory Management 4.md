
Today: 
- Address Translation, and how it is implemented
- Virtual memory and page faults
- Multi-level page tables
- Translation Look Aside Buffers

### Recap

- Logical address space: what the compiler sees and assumes, starting at 0 to maximum (the number of address lines on the CPU, e.g. 48 would have 2^48 memory locations), in evenly-sized pages.
- Physical address space, split into frames of typically the same size as pages.
- Non-contiguous: all pages can be stored in any arbitrary order within the frames. Frames have contiguous ordering.
- Page table: based on oage number of the logical address, we can go to any row as an index to get a corresponding frame number for that 
- Offset within the page and frame remains the same

We use paging to reduce external fragmentation: we do not want tiny spaces of memory left over. Internal fragmentation: partitions were large (100mb) but only 1mb so wasted 99mb. Pages are very small here, so the potential for waste is much less. 

Mapping is implemented by e.g. saying that the top of logical address is 1111. The mapping is mapped onto the lowest page in physical address space. ![](../../../Pasted%20image%2020251110150705.png)

Index 15 (1111) means there are 15 frames sitting below the current frame. The offset is just index * base unit. 

Simply:
- If logical address: extract page number from lofical address
- Use this to retrieve the frame number in the page table
- Substitute the page number with the frame number

This is done in hardware:
- The CPU’s MMU interprets logical address
- The MMU uses a page table
- The resulting physical address is put on the memory bus. 

## Virtual memory
Thinking about how code runs: if we have a very large program, we are only likely going to be using a small amount of its overall functionality. Code has a principle of locality: of all machine code there is, we will only use a small part of that at any given time.

> For loop: do the same bit of code a few thousand times. 
> A huge array of image data: when we process this (editing a video), we only process a small part of this at one point in time.

We assume the entire logical address space is loaded in memory. This is wasteful - we only use a small part of it. We can use only a small amount currently needed. Only when we need to use something large, e.g. an image, when it is needed.

We could load the pages that the process uses on demand. The page file may have a mapping between logical and physical memory spaces, but there may be a large unused part with no mapping.

Logical address space is same as physical. This is required if the entire process needs to be in memory. If we only use the part we need, we can have a much smaller physical address than the physical one. 

### Page faults
The **resident set** of a process are pages with a physical frame associated with it. 

If we move to a different locality, we need to load new data into the physical frame. Trying to access this causes a **page fault**. Page faults create an interrput (blocked state), while I/O reads the page into main memory. Context switches may occur so the CPU can be busy, and once the I/O is complete with another interrupt, the process enters ready state.


### Processing page faults
When we do this, the process must be stored in the same process control block so it can be restored later on. Save all registers and state.

Then, identify the page fault. Determine the page location and issue an I/O request. Switch context if needed. 

Once interrupt received, store the current process state and registers, and analyse the interrupt. Update the page table with the new address in memory, and wait for the original process to be scheduled, and context switch to the original process.

### Processor utilisation 

Virtual memory improves CPU use as each process takes up les memory, allowing more processes to be in memory. This means CPU can be more busy. *Although there is higher overhead, the chance that the CPU will need to work on something from some process also increases.*

This also means the page table becomes more complex. Previously, it had a mapping from page -> frame number. In practice, more information is required:

![](../../../Pasted%20image%2020251110152734.png)

If it not been referenced recently, then it could be removed from memory. If it has not been modified, then it doesn’t need to be written back to a drive. 

Read/Write/Execute protection: can share machine code between two processes (just read permissions for machine code but no modification). 

For a 16-bit machine, the address space is 2^16. Given 10 bits for an offset, and 6 for page number, that allows us to maintain 2^6 = 64 pages.

![](../../../Pasted%20image%2020251110153114.png)

As page tables become bigger and bigger, we can no longer store them in registers; instead, main memory (100x slower than CPU). To maintain speed of address translation, this needs to be addressed (increasing page size reduces page table but increases fragmentation).

### Multi-level page table
Similarly to only using the memory frames we need, we can do something similar with page tables, with a tree-like structure.

We can have a **root page table**, which says the address of the **second-level page table** that contains the page-to-frame mapping. In the root page table are a few addresses at the top and bottom where the mappings are located, in-use. 

> Virtual memory: only load the info that we are currently using into memory.

Having to go to memory for the page-frame mapping, and then having to go back to memory to get the value itself, we double access time. With two page table levels, we 3x access, and in modern machines, there are up to 5 levels of page tables.


### Translation Look Aside Buffers (TLBs)
A look aside buffer is a piece of cache where we store page-frame mappings. 

“likely to use a small subset of information that is typically co-located in the same page or set of pages” 

the number of pages a process will use is going to be fairly limited. When there is a cache that isn’t particularly big, this will still work, as there are only a small number of mappings. 

The first thing we do is look if the TLB has cached it from a recent operation (and if so, use this directly to go to memory for the offset), else, use the page table. 

If there is a TLB hit (may take 20ms to lookup) 

### EXAMples 

Given a page size of 4Kb:
![](../../../Pasted%20image%2020251110154644.png)

Exam: based on what you know about paging, give the correct address translations for a given example. 


