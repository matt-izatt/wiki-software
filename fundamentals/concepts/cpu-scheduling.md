# CPU Scheduling

### **Overview**

**CPU scheduling** is the process by which an operating system decides which of the ready, in-memory processes will be assigned to the CPU for execution. Since modern operating systems support multiprogramming, where multiple processes may reside in memory at the same time, CPU scheduling plays a crucial role in ensuring efficient and fair use of the CPU.

***

### **Need for CPU Scheduling**

In a typical computing environment, processes may be in different states: running, waiting, or ready. Only one process can run on a CPU core at a time (except on multi-core processors). When multiple processes are ready, the CPU scheduler determines which one to execute next. The goals of CPU scheduling include:

* **Maximizing CPU utilization**
* **Maximizing throughput**
* **Minimizing turnaround time**
* **Minimizing waiting time**
* **Minimizing response time**
* **Ensuring fairness**

***

### **Types of Schedulers**

* **Long-term scheduler (job scheduler):** Determines which jobs are admitted into the system.
* **Short-term scheduler (CPU scheduler):** Selects among ready processes for execution.
* **Medium-term scheduler:** Swaps processes in and out of memory to manage multitasking.

The **CPU scheduler** is the most frequently invoked, often making decisions thousands of times per second.

***

### **Scheduling Criteria**

Common metrics used to evaluate scheduling algorithms:

* **CPU Utilization:** Percentage of time the CPU is actively working.
* **Throughput:** Number of processes completed per time unit.
* **Turnaround Time:** Total time taken from submission to completion of a process.
* **Waiting Time:** Time a process spends in the ready queue.
* **Response Time:** Time from submission to the first response (not completion).

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

* **Preemptive Scheduling:** CPU can be taken away from a running process (e.g., Round Robin, Preemptive Priority).
* **Non-Preemptive Scheduling:** Process runs until it finishes or voluntarily yields (e.g., FCFS, SJF).

***

### **Context Switching**

A **context switch** occurs when the CPU changes from one process to another. It involves saving the current process state and loading the state of the new process. Excessive switching can reduce CPU efficiency.

***

### **Real-Time CPU Scheduling**

In **real-time systems**, CPU scheduling must guarantee deadlines:

* **Hard real-time:** Missing a deadline is a system failure.
* **Soft real-time:** Deadlines are important but not mandatory.

Common algorithms include:

* **Rate-Monotonic Scheduling (RMS)**
* **Earliest Deadline First (EDF)**

***

### **Conclusion**

CPU scheduling is essential for multitasking operating systems to manage limited CPU resources effectively. The choice of scheduling algorithm significantly affects system performance and user experience, depending on the nature of the workload and system goals.
