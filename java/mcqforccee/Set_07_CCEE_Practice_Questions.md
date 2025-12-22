# CDAC CCEE MCQ Practice Set 7

## 📝 ADVANCED LEVEL - Multithreading, Synchronization & Memory Management
**Total Questions: 50 | Time Limit: 60 minutes | No Negative Marking**

> **Difficulty: ⭐⭐⭐⭐⭐ Advanced** - These questions cover deep threading concepts, synchronization mechanisms, memory management, and JVM internals. Requires expert-level understanding.

---

### Question 1
What is the output?
```java
class Counter {
    private int count = 0;
    public void increment() { count++; }
    public int getCount() { return count; }
}
```
If 100 threads each call increment() 1000 times, what is the expected count?

A) Exactly 100000  
B) Less than or equal to 100000  
C) More than 100000  
D) Error

---

### Question 2
What is the output?
```java
synchronized void m1() { System.out.print("m1 "); }
synchronized void m2() { System.out.print("m2 "); }
```
If two threads call m1() and m2() on same object simultaneously?

A) Both execute simultaneously  
B) One waits for the other  
C) Deadlock  
D) Error

---

### Question 3
What is the output?
```java
class A {
    synchronized static void m1() { System.out.print("static "); }
    synchronized void m2() { System.out.print("instance "); }
}
```
Can different threads call m1() and m2() simultaneously on same object?

A) No, same lock  
B) Yes, different locks  
C) Depends  
D) Error

---

### Question 4
What is the output?
```java
Object lock = new Object();
synchronized(lock) {
    lock = new Object();
    System.out.println("Changed");
}
```

A) Changed  
B) Error  
C) Deadlock  
D) Nothing

---

### Question 5
What is the output?
```java
Thread.sleep(1000);
```
Which exception must be handled?

A) RuntimeException  
B) InterruptedException  
C) IllegalStateException  
D) No exception

---

### Question 6
What is the output?
```java
volatile int x = 0;
// Thread 1: x++; x++;
// Thread 2: System.out.println(x);
```
What is guaranteed about x?

A) Thread 2 sees 0, 1, or 2  
B) Thread 2 always sees 2  
C) Volatile ensures atomic increment  
D) Error

---

### Question 7
What is the output?
```java
Object lock = new Object();
lock.wait();
```
Outside synchronized block?

A) Waits indefinitely  
B) IllegalMonitorStateException  
C) Works fine  
D) Compile error

---

### Question 8
What is the output?
```java
Thread t = new Thread(() -> {
    while(!Thread.currentThread().isInterrupted()) {
        // work
    }
});
t.start();
t.interrupt();
```
Does the thread stop?

A) Yes, immediately  
B) Eventually, when it checks the flag  
C) No, interrupt doesn't stop threads  
D) InterruptedException

---

### Question 9
What is the output?
```java
ThreadLocal<Integer> tl = new ThreadLocal<>();
tl.set(10);
new Thread(() -> System.out.println(tl.get())).start();
```

A) 10  
B) null  
C) Exception  
D) 0

---

### Question 10
What is the output?
```java
class A {
    void m() {
        synchronized(this) {
            synchronized(this) {
                System.out.println("Nested");
            }
        }
    }
}
new A().m();
```

A) Nested  
B) Deadlock  
C) IllegalMonitorStateException  
D) Error

---

### Question 11
What causes a deadlock?

A) Too many threads  
B) Circular wait for resources  
C) One thread running too long  
D) Thread starvation

---

### Question 12
What is the output?
```java
Lock lock = new ReentrantLock();
lock.lock();
try {
    System.out.println("Locked");
} finally {
    lock.unlock();
}
```

A) Locked  
B) Exception  
C) Deadlock  
D) Nothing

---

### Question 13
What is the output?
```java
ReadWriteLock rwl = new ReentrantReadWriteLock();
rwl.readLock().lock();
rwl.readLock().lock();
System.out.println("Two reads");
```

A) Two reads  
B) Deadlock  
C) Exception  
D) Only one read allowed

---

### Question 14
What is the output?
```java
Semaphore sem = new Semaphore(0);
sem.acquire();
System.out.println("Acquired");
```

A) Acquired  
B) Blocks forever  
C) Exception  
D) Acquired immediately

---

### Question 15
What is the output?
```java
CountDownLatch latch = new CountDownLatch(3);
latch.countDown();
latch.countDown();
latch.await(1, TimeUnit.MILLISECONDS);
System.out.println(latch.getCount());
```

