
## Free space implementations

File allocation tables and i-nodes show which blocks are in use. To keep track of free space though:

Bitmaps and linked lists can be used for free space management. 

- Bitmaps represent each block with a single bit in a map. It grows in size with the disk size but is constant for a given disk.
- Linked lists depend on how much space is in use. 

If we increase block size, we reduce size of the bitmap/linked list, but the more likely internal fragmentation within the blocks occur. (if block size is 4kb but only 1 byte is used - we waste 3.999kb). 

Linked lists can be modified by tracking the number of sequential free blocks for each entry.

![](../../../Images/Pasted%20image%2020251202120832.png)

Bitmaps are the most commonly used today.

Linked lists grow with the number of empty blocks, resulting in no waste of disk space, and only one block of pointers needs to be kept in memory (one block is loaded when needed).


## Recovering file systems
If there is a power cut, there is nothing much that can be done from code to predict this. **Journaling** reduces the probability of inconsistencies. This is problematic for structural blocks: i-nodes, directories and free lists.

Scandisk and FSCK are system utilities to check for block, directory and i-node consistency.

%% The i-node will say which blocks are being used, a table will be updated  %%





### Defragmentation

With RAM, compacting takes a long time - hard drives are even slower. 

On SSDs, a log structured FS prevents fragmentation. However, on HDDs, defrag tools combine free space into large contiguous regions, but is very slow and usually runs in the background. 

## Linux file system

By growing single, double and triple indirect pointers in i-nodes, we can increase the size of files.

Extended file system 3 and 4 added journaling.

Compared to the Unix filesystem, the ext2 has a metadata section within each block group. This is to reduce seek times versus the traditional one which stores all metadata at the start, and data at MAX. 

![](../../../Images/Pasted%20image%2020251202122922.png)


Every directory entry contains the fixed length fields of i-node number, entry size in bytes, type field, and file

![](../../../Images/Pasted%20image%2020251202123217.png)


## Knowledge test
















