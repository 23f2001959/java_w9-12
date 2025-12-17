# 1. Concurrency: Threads and Processes

## What is Concurrency?

Concurrency means **multiple tasks making progress at the same time**.
In Java, concurrency is mainly achieved using **threads**.

---

## Process vs Thread

### Process

* A **process** is an independent program in execution
* Has its **own memory space**
* Heavyweight
* Communication is slow (IPC)

Examples:

* Chrome browser
* VS Code
* Java JVM

---

### Thread

* A **thread** is a lightweight unit inside a process
* Threads **share memory**
* Faster communication
* Less overhead

Java runs multiple threads **inside one JVM process**.

---

## Thread Lifecycle

1. New
2. Runnable
3. Running
4. Blocked / Waiting
5. Terminated

---

## Creating Threads in Java

### Method 1: Extend Thread class

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start(); // NOT run()
    }
}
```

---

### Method 2: Implement Runnable (Preferred)

```java
class Task implements Runnable {
    public void run() {
        System.out.println("Thread running");
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t = new Thread(new Task());
        t.start();
    }
}
```

---

## Why Runnable is Better?

* Java supports **single inheritance**
* Separates **task from thread**

---

## Interview Points

* `start()` creates a new thread
* `run()` is normal method
* Threads share heap memory

---

# 2. Race Conditions

## What is a Race Condition?

A race condition occurs when **multiple threads access shared data**, and the **final result depends on execution order**.

---

## Example of Race Condition

```java
class Counter {
    int count = 0;

    void increment() {
        count++; // NOT atomic
    }
}

public class Main {
    public static void main(String[] args) throws Exception {
        Counter c = new Counter();

        Thread t1 = new Thread(() -> {
            for(int i=0;i<1000;i++) c.increment();
        });

        Thread t2 = new Thread(() -> {
            for(int i=0;i<1000;i++) c.increment();
        });

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        System.out.println(c.count); // may not be 2000
    }
}
```

---

## Why It Happens?

`count++` consists of 3 steps:

1. Read
2. Increment
3. Write

Threads may interleave these steps.

---

## Interview Point

* Race conditions cause **inconsistent results**
* They are **hard to detect**

---

# 3. Mutual Exclusion

## What is Mutual Exclusion?

Mutual exclusion ensures that **only one thread** can access a **critical section** at a time.

---

## Critical Section

Part of code that accesses **shared resources**.

---

## Using synchronized Keyword

### Synchronized Method

```java
class Counter {
    int count = 0;

    synchronized void increment() {
        count++;
    }
}
```

---

### Synchronized Block

```java
void increment() {
    synchronized(this) {
        count++;
    }
}
```

---

## How synchronized Works?

* Uses **monitor lock**
* Only one thread can hold lock
* Other threads wait

---

## Interview Points

* Prevents race conditions
* Can cause performance overhead
* Leads to deadlock if misused

---

# 4. Test and Set

## What is Test and Set?

Test-and-Set is a **low-level atomic operation** used to implement **locks**.

It:

1. Tests a variable
2. Sets it atomically

---

## Conceptual Example (Pseudo Code)

```text
while (testAndSet(lock) == true) {
    // busy waiting
}
critical section
lock = false;
```

---

## Java Equivalent (AtomicBoolean)

```java
import java.util.concurrent.atomic.AtomicBoolean;

class Lock {
    private AtomicBoolean locked = new AtomicBoolean(false);

    void lock() {
        while(locked.getAndSet(true)) {
            // busy wait
        }
    }

    void unlock() {
        locked.set(false);
    }
}
```

---

## Problems with Test and Set

* **Busy waiting** (CPU waste)
* Not fair
* Used in low-level systems

---

## Interview Points

* Atomic operation
* Basis for spinlocks
* Java abstracts it via high-level locks

---

# 5. Monitors

## What is a Monitor?

A monitor is a **high-level synchronization construct** that:

* Ensures mutual exclusion
* Allows threads to wait and notify

---

## Java Monitor

Every Java object has an **intrinsic monitor**.

Used via:

* `synchronized`
* `wait()`
* `notify()`
* `notifyAll()`

---

## Monitor Example (Producer–Consumer)

```java
class Buffer {
    int data;
    boolean available = false;

    synchronized void produce(int value) throws InterruptedException {
        while(available) {
            wait();
        }
        data = value;
        available = true;
        notify();
    }

    synchronized int consume() throws InterruptedException {
        while(!available) {
            wait();
        }
        available = false;
        notify();
        return data;
    }
}
```

---

## How Monitor Works

* `synchronized` → acquire monitor lock
* `wait()` → release lock + sleep
* `notify()` → wake one waiting thread
* `notifyAll()` → wake all

---

## Interview Points

* Monitor = lock + condition
* wait/notify must be inside synchronized block
* Preferred over low-level locking

---

# Quick Comparison Table

| Topic            | Purpose                        |
| ---------------- | ------------------------------ |
| Threads          | Parallel execution             |
| Race Condition   | Data inconsistency             |
| Mutual Exclusion | Prevent conflicts              |
| Test and Set     | Atomic locking                 |
| Monitors         | High-level thread coordination |

---

# One-Line Viva Answers

* **Concurrency**: Multiple tasks executing simultaneously
* **Race condition**: Unpredictable result due to shared data
* **Mutual exclusion**: Only one thread enters critical section
* **Test and set**: Atomic lock mechanism
* **Monitor**: Lock + wait/notify mechanism

---