A) 0  
B) 1  
C) 3  
D) Exception

---

### Question 16
What is the output?
```java
CyclicBarrier barrier = new CyclicBarrier(3);
barrier.await();
```
With only one thread?

A) Continues  
B) Blocks, waiting for 2 more  
C) Exception  
D) Returns immediately

---

### Question 17
What is the output?
```java
Exchanger<String> ex = new Exchanger<>();
String s = ex.exchange("Hello");
```
With only one thread?

A) Returns "Hello"  
B) Blocks forever  
C) Returns null  
D) Exception

---

### Question 18
What is the output?
```java
AtomicReference<String> ref = new AtomicReference<>("A");
ref.compareAndSet("A", "B");
System.out.println(ref.get());
```

A) A  
B) B  
C) null  
D) Exception

---

### Question 19
What is the output?
```java
LongAdder adder = new LongAdder();
adder.add(10);
adder.add(20);
System.out.println(adder.sum());
```

A) 10  
B) 20  
C) 30  
D) 0

---

### Question 20
What is the output?
```java
Phaser phaser = new Phaser(1);
phaser.arriveAndDeregister();
System.out.println(phaser.getRegisteredParties());
```

A) 1  
B) 0  
C) 2  
D) Exception

---

### Question 21
What is the output?
```java
ForkJoinPool pool = ForkJoinPool.commonPool();
System.out.println(pool.getParallelism() > 0);
```

A) true  
B) false  
C) Depends on system  
D) Exception

---

### Question 22
What is weak reference used for?

A) Strong reference  
B) Allow GC when only weak refs exist  
C) Prevent GC  
D) Memory leak

---

### Question 23
What is the output?
```java
SoftReference<String> soft = new SoftReference<>(new String("Hello"));
System.gc();
System.out.println(soft.get() != null);
```

A) true (usually)  
B) false  
C) Exception  
D) Always true

---

### Question 24
What is PhantomReference used for?

A) Access object value  
B) Pre-finalization cleanup  
C) Post-mortem cleanup (enqueued after finalization)  
D) Strong reference

---

### Question 25
What is the output?
```java
String s1 = new String("Hello");
String s2 = new String("Hello");
System.out.println(System.identityHashCode(s1) == System.identityHashCode(s2));
```

A) true  
B) false  
C) Depends  
D) Exception

---

### Question 26
What is the purpose of the happens-before relationship?

A) Performance optimization  
B) Memory visibility guarantee between threads  
C) Thread ordering  
D) Deadlock prevention

---

### Question 27
What is the output?
```java
class Holder {
    int value;
    Holder(int v) { value = v; }
}
Holder h = new Holder(42);
// Another thread reads h.value
```
Without synchronization, what can the other thread see?

A) Only 42  
B) 0 or 42 (partial construction issue)  
C) Always 0  
D) Exception

---

### Question 28
What is double-checked locking issue?

A) Checking twice is slow  
B) Without volatile, instance may be partially constructed  
C) Deadlock  
D) No issue

---

### Question 29
What is the output?
```java
CompletableFuture<String> cf1 = CompletableFuture.supplyAsync(() -> "Hello");
CompletableFuture<String> cf2 = cf1.thenApply(s -> s + " World");
System.out.println(cf2.get());
```

A) Hello  
B) Hello World  
C) World  
D) Exception

---

### Question 30
What is the output?
```java
CompletableFuture.runAsync(() -> {
    throw new RuntimeException("Error");
}).exceptionally(e -> {
    System.out.println("Caught");
    return null;
}).join();
```

A) Exception thrown  
B) Caught  
C) Nothing  
D) Deadlock

---

### Question 31
What is the output?
```java
Stream.of(1, 2, 3, 4, 5)
    .parallel()
    .reduce(0, Integer::sum);
```

A) 15  
B) Order depends on threads  
C) Exception  
D) 0

---

### Question 32
What is the output?
```java
List<Integer> list = new ArrayList<>();
IntStream.range(0, 1000)
    .parallel()
    .forEach(i -> list.add(i));
System.out.println(list.size());
```

A) 1000  
B) Less than 1000 (thread-safety issue)  
C) Exception  
D) 0

---

### Question 33
What is the purpose of ForkJoinTask?

A) Regular task execution  
B) Divide and conquer parallel execution  
C) Sequential execution  
D) IO operations

