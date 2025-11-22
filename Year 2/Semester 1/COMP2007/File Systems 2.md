### Recap

The way devices work creates an array of challenges: 
- delays, caused by seek time, rotational latency and transfer times (on rotational HDDs)
- block erasing on write (and causing write amplification) on SSDs

Therefore, the OS has to manage the performance by using disk scheduling algorithms, such as: First Come, First Served; Shortest Seek Time First; and SCAN. 


## The OS
The OS abstracts the file system away from the device - this gives a uniform and less complex view of the underlying storage mechanism. The logical file system is mapped onto the physical one.  

It also provides decisions for concurrency - multiple processes accessing the file simultaneously, and security (permissions for reading/writing/executing files). 

### Low-level implementations 

- The I/O controller interacts with the device controller (drivers and interrupt handlers).
- The basic file system instructs device drivers in blocks and schedules I/O and manages buffers and caches for data and metadata. 

The filesystem has specific layers depending on the implementation. 
- A bitmap or linked list can be used to model logical blocks for files and free space. The logical filesystem 













