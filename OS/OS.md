|Operating System|Kernel|
| :---: | :---: |	
| Interface between user and computer.| Interface between application and user program.|
| System operations and security.| Provides all the different managements.|
| Computer need Operating System to run.| Operating System needs Kernel to run.|

### KERNEL
A kernel is that part of the operating system which interacts directly with 
the hardware and performs the most crucial tasks.
	a. Heart of OS/Core component.
	b. Very first part of OS to load on start-up.
	c. The term **``KERNEL-SPACE``** is used to describe the area in memory reserved for the kernel. It's more accurate to say that the kernel operates in a privileged mode with access to the entire address space, while user processes operate in a restricted user mode.

#### Types of Kernel
##### 1. Monolithic Kernel
	a. All functions are in the kernel itself, hence fast.
	b. Bulky in size.
	c. Memory required to run is high.
	d. Less reliable, one module crashes -> the whole kernel is down. Modern monolithic kernels often have mechanisms in place to isolate and recover from failures in specific modules without bringing down the entire system.
	e. High performance as communication is fast. (Less mode switching)
	f. Single large process running entirely in a single address space.
			Eg. Linux, Unix, MS-DOS.

##### 2. Micro Kernel
	- Only major functions are in kernel.
		- i. Memory management.
		- ii. Process management.
	- File management and I/O management are in User-space.
	- Smaller in size.
	- More reliable.
	- More stable.
	- Performance is slow.
	- Overhead switching between user mode and kernel mode.
		- Eg. L4 Linux, Symbian OS, MINIX, etc.

##### 3. Hybrid Kernel
	- Combined approach, hence advantages of both kernels. File management in Users-pace and rest in Kernel space. Hybrid kernels typically have certain components, including parts of the file system, running in user space for modularity and stability, but critical components remain in the kernel space.
	- Speed and design of monolithic.
	- Modularity and stability of micro-kernel.
	- IPC (Inter-Process Communication) happens but has lesser overheads.
		- Eg. MacOS, Windows NT/7/10
		
##### 4. Nano Kernel				
##### 5. Exo Kernel

---

### API
- Acts as a link between OS and process, allowing user-level programs to request OS services.
-  They are function definitions that specify how to obtain a specific service. 
-  Delivers user response to system and vice versa. System calls are made via APIs.
-  Can be found in ``glibc`` (GNU C Library) packages in LINUX.

### SYSTEM-CALLS
- A mechanism using which a user program can request a service from the kernel for which it does not have the permission to perform. 
-  They are implemented in C.
-  System Calls are the only way through which a process can go into kernel mode from the user mode.
-  When system call is made, CPU switches to Kernel mode & calls ``SYSTEM CALL HANDLER``.
-  Call Handler uses system call number to call relevant ``SYSTEM CALL SERVICE ROUTINE``.

---

#### How system boots up?
1. PC or system is turned ON.
2. CPU initializes itself, and looks for a firmware program (BIOS) stored in the BIOS Chip.
	-  BIOS chip is a ROM chip found on mother board.
	-  In modern PCs, CPU loads ``UEFI`` (Unified Extensible Firmware Interface).
3. CPU runs the BIOS, which tests and initializes system hardware.
	- BIOS loads the configuration settings.
	- BIOS runs Power On Self Tests (``POST``) process.
4. BIOS handoff responsibility for booting the PC to the OS’s boot-loader.
	- BIOS first reads boot-able sequence from ``CMOS`` battery powered chip.
		 -  ``CMOS`` (Complementary Metal Oxide Semiconductor) lies in the CPU that runs clock, BIOS settings etc.
	- ``BIOS`` looks at the ``MBR`` (Master Boot Record), a special boot sector at the beginning of a disk. The MBR contains code that loads the rest of the operating system, known as a ``bootloader``.
	- The ``BIOS`` or ``UEFI`` examines a storage device on the system to look for a small program, either in the ``MBR`` or on an ``EFI`` 		  system partition, and runs it.
