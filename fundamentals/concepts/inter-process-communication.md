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

# Inter-Process Communication

### **Overview**

Inter-Process Communication (IPC) refers to mechanisms provided by the operating system that allow processes to exchange data and coordinate actions. Since processes in modern operating systems run in isolated memory spaces, IPC is essential for enabling cooperation and communication between them, especially in multitasking and distributed systems.

IPC is used in various contexts, including multitasking within a single system, client-server communication, parallel processing, and real-time applications.

***

### **Why IPC is Needed**

In a multitasking operating system, multiple processes often need to work together rather than operate in complete isolation. Since processes are generally given separate address spaces for security and stability, they cannot directly access each other’s memory. To cooperate effectively, the operating system provides IPC mechanisms. These allow processes to exchange data, coordinate actions, and maintain consistency.

The main reasons why IPC is necessary include:

#### **Data Sharing**

Many applications need to exchange information between processes.

* **Example:** A graphical user interface (GUI) process may display data that is continuously updated by a background process (e.g., a weather widget receiving live updates from a network service).
* **IPC Role:** Provides structured and safe ways for processes to share data without violating isolation. Mechanisms like shared memory and message queues enable this.

#### **Resource Sharing**

Processes frequently need to access common resources such as files, databases, printers, or blocks of memory. Without coordination, this can lead to conflicts or corruption.

* **Example:** Two processes writing to the same file simultaneously could overwrite each other’s data.
* **IPC Role:** IPC mechanisms, often combined with synchronisation tools like locks or semaphores, ensure orderly access to resources, preventing conflicts and maintaining data integrity.

#### **Event Notification**

Processes may need to signal each other about changes in state or system events.

* **Example:** A web server process may notify a logging process whenever a new client connection is established. Similarly, an operating system may inform a process that new input has arrived.
* **IPC Role:** Techniques like signals, pipes, or sockets allow asynchronous notifications so processes can respond quickly to events.

#### **Process Synchronisation**

When processes cooperate on a shared task, their execution must be carefully synchronised to avoid race conditions, deadlocks, or inconsistent results.

* **Example:** In a banking application, one process updating an account balance must not conflict with another process reading or writing to the same balance.
* **IPC Role:** Synchronisation primitives such as mutexes, semaphores, and monitors coordinate process execution to maintain correctness and fairness.

**In summary:**\
IPC is needed because processes must not only execute independently but also share data, coordinate access to resources, respond to events, and synchronise execution. Without IPC, modern multitasking systems would not be able to run interactive applications, client-server models, or distributed systems effectively.

***

### **Types of IPC Mechanisms**

IPC methods can be broadly categorised into message passing and shared memory:

#### **Message Passing**

Processes communicate by sending and receiving messages via the operating system.

**a. Pipes**

* Unidirectional or bidirectional communication channel.
* Commonly used between related processes (e.g., parent-child).
* Types:
  * **Anonymous Pipes:** Exist only while the communicating processes are running.
  * **Named Pipes (FIFOs):** Exist as special files; allow unrelated processes to communicate.

**b. Message Queues**

* A queue structure managed by the OS where messages are stored until retrieved.
* Supports asynchronous communication.
* Messages can be prioritised or ordered.

**c. Sockets**

* Provide communication between processes over a network or the same machine.
* Used in client-server models.
* Support TCP/IP or UDP protocols.

**d. Signals**

* Used to notify a process that a particular event has occurred.
* Lightweight but limited in data transmission (usually only predefined signals).

#### **Shared Memory**

Multiple processes are given access to a common memory space.

* Fastest IPC mechanism (no kernel involvement during access).
* Requires synchronisation (e.g., semaphores or mutexes) to avoid race conditions.
* Common in systems with high performance or large data sharing needs.

***

### **IPC in Distributed Systems**

Inter-Process Communication is not limited to processes running on the same physical machine. In distributed systems, processes may run on different computers connected through a network, yet they must still coordinate, share data, and exchange events. Unlike local IPC, which benefits from shared memory and fast kernel-level communication, distributed IPC faces additional challenges such as network delays, reliability issues, and differences in system architecture.

#### **Challenges of IPC in Distributed Systems**

1. **Network Latency and Reliability**
   * Communication between distributed processes depends on network conditions, which can introduce unpredictable delays.
   * Packets may be lost, duplicated, or arrive out of order, requiring error handling and retransmission mechanisms.
2. **Serialisation and Deserialisation of Data**
   * Since processes on different machines do not share memory, data must be converted into a transferable format before transmission.
   * Serialisation encodes complex data structures (e.g., objects) into byte streams; deserialisation reconstructs them at the receiving end.
   * Common formats include JSON, XML, Protocol Buffers, and Avro.
