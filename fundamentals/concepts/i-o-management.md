# I/O Management

### Overview

Input/Output (I/O) Management is the operating system function responsible for controlling and coordinating communication between software and hardware devices.

Examples of I/O devices include:

* Keyboards
* Mice
* Monitors
* Printers
* Network interfaces
* Disk drives
* USB devices

The operating system provides a consistent interface to these devices, hiding hardware-specific details from applications.

Without I/O management, every application would need to understand the low-level details of each hardware device it uses.

> I/O management answers _"How does the process communicate with the outside world?"_

***

### Goals of I/O Management

The primary objectives of I/O management are:

#### Device Independence

Applications should be able to interact with devices through standard interfaces without needing device-specific knowledge.

#### Efficiency

I/O operations are often much slower than CPU and memory operations. The operating system should minimise waiting and maximise throughput.

#### Resource Sharing

Multiple processes may need access to the same device. The operating system coordinates access safely and fairly.

#### Reliability

Errors such as device failures, network interruptions, or media corruption should be detected and handled appropriately.

#### Protection and Security

Processes should only be allowed to access devices they are authorised to use.

***

### I/O Hardware

Most computer systems contain a variety of I/O devices.

These devices generally consist of:

* A physical device
* A device controller
* Device registers
* Device-specific firmware

The device controller acts as the intermediary between the operating system and the hardware.

Examples include:

* Disk controllers
* Network interface controllers (NICs)
* USB controllers
* Graphics controllers

***

### Device Drivers

A device driver is software that allows the operating system to communicate with a specific hardware device.

The driver translates generic operating system requests into device-specific commands.

Responsibilities include:

* Device initialisation
* Reading and writing data
* Error handling
* Interrupt processing

Benefits of device drivers:

* Hardware abstraction
* Device independence
* Easier operating system design

Applications interact with operating system APIs rather than directly with hardware.

***

### Interrupts

Polling hardware continuously is inefficient.

Instead, modern operating systems rely heavily on interrupts.

An interrupt is a signal sent to the CPU indicating that an event requires attention.

Examples include:

* Keyboard key pressed
* Disk read completed
* Network packet received
* Timer expiration

When an interrupt occurs:

1. The CPU completes its current instruction.
2. The current process state is saved.
3. Control transfers to an Interrupt Service Routine (ISR).
4. The ISR handles the event.
5. The previous process resumes execution.

Benefits:

* Efficient CPU usage
* Faster response to events
* Reduced polling overhead

***

### Polling vs Interrupt-Driven I/O

#### Polling

The CPU repeatedly checks device status.

Advantages:

* Simple implementation
* Predictable behaviour

Disadvantages:

* Wastes CPU cycles
* Poor scalability

#### Interrupt-Driven I/O

Devices notify the CPU when attention is required.

Advantages:

* Better CPU utilisation
* More efficient resource usage

Disadvantages:

* More complex implementation

Modern operating systems primarily use interrupt-driven I/O.

***

### Direct Memory Access (DMA)

Without DMA, data transfers require continuous CPU involvement.

With Direct Memory Access (DMA), a device controller can transfer data directly between a device and memory.

DMA operation:

1. CPU configures the DMA controller.
2. DMA transfers data directly.
3. DMA generates an interrupt when complete.

Benefits:

* Reduced CPU overhead
* Faster data transfers
* Improved system performance

DMA is commonly used by:

* Disk controllers
* Network cards
* Graphics devices

***

### Buffering

A buffer is a temporary memory area used during I/O operations.

Buffering helps accommodate differences in speed between devices and processes.

Examples:

* Keyboard input buffers
* Disk read buffers
* Network receive buffers

Benefits:

* Improved performance
* Reduced waiting
* Better device utilisation

***

### Caching

A cache stores frequently accessed data in faster storage.

Examples:

* Disk cache
* File system cache
* Browser cache

Benefits:

* Reduced I/O operations
* Faster data access
* Improved performance

Unlike buffering, which smooths data transfer, caching aims to avoid repeated transfers entirely.

***

### Spooling

Spooling (Simultaneous Peripheral Operations On-Line) allows data destined for a device to be temporarily stored and processed later.

Common example:

* Print queues

Instead of waiting for a printer to become available, processes submit jobs to a spool area.

The operating system later sends jobs to the printer in sequence.

Benefits:

* Improved sharing
* Reduced waiting
* Better device utilisation

***

### Disk Scheduling

Multiple processes may request disk access simultaneously.

The operating system uses disk scheduling algorithms to determine the order of requests.

Common algorithms include:

#### FCFS (First-Come, First-Served)

Processes requests in arrival order.

Simple but inefficient.

#### SSTF (Shortest Seek Time First)

Services the request closest to the current disk head position.

Reduces seek time but may cause starvation.

#### SCAN (Elevator Algorithm)

The disk head moves in one direction servicing requests before reversing direction.

Provides good overall performance.

#### C-SCAN (Circular SCAN)

The disk head services requests in one direction only, then returns to the start.

Provides more uniform waiting times.

***

### I/O Scheduling

Just as CPUs require scheduling, devices often require scheduling.

The operating system may prioritise requests based on:

* Arrival order
* Priority
* Deadline requirements
* Device characteristics

Goals include:

* Fairness
* Throughput
* Low latency
* Efficient device utilisation

***

### Blocking vs Non-Blocking I/O

#### Blocking I/O

The process waits until the I/O operation completes.

Advantages:

* Simple programming model

Disadvantages:

* CPU time may be wasted waiting

#### Non-Blocking I/O

The process continues execution while the I/O operation progresses.

Advantages:

* Better resource utilisation
* Improved scalability

Disadvantages:

* More complex programming

Modern servers frequently use non-blocking and asynchronous I/O.

***

### Synchronous vs Asynchronous I/O

#### Synchronous I/O

The requesting process waits for completion before continuing.

Example:

A process requests a file read and waits for the data.

#### Asynchronous I/O

The process initiates an operation and continues executing.

The operating system later notifies the process when the operation completes.

Asynchronous I/O improves responsiveness and scalability for high-performance applications.

***

### Error Handling

I/O operations can fail for many reasons:

* Device failure
* Network outages
* Disk corruption
* Permission violations
* Hardware faults

The operating system is responsible for:

* Detecting errors
* Reporting failures
* Retrying operations where appropriate
* Protecting data integrity

Robust error handling is essential for system reliability.

***

### Summary

I/O management provides the mechanisms that allow software to communicate with hardware devices efficiently and safely.

Key concepts include:

* Device drivers
* Interrupts
* DMA
* Buffering
* Caching
* Spooling
* Disk scheduling
* Blocking and non-blocking I/O
* Synchronous and asynchronous I/O

Together, these mechanisms allow modern operating systems to manage hardware resources efficiently while providing a consistent interface to applications.
