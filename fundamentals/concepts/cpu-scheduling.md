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
    visible: false
  pagination:
    visible: true
  metadata:
    visible: false
---

# CPU Scheduling

### **Overview**

CPU scheduling is the process by which an operating system decides which of the ready, in-memory processes will be assigned to the CPU for execution. Since modern operating systems support multiprogramming, where multiple processes may reside in memory at the same time, CPU scheduling plays a crucial role in ensuring efficient and fair use of the CPU.

***

### **Need for CPU Scheduling**

In a typical computing environment, processes continuously move between different states: running, waiting, and ready. While waiting, a process might be paused for I/O completion, user input, or the availability of a shared resource. The CPU,  being the system’s most critical and fastest component, can only execute one process per core at a time. On single-core systems, this means only one process runs at any given moment. Even on multi-core processors, the number of concurrent running processes is still limited to the number of available cores.

When multiple processes are in the ready state, prepared to execute but waiting for CPU time, the operating system’s CPU scheduler determines the order in which they will run. The efficiency and fairness of this scheduling directly affect system performance and user experience.

The goals of CPU scheduling include:

#### **Maximising CPU Utilisation**

The CPU is a costly resource, so it should be kept as busy as possible. Idle CPU time represents wasted processing capacity. Effective scheduling ensures that there is always a process ready to run, minimising idle periods.

#### **Maximising Throughput**

Throughput refers to the number of processes completed per unit of time. By carefully selecting which process to run next, the scheduler can increase overall work done by the system. High throughput is particularly important for batch processing and high-performance computing.

#### **Minimising Turnaround Time**

Turnaround time is the total time taken from process submission to completion. This includes waiting time in the ready queue, execution time, and any I/O delays. Shorter turnaround times improve system efficiency, especially for user-submitted jobs or batch tasks.

#### **Minimising Waiting Time**

Waiting time is the total amount of time a process spends in the ready queue before getting CPU time. Reducing waiting time prevents processes from being stuck in the queue for too long and helps maintain consistent system performance.

#### **Minimising Response Time**

In interactive systems, response time is critical - it’s the time from a user’s request (e.g., clicking a button) until the system produces its first visible output. Scheduling algorithms that prioritise quick responses help keep applications feeling responsive and interactive.

#### **Ensuring Fairness**

Fairness ensures that all processes get a reasonable share of CPU time and no process is starved of resources. A fair scheduler balances priority-based execution with the need to serve lower-priority or long-waiting processes. This is essential in multi-user systems and environments running a mix of foreground and background tasks.

***

### **Types of Schedulers**

Schedulers are components of the operating system that decide which processes run and when. They operate at different stages of process management, each with distinct responsibilities and timeframes. The three main types are:

#### **Long-Term Scheduler (Job Scheduler)**

The long-term scheduler controls the admission of jobs into the system for processing. It decides which processes from the job pool (often on disk) should be loaded into memory and placed into the ready queue.

* **Primary role:** Regulates the degree of multiprogramming - the number of processes in memory at one time.
* **Frequency:** Invoked relatively infrequently compared to other schedulers.
* **Goals:**
  * Maintain a balanced mix of I/O-bound and CPU-bound processes to optimise resource utilisation.
  * Prevent system overload by controlling how many jobs enter the system.
* **Example:** In a batch processing environment, the long-term scheduler might admit only as many jobs as the system can handle efficiently, deferring others until resources free up.

#### **Short-Term Scheduler (CPU Scheduler)**

The short-term scheduler, or CPU scheduler, operates on the ready queue, selecting which ready process will execute next on the CPU.

* **Primary role:** Ensure efficient CPU usage and responsive performance by rapidly switching between processes.
* **Frequency:** Invoked very frequently - often thousands of times per second - whenever a process terminates, blocks, or is preempted.
* **Goals:**
  * Maximise CPU utilisation.
  * Minimise response time for interactive processes.
  * Implement fairness and priority-based execution.
* **Example:** In a time-sharing system, the short-term scheduler might select the next process every few milliseconds, ensuring smooth multitasking.

#### **Medium-Term Scheduler**

The medium-term scheduler temporarily removes (swaps out) processes from memory to reduce the degree of multiprogramming or to free up resources for higher-priority tasks. It can later swap them back in for continued execution.

