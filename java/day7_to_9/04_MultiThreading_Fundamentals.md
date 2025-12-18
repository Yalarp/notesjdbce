# Multi-Threading Fundamentals in Java

## Table of Contents
1. [Introduction to Multi-Threading](#introduction-to-multi-threading)
2. [Process vs Thread](#process-vs-thread)
3. [Multi-Tasking Types](#multi-tasking-types)
4. [Thread Schedulers](#thread-schedulers)
5. [Java's Multi-Threading Support](#javas-multi-threading-support)
6. [Creating Threads](#creating-threads)
7. [Thread Lifecycle](#thread-lifecycle)
8. [Thread Methods](#thread-methods)
9. [Complete Examples](#complete-examples)
10. [User Threads vs Daemon Threads](#user-threads-vs-daemon-threads)

---

## Introduction to Multi-Threading

**Multi-Threading** is the ability of a program to execute multiple tasks concurrently within the same process.

### Key Points:
- Java supports **thread-based multitasking**
- Multiple threads can run **seemingly** simultaneously
- Threads **share memory** (unlike processes)
- Essential for server-side Java (Servlets, JSP, etc.)

---

## Process vs Thread

### What is a Process?

**Process** = A program in execution

**Examples:**
- Running Microsoft Word (one process)
- Running Excel (another process)
- Running Chrome browser (another process)

**Characteristics:**
- Each process has its own **memory space**
- Processes **cannot share memory** directly
- **Heavy-weight** (expensive to create and manage)

### What is a Thread?

**Thread** = One part of a program in execution

**Examples:**
- In Microsoft Word:
  - One thread: Typing
  - Another thread: Spell-checking
  - Another thread: Auto-save

**Characteristics:**
- Multiple threads share the **same memory space**
- Threads **can share memory** (variables, objects)
- **Light-weight** (cheaper to create and manage)

---

## Multi-Tasking Types

### Type 1: Process-Based Multitasking

**Definition:** More than one process running simultaneously.

**Example:**
```
Operating System
├─ Word.exe (writing document)
├─ Excel.exe (calculations)
└─ Chrome.exe (browsing)
```

**Characteristics:**
- Each application is a separate process
- Processes have isolated memory
- Context switching between processes is **expensive**

### Type 2: Thread-Based Multitasking

**Definition:** More than one thread running simultaneously within the same process.

**Example:**
```
Word.exe
├─ Thread 1: User typing
├─ Thread 2: Spell-check running
└─ Thread 3: Auto-save running
```

**Characteristics:**
- All threads share same memory space
- Context switching between threads is **cheaper**
- Communication between threads is **easier**

---

## Process-Based vs Thread-Based

| Aspect | Process-Based | Thread-Based |
|--------|---------------|--------------|
| **Memory** | Separate memory space | Shared memory space ✅ |
| **Communication** | Complex (IPC required) | Simple (shared variables) ✅ |
| **Context Switching** | Expensive | Cheaper ✅ |
| **Resource Usage** | Heavy-weight | Light-weight ✅ |
| **Creation Time** | Slower | Faster ✅ |

**Conclusion:** Thread-based multitasking is **more efficient** than process-based.

**Java's Choice:** Java supports **thread-based multitasking**.

---

## Thread Schedulers

### CPU Reality Check

> "Whether process-based or thread-based, a CPU can handle only **one task at a time**, unless it is a multiprocessor machine. It is just an **impression** given to the user. What the CPU actually does is **context switching** - jumping from one task to another and vice-versa."

### Types of Thread Schedulers:

#### 1. **Pre-emptive Scheduling**

**Definition:** High-priority threads interrupt low-priority threads.

**Example:**
```
Low Priority Thread is running...
↓
High Priority Thread arrives
↓
Low Priority Thread is IMMEDIATELY stopped
↓
High Priority Thread executes
↓
After completion, Low Priority resumes
```

**Characteristics:**
- Priority matters
- Starvation possible (low-priority thread may never run)

#### 2. **Time-Slicing Scheduling**

**Definition:** Each thread gets a fixed time slice (quantum).

**Example:**
```
Time Slices (each 100ms):
[Thread 1] → [Thread 2] → [Thread 3] → [Thread 1] → ...
```

**Characteristics:**
- Fair distribution of CPU time
- Priority has less impact
- No starvation

### JVM's Thread Scheduler

**Key Point:** JVM can have **any scheduler** (pre-emptive or time-slice).

**Why?** JVM implementation is **platform-dependent** (different for Windows, Linux, macOS).

**Java's Solution:** Java provides mechanisms (like `yield()`, `sleep()`, `join()`) that work consistently across different schedulers.

---

## Java's Multi-Threading Support

Java's multi-threading relies on three core components:

### 1. `java.lang.Thread` Class

Main class for creating and managing threads.

### 2. `java.lang.Runnable` Interface

```java
public interface Runnable {
    void run();  // Define thread execution body
}
```

### 3. `java.lang.Object` Class

Provides thread communication methods (`wait()`, `notify()`, `notifyAll()`).

---

## Creating Threads

### Four Steps for Multi-Threading Application:

1. **Create thread**/s
2. **Define thread execution body** (run() method)
3. **Register thread** with thread scheduler (start() method)
4. **Thread scheduler executes** the thread/s

### Two Ways to Create Threads:

#### Method 1: Extending `Thread` Class
#### Method 2: Implementing `Runnable` Interface

---

## Thread Methods

From `java.lang.Thread` class:

| Method | Description |
|--------|-------------|
| `void start()` | Register thread with JVM scheduler |
| `void run()` | Thread execution body (override this) |
| `static void sleep(long ms)` | Make thread sleep for specified time |
| `void setName(String name)` | Set thread name |
| `String getName()` | Get thread name |
| `static Thread currentThread()` | Return currently running thread |
| `void setPriority(int priority)` | Set thread priority (1-10) |
| `int getPriority()` | Get thread priority |
| `void join()` | Wait for thread to complete |
| `boolean isDaemon()` | Check if thread is daemon |

### Thread Priorities:

```java
Thread.MIN_PRIORITY  = 1
Thread.NORM_PRIORITY = 5  (default)
Thread.MAX_PRIORITY  = 10
```

> **Important:** Priorities are **not guaranteed** across different platforms!

---

## Complete Examples

### Example 1: Basic Thread Creation (extends Thread)

```java
public class Th1 extends Thread {
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Hello " + i);
        }
    }
    
    public static void main(String args[]) {
        Th1 t1 = new Th1();  // Create thread
        t1.start();          // Register with scheduler
    }
}
```

**Output:**
```
Hello 0
Hello 1
Hello 2
Hello 3
Hello 4
```

**Line-by-Line Analysis:**

1. **Line 1:** `Th1` extends `Thread` class
2. **Line 2:** Override `run()` method - defines what thread will execute
3. **Lines 3-5:** Thread execution body (print "Hello" 5 times)
4. **Line 9:** Create `Th1` object (thread object)
5. **Line 10:** `t1.start()` - **Critical!**
   - Registers thread with JVM scheduler
   - Scheduler will call `run()` method automatically
   - **Does NOT call `run()` directly!**

**How Many Threads?**
- **2 threads:**
  1. **Main thread** (created by JVM, executes `main()`)
  2. **User-defined thread** `t1`

**Call Stacks:**
```
Main Thread Stack          t1 Thread Stack
┌──────────┐              ┌──────────┐
│ main()   │              │ run()    │
└──────────┘              └──────────┘
```

**Important Point:** After `main()` finishes, main thread dies, but user-defined thread continues execution (managed by JVM).

---

### Example 2: Displaying Thread Information

```java
public class Th2 extends Thread {
    public void run() {
        System.out.println(Thread.currentThread());  // Print thread info
        for (int i = 0; i < 5; i++) {
            System.out.println("Hello " + i);
        }
    }
    
    public static void main(String args[]) {
        System.out.println(Thread.currentThread());  // Print main thread info
        Th2 t1 = new Th2();
        t1.setName("first");  // Set thread name
        t1.start();
    }
}
```

**Output:**
```
Thread[main,5,main]           ← Main thread
Thread[first,5,main]          ← User-defined thread
Hello 0
Hello 1
Hello 2
Hello 3
Hello 4
```

**Thread Information Format:**
```
Thread[name, priority, thread-group]
```

**Explanation:**
- **Line 10:** `Thread.currentThread()` returns reference to the currently executing thread
- **Line 12:** `setName("first")` sets thread name to "first"
- Without `setName()`, default name would be "Thread-0", "Thread-1", etc.

---

### Example 3: Can We Call `run()` Directly? (Anti-Pattern)

```java
public class Th3 extends Thread {
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Hello " + i);
        }
    }
    
    public static void main(String args[]) {
        Th3 t1 = new Th3();
        t1.setName("first");
        t1.run();  // Calling run() directly! ⚠️
    }
}
```

**Output:**
```
Hello 0
Hello 1
Hello 2
Hello 3
Hello 4
```

**What Happened?**

**Yes, we can call `run()` directly**, BUT:
- It's **not thread execution**
- It's a **normal method call**
- Executed by **main thread** (not new thread)
- **No separate call stack** created
- **No concurrent execution**

**Comparison:**

```java
t1.start();  // ✅ Creates new thread, concurrent execution
t1.run();    // ❌ No new thread, sequential execution
```

**Call Stacks:**

```
With start():               With run() directly:
Main Thread    t1 Thread    Main Thread Only
┌─────────┐   ┌─────────┐   ┌─────────┐
│ main()  │   │ run()   │   │ main()  │
└─────────┘   └─────────┘   │ run()   │  ← Just method call
                             └─────────┘
```

**Key Learning:** Always use `start()`, never call `run()` directly!

---

### Example 4: Multiple User-Defined Threads

```java
public class Th4 extends Thread {
    public void run() {
        System.out.println(Thread.currentThread());
        for (int i = 0; i < 5; i++) {
            System.out.println("Hello " + i);
        }
    }
    
    public static void main(String args[]) {
        System.out.println(Thread.currentThread());
        Th4 t1 = new Th4();
        Th4 t2 = new Th4();
        t1.setName("first");
        t2.setName("second");
        t1.start();
        t2.start();
    }
}
```

**Possible Output:** (order unpredictable!)
```
Thread[main,5,main]
Thread[first,5,main]
Thread[second,5,main]
Hello 0
Hello 0
Hello 1
Hello 1
Hello 2
Hello 2
Hello 3
Hello 3
Hello 4
Hello 4
```

**How Many Threads?**
- **3 threads:**
  1. Main thread
  2. t1 (named "first")
  3. t2 (named "second")

**Call Stacks:**
```
Main Thread    t1 Thread      t2 Thread
┌─────────┐   ┌─────────┐   ┌─────────┐
│ main()  │   │ run()   │   │ run()   │
└─────────┘   └─────────┘   └─────────┘
```

**Key Point:** **Output order is unpredictable!** Depends on thread scheduler.

---

### Example 5: Thread.sleep() Demo

```java
public class Th4_a extends Thread {
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Hello  " + Thread.currentThread().getName() + "\t" + i);
            try {
                Thread.sleep(100);  // Sleep for 100ms
            } catch (InterruptedException ie) {
                ie.printStackTrace();
            }
        }
    }
    
    public static void main(String args[]) {
        Th4_a t1 = new Th4_a();
        Th4_a t2 = new Th4_a();
        t1.setName("first");
        t2.setName("second");
        t1.start();
        t2.start();
    }
}
```

**Output:**
```
Hello  first    0
Hello  second   0
Hello  first    1
Hello  second   1
Hello  first    2
Hello  second   2
Hello  first    3
Hello  second   3
Hello  first    4
Hello  second   4
```

**Line-by-Line Analysis:**

1. **Line 6:** `Thread.sleep(100)` makes thread sleep for 100 milliseconds
   - Thread goes to **blocked state**
   - After 100ms, thread goes to **runnable state**
   - **Must wrap in try-catch** (throws `InterruptedException`)

2. **Why InterruptedException?**
   - When thread is sleeping, another thread can **interrupt** it
   - If interrupted, `InterruptedException` is thrown
   - Java **forces** you to handle or declare it

**Thread State Transitions:**
```
Running → sleep(100) → Blocked (100ms) → Runnable → Running
```

**Note:** Output shows more alternating pattern due to sleep(), giving scheduler time to switch threads.

---

### Example 6: implements Runnable

```java
public class Th5 implements Runnable {
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Hello " + i);
        }
    }
    
    public static void main(String args[]) {
        Th5 ob = new Th5();           // Create Runnable object
        Thread t1 = new Thread(ob);   // Pass to Thread constructor
        Thread t2 = new Thread(ob);   // Same Runnable, different Thread
        t1.start();
        t2.start();
    }
}
```

**Output:**
```
Hello 0
Hello 0
Hello 1
Hello 1
Hello 2
Hello 2
Hello 3
Hello 3
Hello 4
Hello 4
```

**Steps for `implements Runnable`:**

1. **Line 1:** Define class that implements `Runnable`
2. **Line 2:** Override `run()` method
3. **Line 9:** Create instance of Runnable class
4. **Lines 10-11:** Create `Thread` objects, passing Runnable instance
5. **Lines 12-13:** Call `start()` on Thread objects

**Why Two Thread Objects But One Runnable?**
- `ob` is the **shared Runnable** (defines the task)
- `t1` and `t2` are **separate threads** (execute the task)
- Both threads execute the **same run() method**

**How Thread and Runnable are Related:**
```java
public class Thread implements Runnable {
    // Thread class implements Runnable interface!
}
```

**Key Learning:** Thread class itself implements Runnable!

---

### `extends Thread` vs `implements Runnable`

| Aspect | extends Thread | implements Runnable |
|--------|----------------|---------------------|
| **Inheritance** | Uses up single inheritance | Class can extend another class ✅ |
| **Flexibility** | Less flexible | More flexible ✅ |
| **Code Reusability** | Thread and task coupled | Thread and task separated ✅ |
| **Use Case** | Simple scenarios | When class already extends another class |

**When to Use `implements Runnable`?**

```java
class MyClass extends SomeOtherClass {
    // Already extending another class
    // Can't use "extends Thread" (multiple inheritance not allowed)
    // MUST use "implements Runnable"
}
```

**Best Practice:** Prefer `implements Runnable` for better design (separation of concerns).

---

## Thread Lifecycle

### Thread States:

```
Born → Runnable → Running → Dead
         ↓           ↑
         Blocked ←───┘
```

#### 1. **Born (New)**
```java
Thread t = new Thread();  // Thread created but not started
```

#### 2. **Runnable** (Ready to run)
```java
t.start();  // Thread registered with scheduler, waiting for CPU
```

#### 3. **Running**
- Thread is executing (`run()` method executing)

#### 4. **Blocked** (Waiting)
Caused by:
- `sleep(ms)` → Timed waiting
- `wait()` → Waiting for notification
- `join()` → Waiting for another thread
- I/O operation

#### 5. **Dead** (Terminated)
- `run()` method completes
- Unhandled exception occurs

**Diagram:**
```
new Thread()
    ↓
  [Born]
    ↓
  start()
    ↓
 [Runnable] ←──────────────┐
    ↓                       │
Scheduler picks            │
    ↓                       │
[Running] ──→ run() ends → [Dead]
    ↓
sleep/wait/join
    ↓
 [Blocked]
    ↓
timeout/notify/join completes
    ↓
    └────────────────────→ [Runnable]
```

---

## User Threads vs Daemon Threads

### User Threads

**Definition:** Normal threads created by programmer or main thread.

**Examples:**
- Main thread
- Threads you create with `new Thread()`

**Characteristics:**
- JVM waits for user threads to complete
- JVM **does not exit** until all user threads finish

### Daemon Threads

**Definition:** Low-priority background threads that provide services to user threads.

**Examples:**
- Garbage Collection thread
- Finalizer thread

**Characteristics:**
- JVM **does not wait** for daemon threads
- JVM **terminates daemon threads** when all user threads finish
- Automatically terminated when program ends

**Making a Thread Daemon:**
```java
Thread t = new Thread();
t.setDaemon(true);  // Must be called BEFORE start()
t.start();
```

**Checking if Thread is Daemon:**
```java
boolean isDaemon = t.isDaemon();
```

### Example: Garbage Collection is Daemon Thread

```java
public class Sample {
    public static void main(String[] args) {
        Sample s1 = new Sample();
        s1 = null;  // Object eligible for GC
        System.gc();  // Request garbage collection
        
        try {
            Thread.sleep(100);  // Give GC time to run
        } catch (InterruptedException ie) {
            ie.printStackTrace();
        }
        
        System.out.println("Main function executed by\t" + 
                           Thread.currentThread().getName());
    }
    
    protected void finalize() {
        System.out.println("inside finalized method");
        System.out.println("finalize method invoked by\t" + 
                           Thread.currentThread());
        System.out.println(Thread.currentThread().isDaemon());
    }
}
```

**Output:**
```
inside finalized method
finalize method invoked by      Thread[Finalizer,8,system]
true
Main function executed by       main
```

**Explanation:**

1. **Line 4:** Object becomes eligible for garbage collection
2. **Line 5:** `System.gc()` suggests JVM to run garbage collection
3. **Line 18:** `finalize()` method called by **Finalizer thread**
4. **Line 22:** `isDaemon()` returns `true` → Finalizer is daemon thread

**Key Learning:** Garbage collection runs in a daemon thread.

---

## join() Method

### Problem: Main Thread Completes First

```java
public class Th9 implements Runnable {
    public void run() {
        synchronized(this) {
            for (int i = 0; i < 5; i++) {
                System.out.println("Hello " + i);
            }
        }
    }
    
    public static void main(String args[]) {
        Th9 ob = new Th9();
        Thread t1 = new Thread(ob);
        Thread t2 = new Thread(ob);
        t1.start();
        t2.start();
        
        System.out.println("Both threads are over");  // ⚠️ Printed immediately!
    }
}
```

**Problem:** "Both threads are over" is printed **before** threads actually complete!

**Why?** Main thread completes its execution before t1 and t2 finish.

### Solution: join() Method

```java
public class Th9_a implements Runnable {
    public void run() {
        synchronized(this) {
            for (int i = 0; i < 5; i++) {
                System.out.println("Hello " + i);
            }
        }
    }
    
    public static void main(String args[]) {
        Th9 ob = new Th9();
        Thread t1 = new Thread(ob);
        Thread t2 = new Thread(ob);
        t1.start();
        t2.start();
        
        try {
            t1.join();  // Main thread waits for t1 to complete
            t2.join();  // Main thread waits for t2 to complete
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        System.out.println("Both threads are over");  // ✅ Printed at the end!
    }
}
```

**How join() Works:**

```
Main Thread: t1.join()
↓
Main thread says: "Join me at your end, t1"
↓
Main thread waits for t1 to complete
↓
t1 completes
↓
Main thread resumes
↓
Main thread: t2.join()
↓
Main thread waits for t2 to complete
↓
t2 completes
↓
Main thread resumes
↓
Print "Both threads are over"
```

**join() Variations:**
```java
t1.join();         // Wait indefinitely
t1.join(1000);     // Wait max 1000ms
t1.join(1000, 500000); // Wait max 1000ms and 500000ns
```

---

## Summary Table

| Concept | Description |
|---------|-------------|
| **Multi-Threading** | Multiple threads executing concurrently |
| **Process** | Program in execution (isolated memory) |
| **Thread** | Part of program in execution (shared memory) |
| **extends Thread** | One way to create thread |
| **implements Runnable** | Another way to create thread (preferred) |
| **start()** | Register thread with scheduler |
| **run()** | Thread execution body |
| **sleep(ms)** | Block thread for specified time |
| **join()** | Wait for thread to complete |
| **User Thread** | Normal thread (JVM waits for it) |
| **Daemon Thread** | Background thread (JVM doesn't wait) |

---

## Key Takeaways

1. **Thread-based multitasking is lighter than process-based**
2. **Two ways to create threads:** extends Thread or implements Runnable
3. **Always call start(), never run() directly**
4. **Thread.currentThread()** returns currently executing thread
5. **sleep()** blocks thread for specified time
6. **join()** makes caller thread wait for called thread
7. **Daemon threads** are background threads terminated when user threads finish
8. **InterruptedException** must be handled for sleep/join/wait
9. **JVM continues running until all user threads complete** (daemon threads ignored)
10. **Thread priorities (1-10) are not guaranteed** across platforms

---

## Interview Questions

### Q1: What is the difference between a process and a thread?
**A:** Process is an independent program with separate memory. Thread is a part of a process that shares memory with other threads. Threads are lighter and faster to create than processes.

### Q2: What are the two ways to create a thread in Java?
**A:** 
1. Extend Thread class and override run() method
2. Implement Runnable interface and implement run() method

### Q3: What is the difference between start() and run()?
**A:** start() creates a new thread and makes scheduler call run(). Calling run() directly is just a normal method call, no new thread is created.

### Q4: Why does sleep() throw InterruptedException?
**A:** When a thread is sleeping, another thread can interrupt it. If interrupted, InterruptedException is thrown. Java forces handling because this can happen unpredictably.

### Q5: What is a daemon thread?
**A:** A background thread that provides services to user threads. JVM does not wait for daemon threads to complete - they are automatically terminated when all user threads finish. Example: Garbage collection thread.

### Q6: What does join() method do?
**A:** Makes the caller thread wait for the called thread to complete. Example: `t1.join()` makes current thread wait until t1 finishes.

### Q7: Why prefer implements Runnable over extends Thread?
**A:** Because Java doesn't support multiple inheritance. If your class already extends another class, you can't extend Thread. Implementing Runnable gives more flexibility and better separation of task from thread.

---

**End of Multi-Threading Fundamentals Notes**
