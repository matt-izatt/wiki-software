# Distributed Shared Memory

### Overview

Distributed Shared Memory (DSM) is a technique that allows memory located on multiple machines to appear as a single shared address space.

Applications can access data using normal memory operations rather than explicitly sending messages between machines.

The goal of DSM is to provide the programming simplicity of shared-memory systems while retaining the scalability of distributed systems.

From the application's perspective, memory appears to be shared across all participating nodes, even though the data is physically distributed.

***

### Why Distributed Shared Memory is Needed

In traditional distributed systems, processes communicate using:

* Message passing
* Remote Procedure Calls (RPCs)
* Network protocols

This can make application development more complex.

For example:

Without DSM -> Node A sends a message to Node B requesting data.

With DSM -> Node A simply reads a memory location.

DSM attempts to hide network communication behind familiar memory operations.

Benefits include:

* Simpler programming model
* Shared data abstraction
* Reduced application complexity
* Easier migration of parallel applications

***

### Shared Memory vs Distributed Shared Memory

#### Shared Memory

Multiple threads access the same physical memory.

Example:

Multiple threads on the same machine accessing a shared variable.

Characteristics:

* Extremely fast access
* Hardware-enforced coherence
* Limited to a single machine

#### Distributed Shared Memory

Memory is physically distributed across multiple machines.

Characteristics:

* Appears shared
* Access may require network communication
* More scalable
* More complex consistency management

DSM attempts to make remote memory access look like local memory access.

***

### Basic Architecture

A DSM system consists of:

#### Nodes

Machines participating in the shared memory system.

#### Memory Manager

Responsible for:

* Tracking memory ownership
* Handling consistency
* Managing replication
* Coordinating updates

#### Communication Layer

Transfers memory pages or objects between nodes.

Applications access memory normally while the DSM system manages communication behind the scenes.

***

### Memory Organisation

DSM systems typically organise memory using one of two approaches.

#### Page-Based DSM

Memory is divided into pages, similar to virtual memory systems.

Examples:

* 4 KB pages
* 8 KB pages

Entire pages move between machines when accessed.

Advantages:

* Simpler implementation
* Leverages virtual memory hardware

Disadvantages:

* False sharing
* Large data transfers

#### Object-Based DSM

Memory is organised as shared objects.

Only specific objects are transferred between nodes.

Advantages:

* Reduced network traffic
* Better granularity

Disadvantages:

* More complex implementation

Modern distributed systems often favour object-based approaches.

***

### Memory Access

When a process accesses memory:

1. The local DSM manager checks whether the data is available locally.
2. If present, access proceeds normally.
3. If not present, the DSM system retrieves the data from another node.
4. The data is cached locally.
5. Execution continues.

This process is similar to demand paging in virtual memory systems.

***

### Consistency Models

A major challenge in DSM is ensuring all nodes see a consistent view of shared data.

Different consistency models provide different guarantees.

#### Strict Consistency

Every read returns the most recent write.

Advantages:

* Easy reasoning

Disadvantages:

* Extremely expensive
* Rarely achievable in distributed systems

#### Sequential Consistency

Operations appear to execute in a single global order.

All nodes observe operations in the same sequence.

Advantages:

* Predictable behaviour

Disadvantages:

* Coordination overhead

#### Causal Consistency

Only causally related operations must appear in the same order.

Independent operations may be observed differently by different nodes.

Advantages:

* Better performance

Disadvantages:

* More complex reasoning

#### Eventual Consistency

Updates eventually propagate to all nodes.

Temporary inconsistencies are allowed.

Advantages:

* High scalability
* High availability

Disadvantages:

* Stale reads possible

Many large-scale distributed systems use eventual consistency.

***

### Coherence Protocols

When multiple nodes cache shared data, updates must be coordinated.

This problem is known as memory coherence.

Common approaches include:

#### Write Invalidate

When a node updates data:

* Other cached copies become invalid.
* Future reads fetch updated data.

Advantages:

* Reduces network traffic.

#### Write Update

When a node updates data:

* New values are immediately propagated to all copies.

Advantages:

* Stronger consistency.

Disadvantages:

* Higher communication overhead.

***

### Replication

DSM systems often replicate memory across nodes.

Benefits:

* Improved availability
* Faster reads
* Fault tolerance

Challenges:

* Maintaining consistency
* Synchronising updates

Replication introduces many of the same challenges found in distributed databases and distributed file systems.

***

### False Sharing

False sharing occurs when unrelated data resides in the same shared memory page.

Example:

* Variable A used by Node 1
* Variable B used by Node 2

If both variables reside on the same page, updates may cause unnecessary page transfers.

Effects:

* Increased network traffic
* Reduced performance

False sharing is one of the most significant performance challenges in page-based DSM systems.

***

### Synchronisation

Shared memory requires synchronisation to avoid race conditions.

Common techniques include:

* Locks
* Mutexes
* Semaphores
* Barriers

DSM systems must implement these mechanisms across the network.

Distributed synchronisation is generally slower and more complex than local synchronisation.

***

### Fault Tolerance

Node failures are inevitable in distributed environments.

DSM systems may use:

* Replication
* Checkpointing
* Recovery protocols
* Redundant coordinators

Fault tolerance becomes more challenging when memory state is distributed across multiple machines.

***

### Advantages of Distributed Shared Memory

* Simplified programming model
* Familiar memory abstraction
* Easier application development
* Supports distributed computation
* Can reduce explicit message passing

DSM attempts to make distributed systems feel more like traditional shared-memory systems.

***

### Disadvantages of Distributed Shared Memory

* Consistency challenges
* Network latency
* False sharing
* Complex fault tolerance
* Synchronisation overhead

Applications may appear simple while the underlying implementation remains highly complex.

***

### Modern Relevance

Pure DSM systems are less common today than they were in early distributed computing research.

However, DSM concepts appear in many modern technologies, including:

* Distributed caches
* In-memory data grids
* Shared-nothing databases
* Clustered memory systems

Examples include:

* Hazelcast
* Apache Ignite
* Redis clusters

While these systems are not pure DSM implementations, they solve many of the same problems.

***

### Relationship to Other Topics

Distributed Shared Memory sits between traditional memory management and distributed systems.

| Concept                   | Scope                  |
| ------------------------- | ---------------------- |
| Memory Management         | One machine            |
| Shared Memory             | Multiple threads       |
| Distributed Shared Memory | Multiple machines      |
| Distributed File Systems  | Shared storage         |
| Distributed Databases     | Shared structured data |

DSM extends the concept of shared memory beyond the boundaries of a single computer.

***

### Summary

Distributed Shared Memory allows memory located on multiple machines to appear as a single shared memory space.

Key concepts include:

* Shared address spaces
* Consistency models
* Coherence protocols
* Replication
* Synchronisation
* Fault tolerance
* False sharing

DSM aims to simplify distributed programming by making remote memory access appear similar to local memory access, though maintaining this illusion introduces significant complexity.
