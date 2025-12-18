# Object Cloning in Java

## Table of Contents
1. [Introduction to Object Cloning](#introduction-to-object-cloning)
2. [Why Object Cloning is Needed](#why-object-cloning-is-needed)
3. [Two Ways to Copy Objects](#two-ways-to-copy-objects)
4. [Cloneable Interface](#cloneable-interface)
5. [Why clone() is Protected](#why-clone-is-protected)
6. [Shallow Copy vs Deep Copy](#shallow-copy-vs-deep-copy)
7. [Complete Code Examples](#complete-code-examples)
8. [Best Practices](#best-practices)

---

## Introduction to Object Cloning

**Object Cloning** is the process of creating an exact copy of an existing object. In Java, when you create a copy, you get a new object with the same state (field values) as the original object.

### Key Points:
- Cloning creates a new object with the same field values
- The new object has a different memory address
- Not all classes are cloneable by default

---

## Why Object Cloning is Needed

### Problem: Reference Assignment vs Object Copying

When you write:
```java
Car c1 = new Car("Nano");
Car c2 = c1;  // This is NOT copying the object
```

**What happens?**
- Both `c1` and `c2` point to the **same object** in memory
- Modifying `c2` will also affect `c1`
- This is called **reference assignment**, not object copying

### Solution: Object Cloning

Cloning creates a **new object** with copied field values:
```java
Car c1 = new Car("Nano");
Car c2 = (Car) c1.clone();  // This creates a new object
```

Now `c1` and `c2` are separate objects with their own memory locations.

---

## Two Ways to Copy Objects

### Method 1: Using `clone()` Method
- Provided by `java.lang.Object` class
- **By default creates Shallow Copy**
- Requires implementing `Cloneable` interface

### Method 2: Using Serialization
- Store object in file system, then read it back
- **Always does Deep Copy**
- Requires implementing `Serializable` interface

**Note:** In this chapter, we focus on the `clone()` method.

---

## Cloneable Interface

### What is Cloneable?
`Cloneable` is a **marker interface** in Java (has no methods).

```java
public interface Cloneable {
    // No methods - it's a marker interface
}
```

### Purpose
- Signals to JVM that this class permits cloning
- If you call `clone()` on a non-cloneable object, you get `CloneNotSupportedException`

### Why Doesn't Object Class Implement Cloneable?

> **Question:** Does Object class implement Cloneable interface?  
> **Answer:** No.

**Reason:**
- If `Object` class implemented `Cloneable`, **every class in Java** would become cloneable automatically
- Java designers wanted to give programmer the **choice** whether to make their class cloneable or not
- This is a design decision for flexibility and security

---

## Why clone() is Protected

### The clone() Method Signature

```java
protected Object clone() throws CloneNotSupportedException
```

### Why Protected Access Modifier?

**Scenario:**
```java
// Developer creates a class
public class MyClass {
    // members and methods
}
```

This class inherits `protected Object clone()` from Object class.

**Question:** Can a client from another package invoke `clone()` on MyClass?

**Answer:**
- **If client creates child class** of MyClass → Yes, can invoke `clone()` through inheritance
- **If client creates object** of MyClass → No, cannot invoke (protected access)

**Purpose:**
- Gives the **developer control** whether clients should be able to clone their objects
- If developer wants to allow cloning, they can **override with public** accessibility:

```java
@Override
public Object clone() throws CloneNotSupportedException {
    return super.clone();
}
```

---

## Shallow Copy vs Deep Copy

### Shallow Copy

**Definition:** Copies the object's direct fields, but if a field is a reference to another object, only the reference is copied (not the object itself).

**Diagram:**
```
Original Object                  Cloned Object
┌─────────────┐                 ┌─────────────┐
│ name: "Nano"│                 │ name: "Nano"│
│ ref: ───────┼────┐    ┌───────┼─ ref:       │
└─────────────┘    │    │       └─────────────┘
                   ├────┘
                   ↓
            ┌──────────────┐
            │ Engine       │
            │ speed: 100   │
            └──────────────┘
```

**Result:** Both original and cloned objects share the **same Engine object**!

### Deep Copy

**Definition:** Copies the object and all objects it references, creating completely independent copies.

**Diagram:**
```
Original Object                  Cloned Object
┌─────────────┐                 ┌─────────────┐
│ name: "Nano"│                 │ name: "Nano"│
│ ref: ───────┼───→             │ ref: ───────┼───→
└─────────────┘                 └─────────────┘
     │                                 │
     ↓                                 ↓
┌──────────────┐              ┌──────────────┐
│ Engine       │              │ Engine       │
│ speed: 100   │              │ speed: 100   │
└──────────────┘              └──────────────┘
```

**Result:** Each object has its **own independent Engine object**.

---

## Complete Code Examples

### Example 1: Error When clone() is Protected

```java
class Engine {
    private int speed;
    
    public Engine(int speed) {
        super();  // Calls Object's constructor
        this.speed = speed;
    }
    
    public int getSpeed() {
        return speed;
    }
    
    public void setSpeed(int speed) {
        this.speed = speed;
    }
}

class Car implements Cloneable {
    private Engine ref;
    private String name;
    
    public Car(String name) {
        super();  // Calls Object's constructor
        this.name = name;
        this.ref = new Engine(100);  // Creating Engine with speed 100
    }
    
    // Getters and setters
    public Engine getRef() {
        return ref;
    }
    
    public void setRef(Engine ref) {
        this.ref = ref;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    // Note: clone() method is NOT overridden here
}

public class Demo {
    public static void main(String[] args) {
        Car c = new Car("Nano");  // Create Car object
        try {
            c.clone();  // ERROR: The method clone() from Object is not visible
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        } 
        System.out.println("Done");
    }
}
```

**Line-by-Line Analysis:**
1. **Line 1-9:** `Engine` class with private `speed` field, constructor, and getter/setter
2. **Line 11:** `Car` implements `Cloneable` interface (marker)
3. **Line 12-13:** Two private fields: `ref` (Engine reference) and `name` (String)
4. **Line 15-19:** Constructor initializes name and creates new Engine with speed 100
5. **Line 47:** Attempt to call `clone()` fails because it's **protected** in Object class
6. **Error:** Cannot access protected method from different package without overriding

**Key Learning:** Even though Car implements Cloneable, `clone()` is still protected, so it cannot be called from outside.

---

### Example 2: Overriding clone() with Protected Access (Still Doesn't Work for Client)

```java
class Engine {
    private int speed;
    
    public Engine(int speed) {
        super();
        this.speed = speed;
    }
    
    public int getSpeed() {
        return speed;
    }
    
    public void setSpeed(int speed) {
        this.speed = speed;
    }
}

class Car implements Cloneable {
    private Engine ref;
    private String name;
    
    public Car(String name) {
        super();
        this.name = name;
        this.ref = new Engine(100);
    }
    
    public Engine getRef() {
        return ref;
    }
    
    public void setRef(Engine ref) {
        this.ref = ref;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();  // Call Object's clone() method
    }
}

public class Test1 {
    public static void main(String[] args) {
        Car c = new Car("Nano");
        try {
            c.clone();  // Still ERROR if called from different package
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        } 
        System.out.println("Done");
    }
}
```

**Line-by-Line Analysis:**
1. **Lines 40-44:** Overriding `clone()` method but keeping it `protected`
2. **Line 43:** `super.clone()` calls Object class's native `clone()` method
3. **Line 53:** Still cannot call from different package because it's protected

**Key Learning:** Overriding with protected access doesn't help clients in other packages.

---

### Example 3: Shallow Copy Demonstration

```java
class Engine {
    private int speed;
    
    public Engine(int speed) {
        super();
        this.speed = speed;
    }
    
    public int getSpeed() {
        return speed;
    }
    
    public void setSpeed(int speed) {
        this.speed = speed;
    }
    
    @Override
    public String toString() {
        return "Engine [speed=" + speed + "]";  // For printing Engine details
    }
}

class Car implements Cloneable {
    private Engine ref;
    private String name;
    
    public Car(String name) {
        super();
        this.name = name;
        this.ref = new Engine(100);  // Speed initialized to 100
    }
    
    public Engine getRef() {
        return ref;
    }
    
    public void setRef(Engine ref) {
        this.ref = ref;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    // Making clone() public so clients can access it
    public Object clone() {
        Car ob = null;
        try {
            ob = (Car) super.clone();  // Call Object's clone() - creates shallow copy
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return ob;  // Return the cloned object
    }
    
    @Override
    public String toString() {
        return "[name=" + name + " ref=" + ref + "]";  // Print Car details
    }
}

public class Test2 {
    public static void main(String[] args) {
        Car c = new Car("Nano");  // Create original Car
        Car c1 = (Car) c.clone();  // Clone the Car
        
        System.out.println(c);   // Print original
        System.out.println(c1);  // Print clone
        
        c1.getRef().setSpeed(400);  // Modify cloned car's engine speed
        
        System.out.println("After Modification");
        
        System.out.println(c);   // Original Car's engine ALSO changed!
        System.out.println(c1);  // Cloned Car's engine changed
    }
}
```

**Execution Flow:**

1. **Line 68:** Create Car `c` with name "Nano" and Engine with speed 100
   - Memory: `c` → Car object → Engine(100)

2. **Line 69:** Clone `c` to create `c1`
   - `clone()` is called on line 48
   - Line 51: `super.clone()` creates **shallow copy**
   - Memory: `c1` → New Car object → **Same Engine object**

3. **Lines 71-72:** Print both cars
   ```
   [name=Nano ref=Engine [speed=100]]
   [name=Nano ref=Engine [speed=100]]
   ```

4. **Line 74:** `c1.getRef().setSpeed(400)`
   - Get Engine reference from `c1`
   - Set its speed to 400
   - **Problem:** Both `c` and `c1` share the same Engine!

5. **Lines 78-79:** Print both cars again
   ```
   [name=Nano ref=Engine [speed=400]]  ← Original also changed!
   [name=Nano ref=Engine [speed=400]]
   ```

**Key Learning:** 
- `super.clone()` creates **shallow copy**
- Reference fields (like `Engine ref`) are copied, but point to **same object**
- Modifying referenced object affects both original and clone

---

### Example 4: Deep Copy Implementation

```java
class Engine {
    private int speed;
    
    public Engine(int speed) {
        super();
        this.speed = speed;
    }
    
    public int getSpeed() {
        return speed;
    }
    
    public void setSpeed(int speed) {
        this.speed = speed;
    }
    
    @Override
    public String toString() {
        return "Engine [speed=" + speed + "]";
    }
}

class Car implements Cloneable {
    private Engine ref;
    private String name;
    
    public Car(String name) {
        super();
        this.name = name;
        this.ref = new Engine(100);
    }
    
    public Engine getRef() {
        return ref;
    }
    
    public void setRef(Engine ref) {
        this.ref = ref;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    // Deep copy implementation
    public Object clone() {
        Car ob = null;
        try {
            ob = (Car) super.clone();  // First do shallow copy
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        // CRITICAL LINE: Create new Engine object for the clone
        ob.ref = new Engine(ref.getSpeed());  // Deep copy of Engine
        return ob;
    }
    
    @Override
    public String toString() {
        return "[name=" + name + " ref=" + ref + "]";
    }
}

public class Test3 {
    public static void main(String[] args) {
        Car c = new Car("Nano");  // Create original Car
        Car c1 = (Car) c.clone();  // Clone the Car
        
        System.out.println(c);   // Print original
        System.out.println(c1);  // Print clone
        
        c1.getRef().setSpeed(400);  // Modify cloned car's engine speed
        
        System.out.println("After Modification");
        
        System.out.println(c);   // Original Car's engine UNCHANGED!
        System.out.println(c1);  // Only cloned Car's engine changed
    }
}
```

**Execution Flow:**

1. **Line 68:** Create Car `c` with name "Nano" and Engine with speed 100
   - Memory: `c` → Car object → Engine(100)

2. **Line 69:** Clone `c` to create `c1`
   - Control goes to `clone()` method (line 48)
   - **Line 51:** `super.clone()` creates shallow copy of Car
     - New Car object created
     - But `ref` still points to same Engine
   - **Line 56:** **CRITICAL - Deep Copy Logic**
     - `new Engine(ref.getSpeed())` creates **new Engine object**
     - Gets speed from original Engine (100)
     - Creates new Engine with same speed
     - Assigns to cloned Car's `ref` field
   - Memory now: `c1` → New Car object → **New Engine(100)**

3. **Lines 71-72:** Print both cars
   ```
   [name=Nano ref=Engine [speed=100]]
   [name=Nano ref=Engine [speed=100]]
   ```

4. **Line 74:** `c1.getRef().setSpeed(400)`
   - Get Engine reference from `c1`
   - This is now a **different Engine object**
   - Set its speed to 400
   - Original Engine remains unchanged

5. **Lines 78-79:** Print both cars again
   ```
   [name=Nano ref=Engine [speed=100]]  ← Original unchanged!
   [name=Nano ref=Engine [speed=400]]  ← Only clone changed!
   ```

**Key Learning:**
- **Line 56** is the key: `ob.ref = new Engine(ref.getSpeed())`
- This creates a **new Engine object** for the cloned Car
- Now original and clone have **separate, independent** Engine objects
- Modifying one doesn't affect the other

---

## Practical Example: Protecting Immutable Class Data

### Problem: Array Reference Leaks in Immutable Classes

```java
class Center {  // Intended to be Immutable
    private String name, address;
    private int prnnos[];  // Array of PRN numbers
    
    public Center(String name, String address, int[] prnnos) {
        super();
        this.name = name;
        this.address = address;
        this.prnnos = prnnos;  // Direct assignment - DANGEROUS!
    }
    
    public int[] getPrnnos() {
        return prnnos;  // Returning direct reference - DANGEROUS!
    }
    
    // Other getters...
}

public class Test {
    public static void main(String args[]) {
        Center c1 = new Center("Vita", "mumbai", new int[]{100, 200, 300, 400, 500});
        System.out.println(c1);  // Center [name=Vita, address=mumbai, prnnos=[100, 200, 300, 400, 500]]
        
        int temp[] = c1.getPrnnos();  // Get reference to internal array
        temp[1] = 0;  // VIOLATION: Modifying internal state!
        
        System.out.println(c1);  // Center [name=Vita, address=mumbai, prnnos=[100, 0, 300, 400, 500]]
        // Immutability is broken!
    }
}
```

**Problem:** Even though Center has no setters, the array can be modified from outside!

### Solution 1: Return Fixed Copy (Hard-coded)

```java
public int[] getPrnnos() {
    int prncopy[] = {100, 200, 300, 400, 500};  // Return new array
    return prncopy;
}
```

**Issue:** Hard-coded values, not flexible.

### Solution 2: Return Cloned Array (Best Practice)

```java
public int[] getPrnnos() {
    int[] prncopy = prnnos.clone();  // Clone the array
    return prncopy;  // Return the copy
}
```

**Why This Works:**
- `prnnos.clone()` creates a **new array** with copied values
- Modifications to returned array don't affect internal `prnnos`
- Maintains true immutability

**Key Learning:** Arrays in Java are objects, and their `clone()` method creates a **shallow copy** (which is sufficient for primitive arrays).

---

## Best Practices

### ✅ DO:

1. **Implement Cloneable interface** if you want your class to support cloning
2. **Override clone() with public access** if you want clients to clone your objects
3. **Implement deep copy** if your class has reference fields
4. **Handle CloneNotSupportedException** appropriately
5. **Use clone() for arrays** when returning internal arrays from immutable classes

### ❌ DON'T:

1. **Don't rely on default clone()** if you have reference fields (shallow copy problem)
2. **Don't forget to implement Cloneable** - you'll get `CloneNotSupportedException`
3. **Don't return internal references** from getters in immutable classes
4. **Don't modify returned arrays** - always work with copies

---

## Summary Table

| Aspect | Shallow Copy | Deep Copy |
|--------|--------------|-----------|
| **Primitive fields** | Copied ✅ | Copied ✅ |
| **String fields** | Copied ✅ (immutable) | Copied ✅ (immutable) |
| **Reference fields** | Reference copied ⚠️ | New object created ✅ |
| **Independence** | Partial (shared references) | Complete |
| **Implementation** | `super.clone()` | `super.clone()` + manual copying |
| **Use case** | Objects with only primitives/Strings | Objects with mutable references |

---

## Key Takeaways

1. **Cloning creates a new object** with copied field values
2. **Cloneable is a marker interface** - signals JVM to allow cloning
3. **clone() is protected** to give developers control over cloneability
4. **Default clone() creates shallow copy** - only copies references
5. **Deep copy requires manual implementation** - create new objects for references
6. **Use clone() for array protection** in immutable classes
7. **Two ways to copy objects:** clone() (shallow by default) and serialization (always deep)

---

## Interview Questions

### Q1: Why is clone() method protected in Object class?
**A:** To give developers the choice whether their class should be cloneable by clients. If a developer wants to allow cloning, they can override with public access.

### Q2: What is the difference between shallow copy and deep copy?
**A:** Shallow copy copies field values, but for reference fields, only the reference is copied (both objects share the same referenced object). Deep copy creates new objects for all reference fields, making completely independent copies.

### Q3: What happens if you call clone() without implementing Cloneable?
**A:** You get `CloneNotSupportedException` at runtime.

### Q4: Does Object class implement Cloneable?
**A:** No. If it did, every class would be cloneable, which Java designers didn't want - they wanted to give programmers the choice.

### Q5: How do you protect an immutable class from array modifications?
**A:** Return a clone of the array in the getter method: `return array.clone();`

---

**End of Object Cloning Notes**
