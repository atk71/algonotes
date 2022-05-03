Operating Systems 
CSDS 338
Spring 2022
[INSTRUCTOR BIO INFO](http://23.254.128.42/oldweb/loui.html)
Case Western Reserve University

## Getting Started
#### Operating System
- serves as an interface between a user and a device.

#### Responsibilities of an OS:
- program management
- file management
- communicate between user and device drivers (I/O)
- error handling
- resource management
- system security and integrity

#### Kernel
- core of the operating system.

#### Shell
- a utility to process user requests
 
#### C (Program)
- each program begins inside a function called "main"
- a function is a series of commands

#### Unix
- data is organized into files
- files are organized into directories
- directories are organized into a filesystem
- a filesystem is a tree-like structure.

#### Process
Programs, when loaded to memory and become a process, gets divided into four sections:
1. Stack: 
	- contains temporary data 
	- store local variables
	- pass arguments to functions along with retreiving instructions at the end of a function call.
2. Heap: dynamically allocated memory for a process during run-time
3. Text: 
	- includes current activity represented by Program Counter as well as the contents of the processor's registers.
	- contains machine code of compiled programs.
	- sharable, so frequently executed programs can share the same copy.
4. Data: contains global and static variables
	1. Read-Only Area
	2. Read-Write Area


## Kernels and Processes
#### Monolithic vs Microkernels
- Microkernels:
	- implements drivers as user-space programs and core features in the kernel
	- more secure, maintainable, and modular
	- but harder to architect properly and may have performance overheads
	- suited for low memory (<= 512k RAM) or real-time OSes
		- airline flight systems
		- nuclear reactor control systems
- Monolithic Kernels:
	- implements drivers as part of the kernel
	- faster than microkernels
	- but less modular, and harder to secure
- kernel architecture should be determined by the end goal

#### Spaces
- Segregated memory spaces ensure kernel processes (in kernel space) are not interfered with by normal programs (in user space).

#### Processes
- represent running operations created by the kernel or the user.
- have an owner and are identified by a process ID (PID).
- need resources (CPU time, memory).
- can be started, stopped, interrupted, or killed.

#### Sending signals to a process
- SIGSTOP: stops process execution without terminating
- SIGCONT: instructs a stopped process to continue
- SIGINT: interrupts a running process
- SIGHUP: the signal sent when a terminal is terminated
- SIGKILL: forcefully terminate a process. Immune by init or systemd only.

#### Fork()
- a clone operations.
- takes current process as input (known as the parent process).
- outputs a cloned process with a new PID (known as the child process).
- forking clones the parent's stack, heap, as well as the file descriptors.
- fork(), wait(), and exec() are often lumped together.

#### Processes vs Threads
- a process is an instance of a program
- a process can spawn child processes and threads
	- threads live inside processes and share the same memory spaces
		- pthread_create(): a new task is created that shares the parent's file descriptors, PIDs, and memory spaces.
	- child processes are independent clones of its parent with separate memory spaces
- a process is independent and isolated from other processes  
- forking processes are expensive in resource requirements:
	- I/O bound: 
		- use threads and concurrency
		- for small tasks
	- CPU bound: 
		- use processes and parallelism
		- execution of applications

#### Scheduler
- limited resources on a systems require effective resource management
- a scheduler decides the next running process from a list of runnables
- a runnable process sits ready for execution

Priority in Linux:
- 140 priorities
- 2 distinct priority ranges
	- Niceness: -20 (highest) to 19 (lowest), default: 0
		- negative values increase importance
	- Real-time: default: 1-99, user-space: 100-139
-  a high priority rank corresponds to low priority

#### Switching tasks
- Preemption: a means for the OS to change running processes.
- Context switching: the OS switches between tasks, allowing each task some runtime to execute.
- NOTE: Think of coaches switching players to avoid exhaustion.

#### Scheduling Algorithms
- FIFO/FCFS: First In, First Out
- SJF: Shortest Job First
- Shortest Completion Time First
- EDF: Earliest Deadline First, if deadline are known
- Shortest Burst First, if bursts can be estimated before i/o
- Rate Monotonic, wake up more = run more
- Round Robin: 
	- for earlier versions of Linux kernels
	- simple and fast implementations using a circular queue
- CFS: Completely Fair Scheduler
	- vruntime: track process' runtime on processor
		- weighed by priority, normalized by load on machine
	- processes with less runtime are given higher priority to the processor
- SMP and NUMA: 
	- Symmetric MultiProcessing
		- two or more processing units share the same memory
		- one schedule() and one load balancing that manages multitasking across multiple cores
	- Non-Uniform Memory Access
		- non-uniform: local memory is accessed faster than shared memory
		- architecture scales better for higher CPU numbers than SMP

#### Parallelism
Applicable when at least two or more programs are running simultaneously. Parallel programming uses parallel hardware (ex: multi-core processors) to accelerate execution. This is acheived by splitting a big task into multiple, smaller tasks, which can be executed simultaneously.

#### Concurrency
Applicable when at least two tasks start, run, and complete in overlapping time. Multiple threads running concurrently on a single core involve frequent context switching.
- execution of multiple instructions at the same time
- occurs in an OS when multiple process threads are concurrently executed
- threads can interact with each other via shared memory or message passing
- Tough to predict speed of execution due to
	- how the OS handles interrupts
	- other processes' activities
	- the OS' scheduling policies

Possible inefficiencies when OS attempts to lock and/or control resources:
1. Non-atomic:
	- non-atomic operations depend on other processes
	- atomic operations are independent of other processes
2. Deadlock: 
	- processes block each other during resource acquisition
	- no process makes progress as each waits on the resource assigned to another
3. Blocking: 
	- processes may block the waiting queue for resources 
	- may block for a long time if dependent on external input
	- very undesirable in cases of processes that need to be called periodically
4. Race Conditions:
	- occurs when a process' output is determined by the timing/sequencing of other uncontrolled events.
	- also possible in multithreaded software, in a distributed environment, or is interdependent on shared resources
5. Starvation:
	- a process is continuously denied resources to complete work
	- possible causes:
		- scheduling errors
		- mutual exclusion algorithm
		- resource leaks

#### File Locking
- A mutual-exclusion mechanism to ensure safe read/writes of files by multiple processes.
- Advisory locking:
	- not enforced
	- works only if participating processes cooperate by explicitly acquiring locks
- Mandatory locking:
	- enforced by the OS
	- doesn't require any cooperation from participating processes

#### Shared Memory
- memory segment shared between two or more processes
- Each process has its own address space
- Inter Process Communication (IPC) makes communication between processes possible 
- shared memory is fast
	- once the memory is mapped, processes do not execute system calls
- writing to shared memory:
	1. ftok: converts a pathname and project identifier to a System V IPC key
	2. shmget: allocates a shared memory segment
	3. shmat: attach shared memory segment identified by *shmid* to the address space of calling process

#### Thread Mutex Locking
- pthread_mutex

#### Message Passing Model of Process Communication
- allows multiple, (in)dependent processes to read/write data to a message queue
- messages stored on queue until retrieved 
- Advantages:
	- easier to implement than shared memory model
	- easier to build parallel hardware as it is tolerant of higher communication latencies
- Disadvantages:
	- slowed communication due to connection setup time
- pipe() functions are a unidirectional alternative

#### Message Passing Example
- Asynchronous sender:
	- not interested in whether the message is accepted or not
	- will send message and move on, hence, no blocking
	- unreliable
- Synchronous sender:
	- will wait until message is delivered and accepted 
	- will block as the sender and receiver creates a rendezvous point and run in sync
	- reliable

#### Necessary Conditions for Deadlock
- The following four conditions must hold simultaneously:
	1. Mutual Exclusion: 
		- at least one resource must be held by a process in a non-shareable mode.
		- other processes must wait until the resource has been freed
	2. Hold and Wait:
		- a process must hold one resource while requesting additional resources currently held by other processes
	3. No (resource allocation) Preemption:
		- resources cannot be released by force
		- a process must voluntarily release the hold on a resource
	4. Circular Wait: 
		- for a set of processes, p_0, p_1, ... , p_n, 
		- p_0 waits for a resource held by p_1
		- p_n waits for a resource held by p_0

#### Livelock
- similar to a deadlock but the states of processes are constantly in flux
- processes are interdependent and are unable to finish their tasks
- Dining Philosophers Problem:
	- may result in a deadlock or a livelock, depending on the setup

#### Peterson's Algorithm
- Achieves mutual exclusion between two threads
- Guarantees that only one thread is in the critical section
- Shared (memory) variables in Peterson’s algorithm: 
	-  int turn 
	-  boolean flag[2]
- However, the algorithm works sometimes when the multiprocessor has strongly ordered memory
- Better to rely on hardware-provided mutual exclusion mechanisms.

#### Semaphore
- a counting semaphore, maintains a set of permits
- acquire() blocks, if necessary, until a permit is received
- release() adds a permit, potentially releasing a blocking acquirer
- no actual permits issued, the semaphore merely acts on the available count
- often used to restrict the number of threads accessing some physical or logical resource

#### Atomicity vs Thread-Safety
- Atomicity refers to an operation's *all-or-nothing* quality
	- if 100% of the task is not possible, no action is taken
- Thread-safety refers to a set of properties, including atomicity, that allows an operation to perform without impeding on the performance of other operations.
	- for example, a process accessible by separate threads, where the access by one thread does not interfere with the operations of another

## Memory
#### Some Examples of Memory
- NUMA: Non-Uniform Memory Access
	- large systems have CPU nodes close together and spread far apart
- NVMe: Non-Volatile Memory express
	- flash memory used as main memory
- zRAM: compressed RAM
	- traditional main memory but compressed to save space
- Deep Archive Storage (Usually compressed)
- Offline Storage (Backup drives, maybe even tapes)

#### Paging and Segmentation
- Paging: a memory management strategy that presents storage locations as virtual addresses of fixed sizes
	- a page table is used to look up the physical location of a process' virtual address
		- MMU: Memory Management Unit
		- TLB: Translation Lookaside Buffer
		- Hash Tables
- Segmentation: a strategy that allows varying sizes of address spaces called segments
- Segment: 
	- alternative to pages
	- odd/custom sizes
	- need the base and length to define a segment
- Page: 
	- a fixed-length contiguous block of virtual memory residing in the process map or address space
	- mapped to physical frames
- Frame: 
	- a fixed-length contiguous block located in RAM; sizing identical to pages
	- mapped to physical memory
- Lot more available Virtual Addresses (Pages or Segments) to Physical Addresses (Frames)
- Fragmentation
	- Internal: occurs when partial page/frame size is used
	- External: occurs when gaps remain after the deallocation/freeing of segments
- In summary, the main memory is divided into:
	- a linear combination of pages and frames 
	- and any number of segments of varying number of pages
	- why all memory maps have addresses ending in 000s 
		- multiples of 4096 page size
	- contiguous segments in virtual memory need not be contiguous when mapped to physical memory
- Decode the mapping in Linux: 
	- [Link 1](https://stackoverflow.com/questions/17021214/how-to-decode-proc-pid-pagemap-entries-in-linux) 
	- [Link 2](https://stackoverflow.com/questions/5748492/is-there-any-api-for-determining-the-physical-address-from-virtual-address-in-li/45128487#45128487)
	- To get physical address in memory, given:
		- PID
		- Virtual Address in process memory map
	- The results may be:
		- an address, but no physical frame
		- an address, a physical frame, but no values
		- an address, a physical frame, and a value

#### malloc()
- a function to dynamically allocate memory (contiguous on the heap)
- ways of allocating memory:
	- first fit: 
		- allocator keeps a list of free blocks (free list)
		- returns first free block that satisfies an incoming request for memory
		- for significantly large blocks, the remainder or *spare change* is returned to the free list as another block
		- performance is reasonably well, as allocations are quick
		- recycling and ordering free blocks:
			- memory location (address)
				- not fast
				- supports efficient merging of adjacent free blocks (coalescence)
				- reduces fragmentation
				- improved locality of reference
			- increasing size
				- equivalent to best fit algorithm
				- free blocks with the *tightest fit* always chosen
				- remainders are unusably small
			- decreasing size
				- equivalent to worst fit algorithm
				- first block on list is always large enough
				- encourages external fragmentation
				- but fast allocations
			- increasing time since last use
				- very fast at adding new free blocks
				- encourages good locality of reference
				- but may cause serious external fragmentation

#### Buddy System
- allocator will only allocate blocks of certain sizes
- has many free lists, one for each permitted size
- permitted sizes, usually in powers of two.
- requests for memory are rounded to a permitted size and the first block on that size's free list is returned
- if a particular free list is empty, the next size up is broken down to meet the request
- coalescence is attempted during block recycling
- Performance:
	- both internal and external fragmentation, but not serious
	- fast allocation and coalescence

#### Two-Level Segregator Fit (TLSF)
- Buddy plus leftovers
- best/worst fit found faster
- provides an implementation of malloc/realloc/free/etc with the following properties:
	- O(1) performance
	- works on user-supplied block of memory instead of a global heap
	- efficient both in terms of memory overhead and processor time
	- low fragmentation
	- For thready-safety, TLSF calls are wrapped in irc_disable()/irq_restore()
- a general purpose dynamic memory allocator specifically designed to meet real-time requirements:
	- Bounded Response Time: 
		- worst-case execution time (WCET) of memory allocation and deallocation must be known in advance and independent of application data
	- Fast:
		- TLSF executes a maximum of 168 processor instructions in an x86 architecture (slightly lower or higher, depending on compiler version and optimization flags)
	- Efficient Memory Usage:
		- fragmentation can have significant impacts
		- TLSF has been rigorously tested to show an average fragmentation below 15% and a maximum fragmentation below 25%.
- included in many Linux distros and applications

#### Choosing memory allocation algorithms
- no one-size-fits-all algorithm
- choose based on performance bottlenecks
	- real-time applications may accept higher average execution times if guarantees are made on a maximum number of processor cycles
	- consider reducing the number of allocations instead of opting for a different algorithm
- Other considerations
	- lot of small allocations or few large allocations
	- sudden spikes in allocation requests or evenly spread out over time
	- lifetime of allocations
- standard allocators must support multi-threading

#### Overview of Linux Memory Management Concepts
###### Slabs
- a set of one or more contiguous pages of memory for an individual cache
- this memory is subdivided into equal segments with the same size as the object type being cached 
- memory allocated by a slab allocator
	- a module or driver may request a private cache of a *specific object type*
	- allocator dynamically resizes each cache as needed

###### HugePages
- CPU allocates RAM in chunks (named pages) of 4Kb for efficiency
- more pages, more time and space to locate each page
- To enable the system to manage large amounts of memory:
	- increase the number of page table entries in the hardware memory management unit
	- increase the page size
- each Page Table Entry consumes memory
	- modern CPU architectures reduce this overhead by supporting bigger pages
		- Huge Pages (Linux)
		- Super Pages (BSD)
		- Large Pages (Windows)
- since the TLB holds limited entries, it is advantageous to have each entry correspond to a larger chunk of memory.

#### Virtual Memory
- area of secondary memory storage space (hard disk or SSD)
	- acts as if it was part of RAM or primary memory
	- developed when physical RAM was an expensive resource
- as RAM becomes full, inactive data gets temporarily moved to virtual memory
	- tables updated to map virtual address to physical location
- swapping data between RAM and virtual memory enables smoother system workflow
	- but RAM is magnitudes faster than virtual memory
	- running threads and manipulating data only occurs in RAM
	- Thrashing: 
		- when the RAM to virtual memory ratio is too small, frequent swaps hinder workflow
		- to prevent thrashing, reduce multitasking or increase RAM capacity
- preferable to use the fastest secondary storage device to host virtual memory
 
#### Paging
###### Demand Paging
- pages should not be loaded, until required
	- store pages in secondary memory, until demanded.
	- lazy swapper
 
###### Pre-Paging
- OS pre-loads pages into memory by guessing in advance 
- Working Set Model:
	- a list of pages maintained with each process in its working set
	- a working set is not lost in case a process is suspended
	- entire working set is brought to memory before a process resumes again
- Advantages: may save time by pre-fetching relevant data
	- possible when aided by a good locality of reference
		- high probability of the next needed page being close
	- implementation depends on its rewards vs cost of fixing page faults
- Disadvantages: preloaded pages may never be used
	- considerable wastage of resources

###### Process Selection
During out of memory failure:
- out_of_memory() is called
	- select_bad_process() with a badness() function is used:
		- most *bad* process is sacrificed
		- Heuristic for the badness function:
			- kernel needs to retain a minimum amount of memory
			- reclaim a large amount of memory
			- processes with small memory footprints are low priority
			- kill the least amount of processes
			- means to elevate and kill user specified processes

###### Page Replacement Algorithms
Similar to cache replacement policies
- Optimal: swaps pages that will occur farthest in the future
- NRU: Not recently used
	- picks a random page from the lowest category for replacement
		3. referenced, modified
		2. referenced, not modified
		1. not referenced, modified
		0. not referenced, not modified
- FIFO
- Random
- LRU: Least recently used
- NFU: Not frequently used 
- LDF: Longest distance first
- Second Chance: similar to clock
	- FIFO with ref bit and Re-Q
- Clock:
	- FIFO with Ref bit and Circ-Q
	- maintain a circular list of pages resident in memory
	- "clock hand" sweeps over pages looking for unused page
		- replace pages inactive for one cycle

Performance of Page replacement algorithms are affected by:
- size of primary storage
	- algorithms that periodically check all memory frames are impractical for large sizes
- taller memory heirarchies
	- CPU cache misses are expensive
- Weakened locality of reference
	- attributed to OOP techniques favoring 
		- large numbers of small functions 
		- data structures like trees and hash tables with chaotic memory reference patterns
		- garbage collection has changed applications' memory access patterns

 Precleaning:
- mechanism that starts I/O on dirty pages with high probability of replacement
- assumes that it is possible to identify pages to be replaced
- can waste resources if cleaned pages get dirty before replacement

Replacement Scope
- Local
	- each process can handle faults independently
	- scalable and more consistent performance
- Global scope is more efficient overall

###### Copy on Write
- virtual memory marked without allocating physical memory
- a physical page allocated only on actual write-time
###### Swapping
- swapping can be a slow process
- still better than a crashing system or killing processes
- swappiness
	- determines the aggressiveness of the kernel preemptiveley swapping pages
- accessing a page not currently in memory raises a page fault
	- major page fault requires accessing disk
	- minor page fault can be fixed by sharing pages already in memory

###### Page table vs Inverted page table
- reduced space complexity
- a hash map
- fits in DRAM since it is proportional in size to DRAM
- each entry in hash table stores both a virtual and physical address
	- virtual address checks for hash conflicts
- only one entry per physical page guarantees total number of entries
- IPTs destroy spatial locality of reference by scattering entries

Heirarchical Page Tables
- space optimization of multi-level page tables
- some data stored at higher levels, pointers to less frequently accessed data
- similar to huffman coding and multi-byte code pages for non-european charsets

###### Cache vs Translation Lookaside Buffer (TLB)
Cache
- a collection of duplicated data
	- used when the cost reading data from cache is cheaper than the original location
- operates as a temporary storage for frequently accessed data for convenience
- buffered memory access
TLB
- is a CPU cache for the MMU to improve virtual address translation speed
- has a fixed number of slots containing page table entries
	- each entry maps a virtual address to a physical address

###### RAM Disk for Windows
- disk stored entirely in its memory
	- faster than physical hard disks
		- boost computer performance
	- temporary data on fast in-memory disk achieves higher performance
		- less junk
		- reduced file system fragmentation
- RAM disk extends physical disk lifespan
	- spares excessive read/writes
		- less noise and heat from hardware
	- reduced wear-and-tear on disk
- unused RAM as a high-performance alternative to slower HDD storage

###### Memory Compression Process
- High memory and CPU usage in Windows 10 and 11
	- memory compression feature optimizes physical RAM consumption by compressing some pages
	- process memory compression allows more processes to be retained in physical memory
	- data retrieval from RAM is faster even with compression/decompression overheads
	- overall benefits
		- Reduced RAM usage, I/O operations, and SSD resources


## Files and I/O
###### Inodes
- index node
- a specific piece of metadata on a given filesystem
	- metadata describes aspects of a file
		- like file checksums for error detection/correction
	- each filesystem has its own set of inodes
		- inode numbers may be reused but never by the same filesystem

###### Unix/Linux files and filesystems
- everything is an inode
- everything is a file
	- a directory is just a special file
	- an object with a path and a name
		- a name is just a string of text representing a property of an object
		- the object in reference is the inode
		- a directory is an inode containing files with their own inodes
- some Unix distros allow file access via inodes
	- circumvents permissions and access checks
	- not implemented in Linux, must traverse a filesystem tree instead
- sockets and pipes are anonymous files without a filename on disk
- filesystems implement a directory tree
	- ext3 and ext4 use HTree
	- xfs uses B+ Tree
	- zfs uses Hash (Merkle) Tree 
- Soft vs Hard Link
	- soft link is a naming alias
	- hard link is an inode alias
- inodes can be renamed but files cannot be re-inoded (must be copied)
	- links provide multiple names for single file
		- updating file updates all links
	- copies are independent and indentical sets of data
		- updating a file does not update other copies

###### Journaling File System
Each OS has its own particular file system
- NTFS for Windows
- APFS for MacOS
- Ext4 for most Linux distros

Journaling
- from the analogy of a diary
- keeps track of uncommitted changes
	- stored chronologically
	- a data structure known as a "journal", usually a circular log
	- in case of a system crash or power failure, journaling enables faster reboots with less chance for data corruption
- depending on actual implementation, a journaling file system may
	- only keep track of stored metadata
		- improved performance but prone to data corruption
	- track both stored data and related metadata
- updating file systems with changes to files and directories requires multiple read/write operations
	- interuptions between writes can render the structure in an invalid state
	- under journaling, recovery involves
		- reading the journal from the file system
		- replaying changes until the file system is consistent
- not perfect but helpful to maintain some consistency 
	- garbage can be preserved or updates lost
	- but saves time at reboot with lower probability of data loss

Physical Journals
- logs an advanced copy of every block that will be written to the main file system later
- the write can be replayed to completion in case of a system failure
- every changed block is committed twice to storage
- useful in cases where absolute fault protection is required

Logical Journals
- logs only changes to file metadata
- trades fault tolerance for better write performance
- allows unjournaled file data and journaled metadata to be out of sync

Log-Structured File Systems
- write-twice policy does not apply
	- the journal is the file system

Copy-on-Write File Systems
- avoid in-place changes to file data by writing changes to new allocations
- updates metadata that points to new allocation and discards the old link

RAID: Redundant Array of Inexpensive/Independent Disks
- combines multiple physical disks into one or more logical units
- RAID Levels:
	- RAID 0 - striping, no mirroring or parity
	- RAID 1 - data mirroring, no parity or striping
	- RAID 2 - bit-level striping with dedicated parity
	- RAID 3 - byte-level striping with dedicated parity
	- RAID 4 - block-level striping with dedicated parity
	- RAID 5 - block-level striping with distributed parity
	- RAID 6 - block-level striping with double distributed parity
	- RAID 60 = RAID 6+0

Triple Modular Redundancy
- a majority voting system producing a single output
- if one system fails, the other two can correct and mask the fault

###### Devices
- Character Device 
	- the driver communicates by sending and receiving single characters (bytes, octets)
	- no buffering is performed
	- not required to be random access
	- any device can be a character device
	- Ex: serial and parallel ports, sounds cards
- Block Devices
	- the driver communicates by sending entire blocks of data
	- accessed through a cache
	- must be random access
	- can contain addressable, reusable data
		- filesystems can only be mounted on block devices
	- Ex: hard disks, USB webcams
- Raw Devices
	- transfer data directly to and from the disk

## Platforms
###### Hypervisor
- A hypervisor abstracts hardware to run an OS.
	- type 1: lightweight OS on bare-metal
	- type 2: software layer on an existing OS
		- slower than type 1 and bare-metal machines
- virtual machine monitor (VMM)
	- creates and runs virtual machines
- allows one host to support multiple guest VMs 
	- shared resources such as memory and processing
	- *noisy neighbor* effect
		- a VM with a large workload may interfere with other VMs
	- security risk
	- cloud computing -> accessibility, scalability, higher ROI
	- outsources security, maintenance, sysadmin roles

###### Container
- a container abstracts an OS in order to run applications and their dependencies. 
	- more like config files to run an individual application
- more lightweight and portable than VMs
	- only requires a container engine like Docker

## Security
#### A Select List of Security Weaknesses
###### sourced from  the Common Weakness Enumeration website
- CWE-22: Improper Limitation of a Pathname to a Restricted Directory ('Path Traversal')
	- attackers may access files and directories outside restricted section
- CWE-119: Improper Restriction of Operations within the Bounds of a Memory Buffer
	- read/writes occuring outside the intended boundary may lead to data leaks and/or corruption
- CWE-120: Buffer Copy without Checking Size of Input ('Classic Buffer Overflow')
	- buffer overflows may lead to systems crashing
- CWE-121: Stack-based Buffer Overflow
	- buffer overflows on stack may cause arbitrary codes to execute
- CWE-122: Heap-based Buffer Overflow
	- usually results from routines like malloc()
- CWE-123: Write-what-where Condition
	- more arbitrary code execution exploits if determined
- CWE-170: Improper Null Termination
	- non-termination or incorrect termination of a string or array
		- a null terminator out of bounds by one count
		- incorrect usage of strncpy()
- CWE-191: Integer Underflow (Wrap or Wraparound)
	- subtractions that result in a value less than the minimum integer value allowed
- CWE-250: Execution with Unnecessary Privileges
	- execution of operations at higher privilege levels undermine system security
- CWE-252: Unchecked Return Value
	- exploits two common programmer assumptions
		- this function call can never fail
		- it doesn't matter if this function call fails
- CWE-269: Improper Privilege Management
	- rogue agents may misuse access privileges
- CWE-362: Concurrent Execution using Shared Resource with Improper Synchronization ('Race Condition')
	- an attacker may interfere in a race condition situation and deploy malicious codes
- CWE-416: Use After Free
	- referencing freed memory with harmful consequences
- CWE-426: Untrusted Search Path
	- may allow attackers to execute programs, access and modify data files and configurations
	- attackers may reroute system's path variable to malicious programs
- CWE-457: Use of Uninitialized Variable
	- control or read junk data before initialization
- CWE-476: NULL Pointer Dereference
	- may cause crashes and exits
- CWE-590: Free of Memory not on the Heap
	- calling free() on an invalid pointer may corrupt memory management data structures
- CWE-672: Operation on a Resource after Expiration or Release
	- expired, released, or revoked resources are accessed with unintended consequences
- CWE-732: Incorrect Permission Assignment for Critical Resource
	- resources may become available to unintended actors
- CWE-761: Free of Pointer not at Start of Buffer
	- vulnerability arises from free() not functioning as intended
- CWE-772: Missing Release of Resource after Effective Lifetime
	- possibility of denial of service attacks by exhausting available resources