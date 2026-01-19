
> Some of these notes were written outside of a lecture environment in the Gonville & Caius College JCR

### Recap

The way devices work creates an array of challenges: 
- delays, caused by seek time, rotational latency and transfer times (on rotational HDDs)
- block erasing on write (and causing write amplification) on SSDs

Therefore, the OS has to manage the performance by using disk scheduling algorithms (reordering operations to make them faster) such as: First Come, First Served; Shortest Seek Time First; and SCAN.  
Cylinder skew: an offset to make sure that the time it takes for the R/W head to move, the desired bits are under the head immediately.

## The OS
The OS abstracts the file system away from the device - this gives a uniform and less complex view of the underlying storage mechanism. The logical file system is mapped onto the physical one.  

It also provides decisions for concurrency - multiple processes accessing the file simultaneously (already open), and security (permissions for reading/writing/executing files - can’t edit OS files). At a lower level, there are lots of abstractions that have to be dealt with.

### Low-level implementations 

There are two types: 
- Shared layers
	- The I/O controller interacts with the device controller (drivers and interrupt handlers) - “go and change the registers of the controller where the file is”
	- The basic file system instructs device drivers in blocks and schedules I/O and manages buffers and caches for data and metadata. 
- File system-specific layers
	- **File organisation:** A bitmap or linked list can be used to model logical blocks for files and free space - ”which blocks make up different files”
	- The logical filesystem manages metadata, directory structures and access protections.  
Applications define the structure of their files.

![](Pasted%20image%2020251124151145.png)



## Disk layout

In some cases there may not be a 1:1 mapping between the logical and physical file system.

At the start of the drive, the **master boot record** is located. It is used by the BIOS to read the boot sector. It has a partition table at its end, with one partition listed as active that contains a **boot block to load the OS.**

The drive is split into multiple partitions. 


### Partitions

Each partition has:
- space reserved for a boot block (although it may not have an OS).
- A super block (master file table) - stats about the partition (size, file number, block side)
- Free space management: 
- Metadata - extra data blocks that contain 
- Data blocks 


### Boot process

- BIOS loads the MBR from the first physical drive
- MBR code reads partition table on the same drive as the MBR
- MBR looks for a **primary partition** marked as **active**
- MBR loads the boot block (program) from the active primary partition
- The boot block loads the rest of the OS starter files


### Directories
Are just special files that group files together. Their structure is defined by the filesystem. A bit is set to indicate that they are directories.

- In NTFS, all attributes are stored in the directory file (file names, disk address).
	- Reduces inefficiencies by not having to seek/read other data. 
- In Unix, the directory contains a pointer to the data structure that contains the file attributes.
	- Keeps directories to the absolute minimum
	- Index to the meta block (an **i-node**) that contains all info about the file (access rights, all parts belonging to it)


Rather than manually manipulating the bits and data associated with directories, we can manipulate them with standard library calls (which then use system calls) for the OS to act on the behalf of the user:
- create/delete
- opendir/closedir
- readdir
- rename, unlink, link, list, update

### Files

Both Windows and Unix have regular files and directories.
- Regular files contain user data in ASCII/binary format
- Directories group them together

Unix also has character and block special files:
- Character special files model serial I/O devices like keyboards and printers

Block special files are used to model e.g. hard drives

When a file is read, its meta block is brought into memory, stored as a file control table. There are both a system-wide and process-specific table. 
- The system-wide table contains generic information: when it was last access, its 
- Process-specific: reading a file, at what point in the file are we currently using (read/write pointer). The file contro
- The file control block are kernel structures, kept in a per-process and system-wide open file table array indirectly indexed through the process file table using a file handle. 

The per-process filetable contains process-specific information:
- the processes currently open files
- reference to the relevant entry in the system-wide file table 
- TODO: this

## File access

Reading `/home/pszgd/COMP2007/helloWorld.txt`:
Recursively read the metadata for the directory, starting from `/`. For each, read the data block for that directory.

Once the metadata for the directory contains `helloWorld.txt`, read the metadata location for it. Then, update the per-process and system filetables. Then, read the data and close the file. Finally, update the per-process and system file tables. 

Retreiving a file comes down to searching a directory file as fast as possible. A simple random order of directory entries is probably inefficient, so indexes/hash tables are used for large directories. 

**However, we still are missing: how blocks are linked to files, and what file control blocks contain.**

![](Pasted%20image%2020251124154734.png)









