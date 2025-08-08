# Event-Driven

### Overview

In event-driven systems, the program typically runs an event loop that listens for incoming events. When an event occurs, the loop invokes the corresponding event handler—a procedure or method registered to process that event. This inversion of control (“the Hollywood Principle”: “Don’t call us, we’ll call you”) decouples event detection from event handling and allows highly interactive, asynchronous, or distributed applications.

#### Key Characteristics

* **Event Loop**\
  A central dispatcher continuously polls or waits for events and routes them to handlers.
* **Callbacks / Handlers**\
  Named functions or methods registered to execute when specific events occur.
* **Asynchronicity**\
  Handlers may run concurrently or be queued, enabling responsive interfaces without blocking.
* **Loose Coupling**\
  Producers of events need not know which handlers will respond, promoting modular design.
* **Event Abstraction**\
  Events are often encapsulated as objects or messages carrying relevant data.

***

### Categories of Event-Driven Paradigms

1. **GUI Programming**\
   User-interface frameworks dispatch mouse, keyboard, and window events.
   * _Examples:_ Java Swing/AWT, Qt, HTML / DOM events in browsers
2. **Server-Side Event Handling**\
   Network servers handle incoming connections, requests, or messages.
   * _Examples:_ Node.js’s `EventEmitter`, Python’s `asyncio`, Java’s NIO callback APIs
3. **Publish–Subscribe (Pub/Sub)**\
   Components publish messages to topics; multiple subscribers react independently.
   * _Examples:_ MQTT, Apache Kafka, Redis Pub/Sub
4. **Reactive Streams & Dataflow**\
   Streams of data trigger pipelines of processing stages.
   * _Examples:_ ReactiveX (RxJS, RxJava), Apache Beam
5. **Hardware / Embedded Systems**\
   Interrupt-driven code responds to hardware signals or timers.
   * _Examples:_ Microcontroller ISR routines, Linux kernel interrupt handlers

***

### Comparison with Other Paradigms

| Aspect         | Event-Driven                                 | Imperative                 | Declarative                  |
| -------------- | -------------------------------------------- | -------------------------- | ---------------------------- |
| Control Flow   | Driven by events, asynchronous callbacks     | Linear, step-by-step       | Specified outcomes, abstract |
| Coupling       | Loose (via events/messages)                  | Tighter (direct calls)     | Varies, often high-level     |
| Concurrency    | Natural via non-blocking handlers            | Explicit threads/locks     | Handled by runtime           |
| Predictability | Can be harder to trace due to asynchronicity | Generally easier to follow | High-level reasoning         |
| Suitability    | Interactive, real-time, distributed apps     | CPU-bound, batch tasks     | Data querying, configuration |

***

### History

Event-driven concepts have roots in early GUI systems of the 1970s and 1980s (e.g., Smalltalk’s MVC and MacApp). Hardware interrupt handlers date back to first operating systems managing I/O devices. The rise of graphical user interfaces (Windows, X11) cemented the event loop model for desktop applications. In the 2000s, server-side JavaScript (Node.js, 2009) popularized non-blocking I/O and event emitters for scalable network services. Modern reactive and IoT platforms have extended event-driven designs into data streaming and distributed messaging.

***

### Advantages

* **Responsiveness**\
  Interfaces and services remain reactive under high I/O loads by avoiding blocking operations.
* **Modularity**\
  Handlers can be added or removed without altering event sources.
* **Scalability**\
  Non-blocking, asynchronous dispatch supports many concurrent connections or inputs.
* **Flexibility**\
  Easily integrates diverse event sources (UI, network, timers, sensors).

### Disadvantages

* **Complexity of Flow**\
  Callback chains and asynchronous logic can lead to “callback hell” or “pyramid of doom.”
* **Debugging Challenges**\
  Tracing the sequence and timing of events often requires specialized tooling or logging.
* **State Management**\
  Shared state across handlers can lead to race conditions if not carefully synchronized.
* **Latency Jitter**\
  Events may queue unpredictably, causing variable response times.

***

### Examples

#### JavaScript (Browser DOM)

```javascript
document.getElementById('btn').addEventListener('click', function(evt) {
  alert('Button clicked at ' + evt.timeStamp);
});
```

#### Node.js (Server-Side)

```javascript
const http = require('http');
const server = http.createServer((req, res) => {
  // 'request' event handler
  res.end('Hello, world!');
});
server.listen(8080);
```