---

### Question 34
What is the output?
```java
Executor executor = Runnable::run;
executor.execute(() -> System.out.println("Run"));
```

A) Run  
B) Exception  
C) Nothing  
D) Compile error

---

### Question 35
What is the output?
```java
ScheduledExecutorService ses = Executors.newScheduledThreadPool(1);
ses.schedule(() -> System.out.println("Delayed"), 100, TimeUnit.MILLISECONDS);
ses.shutdown();
Thread.sleep(200);
```

A) Delayed  
B) Nothing (shutdown cancels)  
C) Exception  
D) Delayed (repeated)

---

### Question 36
What is the output?
```java
BlockingQueue<String> queue = new LinkedBlockingQueue<>();
queue.put("A");
System.out.println(queue.take());
```

A) A  
B) Blocks  
C) Exception  
D) null

---

### Question 37
What is the output?
```java
ConcurrentLinkedQueue<Integer> queue = new ConcurrentLinkedQueue<>();
queue.add(1);
queue.add(2);
System.out.println(queue.poll());
```

A) 1  
B) 2  
C) null  
D) Exception

---

### Question 38
What is the output?
```java
TransferQueue<String> queue = new LinkedTransferQueue<>();
queue.add("Hello");
System.out.println(queue.poll());
```

A) Hello  
B) null  
C) Blocks  
D) Exception

---

### Question 39
What is the output?
```java
DelayQueue<Delayed> queue = new DelayQueue<>();
// Empty queue
queue.poll();
```

A) null  
B) Blocks  
C) Exception  
D) Default element

---

### Question 40
What is the output?
```java
PriorityBlockingQueue<Integer> pq = new PriorityBlockingQueue<>();
pq.add(3);
pq.add(1);
pq.add(2);
System.out.println(pq.poll());
```

A) 3  
B) 1  
C) 2  
D) Random

---

### Question 41
What is the output?
```java
StampedLock lock = new StampedLock();
long stamp = lock.tryOptimisticRead();
// read data
if(!lock.validate(stamp)) {
    // retry with read lock
}
System.out.println("Valid check");
```

A) Valid check  
B) Exception  
C) Deadlock  
D) No output

---

### Question 42
What is the output?
```java
Thread.currentThread().setUncaughtExceptionHandler((t, e) -> 
    System.out.println("Uncaught: " + e.getMessage()));
throw new RuntimeException("Error");
```

A) Runtime error  
B) Uncaught: Error  
C) Nothing  
D) Exception propagates

---

### Question 43
What is the output?
```java
Thread t = new Thread(() -> {
    try { Thread.sleep(10000); }
    catch(InterruptedException e) { System.out.println("Interrupted"); }
});
t.setDaemon(true);
t.start();
// main ends immediately
```

A) Interrupted  
B) Sleeps 10 seconds  
C) JVM exits (daemon), may not print  
D) Exception

---

### Question 44
What is the output?
```java
class Task implements Callable<Integer> {
    public Integer call() throws Exception {
        return 42;
    }
}
ExecutorService es = Executors.newSingleThreadExecutor();
Future<Integer> f = es.submit(new Task());
System.out.println(f.get());
es.shutdown();
```

A) 42  
B) null  
C) Exception  
D) Future

---

### Question 45
What is the output?
```java
CompletableFuture.allOf(
    CompletableFuture.runAsync(() -> System.out.print("1")),
    CompletableFuture.runAsync(() -> System.out.print("2"))
).join();
System.out.println("Done");
```

A) 12Done  
B) 21Done  
C) 1 or 2 order varies, then Done  
D) Done12

---

### Question 46
What is thread confinement?

A) Limiting thread count  
B) Keeping data accessible by only one thread  
C) Thread pooling  
D) Thread priority

---

### Question 47
What is the output?
```java
ThreadPoolExecutor executor = new ThreadPoolExecutor(
    2, 4, 60, TimeUnit.SECONDS, new LinkedBlockingQueue<>());
System.out.println(executor.getCorePoolSize());
```

A) 2  
B) 4  
C) 60  
D) 0

---

### Question 48
What is the output?
```java
Object o = new Object();
synchronized(o) {
    o.notifyAll();
    o.wait(100);
    System.out.println("After wait");
}
```

A) After wait (after 100ms)  
B) IllegalMonitorStateException  
C) After wait (immediately)  
D) Blocks forever

