# Advanced Threading: Executors Framework

## Table of Contents
1. [Introduction to Thread Pools](#introduction-to-thread-pools)
2. [Problem with Manual Thread Management](#problem-with-manual-thread-management)
3. [What is Executor Framework?](#what-is-executor-framework)
4. [ExecutorService Interface](#executorservice-interface)
5. [Types of Thread Pools](#types-of-thread-pools)
6. [Complete Examples](#complete-examples)
7. [Callable and Future](#callable-and-future)
8. [Executor Lifecycle](#executor-lifecycle)

---

## Introduction to Thread Pools

**Thread Pool** = A collection of pre-created, reusable threads ready to execute tasks.

### Advantages:
✅ **Reuse threads** → Avoid creation/destruction overhead  
✅ **Control resource usage** → Limit number of concurrent threads  
✅ **Better performance** → Threads are ready to work  
✅ **Simplified management** → Framework handles thread lifecycle  

---

## Problem with Manual Thread Management

### Without Thread Pool:

```java
// Bad Practice: Creating new thread for each task
for (int i = 0; i < 1000; i++) {
    Thread t = new Thread(new Task());
    t.start();  // Creating 1000 threads!
}
```

**Problems:**
1. **Memory overhead** → Each thread consumes memory (stack space)
2. **CPU overhead** → Creating/destroying threads is expensive
3. **No limit** → Can create too many threads, crash system
4. **No reusability** → Thread dies after task completes

### With Thread Pool:

```java
// Good Practice: Using thread pool
ExecutorService executor = Executors.newFixedThreadPool(10);
for (int i = 0; i < 1000; i++) {
    executor.submit(new Task());  // Reusing 10 threads!
}
```

**Benefits:**
1. **Only 10 threads** created and reused for 1000 tasks
2. **Memory efficient** → Fixed memory footprint
3. **Better CPU utilization** → No creation/destruction overhead
4. **Automatic management** → Framework handles everything

---

## What is Executor Framework?

The **Executor framework** (java.util.concurrent) provides high-level APIs for thread management.

### Core Components:

#### 1. `Executor` Interface
```java
public interface Executor {
    void execute(Runnable command);
}
```

#### 2. `ExecutorService` Interface (extends Executor)
```java
public interface ExecutorService extends Executor {
    <T> Future<T> submit(Callable<T> task);
    Future<?> submit(Runnable task);
    void shutdown();
    List<Runnable> shutdownNow();
    boolean isShutdown();
    boolean isTerminated();
    // ... more methods
}
```

#### 3. `Executors` Class (Factory)
```java
public class Executors {
    public static ExecutorService newFixedThreadPool(int nThreads)
    public static ExecutorService newCachedThreadPool()
    public static ExecutorService newSingleThreadExecutor()
    public static ScheduledExecutorService newScheduledThreadPool(int corePoolSize)
}
```

---

## ExecutorService Interface

**ExecutorService** is the main interface for thread pool management.

### Key Methods:

| Method | Description |
|--------|-------------|
| `submit(Runnable task)` | Submit task, returns Future |
| `submit(Callable<T> task)` | Submit task that returns result |
| `shutdown()` | Graceful shutdown (waits for tasks to complete) |
| `shutdownNow()` | Immediate shutdown (attempts to stop tasks) |
| `isShutdown()` | Check if shutdown was called |
| `isTerminated()` | Check if all tasks completed after shutdown |
| `awaitTermination(timeout, unit)` | Wait for termination |

---

## Types of Thread Pools

### 1. Fixed Thread Pool

```java
ExecutorService executor = Executors.newFixedThreadPool(5);
```

**Characteristics:**
- **Fixed number of threads** (5 in this case)
- If all threads are busy, tasks wait in queue
- Threads are reused

**Use Case:** When you know the optimal number of threads

**Diagram:**
```
Task Queue: [Task6, Task7, Task8, ...]
    ↓
Thread Pool (5 threads)
├─ Thread 1 → executing Task1
├─ Thread 2 → executing Task2
├─ Thread 3 → executing Task3
├─ Thread 4 → executing Task4
└─ Thread 5 → executing Task5
```

### 2. Cached Thread Pool

```java
ExecutorService executor = Executors.newCachedThreadPool();
```

**Characteristics:**
- **Creates threads as needed**
- Reuses idle threads (idle for 60 seconds)
- **No limit** on number of threads (can grow unbounded)

**Use Case:** Many short-lived tasks

**Warning:** Can create too many threads if tasks are long-running!

### 3. Single Thread Executor

```java
ExecutorService executor = Executors.newSingleThreadExecutor();
```

**Characteristics:**
- **Only one thread**
- Tasks execute sequentially
- Guarantees order of execution

**Use Case:** Tasks must execute in order

### 4. Scheduled Thread Pool

```java
ScheduledExecutorService executor = Executors.newScheduledThreadPool(3);
```

**Characteristics:**
- Can **schedule tasks** to run after delay
- Can schedule **periodic tasks**

**Additional Methods:**
- `schedule(task, delay, unit)` → Run once after delay
- `scheduleAtFixedRate(task, initialDelay, period, unit)` → Run periodically
- `scheduleWithFixedDelay(task, initialDelay, delay, unit)` → Run with delay between executions

---

## Complete Examples

### Example 1: Basic ExecutorService Usage

```java
import java.util.concurrent.*;

class MyTask implements Runnable {
    private int taskId;
    
    public MyTask(int id) {
        this.taskId = id;
    }
    
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName() + 
                         " is executing Task-" + taskId);
        try {
            Thread.sleep(2000);  // Simulate work
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("Task-" + taskId + " completed");
    }
}

public class ExecutorDemo1 {
    public static void main(String[] args) {
        // Create thread pool with 3 threads
        ExecutorService executor = Executors.newFixedThreadPool(3);
        
        // Submit 6 tasks
        for (int i = 1; i <= 6; i++) {
            executor.submit(new MyTask(i));
        }
        
        // Shutdown executor
        executor.shutdown();
    }
}
```

**Output:**
```
pool-1-thread-1 is executing Task-1
pool-1-thread-2 is executing Task-2
pool-1-thread-3 is executing Task-3
Task-1 completed
pool-1-thread-1 is executing Task-4
Task-2 completed
pool-1-thread-2 is executing Task-5
Task-3 completed
pool-1-thread-3 is executing Task-6
Task-4 completed
Task-5 completed
Task-6 completed
```

**Execution Flow:**

1. **Executor created** with 3 threads
2. **First 3 tasks** (1, 2, 3) execute immediately on 3 threads
3. **Tasks 4, 5, 6** wait in queue
4. **When Task-1 completes**, thread-1 picks up Task-4
5. **When Task-2 completes**, thread-2 picks up Task-5
6. **When Task-3 completes**, thread-3 picks up Task-6

**Key Learning:** Only 3 threads created for 6 tasks!

---

### Example 2: newCachedThreadPool()

```java
public class ExecutorDemo2 {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newCachedThreadPool();
        
        for (int i = 1; i <= 10; i++) {
            executor.submit(new MyTask(i));
        }
        
        executor.shutdown();
    }
}
```

**Output:**
```
pool-1-thread-1 is executing Task-1
pool-1-thread-2 is executing Task-2
pool-1-thread-3 is executing Task-3
pool-1-thread-4 is executing Task-4
pool-1-thread-5 is executing Task-5
pool-1-thread-6 is executing Task-6
pool-1-thread-7 is executing Task-7
pool-1-thread-8 is executing Task-8
pool-1-thread-9 is executing Task-9
pool-1-thread-10 is executing Task-10
...
```

**Key Learning:** Cached pool creates **new thread for each task** if no idle thread available!

---

### Example 3: newSingleThreadExecutor()

```java
public class ExecutorDemo3 {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newSingleThreadExecutor();
        
        for (int i = 1; i <= 5; i++) {
            executor.submit(new MyTask(i));
        }
        
        executor.shutdown();
    }
}
```

**Output:**
```
pool-1-thread-1 is executing Task-1
Task-1 completed
pool-1-thread-1 is executing Task-2
Task-2 completed
pool-1-thread-1 is executing Task-3
Task-3 completed
pool-1-thread-1 is executing Task-4
Task-4 completed
pool-1-thread-1 is executing Task-5
Task-5 completed
```

**Key Learning:** All tasks execute **sequentially on same thread**!

---

### Example 4: ScheduledExecutorService

```java
import java.util.concurrent.*;

public class ExecutorDemo4 {
    public static void main(String[] args) {
        ScheduledExecutorService executor = Executors.newScheduledThreadPool(2);
        
        // Schedule task to run after 3 seconds
        executor.schedule(() -> {
            System.out.println("Task executed after 3 seconds");
        }, 3, TimeUnit.SECONDS);
        
        // Schedule task to run every 2 seconds
        executor.scheduleAtFixedRate(() -> {
            System.out.println("Periodic task: " + System.currentTimeMillis());
        }, 0, 2, TimeUnit.SECONDS);
        
        // Don't shutdown immediately - let tasks run
        // After some time, you can shutdown
    }
}
```

**Output:**
```
Periodic task: 1234567890123
Periodic task: 1234567892123
Task executed after 3 seconds
Periodic task: 1234567894123
Periodic task: 1234567896123
...
```

**Methods:**
- `schedule(task, 3, SECONDS)` → Run once after 3 seconds
- `scheduleAtFixedRate(task, 0, 2, SECONDS)` → Run every 2 seconds (fixed rate)
- `scheduleWithFixedDelay(task, 0, 2, SECONDS)` → 2 second delay between executions

---

## Callable and Future

### Runnable vs Callable

**Runnable:**
```java
public interface Runnable {
    void run();  // Returns nothing
}
```

**Callable:**
```java
public interface Callable<V> {
    V call() throws Exception;  // Returns a value
}
```

### Using Callable

```java
import java.util.concurrent.*;

class MyCallable implements Callable<Integer> {
    private int num;
    
    public MyCallable(int num) {
        this.num = num;
    }
    
    @Override
    public Integer call() throws Exception {
        System.out.println(Thread.currentThread().getName() + 
                         " is calculating square of " + num);
        Thread.sleep(1000);
        return num * num;  // Return result
    }
}

public class CallableDemo {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThread Pool(2);
        
        // Submit Callable tasks
        Future<Integer> future1 = executor.submit(new MyCallable(5));
        Future<Integer> future2 = executor.submit(new MyCallable(10));
        
        try {
            // Get results (blocking call)
            Integer result1 = future1.get();
            Integer result2 = future2.get();
            
            System.out.println("Result 1: " + result1);  // 25
            System.out.println("Result 2: " + result2);  // 100
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }
        
        executor.shutdown();
    }
}
```

**Output:**
```
pool-1-thread-1 is calculating square of 5
pool-1-thread-2 is calculating square of 10
Result 1: 25
Result 2: 100
```

**Future Methods:**
- `get()` → Wait for result (blocking)
- `get(timeout, unit)` → Wait with timeout
- `isDone()` → Check if task completed
- `cancel(mayInterrupt)` → Cancel task

---

## Executor Lifecycle

### States:

1. **Running** → Accepting new tasks
2. **Shutdown** → Not accepting new tasks, completing existing tasks
3. **Terminated** → All tasks completed

### Shutdown Methods:

#### 1. shutdown() - Graceful

```java
executor.shutdown();  // No new tasks accepted
// Previously submitted tasks will complete
```

**Characteristics:**
- Initiates orderly shutdown
- Previously submitted tasks execute
- No new tasks accepted
- Does NOT wait for tasks to complete

#### 2. shutdownNow() - Immediate

```java
List<Runnable> notExecuted = executor.shutdownNow();
// Attempts to stop all actively executing tasks
// Returns list of tasks that were waiting
```

**Characteristics:**
- Attempts to stop all actively executing tasks
- Halts processing of waiting tasks
- Returns list of tasks that were not executed
- Best-effort attempt (not guaranteed to stop)

### Complete Shutdown Pattern:

```java
executor.shutdown();  // Graceful shutdown

try {
    // Wait for tasks to complete
    if (!executor.awaitTermination(60, TimeUnit.SECONDS)) {
        // Timeout: force shutdown
        executor.shutdownNow();
        
        // Wait again
        if (!executor.awaitTermination(60, TimeUnit.SECONDS)) {
            System.err.println("Executor did not terminate");
        }
    }
} catch (InterruptedException e) {
    executor.shutdownNow();
    Thread.currentThread().interrupt();
}
```

---

## Summary Table

| Thread Pool Type | Number of Threads | Use Case |
|------------------|-------------------|----------|
| **Fixed** | Fixed (e.g., 5) | Known optimal thread count |
| **Cached** | Creates as needed | Many short-lived tasks |
| **Single** | 1 thread | Sequential execution required |
| **Scheduled** | Fixed | Delayed/periodic tasks |

---

## Key Takeaways

1. **Thread pools reuse threads** → Better performance than creating new threads
2. **ExecutorService** is main interface for thread pool management
3. **Executors factory class** provides static methods to create pools
4. **Fixed thread pool** for known thread count
5. **Cached thread pool** creates threads as needed (can grow unbounded)
6. **Single thread executor** for sequential execution
7. **Scheduled executor** for delayed/periodic tasks
8. **Callable returns value**, Runnable doesn't
9. **Future represents async computation result**
10. **Always shutdown executor** when done

---

## Best Practices

### ✅ DO:

1. **Always shutdown executor** when done
2. **Use try-finally** to ensure shutdown:
   ```java
   ExecutorService executor = Executors.newFixedThreadPool(5);
   try {
       // Submit tasks
   } finally {
       executor.shutdown();
   }
   ```

3. **Choose appropriate pool type** based on workload
4. **Use Callable** when you need return values
5. **Handle exceptions** from Future.get()

### ❌ DON'T:

1. **Don't use cached pool** for long-running tasks
2. **Don't forget to shutdown** - executor won't terminate JVM
3. **Don't call get() immediately** after submit - defeats purpose of async
4. **Don't create unbounded pools** - limits resources

---

## Interview Questions

### Q1: What is a thread pool?
**A:** A collection of pre-created, reusable threads managed by a framework to execute tasks efficiently.

### Q2: Advantages of ExecutorService over manual thread creation?
**A:** Reuses threads, controls resource usage, simplifies management, better performance, automatic lifecycle management.

### Q3: Difference between shutdown() and shutdownNow()?
**A:** shutdown() is graceful (completes existing tasks), shutdownNow() is immediate (attempts to stop running tasks).

### Q4: Difference between Runnable and Callable?  
**A:** Callable can return a value and throw checked exceptions. Runnable cannot return value.

### Q5: What is Future?
**A:** Represents the result of an asynchronous computation. Can check if done, get result, or cancel.

---

**End of Executors Framework Notes**
