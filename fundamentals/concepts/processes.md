---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: false
---

# Processes

### **Overview**

A computer process is an instance of a program in execution. It includes the program code, its current activity represented by the value of the program counter, the contents of the processor's registers, and variables. Processes are fundamental units of work in modern computing environments, particularly in multitasking operating systems, where multiple processes run concurrently.

***

### **Characteristics of a Process**

Each process has the following attributes:

#### **Process ID (PID)**

Every process in an operating system is assigned a unique numerical identifier known as the _Process ID_ (PID). This value allows the system and users to track and manage processes individually. The PID is essential for operations like terminating a process, checking its status, or assigning resources. For example, using the `ps` command in Unix-like systems lists all running processes along with their PIDs, enabling precise control over process management.

#### **State**

A process can exist in different states depending on its execution stage:

* **New:** The process is being created.
* **Ready:** The process is prepared to run and is waiting for CPU allocation.
* **Running:** The process is actively executing instructions on the CPU.
* **Waiting (or Blocked):** The process is paused, waiting for a specific event like I/O completion.
* **Terminated:** The process has finished execution and is being removed from the system’s process table.\
  The state transitions are managed by the operating system’s scheduler, which ensures fair resource allocation and efficient execution.

#### **Program Counter**

The program counter (PC) holds the memory address of the next instruction the process will execute. This ensures that even if the process is interrupted, such as by a context switch, it can resume from the exact point where it left off. The program counter is critical for maintaining process flow and enabling multitasking without losing execution progress.

#### **CPU Registers**

CPU registers are small, high-speed storage locations within the processor that store variables, temporary data, and instruction-related values while the process runs. When a context switch occurs, the operating system saves the current process’s register values so they can be restored when the process resumes, ensuring no data or execution state is lost.

#### **Memory Management Information**

Each process has its own allocated memory space, which is divided into specific segments:

* **Code segment:** Contains the executable instructions.
* **Data segment:** Holds global and static variables.
* **Stack segment:** Stores function parameters, return addresses, and local variables.

The operating system maintains pointers and tables to keep track of these memory segments, ensuring that processes do not interfere with each other’s memory, which helps maintain stability and security.

#### **I/O Status Information**

Processes often require access to input/output devices such as keyboards, disk drives, printers, or network interfaces. The I/O status information includes details about which devices are allocated to the process and any pending I/O requests. This data allows the operating system to manage resource sharing, prevent conflicts, and handle asynchronous I/O efficiently.

***

### **Types of Processes**

#### **User Processes**

User processes are created by individual users or applications to perform specific, often interactive, tasks. These processes typically start when a user launches a program, opens a file, or executes a command. Examples include text editors, web browsers, or data analysis programs. User processes operate within the permissions of the user who started them, which means they are limited in terms of system-level access for security reasons. These processes can run in the foreground (directly interacting with the user) or in the background, where they work silently until their output is needed.

#### **System Processes (or Daemons)**

System processes, often called _daemons_ in Unix-like systems, are background tasks that manage essential operating system functions. They usually start automatically when the system boots and run continuously without direct user interaction. Examples include `cron` (for scheduled tasks), `sshd` (for handling secure shell connections), and `systemd` (for managing services). System processes typically run with higher privileges than user processes, allowing them to perform critical functions like managing network connections, handling device input/output, or monitoring system performance.

#### **Foreground and Background Processes**

Processes can also be categorised based on how they interact with the user.

* **Foreground processes** are actively engaged with the user, accepting input through the keyboard, mouse, or other devices and displaying output directly on the screen. Examples include typing in a word processor or browsing in a web browser.
* **Background processes** run without requiring direct user interaction. They might perform tasks like downloading files, processing large datasets, or syncing cloud storage while the user works on something else. Many background processes are system services, but users can also run their own background jobs using commands like `&` in Unix shells.

Efficient multitasking in modern operating systems relies on the smooth coordination between foreground and background processes, ensuring that system resources are shared without noticeable delays for the user.

***

### **Process Management**

Process management is the act of handling processes in an operating system. The operating system (OS) manages processes through the following mechanisms:

#### **Process Creation and Termination**

Processes are created by:

* **System calls** like `fork()` in Unix-like systems or `CreateProcess()` in Windows.
* **Parent-child relationship:** A parent process can spawn one or more child processes.

Processes terminate upon:

* Completion of execution.
* A signal or exception (e.g., segmentation fault).
* An external request (e.g., `kill` command or task manager action).

#### **Process Scheduling**

The OS uses scheduling algorithms to determine which process runs at a given time. Key algorithms include:

* **First-Come, First-Served (FCFS)**\
  Processes are executed in the order they arrive, much like a queue at a store. Simple to implement but can lead to long wait times for shorter jobs if a long one arrives first.
* **Shortest Job Next (SJN)**\
  Also called _Shortest Job First (SJF)_; the process with the smallest execution time runs first. Efficient for average wait time but requires knowing job lengths in advance.
* **Round Robin (RR)**\
  Each process gets a fixed time slice (quantum) in rotation. If it’s not finished, it goes to the back of the queue. Great for fairness and responsiveness, especially in time-sharing systems.
* **Multilevel Queue Scheduling**\
  Processes are grouped into separate queues based on priority or type (e.g., interactive vs. batch), each with its own scheduling algorithm. Higher-priority queues usually get CPU time first.

Schedulers aim to optimise CPU utilisation, throughput, turnaround time, and fairness.

#### **Context Switching**

Context switching is the mechanism the operating system uses to switch the CPU’s focus from one process to another, enabling multitasking. When this happens, the OS must preserve the _execution state_ of the currently running process so it can resume later without losing progress.

The execution state includes:

* **Program Counter (PC):** The address of the next instruction to execute.
* **CPU Registers:** Current working values and temporary data.
* **Memory Management Information:** Data about the process’s memory mappings.
* **I/O Status:** Pending input/output requests or device allocations.

The context switch occurs in several situations, such as:

* A running process’s time slice expires in a time-sharing system.
* A higher-priority process becomes ready to run.
* The current process voluntarily waits for I/O or another event.

During a context switch, the OS performs these steps:

1. **Save the current process state** into its Process Control Block (PCB).
2. **Select the next process** from the ready queue, based on the scheduling policy.
3. **Load the saved state** of the selected process from its PCB into the CPU.

Although context switching is essential for responsiveness and fairness, it introduces _overhead_ because no useful work is done during the switch itself. Operating systems strive to minimise this overhead while ensuring smooth process transitions.

#### **Inter-Process Communication (IPC)**

Processes often need to communicate with each other, especially in multitasking systems. IPC methods include:

* **Pipes**\
  A unidirectional communication channel where data flows in a first-in, first-out manner between processes. Often used between related processes, like a parent and child.
* **Message Queues**\
  A system-managed list where processes can send and receive structured messages. Allows asynchronous communication and works well for passing discrete data packets.
* **Shared Memory**\
  A memory region accessible by multiple processes, enabling very fast data exchange. Requires synchronisation (like semaphores) to prevent read/write conflicts.
* **Sockets**\
  Endpoints for bidirectional communication between processes, either on the same machine or over a network. Commonly used for client-server applications.

#### **Process Synchronisation**

Process synchronisation is the coordination of multiple processes or threads to ensure they work together without interfering with each other, especially when accessing shared resources such as memory, files, or hardware devices. Without proper synchronisation, problems like race conditions, data inconsistency, or deadlocks can occur.

In multiprocessor and multi-threaded environments, multiple execution flows can attempt to read or write shared data at the same time. Synchronisation mechanisms control the order and timing of access to prevent conflicts and maintain system stability.

Key synchronisation mechanisms include:

* **Semaphores**\
  Integer-based counters used to control access to resources. A semaphore can be used to signal availability (increment) or indicate usage (decrement), ensuring that only a set number of processes can access the resource simultaneously.
* **Mutexes (Mutual Exclusion Locks)**\
  Locks that allow only one process or thread at a time to access a resource. A mutex must be acquired before use and released afterward, ensuring exclusive access.
* **Monitors**\
  High-level synchronisation constructs that combine mutual exclusion with condition variables, allowing processes to wait until specific conditions are met before proceeding.

Proper synchronisation ensures:

* **Consistency:** Shared data remains correct even under concurrent access.
* **Fairness:** No process is indefinitely blocked from accessing resources.
* **Deadlock Prevention:** Mechanisms are designed to avoid circular waiting situations that halt progress.

Modern operating systems integrate these mechanisms deeply into their process management, balancing performance with reliability.

***

### **Threads vs. Processes**

Processes and threads are both units of execution in an operating system, but they differ significantly in how they use system resources, communicate, and handle concurrency. Understanding the distinction between the two is essential for designing efficient, scalable, and safe applications.

#### **Processes**

A process is an independent program in execution, with its own:

* **Memory space:** Separate address space, meaning no direct access to another process’s memory.
* **Resources:** Dedicated file descriptors, system handles, and environment variables.
* **State information:** Stored in its Process Control Block (PCB), including registers, program counter, and scheduling data.

Because processes are isolated from one another, they provide strong security and stability - if one process crashes, it typically doesn’t affect others. However, inter-process communication (IPC) mechanisms like pipes, message queues, or shared memory are required for data exchange, which can be slower than communication within a single process.

**Advantages of processes:**

* Strong isolation for stability and security.
* Fault tolerance - errors in one process don’t corrupt others.
* Ideal for running completely separate programs.

**Disadvantages of processes:**

* Higher memory usage due to separate address spaces.
* More CPU overhead for context switching between processes.
* Slower data sharing compared to threads.

#### **Threads**

A thread is often called a _lightweight process_ because it represents an independent execution path within a process but shares many of its resources:

* **Shared memory:** All threads in the same process access the same code, data, and heap segments.
* **Separate stack:** Each thread has its own stack for function calls and local variables.
* **Thread Control Block (TCB):** Maintains state information for scheduling and execution, similar to a PCB but lighter.

Because threads share the same memory space, switching between threads (within the same process) is faster than switching between processes. They are ideal for tasks that need to run concurrently and share large amounts of data, such as in real-time applications, GUI responsiveness, and parallel computations.

**Advantages of threads:**

* Lower overhead in creation and context switching compared to processes.
* Faster communication between threads (shared memory access).
* More responsive applications - threads can perform background tasks without freezing the main program.

**Disadvantages of threads:**

* Less isolation - an error in one thread (e.g., invalid memory access) can crash the entire process.
* Requires careful synchronisation to avoid race conditions, deadlocks, and data corruption.
* Debugging multi-threaded programs is more complex than single-threaded ones.

#### **Use Cases**

* **Processes:** Running separate applications, isolating critical services, implementing strong security boundaries.
* **Threads:** Performing parallel tasks within an application, handling multiple connections in a server, keeping UI responsive while performing background work.

#### **Summary**

<table><thead><tr><th width="257.409423828125">Feature</th><th>Processes</th><th>Threads</th></tr></thead><tbody><tr><td>Memory Space</td><td>Separate</td><td>Shared</td></tr><tr><td>Communication</td><td>Via IPC</td><td>Direct (shared memory)</td></tr><tr><td>Overhead</td><td>Higher</td><td>Lower</td></tr><tr><td>Isolation</td><td>Strong</td><td>Weak</td></tr><tr><td>Fault Impact</td><td>Limited</td><td>Can crash entire process</td></tr><tr><td>Creation Speed</td><td>Slower</td><td>Faster</td></tr><tr><td>Context Switch Speed</td><td>Slower</td><td>Faster</td></tr></tbody></table>

In short: Processes are about isolation and safety; threads are about speed and sharing. Modern applications often use a combination of both: multiple processes for security and stability, and multiple threads within those processes for efficiency and responsiveness.

***

### **Security and Isolation**

Modern operating systems enforce process isolation to ensure that one process cannot interfere with the memory or resources of another. Techniques include:

* **Virtual memory**\
  Creates an abstraction of physical memory, giving each process its own isolated address space. Prevents processes from accessing each other’s memory and enables efficient memory management.
* **Access control**\
  Defines permissions for users and processes, specifying who can read, write, or execute files and resources. Helps enforce security policies and protect sensitive data.
* **Privilege levels**\
  CPU-enforced execution modes (like user mode and kernel mode) that restrict what instructions a process can run. Prevents untrusted code from directly accessing critical system resources.