---

### Question 49
What is the output?
```java
Condition cond = new ReentrantLock().newCondition();
cond.signal();
```
Outside lock?

A) Works fine  
B) IllegalMonitorStateException  
C) Nothing  
D) Signals waiting thread

---

### Question 50
What is the output?
```java
class ImmutableStack<T> {
    private final List<T> list;
    ImmutableStack() { this.list = new ArrayList<>(); }
    ImmutableStack<T> push(T item) {
        ImmutableStack<T> newStack = new ImmutableStack<>();
        newStack.list.addAll(this.list);
        newStack.list.add(item);
        return newStack;
    }
}
```
Is this truly immutable and thread-safe?

A) Yes, fully immutable  
B) No, internal list is modified in push()  
C) Yes, new object created  
D) Depends on T

---

---

# 📝 Answer Key with Explanations

---

### Question 1
**Correct Answer: B) Less than or equal to 100000**

**Explanation:** count++ is not atomic (read-modify-write). Race conditions cause lost updates.

---

### Question 2
**Correct Answer: B) One waits for the other**

**Explanation:** Both methods synchronize on same object (this). Only one thread can hold lock.

---

### Question 3
**Correct Answer: B) Yes, different locks**

**Explanation:** Static sync uses class lock. Instance sync uses object lock. Different locks.

---

### Question 4
**Correct Answer: A) Changed**

**Explanation:** Sync acquired on original lock object. Reassigning variable doesn't change the lock held.

---

### Question 5
**Correct Answer: B) InterruptedException**

**Explanation:** sleep() throws checked InterruptedException. Must be caught or declared.

---

### Question 6
**Correct Answer: A) Thread 2 sees 0, 1, or 2**

**Explanation:** volatile ensures visibility but not atomicity. x++ is still non-atomic.

---

### Question 7
**Correct Answer: B) IllegalMonitorStateException**

**Explanation:** wait() must be called while holding the object's monitor (synchronized block).

---

### Question 8
**Correct Answer: B) Eventually, when it checks the flag**

**Explanation:** interrupt() sets flag. Thread must check isInterrupted() to respond.

---

### Question 9
**Correct Answer: B) null**

**Explanation:** ThreadLocal values are thread-specific. New thread has no value set.

---

### Question 10
**Correct Answer: A) Nested**

**Explanation:** Synchronized is reentrant. Same thread can acquire same lock multiple times.

---

### Question 11
**Correct Answer: B) Circular wait for resources**

**Explanation:** Deadlock requires mutual exclusion, hold and wait, no preemption, circular wait.

---

### Question 12
**Correct Answer: A) Locked**

**Explanation:** Lock/unlock with try-finally is standard pattern. Works correctly.

---

### Question 13
**Correct Answer: A) Two reads**

**Explanation:** Multiple threads can hold read lock simultaneously. Same thread can acquire it twice.

---

### Question 14
**Correct Answer: B) Blocks forever**

**Explanation:** Semaphore(0) has no permits. acquire() blocks waiting for permits.

---

### Question 15
**Correct Answer: B) 1**

**Explanation:** Started at 3, two countDowns = 1. await times out. getCount() returns 1.

---

### Question 16
**Correct Answer: B) Blocks, waiting for 2 more**

**Explanation:** CyclicBarrier waits for all parties. With only 1 of 3, it blocks.

---

### Question 17
**Correct Answer: B) Blocks forever**

**Explanation:** Exchanger needs two threads. Single thread blocks waiting for partner.

---

### Question 18
**Correct Answer: B) B**

**Explanation:** CAS succeeds - expected "A" matches current, updates to "B".

---

### Question 19
**Correct Answer: C) 30**

**Explanation:** LongAdder adds values. 10 + 20 = 30.

---

### Question 20
**Correct Answer: B) 0**

**Explanation:** arriveAndDeregister removes the party. 1 - 1 = 0 registered.

---

### Question 21
**Correct Answer: A) true**

**Explanation:** Common pool parallelism is based on available processors. Always > 0.

---

### Question 22
**Correct Answer: B) Allow GC when only weak refs exist**

**Explanation:** Weak references don't prevent GC. Object collected when only weak refs exist.

---

### Question 23
**Correct Answer: A) true (usually)**

**Explanation:** Soft references cleared only when memory needed. Usually survives gc() call.

---

### Question 24
**Correct Answer: C) Post-mortem cleanup (enqueued after finalization)**

