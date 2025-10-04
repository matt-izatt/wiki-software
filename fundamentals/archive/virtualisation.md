# Virtualisation

### **Overview**

**Virtualisation** is the process of creating a virtual version of computing resources—such as hardware platforms, operating systems, storage devices, or network resources—rather than relying on physical counterparts. It allows multiple virtual systems (or **virtual machines**) to run on a single physical machine, improving flexibility, resource utilization, and scalability.

Virtualisation is a cornerstone of modern IT infrastructure, enabling cloud computing, data center efficiency, software testing, and high availability systems.

***

### **Types of Virtualisation**

#### **1. Hardware Virtualisation (System Virtualisation)**

* Enables multiple virtual machines (VMs) to run on a single physical machine using a **hypervisor**.
* Each VM runs its own OS and applications, isolated from others.
* Commonly used in servers and data centers.

**Subtypes:**

* **Full Virtualisation:** Emulates the complete hardware so the guest OS runs unmodified.
* **Paravirtualisation:** The guest OS is aware it's running in a virtualised environment and interacts with the hypervisor for better performance.

#### **2. Operating System Virtualisation (Containerisation)**

* Allows multiple isolated user-space instances (containers) to run on a single OS kernel.
* Lightweight and efficient compared to full VMs.
* Examples: **Docker**, **LXC**

#### **3. Application Virtualisation**

* Runs applications in isolated containers or sandboxes.
* The app behaves as if it were installed locally but is separated from the OS.
* Useful for testing and running incompatible or legacy software.

#### **4. Storage Virtualisation**

* Pools multiple physical storage devices into a single virtual storage unit.
* Simplifies management and enhances redundancy and performance.
* Examples: RAID, SAN virtualization

#### **5. Network Virtualisation**

* Abstracts physical network resources into logical units.
* Supports **virtual LANs (VLANs)**, **software-defined networking (SDN)**, and **network function virtualisation (NFV)**.

#### **6. Desktop Virtualisation**

* Hosts user desktops in a central server and delivers them remotely.
* Examples: **Virtual Desktop Infrastructure (VDI)**, **Remote Desktop Services (RDS)**

***

### **Hypervisors**

A **hypervisor** is the software layer that enables virtualisation by managing virtual machines.

#### **Types of Hypervisors:**

* **Type 1 (Bare-metal):** Runs directly on hardware. Examples: VMware ESXi, Microsoft Hyper-V, Xen
* **Type 2 (Hosted):** Runs on top of a host OS. Examples: VirtualBox, VMware Workstation, Parallels

***

### **Benefits of Virtualisation**

* **Resource Efficiency:** Maximizes hardware usage by consolidating workloads.
* **Isolation:** VMs are sandboxed from each other for security and stability.
* **Scalability:** Easy to scale systems up or down.
* **Portability:** VMs and containers can be moved across systems.
* **Disaster Recovery:** Simplifies backups and restores of entire systems.
* **Testing and Development:** Safe environment for running multiple OSes and configurations.

***

### **Challenges and Considerations**

* **Performance Overhead:** VMs may run slower than native systems.
* **Security Risks:** Shared resources may lead to vulnerabilities if not properly managed.
* **Licensing:** Software licensing can become more complex.
* **Management Complexity:** Requires specialized tools and expertise.

***

### **Virtualisation in Cloud Computing**

Virtualisation is a foundational technology for **cloud computing**, enabling service models like:

* **Infrastructure as a Service (IaaS):** Provisioning virtual machines (e.g., AWS EC2)
* **Platform as a Service (PaaS):** Providing platforms for application deployment
* **Software as a Service (SaaS):** Hosting software for access over the internet

Cloud providers use virtualisation to optimize server usage, provide elasticity, and support multi-tenancy.

***

### **Popular Virtualisation Tools and Platforms**

* **VMware vSphere**
* **Microsoft Hyper-V**
* **KVM (Kernel-based Virtual Machine)**
* **Xen Project**
* **VirtualBox**
* **Docker (for containers)**
* **Proxmox VE**

***

### **Conclusion**

Virtualisation is a transformative technology that enables more agile, cost-effective, and scalable computing. From running multiple operating systems on a single machine to powering the infrastructure of cloud computing, it has become an integral part of modern IT and software development practices.