3. **Protocol Management**
   * Communication requires agreed-upon protocols to define how messages are structured, transmitted, and acknowledged.
   * Examples: HTTP, TCP/IP, gRPC protocols, or custom application-level protocols.
   * Protocols ensure interoperability between heterogeneous systems running different hardware or operating systems.

#### **Technologies for Distributed IPC**

* **Remote Procedure Calls (RPC)**
  * Allows a process on one machine to call a function (procedure) in another machine as if it were local.
  * Handles network communication, marshalling arguments, and returning results transparently.
  * Example: SunRPC, ONC RPC.
* **Remote Method Invocation (RMI)**
  * Java-specific implementation of remote calls where objects on one JVM can invoke methods on objects in another JVM.
  * Provides object-oriented semantics across distributed systems.
* **gRPC**
  * A modern, high-performance RPC framework developed by Google.
  * Uses Protocol Buffers for efficient serialisation and supports multiple programming languages.
  * Widely used in microservices architectures due to its low latency and strong typing.
* **WebSockets**
  * Provides a full-duplex communication channel over a single TCP connection.
  * Enables real-time bidirectional communication between clients (e.g., browsers) and servers.
  * Commonly used in chat applications, gaming, and live dashboards.
* **Message Brokers (e.g., RabbitMQ, Kafka)**
  * Provide asynchronous, decoupled communication between distributed processes.
  * Producers publish messages to a broker, and consumers receive them at their own pace.
  * Useful for event-driven systems, logging pipelines, and large-scale distributed architectures.

**In summary:**\
IPC in distributed systems extends beyond local communication, addressing network constraints, data serialisation, and protocol management. Technologies such as RPC, RMI, gRPC, WebSockets, and message brokers provide different trade-offs in terms of performance, reliability, and scalability, making them fundamental to modern cloud-based and distributed applications.

***

### **Operating System Support**

Different operating systems provide their own APIs, primitives, and tools for implementing IPC. While the underlying goals are similar - data sharing, synchronisation, and event signalling - the mechanisms vary in design and implementation. Understanding OS-specific support is essential for writing portable or system-optimised applications.

#### **Unix**

Unix-like systems (including Linux) provide a wide range of IPC mechanisms, many of which conform to POSIX or System V IPC standards.

* **Pipes and FIFOs (Named Pipes):**
  * Standard mechanism for unidirectional or bidirectional communication between processes.
  * Useful for communication between parent and child processes.
  * FIFOs extend pipes to unrelated processes via a name in the filesystem.
* **Message Queues:**
  * Allow processes to send and receive structured messages asynchronously.
  * Useful for passing small packets of data without direct memory sharing.
* **Shared Memory (shm):**
  * The fastest form of IPC, where multiple processes map the same region of physical memory into their address space.
  * Requires synchronisation mechanisms (like semaphores) to avoid conflicts.
* **Semaphores:**
  * Used to control access to shared resources by multiple processes.
  * Commonly paired with shared memory to ensure safe concurrent access.
* **Inspection Tools:**
  * `ipcs` and `ipcrm`: Manage and remove System V IPC objects (message queues, shared memory segments, semaphores).
  * `/proc`: Virtual filesystem exposing process and system information, including IPC details.
  * `ps`: Lists running processes and their relationships.
  * `netstat`: Inspects socket-based IPC and networking connections.

#### **Mac**

macOS, built on the Darwin kernel (a hybrid of Mach and BSD), supports both BSD-style IPC mechanisms and Mach-specific IPC features.

* **Mach Ports:**
  * Core IPC mechanism in macOS and iOS.
  * Provide message-based communication channels, supporting both local and distributed IPC.
  * Used internally by Apple’s system services, such as launchd.
* **BSD IPC Mechanisms:**
  * Similar to Unix: pipes, sockets, message queues, shared memory, and semaphores.
  * Offer POSIX compliance for cross-platform application development.
* **Integration:**
  * Applications can use either Mach IPC (low-level, powerful) or POSIX IPC (portable across Unix-like systems).
  * Apple’s frameworks (like XPC) abstract some of these mechanisms for application developers.

#### **Windows**

Windows provides its own rich set of IPC mechanisms, many of which integrate deeply with its graphical and component-based architecture.

* **Named Pipes:**
  * Support bidirectional communication between processes, even across a network.
  * Widely used in client-server applications.
* **Mailslots:**
  * Simpler, message-oriented IPC mechanism.
  * Useful for broadcast-style communication, where multiple processes receive messages from one sender.
* **Shared Memory (Memory-Mapped Files):**
  * Processes map the same file into memory, enabling shared access to data.
  * Often paired with synchronisation primitives like mutexes or events.