**Explanation:** PhantomReference enqueued after finalization, before memory reclaimed.

---

### Question 25
**Correct Answer: B) false**

**Explanation:** identityHashCode returns different values for different objects.

---

### Question 26
**Correct Answer: B) Memory visibility guarantee between threads**

**Explanation:** Happens-before establishes visibility. If A happens-before B, A's effects visible to B.

---

### Question 27
**Correct Answer: B) 0 or 42 (partial construction issue)**

**Explanation:** Without happens-before, other thread may see partially constructed object.

---

### Question 28
**Correct Answer: B) Without volatile, instance may be partially constructed**

**Explanation:** Object assignment may be reordered. Other thread sees non-null but incomplete object.

---

### Question 29
**Correct Answer: B) Hello World**

**Explanation:** thenApply transforms result. "Hello" + " World" = "Hello World".

---

### Question 30
**Correct Answer: B) Caught**

**Explanation:** exceptionally handles exceptions in CompletableFuture chain.

---

### Question 31
**Correct Answer: A) 15**

**Explanation:** Parallel reduce with associative operation gives correct result.

---

### Question 32
**Correct Answer: B) Less than 1000 (thread-safety issue)**

**Explanation:** ArrayList is not thread-safe. Parallel modifications cause lost updates.

---

### Question 33
**Correct Answer: B) Divide and conquer parallel execution**

**Explanation:** ForkJoinTask for recursive decomposition. fork() spawns subtasks, join() waits.

---

### Question 34
**Correct Answer: A) Run**

**Explanation:** Custom executor that runs task in current thread. Prints "Run".

---

### Question 35
**Correct Answer: A) Delayed**

**Explanation:** shutdown() doesn't cancel already scheduled tasks. Task executes.

---

### Question 36
**Correct Answer: A) A**

**Explanation:** put() and take() work. Queue has "A", take removes and returns it.

---

### Question 37
**Correct Answer: A) 1**

**Explanation:** ConcurrentLinkedQueue is FIFO. poll() returns first element (1).

---

### Question 38
**Correct Answer: A) Hello**

**Explanation:** add() doesn't block. poll() returns "Hello" immediately.

---

### Question 39
**Correct Answer: A) null**

**Explanation:** poll() on empty DelayQueue returns null immediately.

---

### Question 40
**Correct Answer: B) 1**

**Explanation:** PriorityBlockingQueue is min-heap. poll() returns smallest (1).

---

### Question 41
**Correct Answer: A) Valid check**

**Explanation:** Optimistic read doesn't block. validate() checks if write occurred.

---

### Question 42
**Correct Answer: B) Uncaught: Error**

**Explanation:** UncaughtExceptionHandler handles exceptions in main thread.

---

### Question 43
**Correct Answer: C) JVM exits (daemon), may not print**

**Explanation:** Daemon threads don't prevent JVM exit. Main ends, JVM may exit immediately.

---

### Question 44
**Correct Answer: A) 42**

**Explanation:** Callable returns value. get() retrieves it.

---

### Question 45
**Correct Answer: C) 1 or 2 order varies, then Done**

**Explanation:** Async tasks run in parallel. Order not guaranteed. allOf waits for both.

---

### Question 46
**Correct Answer: B) Keeping data accessible by only one thread**

**Explanation:** Thread confinement: data belongs to one thread, avoiding synchronization.

---

### Question 47
**Correct Answer: A) 2**

**Explanation:** getCorePoolSize() returns core pool size parameter (2).

---

### Question 48
**Correct Answer: A) After wait (after 100ms)**

**Explanation:** notifyAll with no waiters does nothing. wait(100) times out. Continues.

---

### Question 49
**Correct Answer: B) IllegalMonitorStateException**

**Explanation:** Condition operations require holding the associated lock.

---

### Question 50
**Correct Answer: B) No, internal list is modified in push()**

**Explanation:** New object's list is modified (addAll, add). Not properly immutable.

---

## 📊 Score Guide

| Score | Level | Next Step |
|-------|-------|-----------|
| 45-50 | Excellent! | Move to Set 8 |
| 35-44 | Good | Review concurrency in depth |
| 25-34 | Average | More threading practice |
| 0-24 | Needs Work | Review Sets 5-6 |

---

**Difficulty: ⭐⭐⭐⭐⭐ ADVANCED** | **Next: Set 8 (🔥 Expert)**
