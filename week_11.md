# 1. Monitoring (in Java Concurrency)

## What is Monitoring?

In Java, **monitoring** refers to **controlling and coordinating access to shared resources** by multiple threads to ensure:

* Mutual exclusion
* Safe communication between threads

Java implements monitoring using **monitors** (built-in to every object).

---

## Java Monitor

A **monitor** is a synchronization mechanism that consists of:

1. A **lock (mutex)**
2. **Condition variables** (`wait`, `notify`, `notifyAll`)

Every Java object has an **intrinsic monitor lock**.

---

## Keywords Used in Monitoring

* `synchronized`
* `wait()`
* `notify()`
* `notifyAll()`

---

## Example: Monitoring with synchronized

```java
class SharedResource {
    synchronized void access() {
        System.out.println(Thread.currentThread().getName() + " entered");
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {}
        System.out.println(Thread.currentThread().getName() + " exited");
    }
}
```

Only **one thread** can execute `access()` at a time.

---

## wait() and notify()

```java
synchronized(obj) {
    obj.wait();   // releases lock and waits
    obj.notify(); // wakes up waiting thread
}
```

---

## Interview Points

* wait/notify must be inside synchronized block
* wait releases lock, sleep does not
* notify wakes one thread, notifyAll wakes all

---

# 2. Thread

## What is a Thread?

A **thread** is the **smallest unit of execution** within a process.

Java uses **multithreading** to perform multiple tasks concurrently.

---

## Thread Lifecycle

1. New
2. Runnable
3. Running
4. Waiting / Blocked
5. Terminated

---

## Creating Threads in Java

### Method 1: Extending Thread Class

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running");
    }
}
```

---

### Method 2: Implementing Runnable (Preferred)

```java
class MyTask implements Runnable {
    public void run() {
        System.out.println("Thread running");
    }
}
```

---

## Important Thread Methods

| Method        | Description      |
| ------------- | ---------------- |
| `start()`     | Starts thread    |
| `run()`       | Task logic       |
| `sleep()`     | Pause execution  |
| `join()`      | Wait for thread  |
| `interrupt()` | Interrupt thread |

---

## Interview Points

* `start()` creates new thread
* `run()` is normal method
* Threads share heap memory

---

# 3. Concurrent Programming

## What is Concurrent Programming?

Concurrent programming allows **multiple tasks to progress at the same time** by:

* Using multiple threads
* Managing shared resources safely

---

## Problems in Concurrent Programming

* Race conditions
* Deadlocks
* Starvation
* Inconsistent data

---

## Example of Concurrent Programming

```java
class Task implements Runnable {
    public void run() {
        System.out.println(Thread.currentThread().getName());
    }
}

public class Main {
    public static void main(String[] args) {
        for(int i=0;i<5;i++) {
            new Thread(new Task()).start();
        }
    }
}
```

---

## Java Concurrency Tools

* `synchronized`
* `volatile`
* `Locks`
* `Executors`
* `Atomic classes`

---

## Executor Framework Example

```java
ExecutorService executor = Executors.newFixedThreadPool(3);
executor.submit(() -> System.out.println("Task executed"));
executor.shutdown();
```

---

## Interview Points

* Concurrency improves performance
* Harder to debug than sequential code
* Requires synchronization

---

# 4. Thread-Safe Collections

## What is Thread-Safe Collection?

A thread-safe collection allows **multiple threads to access it safely** without data corruption.

---

## Non-Thread-Safe Collections

* ArrayList
* HashMap
* HashSet

---

## Thread-Safe Collection Types

### 1. Legacy Synchronized Collections

* `Vector`
* `Hashtable`

(Older, slow)

---

### 2. Synchronized Wrapper Collections

```java
List<Integer> list =
    Collections.synchronizedList(new ArrayList<>());
```

---

### 3. Concurrent Collections (Recommended)

| Collection              | Description         |
| ----------------------- | ------------------- |
| `ConcurrentHashMap`     | Thread-safe Map     |
| `CopyOnWriteArrayList`  | Safe list for reads |
| `CopyOnWriteArraySet`   | Safe set            |
| `ConcurrentLinkedQueue` | Non-blocking queue  |

---

## Example: ConcurrentHashMap

```java
ConcurrentHashMap<Integer, String> map =
    new ConcurrentHashMap<>();

map.put(1, "Java");
map.put(2, "Spring");
```

---

## Why Concurrent Collections Are Better?

* Fine-grained locking
* High performance
* No full blocking

---

## Interview Points

* ConcurrentHashMap allows concurrent reads/writes
* No `ConcurrentModificationException`
* Preferred over synchronized collections

---

# Comparison Table

| Topic                  | Purpose                 |
| ---------------------- | ----------------------- |
| Monitoring             | Thread coordination     |
| Thread                 | Execution unit          |
| Concurrent Programming | Parallel task execution |
| Thread-Safe Collection | Safe shared data        |

---

# One-Line Viva Answers

* **Monitoring**: Controls thread access using locks
* **Thread**: Smallest execution unit
* **Concurrency**: Multiple tasks executing together
* **Thread-safe collection**: Safe for multi-thread access

---