* **Primary role:** Improve CPU and memory usage by managing the mix of active processes.
* **Frequency:** Invoked occasionally, usually when memory contention or heavy CPU load is detected.
* **Goals:**
  * Reduce CPU congestion.
  * Improve responsiveness by prioritising interactive or urgent processes.
  * Rebalance workload when too many processes compete for resources.
* **Example:** A background process might be swapped out to disk to give more memory and CPU time to an active, user-facing application.

#### **Relationship Between Schedulers:**

* **Long-term scheduler** controls the entry of new processes.
* **Medium-term scheduler** adjusts the mix of processes in memory.
* **Short-term scheduler** decides the immediate next process to execute.\
  Together, they ensure the system remains efficient, responsive, and stable.

***

### **Scheduling Criteria**

To evaluate and compare CPU scheduling algorithms, operating systems use a set of performance metrics. These criteria help determine how well a scheduling method balances system efficiency with user satisfaction. The most commonly used metrics are:

#### **CPU Utilisation**

* **Definition:** The percentage of time the CPU is actively executing processes rather than sitting idle.
* **Goal:** Keep the CPU as busy as possible to maximise productivity and avoid wasted resources.
* **Ideal Range:** In practice, CPU utilisation typically ranges from 40% in lightly loaded systems to up to 90% in heavily loaded systems.
* **Importance:** A higher utilisation means the CPU is being used efficiently, but pushing utilisation too high may increase waiting time for other processes.

#### **Throughput**

* **Definition:** The number of processes completed in a given time unit (e.g., jobs per second).
* **Goal:** Maximise the total work accomplished by the system.
* **Importance:** Higher throughput means better overall performance, especially in batch processing systems where many jobs must be completed.
* **Trade-offs:** Algorithms optimised for throughput may favour short jobs, potentially causing longer jobs to wait longer.

#### **Turnaround Time**

* **Definition:** The total time taken for a process from submission to completion. This includes waiting time in the ready queue, execution time, and any I/O delays.
* **Formula:** Turnaround Time=Completion Time−Submission Time
* **Goal:** Minimise turnaround time so that processes complete quickly.
* **Importance:** Particularly relevant in batch systems, where users or administrators care about how long jobs take to finish.

#### **Waiting Time**

* **Definition:** The total amount of time a process spends waiting in the ready queue for CPU allocation.
* **Formula:** Waiting Time=Turnaround Time−Execution Time
* **Goal:** Reduce waiting time to prevent processes from being stuck in the queue unnecessarily.
* **Importance:** High waiting times lead to inefficiency and user frustration. Scheduling algorithms such as Shortest Job Next (SJN) are designed specifically to minimise average waiting time.

#### **Response Time**

* **Definition:** The time from the submission of a process until the system produces its **first visible response**, not the time until completion.
* **Goal:** Minimise response time to ensure interactive systems (like GUIs or real-time applications) feel responsive to the user.
* **Importance:** Especially critical in time-sharing and interactive environments, where users expect immediate feedback.
* **Note:** Response time differs from turnaround time—an application might take long to finish but should start responding quickly.

#### **Summary:**

* For system administrators, metrics like CPU utilisation and throughput matter most.
* For users, turnaround time, waiting time, and response time are more noticeable and directly affect their experience.
* A good scheduling algorithm strikes a balance across all these criteria, depending on whether the system is batch-oriented, interactive, or real-time.

***

### **CPU Scheduling Algorithms**

#### **1. First-Come, First-Served (FCFS)**

* Non-preemptive.
* Processes are scheduled in the order they arrive.
* Simple but can lead to poor average waiting times (convoy effect).

#### **2. Shortest Job Next (SJN) / Shortest Job First (SJF)**

* Non-preemptive or preemptive (Shortest Remaining Time First).
* Selects the process with the shortest expected processing time.
* Optimal in terms of average waiting time but hard to predict execution time accurately.

#### **3. Round Robin (RR)**

* Preemptive.
* Each process gets a fixed time slice (quantum).
* Good for time-sharing systems.
* Can lead to high overhead from frequent context switches.

#### **4. Priority Scheduling**

* Each process is assigned a priority.
* Higher priority processes are selected first.
* Can be preemptive or non-preemptive.
* Risk of **starvation** (low-priority processes never get CPU); **aging** can counter this.

#### **5. Multilevel Queue Scheduling**

* Processes are divided into different queues based on type (e.g., system, interactive, batch).
* Each queue has its own scheduling algorithm.
* Fixed priority or time-sharing between queues.

