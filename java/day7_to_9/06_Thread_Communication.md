# Thread Communication in Java

## Table of Contents
1. [Introduction to Thread Communication](#introduction-to-thread-communication)
2. [The Deadlock Problem](#the-deadlock-problem)
3. [wait(), notify(), and notifyAll()](#wait-notify-and-notifyall)
4. [Why These Methods Are in Object Class](#why-these-methods-are-in-object-class)
5. [wait() vs sleep()](#wait-vs-sleep)
6. [Producer-Consumer Pattern](#producer-consumer-pattern)
7. [Complete Examples](#complete-examples)

---

## Introduction to Thread Communication

**Thread Communication** = Threads coordinating with each other to avoid deadlock and ensure proper execution flow.

### The Need:

Even with synchronization, there's a danger of **deadlock** inside synchronized methods/blocks.

---

## The Deadlock Problem

### Scenario:

```java
synchronized void method() {
    // Thread T1 enters, acquires lock
    // T1 gets stuck (waiting for some condition)
    // T1 can't release lock!
    // Other threads can't acquire lock!
    // System HANGS! 🚫
}
```

### Example Situation:

**ATM Withdrawal:**
```java
synchronized void withdraw(int amount) {
    if (balance < amount) {
        // Insufficient balance
        // Thread keeps waiting inside synchronized method
        // Lock is NOT released
        // No other thread can deposit money!
        // DEADLOCK! 🚫
    }
}
```

**Problem:** Thread realizes it can't continue but is **stuck** inside synchronized method, holding the lock!

### Solution: Thread Communication

Thread should:
1. **Release the lock** when it can't continue
2. **Go to wait state**
3. Let **other threads** execute
4. Other thread **notifies** when condition is met
5. **Resume execution**

---

## wait(), notify(), and notifyAll()

These methods enable **inter-thread communication**.

### 1. wait() Method

**Signature:**
```java
public final void wait() throws InterruptedException
```

**Purpose:** Makes thread **release the lock** and go to **wait pool**.

**Usage:**
```java
synchronized void method() {
    if (condition_not_met) {
        wait();  // Release lock, go to wait pool
    }
}
```

**Effects:**
- Thread **releases the lock** immediately
- Thread goes to **wait pool** (not runnable)
- Thread **waits** until another thread calls `notify()`

### 2. notify() Method

**Signature:**
```java
public final void notify()
```

**Purpose:** Moves **one thread** from wait pool to **seeking lock state**.

**Usage:**
```java
synchronized void method() {
    // Condition is now met
    notify();  // Wake up one waiting thread
}
```

**Effects:**
- **One thread** (chosen by JVM) moves from wait pool to seeking lock state
- Thread **does not immediately execute** (must first acquire lock)

### 3. notifyAll() Method

**Signature:**
```java
public final void notifyAll()
```

**Purpose:** Moves **all threads** from wait pool to **seeking lock state**.

**Effects:**
- **All waiting threads** move to seeking lock state
- All threads compete for the lock
- Only **one thread** gets the lock at a time

---

## Why These Methods Are in Object Class

### Question: Why are wait(), notify(), notifyAll() in Object class?

**Answer:** Because **every object has a lock**.

### Explanation:

1. **Object lock mechanism**
   - Every object has a lock
   - Synchronization uses object locks

2. **wait() releases lock**
   - wait() must release the **object's lock**
   - Makes sense to be part of Object class

3. **notify() is about object's lock**
   - notify() wakes threads waiting for **this object's lock**
   - Related to the object itself

4. **Universal availability**
   - All classes inherit from Object
   - All objects can be used for synchronization

---

## Must Be Called from synchronized Context

### Rule:

> wait(), notify(), and notifyAll() **MUST** be called from synchronized method or block.

**Why?**
- These methods control the **lock**
- Lock concept exists only in synchronized context
- Compiler ensures you have the lock before calling these methods

### Correct Usage:

```java
synchronized void method() {
    wait();     // ✅ Correct - inside synchronized method
    notify();   // ✅ Correct
}

synchronized(this) {
    wait();     // ✅ Correct - inside synchronized block
    notifyAll(); // ✅ Correct
}
```

### Incorrect Usage:

```java
void method() {
    wait();     // ❌ ERROR: IllegalMonitorStateException
    notify();   // ❌ ERROR
}
```

---

## wait() vs sleep()

| Aspect | wait() | sleep() |
|--------|--------|---------|
| **Package** | java.lang.Object | java.lang.Thread |
| **Releases lock?** | ✅ Yes | ❌ No |
| **Must be in synchronized?** | ✅ Yes | ❌ No |
| **Woken up by** | notify()/notifyAll() | Timeout only |
| **Static method?** | ❌ No | ✅ Yes |
| **Use case** | Thread coordination | Delay execution |

### Example Demonstrating the Difference:

```java
class SharedResource {
    synchronized void method1() {
        System.out.println(Thread.currentThread().getName() + " entered method1");
        try {
            wait(2000);  // Releases lock, wait for 2 seconds or until notified
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(Thread.currentThread().getName() + " resuming method1");
    }
    
    synchronized void method2() {
        System.out.println(Thread.currentThread().getName() + " entered method2");
        try {
            Thread.sleep(2000);  // Does NOT release lock, sleep for 2 seconds
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(Thread.currentThread().getName() + " resuming method2");
    }
}
```

**With wait():**
```
T1 entered method1
T2 entered method1 (entered while T1 is waiting)
T1 resuming method1
T2 resuming method1
```

**With sleep():**
```
T1 entered method2
(T2 waits because T1 holds lock during sleep)
T1 resuming method2
T2 entered method2
T2 resuming method2
```

**Key Difference:** wait() allows other threads to acquire lock, sleep() doesn't!

---

## Producer-Consumer Pattern

Classic example of thread communication.

### Scenario:

- **Producer** produces items and puts them in a buffer
- **Consumer** consumes items from the buffer
- **Buffer** has limited capacity

### Rules:

1. Producer should **wait** if buffer is full
2. Consumer should **wait** if buffer is empty
3. Producer should **notify** consumer when it adds items
4. Consumer should **notify** producer when it removes items

### Code Example:

```java
class SharedBuffer {
    private int buffer;
    private boolean available = false;
    
    // Producer calls this
    synchronized void produce(int value) {
        while (available) {  // Buffer already has value
            try {
                System.out.println("Producer waiting...");
                wait();  // Wait until consumer consumes
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        
        buffer = value;
        available = true;
        System.out.println("Produced: " + value);
        notify();  // Notify consumer
    }
    
    // Consumer calls this
    synchronized int consume() {
        while (!available) {  // Buffer is empty
            try {
                System.out.println("Consumer waiting...");
                wait();  // Wait until producer produces
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        
        available = false;
        System.out.println("Consumed: " + buffer);
        notify();  // Notify producer
        return buffer;
    }
}

class Producer extends Thread {
    private SharedBuffer buffer;
    
    public Producer(SharedBuffer buffer) {
        this.buffer = buffer;
    }
    
    public void run() {
        for (int i = 1; i <= 5; i++) {
            buffer.produce(i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class Consumer extends Thread {
    private SharedBuffer buffer;
    
    public Consumer(SharedBuffer buffer) {
        this.buffer = buffer;
    }
    
    public void run() {
        for (int i = 1; i <= 5; i++) {
            buffer.consume();
            try {
                Thread.sleep(1500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class ProducerConsumerDemo {
    public static void main(String[] args) {
        SharedBuffer buffer = new SharedBuffer();
        Producer producer = new Producer(buffer);
        Consumer consumer = new Consumer(buffer);
        
        producer.start();
        consumer.start();
    }
}
```

**Output:**
```
Produced: 1
Consumed: 1
Produced: 2
Consumed: 2
Producer waiting...
Consumed: 3
Produced: 3
Producer waiting...
...
```

**Execution Flow:**

1. **Producer produces first item**
   - Sets `available = true`
   - Calls `notify()` to wake consumer
   
2. **Consumer consumes**
   - Sets `available = false`
   - Calls `notify()` to wake producer
   
3. **Producer tries to produce again**
   - If `available == true` (buffer full), calls `wait()`
   
4. **Consumer consumes**
   - Sets `available = false`
   - Calls `notify()` to wake producer
   
5. **Cycle continues...**

**Key Points:**
- **wait() inside while loop** (not if) → Handles spurious wakeups
- **notify() after changing condition** → Wake waiting thread
- **Perfect coordination** → No item produced when buffer full, no consumption when buffer empty

---

## Complete Examples

### Example: Transaction Class (Bank Account)

```java
class Transaction {
    private int balance = 0;
    
    synchronized void deposit(int amount) {
        System.out.println(Thread.currentThread().getName() + 
                         " is depositing " + amount);
        balance += amount;
        System.out.println("Balance after deposit: " + balance);
        notify();  // Notify waiting withdrawal thread
    }
    
    synchronized void withdraw(int amount) {
        while (balance < amount) {
            System.out.println(Thread.currentThread().getName() + 
                             " is waiting. Current balance: " + balance + 
                             ", Required: " + amount);
            try {
                wait();  // Wait for deposit
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        
        System.out.println(Thread.currentThread().getName() + 
                         " is withdrawing " + amount);
        balance -= amount;
        System.out.println("Balance after withdrawal: " + balance);
    }
}

public class TransactionDemo {
    public static void main(String[] args) {
        Transaction t = new Transaction();
        
        // Withdrawal thread
        Thread t1 = new Thread(() -> {
            t.withdraw(5000);
        });
        t1.setName("Withdrawal");
        
        // Deposit thread
        Thread t2 = new Thread(() -> {
            try {
                Thread.sleep(2000);  // Delay deposit
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            t.deposit(10000);
        });
        t2.setName("Deposit");
        
        t1.start();
        t2.start();
    }
}
```

**Output:**
```
Withdrawal is waiting. Current balance: 0, Required: 5000
(2 seconds delay)
Deposit is depositing 10000
Balance after deposit: 10000
Withdrawal is withdrawing 5000
Balance after withdrawal: 5000
```

**Execution Flow:**

1. **T1 (Withdrawal) starts**
   - Checks balance (0) < amount (5000)
   - Prints waiting message
   - Calls `wait()` → Releases lock, goes to wait pool

2. **T2 (Deposit) starts**
   - Sleeps for 2 seconds
   - Acquires lock (T1 released it)
   - Deposits 10000
   - Calls `notify()` → Wakes T1

3. **T1 resumes**
   - Checks balance again (while loop)
   - balance (10000) >= amount (5000) ✓
   - Withdraws 5000
   - Method completes

**Key Learning:** `wait()` allows other threads to execute and fix the condition!

---

## Key Takeaways

1. **Thread communication** prevents deadlock in synchronized code
2. **wait()** releases lock and waits for notification
3. **notify()** wakes one waiting thread
4. **notifyAll()** wakes all waiting threads
5. **All three methods are in Object class** because every object has a lock
6. **Must be called from synchronized context** (method or block)
7. **wait() releases lock, sleep() doesn't**
8. **Use while loop with wait()**, not if (handles spurious wakeups)
9. ** notify() after changing condition** that waiting threads are waiting for
10. **Producer-Consumer pattern** is classic example of thread communication

---

## Best Practices

### ✅ DO:

1. **Always use while loop** with wait():
   ```java
   while (condition) {
       wait();
   }
   ```

2. **Call notify()/notifyAll() after changing condition**:
   ```java
   condition = true;
   notify();
   ```

3. **Use notifyAll()** if multiple threads might be waiting for different conditions

4. **Handle InterruptedException** properly

### ❌ DON'T:

1. **Don't call wait() from non-synchronized context**:
   ```java
   void method() {
       wait();  // ❌ IllegalMonitorStateException
   }
   ```

2. **Don't use if instead of while** with wait():
   ```java
   if (condition) {
       wait();  // ❌ Vulnerable to spurious wakeups
   }
   ```

3. **Don't forget to call notify()** after fixing condition

4. **Don't confuse wait() with sleep()**

---

## Summary Table

| Method | Purpose | Releases Lock? | Must be synchronized? |
|--------|---------|----------------|----------------------|
| `wait()` | Wait for notification | ✅ Yes | ✅ Yes |
| `wait(ms)` | Wait for notification or timeout | ✅ Yes | ✅ Yes |
| `notify()` | Wake one waiting thread | ❌ No | ✅ Yes |
| `notifyAll()` | Wake all waiting threads | ❌ No | ✅ Yes |
| `sleep(ms)` | Pause execution | ❌ No | ❌ No |

---

## Interview Questions

### Q1: What is the difference between wait() and sleep()?
**A:** wait() releases the lock and must be called from synchronized context. sleep() doesn't release the lock and can be called from anywhere. wait() is for thread coordination, sleep() is for pausing execution.

### Q2: Why are wait(), notify(), and notifyAll() in Object class?
**A:** Because every object has a lock, and these methods control the lock mechanism. They need to be available for all objects used in synchronization.

### Q3: What happens if you call wait() from non-synchronized method?
**A:** You get `IllegalMonitorStateException` at runtime.

### Q4: Difference between notify() and notifyAll()?
**A:** notify() wakes one waiting thread (chosen by JVM). notifyAll() wakes all waiting threads. Use notifyAll() when multiple threads might be waiting for different conditions.

### Q5: Why use while loop instead of if with wait()?
**A:** To handle spurious wakeups (thread waking up without notification). while loop rechecks the condition after waking up.

### Q6: What is deadlock and how does thread communication prevent it?
**A:** Deadlock is when a thread holds a lock but can't proceed, blocking other threads. Thread communication allows the thread to release lock (via wait()) so other threads can run and fix the condition.

---

**End of Thread Communication Notes**
