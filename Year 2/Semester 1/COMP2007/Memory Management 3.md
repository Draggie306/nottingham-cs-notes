

Recap:

- Dynamic partitioning results in external fragmentation (though solves internal fragmentation), but this makes managing free space difficult

The last 12 bits are used to determine where in the segment the memory is, while the top 2 are used for the base and bound.

Dynamic partitioning is required to reduce internal fragmentation and handle sparse address spaces (segmentation). 

A simple data structure that can be used to manage free space is a bitmap. Memory is split into blocks (pages) of e.g. 4kb sin size, and a bitmap is set up so that each bit is 0 if the memory block is free, and 1 if it is used. 32MB of memory can be represented as 8192 bitmap entries which occupy 1KB of storage only. The size of the bitmap depends on the size of memory and size of allocation unit (block size).

To find a gap of 128KB with a bitmap, it is typically a very long operation. Thus, there is a tradeoff between the bitmap size and block size. Larger blocks increase internal fragmentation while smaller blocks increase searching speeds. 

Instead, linked lists are used. These have a variable number of free and used partitions, with each link containing data, start of the block ,the block size, and a flag if it is free or used. The **first fit** scans from the start until a sufficiently large gap is found. If the space is the exact size, allocate it there.Otherwise, split into the first entry and mark as “used” with the second set as remaining and marked free.

The next fit algorithm maintains a record of where the last search stopped the previous time. All memory gets an even chance to be allocated; first fit focuses on the start of the list. *However, this performs worse than first fit.*

> question: how is a gap found if the linked list nodes only record the start address and size of that address, not free addresses?


Best fit searches the entire list for the smallest hold to satisfy the request. It is slower than first fit but results in many small holes. If we always try to match a section as close as possible, we end up with leaving very small addresses leftover, wasting memory.

Then, worst fit finds the largest available partition and splits it. The leftover part is still large (more useful) but is not good in practice. 

- First fit: allocate first block that is large enough
- Next fit: allocate next block that is large enough starting from the current location
- Best fit: the block that matches the required size the closest; O(N)
- Worst fit: the largest possible block; O(N)

Quick fit maintains list of commonly used sizes, e.g. 4, 8, 12, 16KB holes, with the required access being placed into the nearest size list. This increases speeds to find the required hole; however, it still creates many tiny holes. 

### Coalescing 

This is the joining of two adjacent entries when the linked list becomes free. Both neighbours are examined when a block is made free, 


### Taking a step back

![](Pasted%20image%2020251104122641.png)

We are expecting everything to be contiguous in address space. For example, if the heap gets too big between other processes, we are forced to move it out into another range. It would be good to say: “this gap is now used up, let’s add another one somewhere else”.

Paging uses fixed partitioning an code re-location, a non-contiguous memory management scheme. 
- Memory is split into much smaller blocks.
- A process is allocated at least 1 block (a 11kb process uses 3x4kb blocks)
- Blocks do not have to be stored in contiguous physical memory locations, and the process just perceives the blocks to be contiguous (they *are* adjacent in logical address space). 

Benefits of non-contiguous schemes include that internal fragmentation is reduced to a few last blocks only, and there is no external fragmentation (no gaps between each block).


![](Pasted%20image%2020251104123206.png)

A page is a block of contiguous memory in logical address space, and a frame is a contiguous block in physical memory. 

Every page has its own offset that allows translation.

Pages are mapped onto frames, of commonly the same size between 512bytes and 1gb. A page table has a page number as an index into the page table which responds to the frame number. 

A page number of 0000 means it is the lowest in the page (start of the program), and it may be mapped to a frame number 1010 meaning there are 10 frames below. With a 12 bit offset, we have 4KB pages. Once the offset is all 1s, we then flip to zero and go to the next page, until we reach the end of the page number (e.g. 4 bits gives us 16 pages, with these 12 bit offset, we get 16x4KB pages each).

![](Pasted%20image%2020251104124543.png)

Translating can be done by mapping the page number in the page table to the physical address. There is one page table per process 





























