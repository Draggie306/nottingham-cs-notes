

A traditional file system does: 
- The i-node is allocated, initialised and written for the file.
	- i-nodes are usually located at the start of the disk
- All the parts belonging to the file (i-nodes, directories, data) are scattered across the file (random access) - so rotational drives will cause reading to be very slow (SSDs lower extent).

Interacting with `/foo/bar`: read the i-node of /foo, then read the data of the directory. Then, read the data of the 

![](../../../Pasted%20image%2020251201151208.png)

Lots of data complexity occurs before data is even read/written



## Log structured filesystem

The old-fashioned: i-nodes point to data blocks and directories. What would be better is that all data, i-nodes and directories are clustered together, reducing seek movement.

Before:
![](../../../Pasted%20image%2020251201151523.png)

After:
![](../../../Pasted%20image%2020251201151539.png)

The solution to this is buffering: if we buffer writing into memory, we can then organise similar data to be in the same place to minimise delays. 

However, processes and files are alike: they come and go. If they are clustered together at a given point in time, and files go, then we still end up with holes left throughout the disk.

The solution is to have a writer and cleaner thread at different ends of the filesystem. 

Before:
![](../../../Pasted%20image%2020251201151837.png)

After:

![](../../../Pasted%20image%2020251201151859.png)

This greatly increases disk performance, but the cleaner thread needs overhead CPU time. Writes are more robust, as multiple are performed as a single operation (multiple small writes are more likely to cause inconsistencies).

### Log structured filesystems on SSDs

As SSDs suffer from write amplification (entire block must be erased to update a single page’s data). 

> In practice, it is not uncommon for a block to have 1024 pages. 

Instead of writing in the same location, the page can be marked as dirty - as the user is probably using the device, defer this expensive operation for later.

When the user is not waiting, the cleaner thread can take the remaining pages in the block and append them to the end of the log. 

The log-structured FS is typically implemented in the controller. The controller does this in the background. Once at the end of the drive, the log structure wraps around to the start. This prevents wear levelling.

#### Challenges and solutions
The inode points to the block. If the controller changes the blocks underneath without changing the i-node, it begins scrambling metadata and inodes.

The solution to this is to have a logical address space in the filesystem that is mapped onto the physical address space. 

This is not difficult: somewhere on the drive there is a mapping table, that will be inspected to be mapped to the correct physical address. It may begin by every logical address has the same physical address location, but it may eventually look like this:

![](../../../Pasted%20image%2020251201152648.png)


## Journalling file system

We can simplify traversing file systems, i-nodes and directories by using a journalling file system.

We usually have to:
- Remove the file’s entry in the dir
- Add the file’s i-node to the pool of free i-node
- Add the file data blocks to the free list

If there is a crash anywhere here, we can lose references to i-nodes, data blocks and have inaccessible blocks. 

A journalling FS logs all events before they take place. The general concept is thus:
![](../../../Pasted%20image%2020251201153112.png)


## Virtual file systems

A data object has a name associated: it can be stored as CSV or XML. We can use an interface that contains all the access methods needed for the filesystem.

> **An interface is a contract: any class that implements it, provides the code that implements the functionality.** 

This interface uses the data access object pattern.

The posix interface is used by Unix and Linux to unify different file systems. Every file system will provide its specification of the functions.

Each file system will implement a function that includes the address for different functions, that has an implementation for the system calls contained in the interface. These implementations can be for remote filesystems.

Every file system is registered with the VFS.

![](../../../Pasted%20image%2020251201154232.png)