#### **6. Multilevel Feedback Queue**

* Allows processes to move between queues based on their behavior and age.
* Adaptable and widely used in general-purpose OSes.
* Helps balance response time and throughput.

***

### **Preemptive vs. Non-Preemptive Scheduling**

CPU scheduling algorithms can be broadly classified into **preemptive** and **non-preemptive** types, based on whether a running process can be interrupted and forced to yield the CPU. The choice between these two approaches affects system responsiveness, fairness, and overall performance.

#### **Preemptive Scheduling**

In preemptive scheduling, the operating system can **interrupt a running process** and reassign the CPU to another process. This is typically done when:

* A higher-priority process enters the ready queue.
* The running process has consumed its allocated CPU time slice (quantum).
* The system enforces fairness in a multi-user or time-sharing environment.

#### **Examples:**

* **Round Robin (RR):** Each process gets a fixed time slice; if it doesn’t finish, it is preempted and placed back in the queue.
* **Preemptive Priority Scheduling:** A higher-priority process can preempt a lower-priority one.
* **Shortest Remaining Time First (SRTF):** A process with a shorter remaining burst time can preempt a running longer job.

#### **Advantages:**

* Improves responsiveness in interactive systems.
* Ensures fairness by preventing any single process from monopolising the CPU.
* Allows higher-priority tasks to run immediately when they arrive.

#### **Disadvantages:**

* Involves more overhead due to frequent context switching.
* More complex to implement and manage.
* Can cause starvation of lower-priority processes if higher-priority ones keep arriving.

#### **Non-Preemptive Scheduling**

In non-preemptive scheduling, once a process gains control of the CPU, it **runs until completion** or until it voluntarily yields (e.g., when waiting for I/O). The operating system does not forcibly take the CPU away from it.

#### **Examples:**

* **First-Come, First-Served (FCFS):** Processes run in the order they arrive.
* **Shortest Job First (SJF):** The shortest job runs first, and once it starts, it cannot be interrupted.

#### **Advantages:**

* Simpler to implement, with minimal scheduling overhead.
* Predictable execution, since once a process starts, it will not be interrupted.
* Fewer context switches, making it efficient for batch jobs or long-running tasks.

#### **Disadvantages:**

* Poor responsiveness in interactive systems, since one long job can delay all others.
* Less fair, as processes cannot be interrupted even if a higher-priority task arrives.
* Risk of convoy effect: a long process delays all others behind it in the queue.

***

### **Comparison of Preemptive vs. Non-Preemptive Scheduling**

| Feature            | Preemptive Scheduling                             | Non-Preemptive Scheduling                |
| ------------------ | ------------------------------------------------- | ---------------------------------------- |
| CPU Control        | Can be taken away from a process                  | Held until completion or voluntary yield |
| Complexity         | Higher (requires timers, priorities, interrupts)  | Lower (simpler to implement)             |
| Context Switching  | Frequent, adds overhead                           | Minimal, more efficient                  |
| Responsiveness     | High (suitable for interactive systems)           | Low (long jobs delay others)             |
| Fairness           | Better fairness, prevents monopolisation          | Less fair, prone to convoy effect        |
| Risk of Starvation | Higher (low-priority tasks may wait indefinitely) | Lower (each process eventually runs)     |

In short:

* **Preemptive scheduling** is best for **interactive, real-time, or multi-user systems** where responsiveness is key.
* **Non-preemptive scheduling** is better suited to **batch systems** where fairness and simplicity outweigh immediate responsiveness.

***

### **Context Switching**

A context switch is the process of storing the state of a currently running process or thread so that it can be resumed later, and then loading the saved state of another process or thread into the CPU for execution. It is the fundamental mechanism that allows multitasking, time-sharing, and concurrency in modern operating systems.

#### **Steps in a Context Switch**

When the CPU scheduler decides to switch from one process to another, the operating system performs the following actions:

1. **Save the current process state** into its **Process Control Block (PCB)** or **Thread Control Block (TCB)**. This includes the program counter, CPU registers, stack pointer, and scheduling information.
2. **Update process tables** so the OS knows this process is now in the waiting or ready state.
3. **Load the saved state** of the next process (selected by the CPU scheduler) from its PCB/TCB into the CPU.
4. **Resume execution** from the exact point where the next process left off.

