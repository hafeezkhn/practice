# 🧠 C++ Architecture & Design Cheatsheet 

A full reference covering modern C++, design patterns, synchronization, IPC, embedded system use cases, and advanced system design topics.

---

## 🧠 Design and Architecture Models to Study

### 🎯 Software Architecture Models

* Layered Architecture
* Hexagonal (Ports and Adapters)
* Clean Architecture (Onion)
* Microkernel (Plug-in Architecture)
* Reactive Systems (Actor Model)
* Publisher-Subscriber Systems
* Event-driven Architectures
* CQRS (Command Query Responsibility Segregation)

### 🎯 Embedded Systems Models

* Control-Loop Model (Periodic Sampling)
* Real-Time Finite State Machine (FSM)
* Task Scheduling Models (Round-robin, RTOS)
* Event-driven Embedded Systems
* Sensor Fusion Models (Kalman Filter, Complementary Filter)

---

## 🧱 Composite Pattern & Smart Pointers

### Why use `std::shared_ptr` in Composite Pattern?

* Manages lifetime of components in a tree-like structure.
* Allows shared ownership of nodes, enabling reuse.

### When should `std::weak_ptr` be used?

* To avoid cyclic references (e.g., child holding a back-reference to parent).

### Can `unique_ptr` be used in Composite Pattern?

* Yes, if ownership is strictly hierarchical and components are not shared.

### Best Practice:

* Use `unique_ptr` where possible.
* Use `shared_ptr` with `weak_ptr` to handle shared and non-owning relationships.

---

## ❓ Conceptual Q\&A

### 🔁 Why not use `lock()` and `unlock()` directly in C++?

**Answer**: Prefer RAII like `std::lock_guard` or `std::unique_lock` to avoid deadlocks and make code exception-safe.

### 🔄 Composite Pattern and Smart Pointers

* `shared_ptr`: automatic memory management.
* `weak_ptr`: break ownership cycles.
* `unique_ptr`: strict ownership.
* Smart pointers embody RAII.

### Smart Pointer Impact on Copy/Assignment

* `shared_ptr`: shared ownership.
* `unique_ptr`: move-only semantics.

### Which Design Patterns Leverage Smart Pointers?

* Composite, Observer, Factory, Decorator.

### What is RAII and why is it critical?

* Resource Acquisition Is Initialization: resources (locks, memory, files) are acquired and released by objects' lifetime, ensuring exception safety and no leaks.

### How does Dependency Inversion relate to testability?

* High-level modules depend on abstractions, making components easily mockable during testing.

### Why prefer interfaces over inheritance?

* Interfaces promote composition over inheritance, reducing tight coupling and supporting better modularity.

### Difference between Observer and Callback?

* Observer: multiple subscribers notified via publisher.
* Callback: single function called when event occurs.

### When to choose Strategy vs State pattern?

* Strategy: interchangeable algorithms at runtime.
* State: object changes behavior as its internal state changes.

### Factory vs Abstract Factory?

* Factory: creates one product.
* Abstract Factory: creates families of related products.

---

## ⚙️ Advanced Modern C++ Concepts

* Move Semantics (`std::move`, `&&`)
* Lambda Expressions, `std::function`
* RAII for safety
* `constexpr`, `noexcept`, `decltype`, `auto`
* Ranges/Views (C++20)
* Coroutines (C++20)
* Concepts (C++20)
* Modules (C++20)

---

## 🏛️ SOLID Principles

| Principle             | Description                                 |
| --------------------- | ------------------------------------------- |
| Single Responsibility | Each class does one thing                   |
| Open/Closed           | Open for extension, closed for modification |
| Liskov Substitution   | Subtypes replace base types                 |
| Interface Segregation | Small, specific interfaces                  |
| Dependency Inversion  | Depend on abstractions                      |

---

## 🧠 Design Patterns Summary

| Type       | Patterns                                     |
| ---------- | -------------------------------------------- |
| Creational | Factory, Builder, Singleton                  |
| Structural | Composite, Adapter, Decorator, Proxy         |
| Behavioral | Observer, Strategy, Command, State, Mediator |

**Additional Patterns to Study**:

* Visitor
* Chain of Responsibility
* Flyweight
* Prototype
* Bridge

---

## 🔗 IPC Mechanisms

### UNIX Domain & TCP Sockets

* `send()`, `recv()`, client-server communication.

### Named Pipes (FIFOs)

* Persistent file-based IPC.

### Shared Memory (`mmap`, `shmget`)

* Fast, zero-copy memory sharing.

### Message Queues

* POSIX, SysV queues.

### Signals & Semaphores

* Lightweight signaling mechanisms.

---

## 🌐 Inter-Node Communication

| Mechanism      | Use Case                            |
| -------------- | ----------------------------------- |
| TCP/IP Sockets | Peer-to-peer communication          |
| gRPC           | Remote procedure calls              |
| ZeroMQ         | Lightweight pub-sub messaging       |
| DDS            | Real-time pub-sub for robotics/ADAS |
| MQTT           | IoT lightweight messaging           |
| REST           | Web service communication           |

**Important Topics**:

* Serialization: Protobuf, JSON, FlatBuffers
* Secure channels: TLS, mTLS
* Heartbeats, retries, and QoS for distributed systems

---

## 🕹️ Synchronization Models

### 1️⃣ Wait-and-Send (Condition Variable)

```cpp
std::mutex mtx;
std::condition_variable cv;
bool data_ready = false;

void producer() {
    std::lock_guard<std::mutex> lock(mtx);
    data_ready = true;
    cv.notify_one();
}

void consumer() {
    std::unique_lock<std::mutex> lock(mtx);
    cv.wait(lock, [] { return data_ready; });
}
```

### 2️⃣ Callback (Asynchronous Event)

```cpp
void onDataReceived(const std::string& data) {
    std::cout << "Received: " << data << std::endl;
}

void asyncReceive(std::function<void(std::string)> callback) {
    std::this_thread::sleep_for(std::chrono::seconds(2));
    callback("Sensor Data");
}

int main() {
    asyncReceive(onDataReceived);
}
```

### Summary Table

| Feature     | Wait-and-Send      | Callback      |
| ----------- | ------------------ | ------------- |
| Blocking    | Yes                | No            |
| Trigger     | Condition Met      | Event Occurs  |
| Usage       | Thread Sync        | Event Systems |
| Complexity  | Lower              | Higher        |
| Performance | CPU Waste Possible | CPU Efficient |

---

## 🔖 Additional Study Topics

### System Design Topics:

* Resource Constrained Architectures (Embedded Edge)
* Real-Time Scheduling (Priority Inversion, Deadlines)
* Safety-Critical Software (ISO 26262)
* Multicore Synchronization (lock-free queues, atomic ops)
* Linux Device Drivers (Udev, Sysfs, Kernel IPC)
* Debugging Techniques (GDB, Valgrind, Trace32)

### References

* "Effective Modern C++" — Scott Meyers
* "C++ Concurrency In Action" — Anthony Williams
* "Design Patterns" — Gamma et al.
* "Real-Time Concepts for Embedded Systems" — Qing Li
* POSIX IEEE 1003 Standard
* AUTOSAR Software Architecture

---

🧑‍💻 Created by **Hafiz – [Programmical](https://github.com/hafeezkhn)**
🎯 For embedded developers, system programmers, and C++ software architects.