5. The boot loader is a small program that has the large task of booting the 
   rest of the OS.
	-  Windows uses a boot loader named Windows Boot Manager (``Bootmgr.exe``)
	-  Linux systems use ``GRUB`` (Grand Unified Boot loader) or ``LILO`` (Linux Loader).
	-  MacOS use something called ``boot.efi``.
	
---

### 32 bits v/s 64 bit OS
|32 Bit|64-Bit|
|:---:|:---:|
|32-bit OS has 32-bit sized registers, it can  access (2^32) unique memory addresses. i.e.,4 GB of physical memory.|64-bit OS has 64-bit sized registers, it can access (2^64) unique memory addresses. i.e.,17,179,869,184 GB.|
|32-bit CPU architecture can process 32 bits of data and information.|64-bit CPU architecture can  process 64 bits of data and information.|

### Advantages of 64-Bit OS
   -  64-bit CPU can access (2^64) memory addresses. 
   -  Better Resource Usage and Better CPU Performance.
   -  64-bit CPU can run both 32-bit and 64-bit OS.

---

### How OS creates a process?
   1. Load the program into the main memory.
   2. Allocate the runtime stack.
   3. Allocate the heap memory.
   4. Allocate I/O handles such as input, output, and error.
   5. OS hands off the control to the starting point of the loaded program, which may or may not be ``main()``.


### What is process table?
A table like data structure that is used by OS to track the processes.
Each entry in the process table is a ``PCB`` block.

### What is ``PCB``?
``PCB`` (Program Counter Block) is also a data structure that is used by OS to 
maintain each process. It stores all the information related to a process
such as processID, program counter, process state, priority etc.

### What is registers in ``PCB``?
Registers is also a data structure in the ``PCB``. When a processes is running
and it's time slice expires, the current value of process specific registers 
would be stored in the ``PCB`` and the process would be swapped out. When the process is scheduled to  be run, the register values is read from the PCB and written to the ``CPU`` registers. This is the main purpose of the registers in the ``PCB``.
	
### Degree of Multi-programming
The number of processes that can be accommodated in the ready queue. It is handled by ``LTS`` (Long Term Scheduler). The degree of multiprogramming is typically managed by both the long-term scheduler (admitting processes to the system) and the short-term scheduler (selecting processes for execution from the ready queue).


### Why do we need ``MTS`` (Medium term Scheduler)?
- ``MTS`` perform swapping of processes, swapping is necessary to improve process mix or because a change in memory requirements has over-committed available memory, requiring memory to be freed up.


### Orphan Process:
- The process whose parent process has been terminated and it is still running.
- They are further adopted by init process (``pID = 1``).

### Zombie process:
- The process whose execution is execution is completed but it still
has an entry in the process table.
- Once parent gets the exit status code using the wait system call, the zombie process is eliminated from the process table. This is known as reaping the zombie process.
- As entry of the child process in the process table can only be removed, after the parent process reads the exit status of the child process. Hence, the child process remains a zombie till it is removed from the process table.

> **Note**: The runtime mapping from virtual to physical address is done by a hardware device called the memory-management unit (``MMU``).

### How OS manages the isolation and protect? (Memory Mapping and Protection)
- OS provides Virtual Address Space (``VAS``) concept.
- To separate memory space, we need the ability to determine the range of legal addresses that the process may access and to ensure that the process can access only these legal addresses.
- Relocation Register contains value of smallest physical address (``Base address [R]``) and the Limit Register contains the range of logical addresses. The relocation register typically contains the value added to each address generated by a program to produce a physical address. It doesn't represent the smallest physical address.
- Each logical address must be less than the limit register.
- ``MMU`` maps logical address dynamically by adding value in the relocation register. The MMU performs dynamic address translation based on the values in the relocation and limit registers.
- When CPU scheduler selects a process for execution, the dispatcher loads the relocation and limit registers with the correct values as part of the context switch. 

Since every address generated by the CPU is checked against these registers, 
we can protect both OS and other users programs and data.

---
