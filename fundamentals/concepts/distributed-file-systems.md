# Distributed File Systems

### Overview

A Distributed File System (DFS) is a file system that stores data across multiple machines while presenting it to users and applications as a single, unified file system.

Instead of storing files on a single server or disk, a distributed file system spreads data across multiple nodes connected by a network.

To applications, the files appear to reside in a normal directory structure, even though the data may be distributed across many physical machines.

Distributed file systems provide:

* Scalability
* Fault tolerance
* High availability
* Improved performance
* Shared access

Modern cloud platforms, data processing systems, and container platforms rely heavily on distributed storage.

***

### Why Distributed File Systems are Needed

Traditional file systems operate on a single machine.

As systems grow, several challenges emerge:

* Storage capacity limits
* Single points of failure
* Performance bottlenecks
* Limited scalability
* Difficult data sharing

For example:

A single file server may become overloaded when thousands of users or applications attempt to access it simultaneously.

Distributed file systems solve these problems by distributing storage and access across multiple nodes.

Benefits include:

* Horizontal scalability
* Improved reliability
* Better performance
* Geographic distribution
* Simplified data sharing

***

### Basic Architecture

A distributed file system typically consists of:

#### Clients

Applications that read and write files.

#### Storage Nodes

Machines that store file data.

#### Metadata Services

Components that track:

* File names
* Directory structure
* File locations
* Permissions
* Replication information

A client often interacts with metadata services first to locate a file and then communicates directly with storage nodes.

***

### Transparency

One of the primary goals of a distributed file system is transparency.

Applications should not need to know:

* Where files are stored
* How many storage nodes exist
* Whether data has been replicated
* Which machine serves a request

The system should appear to behave like a normal local file system.

***

### Data Distribution

Files are often divided into smaller pieces and distributed across multiple machines.

These pieces may be called:

* Blocks
* Chunks
* Segments

Benefits include:

* Parallel access
* Better load balancing
* Improved scalability

Large files can be read and written by multiple nodes simultaneously.

***

### Replication

Replication creates multiple copies of data across different storage nodes.

Example:

File Block A

* Copy 1 → Node 1
* Copy 2 → Node 5
* Copy 3 → Node 9

Benefits:

* Fault tolerance
* High availability
* Improved read performance

If one node fails, another replica can continue serving requests.

Replication is one of the most important features of distributed file systems.

***

### Fault Tolerance

Distributed systems must assume that hardware failures will occur.

Common failures include:

* Disk failures
* Network failures
* Server crashes
* Power outages

A distributed file system should continue operating despite these failures.

Techniques include:

* Replication
* Automatic failover
* Self-healing
* Data recovery mechanisms

The goal is to eliminate single points of failure.

***

### Consistency

When data exists in multiple locations, consistency becomes a challenge.

Questions include:

* When should replicas be updated?
* What happens if updates conflict?
* What if a node becomes temporarily unavailable?

Different systems provide different consistency guarantees.

#### Strong Consistency

All clients immediately see the latest write.

Advantages:

* Predictable behaviour

Disadvantages:

* Higher coordination costs

#### Eventual Consistency

Replicas may temporarily differ but eventually converge.

Advantages:

* Better scalability
* Higher availability

Disadvantages:

* Clients may temporarily see stale data

***

### Distributed File System Operations

Common file operations include:

* Create
* Read
* Write
* Delete
* Rename

The distributed file system must ensure these operations work correctly across multiple nodes.

Many systems also provide:

* Access control
* Auditing
* Quotas
* Versioning

***

### Caching

Distributed file systems often use caching to improve performance.

Data may be cached:

* On clients
* On storage nodes
* In memory

Benefits:

* Reduced network traffic
* Faster reads
* Lower latency

Challenges:

* Cache invalidation
* Consistency management

Caching significantly improves performance in large-scale systems.

***

### Distributed File System Models

Different distributed file systems are designed for different workloads.

#### Shared File Systems

Multiple clients access the same files simultaneously.

Examples:

* NFS
* SMB
* CephFS

Commonly used in enterprise environments.

#### Distributed Data Platforms

Optimised for large-scale analytics and batch processing.

Examples:

* HDFS
* GFS

Designed for very large files and high-throughput workloads.

#### Object Storage Systems

Store objects rather than traditional files.

Examples:

* Amazon S3
* MinIO

Often used for cloud-native applications.

***

### Hadoop Distributed File System (HDFS)

HDFS is one of the most widely known distributed file systems.

Key components:

#### NameNode

Stores metadata.

Responsible for:

* Directory structure
* Block locations
* File system namespace

#### DataNodes

Store actual file blocks.

Characteristics:

* Large block sizes
* Automatic replication
* Fault tolerance
* Optimised for sequential access

HDFS is commonly used for big data processing.

***

### Google File System (GFS)

The Google File System influenced many modern distributed storage systems.

Characteristics:

* Large-scale operation
* Commodity hardware
* Fault tolerance
* Automatic replication

Many concepts later inspired HDFS.

***

### Ceph

Ceph is a distributed storage platform that provides:

* Object storage
* Block storage
* File storage

Key features:

* No single point of failure
* Self-healing
* Automatic rebalancing
* Strong scalability

Ceph is widely used in private cloud environments.

***

### Distributed Storage in Kubernetes

Container platforms often require persistent storage.

Kubernetes commonly integrates with distributed storage systems to provide:

* Persistent volumes
* High availability
* Dynamic provisioning
* Multi-node access

Examples include:

* Ceph
* Longhorn
* OpenEBS

This allows containers to retain data even when individual nodes fail.

***

### CAP Theorem

Distributed file systems are influenced by the CAP Theorem.

The theorem states that during a network partition, a system can prioritise only two of the following:

* Consistency
* Availability
* Partition Tolerance

Since network partitions are unavoidable, distributed systems must choose trade-offs between consistency and availability.

Many distributed storage systems make different choices depending on their goals.

***

### Advantages of Distributed File Systems

* Horizontal scalability
* Fault tolerance
* High availability
* Improved performance
* Shared access
* Geographic distribution

Distributed file systems enable storage systems to grow beyond the limits of a single machine.

***

### Disadvantages of Distributed File Systems

* Increased complexity
* Network dependency
* Consistency challenges
* Operational overhead
* More difficult debugging

Building reliable distributed storage is significantly more complex than building local storage systems.

***

### Summary

Distributed file systems allow data to be stored across multiple machines while appearing as a single file system to users and applications.

Key concepts include:

* Metadata services
* Storage nodes
* Replication
* Fault tolerance
* Consistency
* Caching
* Distributed storage platforms
* CAP Theorem

Distributed file systems form the storage foundation of modern cloud platforms, container orchestration systems, and large-scale distributed applications.
