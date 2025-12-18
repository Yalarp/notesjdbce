# ReentrantLock and Conditions in Java

## Table of Contents
1. [Limitations of Implicit Synchronization](#limitations-of-implicit-synchronization)
2. [What is ReentrantLock?](#what-is-reentrantlock)
3. [Lock Fairness](#lock-fairness)
4. [tryLock() Method](#trylock-method)
5. [Condition Objects](#condition-objects)
6. [Complete Examples](#complete-examples)
7. [synchronized vs ReentrantLock](#synchronized-vs-reentrantlock)

---

## Limitations of Implicit Synchronization

**Implicit Synchronization** = Using `synchronized` keyword

### Limitations:

1. **No timeout** → Thread waits indefinitely for lock
2. **No fairness guarantee** → Any thread can get lock  
3. **No try-and-fail** → Can't attempt to acquire without blocking
4. **No fine control** → Lock and unlock happen automatically
5. **Single condition** → Only one wait set per object

---

## What is ReentrantLock?

**ReentrantLock** = Explicit lock implementation providing more flexible locking operations.

### Features:

✅ **Lock with timeout** (tryLock)  
✅ **Fair/unfair locking**  
✅ **Multiple conditions** (Condition objects)  
✅ **Lock testing** without acquiring  
✅ **Interruptible lock acquisition**  

### Basic Usage:

```java
import java.util.concurrent.locks.ReentrantLock;

ReentrantLock lock = new ReentrantLock();

lock.lock();  // Acquire lock
try {
    // Critical section
} finally {
    lock.unlock();  // MUST unlock in finally block!
}
```

> **CRITICAL:** Always unlock in `finally` block to prevent deadlock!

---

## Lock Fairness

### Unfair Lock (Default):

```java
ReentrantLock lock = new ReentrantLock();  // unfair by default
```

**Behavior:** Any thread can acquire lock (no guarantee of order)  
**Advantage:** Higher throughput  
**Disadvantage:** Starvation possible  

### Fair Lock:

```java
ReentrantLock lock = new ReentrantLock(true);  // fair lock
```

**Behavior:** Threads acquire lock in **FIFO order** (first-come, first-served)  
**Advantage:** No starvation  
**Disadvantage:** Lower throughput  

### Example:

```java
class Demo {
    private ReentrantLock fairLock = new ReentrantLock(true);
    
    public void method() {
        fairLock.lock();
        try {
            System.out.println(Thread.currentThread().getName() + " acquired lock");
            Thread.sleep(100);
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            System.out.println(Thread.currentThread().getName() + " released lock");
            fairLock.unlock();
        }
    }
}
```

**With Fair Lock:** Threads execute in order they requested lock  
**With Unfair Lock:** Order is unpredictable  

---

## tryLock() Method

### Problem with lock():

```java
lock.lock();  // Waits FOREVER if lock not available
```

### Solution: tryLock()

#### Variant 1: Non-blocking

```java
if (lock.tryLock()) {  // Returns immediately
    try {
        // Got the lock!
    } finally {
        lock.unlock();
    }
} else {
    // Couldn't get lock, do something else
}
```

#### Variant 2: With Timeout

```java
if (lock.tryLock(2, TimeUnit.SECONDS)) {  // Wait max 2 seconds
    try {
        // Got the lock!
    } finally {
        lock.unlock();
    }
} else {
    // Timeout: couldn't get lock
}
```

### Complete Example:

```java
import java.util.concurrent.locks.*;
import java.util.concurrent.TimeUnit;

class TryLockDemo {
    private ReentrantLock lock = new ReentrantLock();
    
    public void method1() {
        if (lock.tryLock()) {
            try {
                System.out.println(Thread.currentThread().getName() + 
                                 " acquired lock in method1");
                Thread.sleep(5000);  // Hold lock for 5 seconds
            } catch (InterruptedException e) {
                e.printStackTrace();
            } finally {
                lock.unlock();
            }
        } else {
            System.out.println(Thread.currentThread().getName() + 
                             " could not acquire lock, doing alternative work");
        }
    }
    
    public void method2() {
        try {
            if (lock.tryLock(2, TimeUnit.SECONDS)) {
                try {
                    System.out.println(Thread.currentThread().getName() + 
                                     " acquired lock in method2");
                } finally {
                    lock.unlock();
                }
            } else {
                System.out.println(Thread.currentThread().getName() + 
                                 " timeout waiting for lock");
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

**Output Scenario:**
```
T1 acquired lock in method1
T2 timeout waiting for lock
(after 5 seconds)
T1 released lock
```

---

## Condition Objects

**Condition** = More powerful alternative to wait()/notify().

### Creating Conditions:

```java
ReentrantLock lock = new ReentrantLock();
Condition condition = lock.newCondition();  // Create condition
```

### Condition Methods:

| Method | Equivalent to | Description |
|--------|----------------|-------------|
| `await()` | `wait()` | Releases lock and waits |
| `signal()` | `notify()` | Wakes one waiting thread |
| `signalAll()` | `notifyAll()` | Wakes all waiting threads |

### Multiple Conditions:

```java
Condition notFull = lock.newCondition();   // Producer waits on this
Condition notEmpty = lock.newCondition();  // Consumer waits on this
```

### Producer-Consumer with Conditions:

```java
import java.util.concurrent.locks.*;

class BoundedBuffer {
    private int[] buffer;
    private int count, putIndex, getIndex;
    private ReentrantLock lock = new ReentrantLock();
    private Condition notFull = lock.newCondition();
    private Condition notEmpty = lock.newCondition();
    
    public BoundedBuffer(int size) {
        buffer = new int[size];
    }
    
    public void put(int value) throws InterruptedException {
        lock.lock();
        try {
            while (count == buffer.length) {
                notFull.await();  // Wait until buffer not full
            }
            buffer[putIndex] = value;
            putIndex = (putIndex + 1) % buffer.length;
            count++;
            System.out.println("Produced: " + value);
            notEmpty.signal();  // Signal consumer
        } finally {
            lock.unlock();
        }
    }
    
    public int get() throws InterruptedException {
        lock.lock();
        try {
            while (count == 0) {
                notEmpty.await();  // Wait until buffer not empty
            }
            int value = buffer[getIndex];
            getIndex = (getIndex + 1) % buffer.length;
            count--;
            System.out.println("Consumed: " + value);
            notFull.signal();  // Signal producer
            return value;
        } finally {
            lock.unlock();
        }
    }
}
```

**Advantages over wait/notify:**
- **Multiple conditions** → Separate conditions for different scenarios
- **More precise signaling** → Signal specific waiting threads
- **Better readability** → Clear what each condition represents

---

## Complete Examples

### Example: Bank Transaction with ReentrantLock

```java
import java.util.concurrent.locks.*;

class BankAccount {
    private int balance = 1000;
    private ReentrantLock lock = new ReentrantLock();
    private Condition sufficientFunds = lock.newCondition();
    
    public void withdraw(int amount) {
        lock.lock();
        try {
            while (balance < amount) {
                System.out.println(Thread.currentThread().getName() + 
                                 " waiting for sufficient funds");
                sufficientFunds.await();
            }
            balance -= amount;
            System.out.println(Thread.currentThread().getName() +  
                             " withdrew " + amount + ", balance: " + balance);
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
    
    public void deposit(int amount) {
        lock.lock();
        try {
            balance += amount;
            System.out.println(Thread.currentThread().getName() + 
                             " deposited " + amount + ", balance: " + balance);
            sufficientFunds.signalAll();  // Wake up waiting withdrawals
        } finally {
            lock.unlock();
        }
    }
}
```

---

## synchronized vs ReentrantLock

| Feature | synchronized | ReentrantLock |
|---------|-------------|---------------|
| **Ease of use** | Simple ✅ | More complex |
| **Lock/Unlock** | Automatic ✅ | Manual |
| **Fair locking** | ❌ No | ✅ Yes (optional) |
| **tryLock** | ❌ No | ✅ Yes |
| **Timeout** | ❌ No | ✅ Yes |
| **Interruptible** | ❌ No | ✅ Yes |
| **Multiple conditions** | ❌ No | ✅ Yes |
| **Performance** | Slightly faster | Slightly slower |
| **Risk** | Lower (auto unlock) | Higher (forget unlock) |

### When to Use synchronized:

- ✅ Simple use cases
- ✅ Default choice for most situations
- ✅ Less risk of programmer error

### When to Use ReentrantLock:

- ✅ Need tryLock() functionality
- ✅ Need fair locking
- ✅ Need timeout for lock acquisition
- ✅ Need multiple conditions
- ✅ Need to interrupt waiting threads

---

## Best Practices

### ✅ DO:

1. **Always unlock in finally block:**
   ```java
   lock.lock();
   try {
       // Critical section
   } finally {
       lock.unlock();  // MUST be in finally!
   }
   ```

2. **Use try-finally pattern** immediately after lock()

3. **Prefer synchronized** for simple cases

4. **Use fair lock** only when necessary (performance cost)

### ❌ DON'T:

1. **Don't forget to unlock:**
   ```java
   lock.lock();
   // ... work ...
   lock.unlock();  // ❌ If exception occurs, never unlocks!
   ```

2. **Don't unlock without locking first**

3. **Don't use ReentrantLock** unless you need its advanced features

---

## Summary

**ReentrantLock provides:**
- More flexible locking than synchronized
- tryLock() for non-blocking attempts
- Fair locking option
- Multiple Condition objects
- Interruptible lock acquisition

**Key Takeaways:**
1. Always unlock in finally block
2. Use synchronized for simple cases
3. Use ReentrantLock for advanced scenarios
4. Be careful - manual unlock is error-prone

---

## Interview Questions

### Q1: Difference between synchronized and ReentrantLock?
**A:** synchronized is simpler (auto lock/unlock), ReentrantLock provides tryLock(), fair locking, timeouts, and multiple conditions.

### Q2: What is fair locking?
**A:** Threads acquire lock in FIFO order (first-come, first-served), preventing starvation but with lower throughput.

### Q3: What is tryLock()?
**A:** Non-blocking method to attempt lock acquisition. Returns immediately with true/false instead of waiting.

### Q4: Why unlock in finally block?
**A:** To ensure lock is released even if exception occurs, preventing deadlock.

### Q5: What are Condition objects?
**A:** More powerful alternative to wait/notify, allowing multiple wait sets and more precise signaling.

---

**End of ReentrantLock Notes**