This ensures that processes appear to run **concurrently**, even though only one is actually running on a single CPU core at a time.

#### **Causes of Context Switching**

Context switches occur in several scenarios, including:

* **Preemptive scheduling:** A running process is interrupted when its time slice expires or a higher-priority process arrives.
* **I/O requests:** A process voluntarily gives up the CPU while waiting for input/output operations to complete.
* **Interrupt handling:** The CPU is interrupted by hardware (e.g., keyboard, disk, or timer) and switches to the corresponding interrupt service routine.
* **System calls:** A process requests a kernel service, requiring the CPU to switch to kernel mode execution.

#### **Overhead of Context Switching**

Although context switching is essential for multitasking, it introduces **overhead**, since no useful work is done during the switch itself. This overhead includes:

* **CPU time** spent saving and restoring registers.
* **Cache invalidation,** as switching processes may reduce the effectiveness of CPU caches.
* **Increased latency** if context switches happen too frequently.

Excessive switching—sometimes called _thrashing_—can significantly reduce CPU efficiency, as more time is spent switching between processes than executing them.

#### **Optimising Context Switching**

Operating systems aim to minimise unnecessary context switches by:

* Using efficient scheduling algorithms to balance fairness and overhead.
* Grouping related tasks to reduce frequent switching.
* Employing processor features such as hardware support for fast context saving/restoring.

#### **In summary:**

Context switching is what makes modern multitasking possible. However, while it provides the illusion of parallelism, it comes with costs. Good scheduling strategies aim to minimise overhead while still ensuring fairness, responsiveness, and efficiency.

***

### **Real-Time CPU Scheduling**

In real-time systems, CPU scheduling is not just about fairness or efficiency—it is about meeting time constraints. Many applications, such as medical devices, industrial automation, flight control systems, and multimedia applications, require tasks to complete within strict deadlines. If deadlines are missed, the system may fail to perform its intended function.

Real-time CPU scheduling ensures that critical tasks are given the necessary CPU time to meet their deadlines.

#### **Types of Real-Time Systems**

* **Hard Real-Time Systems**\
  In hard real-time systems, missing a deadline is considered a system failure. These systems often control safety-critical operations where lateness could cause catastrophic outcomes.
  * **Examples:** Pacemakers, automotive braking systems, flight controllers.
  * **Requirement:** Guarantees of deadline compliance are absolute—worst-case execution times must be predictable and tightly controlled.
* **Soft Real-Time Systems**\
  In soft real-time systems, **deadlines are important but not mandatory**. Missing an occasional deadline may degrade performance but does not lead to system failure.
  * **Examples:** Video streaming, online gaming, or multimedia playback.
  * **Requirement:** Scheduling favours tasks with deadlines but allows occasional misses, prioritising average responsiveness over strict guarantees.

#### **Common Real-Time Scheduling Algorithms**

**Rate-Monotonic Scheduling (RMS)**

* **Type:** Fixed-priority, preemptive scheduling.
* **How it works:** Each periodic task is assigned a static priority based on its frequency—the shorter the period (higher rate), the higher the priority.
* **Strengths:** Simple, predictable, and widely used in real-time operating systems.
* **Weaknesses:** Works best for periodic tasks with fixed execution times; not as efficient when task deadlines vary.

**Earliest Deadline First (EDF)**

* **Type:** Dynamic-priority, preemptive scheduling.
* **How it works:** At any scheduling decision point, the task with the **closest deadline** is given the highest priority.
* **Strengths:** Highly efficient—EDF can achieve full CPU utilisation (up to 100%) if tasks are schedulable.
* **Weaknesses:** More complex to implement than RMS; requires continuous recalculation of deadlines.

#### **Key Challenges in Real-Time Scheduling**

* **Predictability:** Execution times must be accurately estimated.
* **Overload Handling:** If too many tasks arrive, the system must decide which deadlines to meet and which to sacrifice.
* **Resource Contention:** Shared resources (e.g., I/O devices) may cause priority inversion, where a low-priority task blocks a higher-priority one. Mechanisms like _priority inheritance_ are used to solve this.

**In summary:**

* Hard real-time scheduling prioritises guarantees: deadlines _must_ be met.
* Soft real-time scheduling prioritises performance: deadlines _should_ be met most of the time.
* RMS and EDF are the two most widely used scheduling algorithms, each with trade-offs in predictability and efficiency.

