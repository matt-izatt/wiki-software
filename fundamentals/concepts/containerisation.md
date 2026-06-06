# Containerisation

### Overview

Containerisation is a lightweight virtualisation technology that packages an application together with its dependencies into a self-contained unit called a **container**.

A container includes:

* Application code
* Runtime environment
* Libraries
* Configuration files
* Dependencies

Unlike virtual machines, containers do **not** contain a complete operating system. Instead, they share the host operating system kernel while remaining isolated from one another.

Containerisation enables applications to run consistently across development, testing, and production environments.

> * **CPU Scheduling** → Share CPUs between processes
> * **Memory Management** → Share memory between processes
> * **I/O Management** → Share devices between processes
> * **Virtualisation** → Share hardware between operating systems
> * **Containerisation** → Share an operating system between applications

***

### Why Containerisation is Needed

Traditionally, applications were installed directly onto operating systems.

This approach often led to problems such as:

* Dependency conflicts
* Environment inconsistencies
* Difficult deployments
* Poor scalability
* Resource inefficiency

For example:

* Application A requires Python 3.10
* Application B requires Python 3.12

Running both applications on the same server may create conflicts.

Containers solve this problem by packaging each application's dependencies separately while still sharing the host operating system.

Benefits include:

* Consistent deployments
* Simplified distribution
* Faster scaling
* Improved portability
* Better resource utilisation

***

### Containers vs Virtual Machines

Containers and virtual machines both provide isolation, but they operate at different layers.

#### Virtual Machines

Virtualise hardware.

Architecture:

Hardware → Hypervisor → Guest OS → Application

Characteristics:

* Full operating system per VM
* Strong isolation
* Larger resource requirements
* Slower startup times

#### Containers

Virtualise the operating system.

Architecture:

Hardware → Host OS → Container Runtime → Containers

Characteristics:

* Shared kernel
* Lightweight
* Fast startup
* High density

Containers typically start in seconds or milliseconds compared to virtual machines, which may take minutes.

***

### Container Architecture

A container consists of:

* Application
* Libraries
* Runtime
* File system
* Configuration

Containers share the host kernel while maintaining isolated environments.

To the application, it appears as if it has its own:

* Processes
* Network interfaces
* File system
* Users
* Hostname

In reality, these resources are provided through operating system isolation mechanisms.

***

### Linux Namespaces

Namespaces provide isolation between containers.

Each container receives its own view of system resources.

Common namespace types include:

#### PID Namespace

Provides isolated process trees.

Processes inside a container cannot normally see processes running in other containers.

#### Network Namespace

Provides isolated network stacks.

Each container can have its own:

* IP addresses
* Routing tables
* Network interfaces

#### Mount Namespace

Provides isolated file system views.

Containers can mount their own file systems without affecting the host.

#### UTS Namespace

Provides isolated hostnames and domain names.

#### User Namespace

Provides isolated user and group identifiers.

Namespaces create the illusion that each container has its own operating system environment.

***

### Control Groups (cgroups)

Namespaces provide isolation.

Control Groups (cgroups) provide resource control.

Cgroups allow the operating system to limit and monitor resource usage.

Resources commonly controlled include:

* CPU
* Memory
* Disk I/O
* Network bandwidth

Examples:

* Limit a container to 2 CPU cores
* Restrict memory usage to 1 GB
* Prevent a container from consuming all system resources

Together, namespaces and cgroups form the foundation of containerisation.

***

### Container Images

A container image is a read-only template used to create containers.

Images contain:

* Application code
* Dependencies
* Runtime components
* Configuration

Characteristics:

* Immutable
* Portable
* Versioned

Examples:

* Ubuntu image
* Nginx image
* PostgreSQL image
* ASP.NET image

Containers are created from images.

***

### Image Layers

Container images are built from multiple layers.

For example:

Layer 1 → Base Linux image

Layer 2 → Runtime installation

Layer 3 → Application dependencies

Layer 4 → Application code

Benefits:

* Efficient storage
* Faster downloads
* Layer reuse
* Improved caching

Only changed layers need to be rebuilt or transferred.

***

### Container Runtimes

A container runtime is responsible for creating and managing containers.

Responsibilities include:

* Starting containers
* Stopping containers
* Resource isolation
* Network configuration
* Storage management

Examples:

* Docker Engine
* containerd
* CRI-O

The runtime interacts with the operating system to create isolated execution environments.

***

### Container Networking

Containers often need to communicate with:

* Other containers
* External systems
* Databases
* Users

Common networking models include:

#### Bridge Networking

Containers communicate through a virtual network on a host.

#### Host Networking

Containers use the host's network stack directly.

#### Overlay Networking

Containers communicate across multiple hosts.

Overlay networks are commonly used in orchestration platforms.

***

### Container Storage

Containers are designed to be ephemeral.

When a container is removed, its writable storage is typically lost.

Persistent data is usually stored using:

#### Volumes

Managed storage independent of container lifecycle.

#### Bind Mounts

Directories mapped directly from the host file system.

Benefits:

* Persistent data
* Easier backups
* Data sharing between containers

***

### Container Security

Containers improve isolation but do not provide the same level of isolation as virtual machines.

Common security practices include:

* Running as non-root users
* Using minimal base images
* Applying resource limits
* Scanning images for vulnerabilities
* Restricting container capabilities

Security remains a shared responsibility between the operating system, runtime, and application.

***

### Container Orchestration

Managing a few containers manually is straightforward.

Managing thousands of containers requires orchestration.

Container orchestration platforms provide:

* Scheduling
* Scaling
* Self-healing
* Service discovery
* Rolling deployments

The most widely used orchestration platform is:

* Kubernetes

Other examples include:

* Docker Swarm
* Nomad

***

### Containers in Modern Cloud Platforms

Modern cloud-native applications are often built around containers.

Benefits include:

* Rapid deployment
* Horizontal scaling
* Environment consistency
* Infrastructure portability
* Efficient resource utilisation

Most modern microservice architectures are deployed using containers.

***

### Advantages of Containerisation

* Lightweight
* Fast startup times
* High density
* Portable
* Consistent environments
* Efficient resource usage
* Simplified deployments

***

### Disadvantages of Containerisation

* Weaker isolation than virtual machines
* Shared kernel dependency
* Additional operational complexity
* Security considerations
* Persistent storage management challenges

Containers trade some isolation for efficiency and speed.

***

### Summary

Containerisation packages applications and their dependencies into isolated execution environments that share a host operating system kernel.

Key concepts include:

* Containers
* Images
* Layers
* Namespaces
* cgroups
* Container runtimes
* Networking
* Storage
* Orchestration

Containerisation forms the foundation of modern cloud-native application development and deployment.
