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

# Threads and Concurrency

### **Overview**

A thread is the smallest unit of execution that can be scheduled by the operating system. While a process represents an independent program in execution, a process can contain multiple threads that share the same memory space and resources. Threads allow tasks to be performed concurrently, improving responsiveness and resource utilisation.

Concurrency refers to the ability of a system to deal with multiple tasks at once, which may involve overlapping in time. In modern computing, concurrency is critical for multitasking, parallel processing, and efficiently using multi-core CPUs.

***

### **Concurrency vs. Parallelism**

* **Concurrency:** Multiple tasks are in progress within the same time frame, but not necessarily running at the same instant. Example: While one thread waits for network data, another processes user input.
* **Parallelism:** Multiple tasks are executed literally at the same time on different CPU cores. Example: Two threads performing separate calculations on separate cores simultaneously.

**Analogy:**\
Concurrency is like a chef cooking several dishes by switching between them quickly. Parallelism is like multiple chefs cooking different dishes at the same time.

***

### **Characteristics of a Thread**

Each thread, like a process, has a set of attributes that define its execution state and control its behaviour within a program:

#### **Thread ID (TID)**

Every thread in an operating system is assigned a unique identifier within its process, called the Thread ID (TID). The TID allows the OS and debuggers to track individual threads, manage their scheduling, and perform operations like suspension or termination.

#### **State**

A thread can be in various states depending on its execution progress:

* **New:** The thread is created but has not yet started executing.
* **Runnable:** The thread is ready to run and waiting for CPU allocation.
* **Running:** The thread is actively executing instructions.
* **Waiting/Blocked:** The thread is paused, waiting for a resource, event, or signal.
* **Terminated:** The thread has finished execution and is awaiting cleanup.

State transitions are managed by the OS’s thread scheduler, which ensures efficient sharing of CPU time among threads.

#### **Program Counter**

The program counter holds the address of the next instruction for the thread to execute. This ensures that if a thread is preempted or paused, it can resume exactly where it left off. Since threads within the same process share code, each thread’s program counter points to its own current execution position.

#### **Registers**

Each thread has its own set of CPU registers, storing variables, intermediate results, and control data during execution. The OS saves and restores these registers during a context switch between threads, ensuring accurate execution continuity.

#### **Stack**

Unlike processes, threads share code and data segments, but each thread has its own private stack. The stack stores function call information, local variables, and return addresses, keeping each thread’s execution context separate from others.

#### **Shared Memory and Resources**

All threads in a process share the same code, global variables, and heap memory. This shared environment enables fast communication and data sharing but requires careful synchronisation to avoid race conditions and data corruption.

#### **Thread Control Block (TCB)**

Similar to a process’s Process Control Block (PCB), the TCB holds all the metadata about a thread, including its TID, state, program counter, registers, scheduling priority, and stack pointer. The OS uses the TCB to manage thread execution.

***

### **Types of Threads**

#### **User-Level Threads (ULTs)**

User-level threads are managed entirely in user space by a thread library, without direct kernel involvement for scheduling.

* **Advantages:**
  * Very fast to create and manage.
  * No need for kernel mode transitions for thread operations.
* **Disadvantages:**
  * If one thread performs a blocking system call, the entire process may block.
  * Cannot take full advantage of multiple CPU cores without kernel support.

#### **Kernel-Level Threads (KLTs)**

Kernel-level threads are managed directly by the operating system’s kernel. Each thread is known to the scheduler, which can assign them to different CPU cores.

* **Advantages:**
  * True parallelism on multiprocessor systems.
  * One blocked thread doesn’t necessarily block others in the same process.
* **Disadvantages:**
  * Slower to create and manage compared to ULTs due to kernel overhead.

#### **Hybrid Thread Models**

Some systems use a mix of user and kernel threads. In these models, user-level threads are mapped to a smaller or equal number of kernel threads (M:N mapping).

* **Advantages:**
  * Combines fast thread creation with better CPU utilisation.
  * Can balance flexibility and performance.

***

### **Thread Management**

Thread management refers to the mechanisms and operations the operating system uses to control thread creation, execution, coordination, and termination. It ensures that threads share CPU time fairly, access resources safely, and work together without interfering with each other’s execution.

#### **Thread Creation and Termination**

* **Creation:** Threads can be created through language-specific libraries or APIs:
  * **POSIX threads (pthreads):** `pthread_create()` in C/C++.
  * **Java:** Extending the `Thread` class or implementing `Runnable`.
  * **C#:** Using `Thread` or `Task` classes.
* **Termination:**
  * Occurs naturally when the thread’s `run()` method or equivalent completes.
  * Can be triggered externally, though this is often discouraged due to resource safety concerns.

#### **Thread Synchronisation**

When multiple threads share resources, careful synchronisation is required to avoid inconsistencies. Without it, issues like race conditions and data corruption can occur.

Common synchronisation mechanisms include:

* **Mutexes:** Locks that ensure only one thread can access a resource at a time.
* **Semaphores:** Counters that control access to a fixed number of resource instances.
* **Condition Variables:** Allow threads to wait for certain conditions to be true before proceeding.
* **Read-Write Locks:** Allow multiple readers but only one writer at a time.
* **Barriers:** Synchronise a group of threads so they all wait until a certain point before continuing.

Proper synchronisation ensures:

* **Consistency:** Shared data remains correct even under concurrent access.
* **Fairness:** No thread is indefinitely blocked from resources.
* **Deadlock Prevention:** Avoids circular waiting situations that halt progress.

#### **Thread Scheduling**

The operating system’s thread scheduler determines which thread runs at any given time. Efficient scheduling is key to maximising CPU usage and maintaining application responsiveness.

* **Preemptive Scheduling:** The OS can interrupt a running thread to switch to another, ensuring fair CPU allocation and preventing one thread from monopolising the CPU.
* **Cooperative Scheduling:** Threads voluntarily yield control, requiring careful developer design to avoid blocking other threads.
* **Priorities:** Threads can have priority levels, affecting how often they are chosen to run. Higher-priority threads are generally scheduled before lower-priority ones.

Schedulers aim to optimise:

* CPU utilisation
* Throughput
* Response time
* Fairness between threads

***

### **Common Concurrency Issues**

In a multithreaded or concurrent environment, improper coordination between threads can lead to serious problems that affect program correctness, performance, and stability. These issues often arise from poor synchronisation, incorrect resource management, or scheduling imbalances.

#### **Race Conditions**

A race condition occurs when two or more threads access shared data without proper synchronisation, and the final outcome depends on the timing or sequence of thread execution. This can lead to inconsistent or corrupted data.

* **Example:** Two threads incrementing the same shared counter simultaneously might overwrite each other’s updates, resulting in incorrect totals.
* **Prevention:** Use mutual exclusion mechanisms such as mutexes, semaphores, or atomic operations to ensure that only one thread accesses the shared resource at a time.

#### **Deadlocks**

A deadlock occurs when two or more threads are waiting indefinitely for resources held by each other, creating a circular waiting chain where no thread can proceed.

* **Example:**
  * Thread A holds a lock on Resource 1 and waits for Resource 2.
  * Thread B holds a lock on Resource 2 and waits for Resource 1.\
    Both threads are now stuck forever.
* **Prevention:**
  * Lock ordering: Always acquire locks in a consistent, predetermined order.
  * Timeout mechanisms: Automatically release resources if a thread waits too long.
  * Deadlock detection: The system periodically checks for deadlocks and intervenes.

#### **Livelocks**

In a livelock, threads are not blocked, but they continually change state in response to each other and make no actual progress toward completing their tasks.

* **Example:** Two threads repeatedly yield to let the other run, each trying to be “polite,” resulting in neither completing its work.
* **Prevention:**
  * Introduce randomness or back-off strategies so that one thread can eventually proceed.
  * Ensure algorithms guarantee progress under all conditions.

#### **Starvation**

Starvation happens when a thread is perpetually denied access to the CPU or a needed resource because higher-priority threads monopolise it.

* **Example:** In a priority-based scheduler, a low-priority thread might never run if higher-priority threads are always ready.
* **Prevention:**
  * Implement priority aging: Gradually increase the priority of waiting threads over time.
  * Use fair scheduling policies that guarantee all threads get some CPU time.

***

### **Advantages and Disadvantages of Multithreading**

Multithreading offers significant benefits in terms of responsiveness, performance, and efficient resource use. However, it also introduces challenges related to complexity, debugging, and potential concurrency bugs.

#### **Advantages**

* **Improved Application Responsiveness**\
  Multithreading allows applications to remain responsive while performing background tasks. For example, a graphical user interface can continue to accept user input while a separate thread loads data or processes computations in the background.
* **Efficient Use of CPU Resources**\
  Threads can take advantage of idle CPU cycles, especially on multi-core and multi-processor systems. This ensures that the CPU is kept busy, improving overall system throughput and performance.
* **Simplified Modelling of Concurrent Tasks**\
  Using multiple threads allows developers to model real-world problems more naturally, where multiple activities happen simultaneously. For instance, a web server can dedicate one thread per client connection, simplifying logic.
* **Faster Communication and Data Sharing**\
  Since threads within the same process share the same memory space, data can be exchanged without the overhead of inter-process communication mechanisms. This enables quick coordination between threads.
* **Better Resource Utilisation**\
  Threads can be used to overlap computation with I/O operations. While one thread waits for disk or network data, another can use the CPU for processing tasks.

#### **Disadvantages**

* **Increased Complexity in Program Design**\
  Writing correct multi-threaded code is significantly more challenging than writing single-threaded programs. Developers must carefully design synchronisation, communication, and task coordination.
* **Higher Risk of Concurrency Bugs**\
  Problems like race conditions, deadlocks, livelocks, and starvation are more likely to occur when multiple threads share resources without proper controls. These bugs can be intermittent and difficult to reproduce.
* **Difficult Debugging and Testing**\
  Multi-threaded programs are harder to debug because issues may only appear under certain timing conditions. This makes testing more complex and time-consuming.
* **Synchronisation Overhead**\
  While locks and other synchronisation primitives are necessary for thread safety, they introduce performance costs. Excessive locking can even lead to bottlenecks that reduce the benefits of multithreading.
* **Reduced Isolation**\
  Threads within the same process share memory and resources, meaning that a fault in one thread (such as writing to an invalid memory address) can crash the entire process. This makes fault containment weaker compared to separate processes.
* **Potential Oversubscription of CPU**\
  Creating too many threads can cause excessive context switching, increasing CPU overhead and reducing performance instead of improving it.
