

# File system implementations

### File access

Files are made of multiple blocks - wither sequential or random access (Essential for databases). The key issues is how to associate and group processes together. 

We should know: where the file starts and how large the file is, and everything can be worked out - similar to dynamic memory allocation. 

When we store files in the file system, they can be stored one after another. However, over time, files are grown/shrunk or deleted, creating gaps. The same principle as memory, to find a suitable gap, is applied to the disk. 


### Contiguous allocation

Only the location of the first block and the length of the file must be stored, in the FCB. This also creates the optimal read/write performance: if the file is stored contiguously, blocks are located in adjacent sectors with reducing seek time and rotational latency. Even on an SSD, this is good, as each block needs to be fully accessed (all pages in the block) before writing - if they are all part of one file, there is a speed gain. 

Disadvantages include that the exact size of a file is not always known beforehand, and requires allocation algorithms to decide the free blocks to allocate. Deleting a file results in external fragmentation, requiring defragmentation (slow). 

Contiguous allocation is still used for CD-ROMs and DVDs. External fragmentation is less of an issues, as they are write-once.

> Solving external fragmentation in memory: memory is divided into tiny blocks stacked on top, managed in a page table.


### Linked lists
To avoid external fragmentation, files are stored in separate blocks (like paging) that are linked to one another (in a linked list). Only the address of the first block is stored in the file metadata, and each block contains a data pointer to the next block.

This is easy to maintain (only the first address has to be maintained), files can grow dynamically, there is no external fragmentation. 

However, it results in internal fragmentation (the last half of the block is usually unused) and results in slow disk access; larger blocks will improve speed but increase internal fragmentation.

It also creates a nitpick: the block contains both data and a pointer. Pages are typically a power of 2 in size: mapping pages to blocks becomes more difficult and wasteful. Also if one block is corrupted, access to the rest of the file is lost too. 


### File allocation table 
The key issue is the pointer being stored as part of the block. Instead, there could be a file allocation table where links between blocks are stored, and blocks themselves are purely used to store data. 

Linked list pointers are stored in a separate index table.

![Pasted image 20251125122017](../../../Images/Pasted%20image%2020251125122017.png)

The first block of jack.doc is in location 10. In the FAT, it says that in block 10, the next block is 26.

The advantages:
- Block size remains a power of 2
- The index table can be kept in-memory, improving sequential access speeds. The table can be loaded into memory, with all links

Disadvantages:
- The size of the FAT grows proportionally with disk size.
- A 200gb disk with 1kb blocks requires 200mn entries, with 4 bytes per entry, will occupy 800MB. 

This is wasteful: it is more efficient to just load the 1% of files that are actually being used. 

### i-nodes
(index node)

Each file has a small structure on the disk called an i-node, containing attributes and block pointers. An i-node is only loaded when the file is open, though are stored in the system-wide file table.
They are made of:
- direct block pointers (contain a block address of the location where the file's data are stored) and/or 
- indirect block pointers. Don't contain the address of the block of data of a file, it contains the data of a block that contains the data of the file. 

> If every i-node contains n bytes, and k files can be open at any point, n * k bytes of memory are required.

If we have 12 direct blocks, we can can store 4 * 12 = 48kb data.

![Pasted image 20251125122842](../../../Images/Pasted%20image%2020251125122842.png)


Similar to page tables, we can have many levels of indirections

> Stores the addr of block, which stores addr of block, that stores the addr of data belonging to the file.

Meaning, that 256 ^ 2 addresses can be stored = 65k file size 

A triple indirect pointer is:
(12 + 256 + 256^2 + 256^3) * block size = a large number 

Once we know the name of a directory, we have the index, then we can read the i-node which allows us to reconstruct the file. A directory simply contains the filename and i-node pointer. All metadata for the file (type, size, date, owner, block pointers, permission) are stored in the i-node. 

![Pasted image 20251125123551](../../../Images/Pasted%20image%2020251125123551.png)


### Lookup example

![Pasted image 20251125123738](../../../Images/Pasted%20image%2020251125123738.png)

The root i-node will always sit at 0 or 1. This will say that the contents of the directory is stored in block 2. REading the data in block 2, we read the contents  - the mappings. In this, we can work out the i-node representing the file is in block 6. Reading this i-node, /urs data is in block 132. Reading gdm, it says that the inode is in block 26, readin this we see that mbox is in block 60.


### Linking

To share files between directories:

- An inode is an index for an object representing a file.
- A pointer is a name for a memory location where a value is stored.
- If 2 variables have the same pointer, they will have the same value. Therefore, we can also apply this with i-nodes.

#### Hard links
A hard link: 2 directories (Each with their own mapping) that references the same i-node.

A counter in the i-node has a link reference counter: if it reaches 0, the file is no longer in use. 

These are the fastest way to link files. However:

- If the owner of the file deletes it, if the i-node also is deleted, any hard link referencing it will point to an invalid i-node.
- If the i-node gets recycled to point to another file, the hard link will point to the wrong file.
- *The only solution is to delete the file, leaving the i-node intact only if the reference count is larger than 0.* 


#### Soft links
If the file belongs to directory C, we can include a small file where inside it stores the absolute path to the file to link to, instead of the i-node. "read the file, find the path there, and follow the path to the file". This requires a path lookup before accessing the path, whereas the hard link gives the i-node to go to the file immediately. 

These can link (almost) anything in any location. Plus, there are no issues with deleting the original file, and can also reference files across different machines. 

However:
- We must go to find the file that contains the file, open it, read the information, find the path, and go to the path to find the file being looked up. **This requires an extra file lookup and an extra i-node for the link file.**


### Test

![[Pasted image 20251125124612 1.png]]








