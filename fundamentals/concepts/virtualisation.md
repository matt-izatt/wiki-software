# Virtualisation

### Overview

Virtualisation is a technology that allows multiple virtual computers, known as **Virtual Machines (VMs)**, to run on a single physical computer.

Each virtual machine behaves as if it were an independent computer with its own:

* Operating system
* CPU resources
* Memory
* Storage
* Network interfaces

The software responsible for creating and managing virtual machines is called a **hypervisor**.

Virtualisation enables better hardware utilisation, workload isolation, scalability, and flexibility.

> * **CPU Scheduling** → sharing CPU time between processes
> * **Memory Management** → sharing RAM between processes
> * **I/O Management** → sharing devices between processes
> * **Virtualisation** → sharing an entire physical machine between multiple operating systems

***

### Why Virtualisation is Needed

Historically, applications were often deployed on dedicated physical servers.

This approach led to several problems:

* Low hardware utilisation
* High infrastructure costs
* Difficult scaling
* Complex disaster recovery
* Inefficient resource allocation

Virtualisation addresses these issues by allowing multiple workloads to share the same physical hardware safely and efficiently.

Benefits include:

* Improved resource utilisation
* Reduced hardware costs
* Easier management
* Faster provisioning
* Better isolation
* Improved disaster recovery

***

### Virtual Machine Concepts

A Virtual Machine (VM) is a software-based emulation of a physical computer.

Each VM contains:

* Guest operating system
* Virtual CPU (vCPU)
* Virtual memory
* Virtual storage
* Virtual network adapters

To the guest operating system, the VM appears to be a real physical machine.

Examples:

* Running Windows inside Linux
* Running Linux inside Windows
* Running multiple Linux servers on a single host

***

### Hypervisors

A hypervisor is software that creates and manages virtual machines.

Its responsibilities include:

* CPU scheduling
* Memory allocation
* Device virtualisation
* Resource isolation
* VM lifecycle management

The hypervisor sits between virtual machines and physical hardware.

***

### Type 1 Hypervisors (Bare-Metal)

A Type 1 hypervisor runs directly on the hardware.

Architecture:

Hardware → Hypervisor → Virtual Machines

Advantages:

* Better performance
* Stronger isolation
* Lower overhead
* Enterprise-grade scalability

Examples:

* VMware ESXi
* Microsoft Hyper-V
* Xen

Commonly used in data centres and cloud platforms.

***

### Type 2 Hypervisors (Hosted)

A Type 2 hypervisor runs as an application on top of an existing operating system.

Architecture:

Hardware → Host OS → Hypervisor → Virtual Machines

Advantages:

* Easier installation
* Suitable for development and testing

Disadvantages:

* Additional overhead
* Lower performance

Examples:

* VirtualBox
* VMware Workstation
* Parallels Desktop

***

### CPU Virtualisation

CPU virtualisation allows multiple virtual machines to share physical CPU resources.

The hypervisor:

* Creates virtual CPUs (vCPUs)
* Schedules vCPUs onto physical CPU cores
* Saves and restores CPU state during context switches

This is conceptually similar to operating system process scheduling, but at the virtual machine level.

Benefits:

* Efficient CPU utilisation
* Workload isolation
* Flexible resource allocation

***

### Memory Virtualisation

Memory virtualisation allows each VM to believe it owns a continuous block of memory.

The hypervisor maps:

Guest Virtual Address → Guest Physical Address → Host Physical Address

Techniques include:

* Shadow page tables – Hypervisor-managed mappings between guest and host memory.
* Nested page tables – Hardware-assisted translation from guest memory to physical memory.
* Memory overcommitment – Allocating more virtual memory than physically available.
* Ballooning – Reclaiming memory from VMs when the host needs RAM.

Benefits:

* Isolation between VMs
* Efficient RAM utilisation
* Dynamic memory allocation

***

### Storage Virtualisation

Virtual machines use virtual disks rather than direct access to physical storage.

Examples:

* VHD – Virtual Hard Disk format used by Microsoft
* VHDX – Newer Microsoft virtual disk format with larger capacity support
* VMDK – Virtual disk format used by VMware
* QCOW2 – Virtual disk format used by QEMU with snapshot support

The hypervisor maps virtual disk operations to physical storage devices.

Benefits:

* Easy backup
* Snapshots
* Migration
* Flexible storage management

***

### Network Virtualisation

Virtual machines are connected using virtual networking components.

Examples:

* Virtual switches
* Virtual routers
* Virtual network adapters

The hypervisor can create isolated networks entirely in software.

Benefits:

* Network segmentation
* Security isolation
* Flexible topology design

Cloud providers rely heavily on network virtualisation.

***

### Virtual Machine Snapshots

A snapshot captures the state of a virtual machine at a specific point in time.

A snapshot may include:

* Memory contents
* CPU state
* Disk state
* Device state

Benefits:

* Fast rollback
* Safe experimentation
* Simplified upgrades

Snapshots are useful but should not replace proper backups.

***

### Live Migration

Live migration allows a running virtual machine to move between physical hosts with minimal downtime.

Process:

1. Memory pages are copied to the target host.
2. VM state is synchronised.
3. Execution transfers to the new host.
4. Network connections remain active.

Benefits:

* Hardware maintenance
* Load balancing
* High availability

This capability is widely used in cloud environments.

***

### Hardware-Assisted Virtualisation

Modern CPUs include features specifically designed for virtualisation.

Examples:

* Intel VT-x
* Intel VT-d
* AMD-V

These technologies:

* Reduce virtualisation overhead
* Improve performance
* Enhance security
* Simplify hypervisor design

Modern virtualisation platforms rely heavily on these features.

***

### Containers vs Virtual Machines

Although often compared, containers and virtual machines solve different problems.

#### Virtual Machines

* Include a complete guest operating system
* Strong isolation
* Higher resource usage
* Slower startup times

Examples:

* Linux VM
* Windows VM

#### Containers

* Share the host operating system kernel
* Lightweight
* Fast startup
* Higher density

Examples:

* Docker containers
* Kubernetes pods

Containers virtualise the operating system, while virtual machines virtualise the hardware.

***

### Virtualisation in Cloud Computing

Cloud computing is built on virtualisation.

Cloud providers use virtualisation to:

* Share physical infrastructure
* Isolate customers
* Scale resources dynamically
* Improve hardware utilisation

Examples include:

* Amazon Web Services EC2 instances
* Microsoft Virtual Machines
* Google Compute Engine

Users receive virtual machines without needing to manage physical hardware.

***

### Advantages of Virtualisation

* Better hardware utilisation
* Reduced costs
* Strong isolation
* Simplified management
* Easier backups and recovery
* Live migration support
* Faster provisioning

***

### Disadvantages of Virtualisation

* Additional complexity
* Performance overhead
* Resource contention
* Licensing considerations
* Potential hypervisor vulnerabilities

Modern hardware support has significantly reduced performance penalties.

***

### Summary

Virtualisation allows multiple virtual machines to share the same physical hardware while remaining isolated from one another.

Key concepts include:

* Hypervisors
* Virtual machines
* CPU virtualisation
* Memory virtualisation
* Storage virtualisation
* Network virtualisation
* Snapshots
* Live migration
* Hardware-assisted virtualisation

Virtualisation forms the foundation of modern cloud computing, data centres, and enterprise infrastructure.
