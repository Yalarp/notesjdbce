# Synchronization and Locks in Java

## Table of Contents
1. [Introduction to Synchronization](#introduction-to-synchronization)
2. [Race Condition Problem](#race-condition-problem)
3. [The synchronized Keyword](#the-synchronized-keyword)
4. [Object Lock Mechanism](#object-lock-mechanism)
5. [Class Lock Mechanism](#class-lock-mechanism)
6. [synchronized Method vs Block](#synchronized-method-vs-block)
7. [Thread-Safe Classes](#thread-safe-classes)
8. [Complete Examples](#complete-examples)

---

## Introduction to Synchronization

**Synchronization** is a mechanism to control access of multiple threads to shared resources to avoid **data corruption**.

###Why Synchronization is Needed?

When threads share memory, there's a risk of **race condition**.

---

## Race Condition Problem

### What is Race Condition?

**Race Condition** = Two or more threads accessing shared data simultaneously, and at least one thread is modifying the data.

### Example Scenario:

```
Thread 1: Reading from file
Thread 2: Writing to file
```

**Problem:**
- While Thread 1 is reading, Thread 2 might write
- While Thread 2 is writing, Thread 1 might read
- **Result:** Data corruption! (inconsistent/partial data)

### Code Example (Without Synchronization):

```java
public class Th6 implements Runnable {
    public void run() {  // NOT synchronized
        for (int i = 0; i < 5; i++) {
            System.out.println("Hello " + i);
        }
    }
    
    public static void main(String args[]) {
        Th6 ob = new Th6();
        Thread t1 = new Thread(ob);
        Thread t2 = new Thread(ob);
        t1.start();
        t2.start();
    }
}
```

**Output:** (unpredictable, interleaved)
```
Hello 0
Hello 0
Hello 1
Hello 1
Hello 2
Hello 2
...
```

**Problem:** Both threads execute `run()` simultaneously, output is mixed!

---

## The synchronized Keyword

**synchronized** ensures that only one thread can execute a method or block at a time.

### Syntax Options:

#### Option 1: synchronized Method

```java
synchronized public void run() {
    // Only one thread can execute this method at a time
}
```

#### Option 2: synchronized Block

```java
public void run() {
    synchronized(this) {
        // Only one thread can execute this block at a time
    }
}
```

---

## Object Lock Mechanism

### What is Object Lock?

> "In Java, every object has a lock. This lock can be accessed by only one thread at a time."

### How It Works:

1. **Thread T1 enters synchronized method/block**
   - T1 **acquires the lock** on the object
   - Other threads trying to enter synchronized methods/blocks must **wait**

2. **T1 completes synchronized method/block**
   - T1 **releases the lock** automatically
   - Another waiting thread can now **acquire the lock**

3. **Which thread gets the lock next?**
   - Depends on **thread scheduler** (same thread might reacquire!)

### Important Points:

✅ **Acquiring and releasing lock is automatic** (you don't write code for it)  
✅ **One lock per object** (not per method)  
✅ **Thread with lock can call ALL synchronized methods** of that object  
✅ **Lock applies only to non-static synchronized methods/blocks**

---

## Complete Examples

### Example 1: With synchronized Method

```java
public class Th6 implements Runnable {
    synchronized public void run() {  // Synchronized!
        for (int i = 0; i < 5; i++) {
            System.out.println("Hello " + i);
        }
    }
    
    public static void main(String args[]) {
        Th6 ob = new Th6();
        Thread t1 = new Thread(ob);
        Thread t2 = new Thread(ob);
        t1.start();
        t2.start();
    }
}
```

**Output:** (sequential, not mixed)
```
Hello 0
Hello 1
Hello 2
Hello 3
Hello 4
Hello 0
Hello 1
Hello 2
Hello 3
Hello 4
```

**Line-by-Line Analysis:**

1. **Line 2:** `run()` method is synchronized
2. **Line 10:** Both threads share **same object** `ob`
3. **Execution:**
   - T1 starts, enters `run()`, **acquires lock on `ob`**
   - T2 tries to enter `run()`, but lock is held by T1
   - T2 goes to "**seeking lock state**" (waiting)
   - T1 completes `run()`, **releases lock**
   - T2 acquires lock, executes `run()`

**Result:** Complete output from one thread, then complete output from other thread.

---

### Example 2: With synchronized Block

```java
public class Th7 implements Runnable {
    public void run() {
        synchronized(this) {  // synchronized block
            for (int i = 0; i < 5; i++) {
                System.out.println("Hello " + i);
            }
        }
    }
    
    public static void main(String args[]) {
        Th7 ob = new Th7();
        Thread t1 = new Thread(ob);
        Thread t2 = new Thread(ob);
        t1.start();
        t2.start();
    }
}
```

**Output:** (same as synchronized method)
```
Hello 0
Hello 1
Hello 2
Hello 3
Hello 4
Hello 0
Hello 1
Hello 2
Hello 3
Hello 4
```

**Synchronized Block Syntax:**
```java
synchronized(object) {
    // Critical section
    // Only one thread can execute this block at a time
}
```

**What is `this`?**
- `this` refers to the current object
- Lock is acquired on **`this` object**

---

### Example 3: Different Objects = Different Locks!

```java
public class Th8 implements Runnable {
    public void run() {
        synchronized(this) {
            for (int i = 0; i < 5; i++) {
                System.out.println("Hello " + i);
            }
        }
    }
    
    public static void main(String args[]) {
        Th8 ob = new Th8();
        Th8 ob1 = new Th8();  // Different object!
        Thread t1 = new Thread(ob);
        Thread t2 = new Thread(ob1);  // Different object!
        t1.start();
        t2.start();
    }
}
```

**Output:** (mixed again!)
```
Hello 0
Hello 0
Hello 1
Hello 1
Hello 2
Hello 2
...
```

**Why Mixed Output?**

- T1 uses object `ob` → Lock on `ob`
- T2 uses object `ob1` → Lock on `ob1`
- **Different objects = Different locks!**
- Both threads can run simultaneously (no contention)

**Key Learning:** Synchronization works only when threads share the **same object**!

---

## synchronized Method vs Block

### synchronized Method

```java
synchronized public void myMethod() {
    // ALL statements in method are protected
    statement1;
    statement2;
    statement3;
}
```

**Advantages:**
- Simple syntax
- Entire method protected

**Disadvantages:**
- **All** statements are synchronized (even if not needed)
- Can reduce performance (more locking)

### synchronized Block

```java
public void myMethod() {
    statement1;  // Not synchronized
    
    synchronized(this) {
        statement2;  // Only this statement needs protection
    }
    
    statement3;  // Not synchronized
}
```

**Advantages:**
- **Fine-grained control** - only critical section is synchronized
- Better performance (less locking)

**Disadvantages:**
- More verbose
- Need to identify critical section

**Best Practice:** Use synchronized block when only part of method needs synchronization.

---

## Class Lock Mechanism

### What is Class Lock?

Every class in Java has a **class lock** (lock on the `Class` object).

### When is Class Lock Used?

For **static synchronized methods**.

```java
class MyClass {
    static synchronized void method1() {
        // Thread needs CLASS lock to execute this
    }
    
    synchronized void method2() {
        // Thread needs OBJECT lock to execute this
    }
}
```

### How It Works:

```
Object Locks (one per instance)      Class Lock (one per class)
┌─────────────┐                      ┌─────────────┐
│ obj1 lock   │                      │ MyClass     │
└─────────────┘                      │ class lock  │
┌─────────────┐                      └─────────────┘
│ obj2 lock   │
└─────────────┘
```

**Key Points:**
- **Object lock** → Used by non-static synchronized methods
- **Class lock** → Used by static synchronized methods
- **Independent** → Thread can hold object lock AND class lock simultaneously

### Example: Class Lock

```java
class ClassLock1 {
    static synchronized void staticMethod() {
        for (int i = 0; i < 5; i++) {
            System.out.println(Thread.currentThread().getName() + " : " + i);
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class Demo {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> ClassLock1.staticMethod());
        Thread t2 = new Thread(() -> ClassLock1.staticMethod());
        
        t1.setName("Thread-1");
        t2.setName("Thread-2");
        
        t1.start();
        t2.start();
    }
}
```

**Output:**
```
Thread-1 : 0
Thread-1 : 1
Thread-1 : 2
Thread-1 : 3
Thread-1 : 4
Thread-2 : 0
Thread-2 : 1
Thread-2 : 2
Thread-2 : 3
Thread-2 : 4
```

**Explanation:**
- Both threads call the **same static method**
- Static method is synchronized → Uses **class lock**
- Only **one class lock** exists for `ClassLock1` class
- Thread-1 acquires class lock first, completes
- Thread-2 then acquires class lock, completes

---

## Thread-Safe Classes

**Thread-Safe Class** = Class with synchronized non-static methods/blocks.

**Examples:**
- `StringBuffer` (thread-safe)
- `Vector` (thread-safe)
- `Hashtable` (thread-safe)

**Non-Thread-Safe Examples:**
- `StringBuilder` (not synchronized, faster)
- `ArrayList` (not synchronized)
- `HashMap` (not synchronized)

### Example: Making a Class Thread-Safe

```java
public class BankAccount {
    private int balance = 1000;
    
    // Thread-safe method
    synchronized public void withdraw(int amount) {
        if (balance >= amount) {
            System.out.println(Thread.currentThread().getName() + 
                             " is withdrawing " + amount);
            balance -= amount;
            System.out.println("Balance after withdrawal: " + balance);
        } else {
            System.out.println("Insufficient balance!");
        }
    }
    
    synchronized public int getBalance() {
        return balance;
    }
}
```

**Why synchronized?**
- Two threads might try to withdraw simultaneously
- Without synchronization → both might withdraw even if balance is insufficient
- With synchronization → only one thread can withdraw at a time

---

## Summary Comparison Table

| Aspect | Non-synchronized | synchronized Method | synchronized Block |
|--------|------------------|---------------------|--------------------|
| **Thread Safety** | ❌ Not safe | ✅ Safe | ✅ Safe |
| **Performance** | Fast | Slower | Moderate |
| **Scope** | N/A | Entire method | Only block |
| **Flexibility** | N/A | Low | High ✅ |
| **Use Case** | Single thread | Simple cases | Fine-grained control ✅ |

---

## Object Lock vs Class Lock

| Aspect | Object Lock | Class Lock |
|--------|-------------|------------|
| **Used by** | Non-static synchronized methods | Static synchronized methods |
| **Number of locks** | One per object instance | One per class |
| **Acquired on** | `this` object | `ClassName.class` object |
| **Independent?** | Yes, from other objects | Yes, from object locks |
| **Example** | `synchronized void method()` | `static synchronized void method()` |

---

## Key Takeaways

1. **Synchronization prevents race condition** by allowing only one thread to execute synchronized code
2. **Object lock** is automatically acquired/released when entering/exiting synchronized method/block
3. **Every object has one lock**, not one per method
4. **Thread with lock can call ALL synchronized methods** of that object
5. **Different objects = different locks** → no synchronization between them
6. **synchronized method** protects entire method
7. **synchronized block** protects only specified block (better performance)
8. **Class lock** is for static synchronized methods
9. **Object locks and class locks are independent**
10. **Thread-safe classes** have synchronized methods

---

## Interview Questions

### Q1: What is synchronization in Java?
**A:** Synchronization is a mechanism to control access of multiple threads to shared resources, preventing race conditions and data corruption.

### Q2: What is race condition?
**A:** When two or more threads access shared data simultaneously and at least one modifies it, leading to unpredictable and incorrect results.

### Q3: What is object lock?
**A:** Every object in Java has a lock that can be acquired by only one thread at a time. When a thread enters a synchronized method/block, it automatically acquires the object lock.

### Q4: Difference between synchronized method and block?
**A:** 
- **Method:** Entire method is synchronized
- **Block:** Only specified block is synchronized (better performance, fine-grained control)

### Q5: What is class lock?
**A:** A lock on the Class object itself, used when static methods are synchronized. Only one class lock exists per class.

### Q6: Can a thread hold both object lock and class lock?
**A:** Yes, they are independent. A thread can hold an object lock and class lock simultaneously.

### Q7: What are thread-safe classes?
**A:** Classes with synchronized methods/blocks that can be safely used by multiple threads. Examples: StringBuffer, Vector, Hashtable.

---

**End of Synchronization and Locks Notes**