* **Windows Messages:**
  * Used extensively in GUI applications.
  * Processes can send messages (like keyboard input, window events) to each other’s message queues.
* **COM (Component Object Model):**
  * High-level IPC mechanism enabling communication between components, often across process boundaries.
  * Provides language-independent and location-transparent communication.
  * Used extensively in Windows applications, system services, and automation.

**In summary:**

* **Unix:** emphasise low-level, flexible primitives such as pipes, message queues, and shared memory, with command-line tools for inspection.
* **Mac:** builds on Unix IPC but adds Mach ports and higher-level frameworks for system-level and application IPC.
* **Windows:** provides both low-level and high-level IPC, integrating them with its graphical and component-driven environment.

Together, these mechanisms highlight how operating systems balance efficiency, portability, and abstraction in supporting inter-process communication.

***

### **Security Considerations**

While IPC enables processes to share data and coordinate their actions, it also introduces security risks. If not properly controlled, IPC channels can become avenues for unauthorised access, privilege escalation, or data leakage. To maintain system security and stability, operating systems and applications must enforce strict protections around IPC mechanisms.

#### **1. Protecting IPC Channels**

* **Access Control:** IPC mechanisms (such as shared memory, pipes, or message queues) must enforce ownership and permission checks to prevent one process from reading or writing to another process’s communication channel without authorisation.
* **Example:** On Unix/Linux systems, shared memory segments and message queues are assigned user/group permissions, similar to files, ensuring that only authorised processes can access them.
* **Risk if unchecked:** Malicious processes could inject or intercept messages, modify shared memory, or flood IPC channels to cause denial of service.

#### **2. Permission Checks and Authentication**

* **Local IPC:** Operating systems apply permission models similar to file system permissions. Processes must have the correct privileges to create, read, or write IPC resources.
* **Remote IPC:** Since processes may communicate over networks, authentication is critical to ensure that only trusted processes or machines can establish communication.
* **Example:** Windows named pipes and COM objects support Access Control Lists (ACLs) to define which users or processes are allowed to use them.

#### **3. Encryption and Data Integrity**

* **Remote IPC** (such as sockets, RPC, or message brokers) is vulnerable to **eavesdropping** and **tampering** if messages are sent in plaintext.
* **Encryption:** Transport-layer security (TLS/SSL) or application-layer encryption should be used to protect confidentiality and integrity of data in transit.
* **Checksums/Hashes:** Adding integrity checks prevents undetected message corruption or modification during transmission.

#### **4. Sandboxing and IPC Restrictions**

* **Sandboxed Environments:** Many modern operating systems and platforms (e.g., iOS, Android, and web browsers) place applications in sandboxes with **restricted IPC capabilities** to limit the risk of data leakage.
* **Example:**
  * iOS apps cannot freely open shared memory or arbitrary sockets; they must use system-provided APIs like XPC for controlled IPC.
  * Browsers isolate tabs and extensions into separate processes, allowing only limited and audited IPC channels.
* **Goal:** Prevent one compromised process from spying on or manipulating another.

#### **5. Mitigating Common IPC Security Risks**

* **Race Conditions:** Ensure proper synchronisation so attackers cannot exploit timing gaps to gain access.
* **Privilege Escalation:** Never allow untrusted processes to send privileged commands through IPC without validation.
* **Resource Exhaustion:** Limit the size and number of messages/queues to avoid denial-of-service attacks.

**In summary:**\
IPC security is about more than just functionality—it’s about ensuring that only authorised processes communicate, sensitive data is protected, and isolated environments stay isolated. By applying permissions, authentication, encryption, and sandboxing, operating systems reduce the risk of IPC becoming a security vulnerability.

***

### **Examples of IPC Usage**

IPC is used in nearly all modern applications to enable processes to cooperate and share information. Some common real-world examples include:

* **Web Browsers:**\
  Modern browsers (e.g., Chrome, Firefox) use multiple processes - separate processes for rendering tabs, managing plugins, and handling network requests. IPC channels allow these processes to exchange rendering data, user inputs, and status updates securely.
* **Client-Server Communication:**\
  A server process (such as a web server or database server) receives requests from client processes over sockets. This enables distributed communication between applications across machines or networks.
* **Sensor and Data Processing:**\
  In embedded or IoT systems, a sensor process collects raw data and passes it to a processing unit via shared memory, enabling fast and efficient real-time analysis.
* **Operating System Services:**\
  User applications communicate with background system services (e.g., printing service, window manager) using message queues or signals, ensuring smooth integration with the OS.
* **Distributed Systems:**\
  Microservices exchange messages using message brokers (e.g., Kafka, RabbitMQ), enabling scalable and decoupled system architectures.

