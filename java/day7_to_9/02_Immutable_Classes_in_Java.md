# Immutable Classes in Java

## Table of Contents
1. [What is Immutability?](#what-is-immutability)
2. [Why Immutable Classes?](#why-immutable-classes)
3. [Rules for Creating Immutable Classes](#rules-for-creating-immutable-classes)
4. [Why Immutable Classes Must Be Final](#why-immutable-classes-must-be-final)
5. [Complete Code Examples](#complete-code-examples)
6. [Handling Mutable Fields](#handling-mutable-fields)
7. [Best Practices](#best-practices)

---

## What is Immutability?

**Immutability** means that once an object is created, its state (field values) cannot be changed.

### Characteristics of Immutable Objects:
- No setter methods
- All fields are `final` and `private`
- Class is declared as `final` (cannot be subclassed)
- Safe to share across threads (thread-safe by nature)

### Examples of Immutable Classes in Java:
- `String`
- `Integer`, `Long`, `Double` (wrapper classes)
- `BigDecimal`, `BigInteger`
- `LocalDate`, `LocalDateTime` (Java 8+)

---

## Why Immutable Classes?

### Advantages:

1. **Thread Safety**
   - No synchronization needed
   - Can be safely shared between multiple threads
   - No race condition concerns

2. **Simplicity**
   - Object state never changes after creation
   - Easier to understand and reason about

3. **Security**
   - Cannot be modified by malicious code
   - Safe to pass as parameters

4. **Caching**
   - Can be safely cached and reused
   - Example: String pool in Java

5. **HashMap Keys**
   - Perfect for use as HashMap/HashSet keys
   - Hash code never changes

### Example of Thread Safety Issue with Mutable Class:

```java
class Mutable {
    private int value;
    
    public void setValue(int value) {
        this.value = value;
    }
    
    public int getValue() {
        return value;
    }
}

// Two threads could modify simultaneously - Not thread-safe!
```

### Same Example with Immutable Class:

```java
final class Immutable {
    private final int value;
    
    public Immutable(int value) {
        this.value = value;
    }
    
    public int getValue() {
        return value;
    }
}

// Cannot be modified after creation - Thread-safe!
```

---

## Rules for Creating Immutable Classes

> **CRITICAL:** All 6 rules MUST be followed to create a truly immutable class.

### Rule 1: Declare the Class as `final`
```java
final class ImmutableClass {
    // ...
}
```

**Why?** Prevents subclasses from adding mutability (explained in detail below).

### Rule 2: Make All Fields `private`
```java
private final String name;
private final int age;
```

**Why?** Prevents direct access and modification from outside.

### Rule 3: Make All Fields `final`
```java
private final String name;  // Cannot be reassigned after initialization
```

**Why?** Ensures fields can only be assigned once (in constructor).

### Rule 4: No Setter Methods
```java
//  public void setName(String name) { ... }  // DO NOT provide this!
```

**Why?** Setter methods would allow modification of state.

### Rule 5: Initialize All Fields via Constructor
```java
public ImmutableClass(String name, int age) {
    this.name = name;
    this.age = age;
}
```

**Why?** Only place where fields can be assigned.

### Rule 6: Handle Mutable Fields Carefully
```java
// If field is mutable (like array, Date, List):
// - Make defensive copy in constructor
// - Return defensive copy in getter
```

**Why?** Prevents external modification through references.

---

## Why Immutable Classes Must Be Final

### The Problem: Subclass Can Add Mutability

> **Quote from Documentation:**  
> "The standard argument for making immutable classes final is that if you don't do this, then subclasses can add mutability, thereby violating the contract of the superclass. Clients of the class will assume immutability, but will be surprised when something mutates out from under them."

### Example Problem:

```java
// Immutable base class (NOT final - mistake!)
class Base {
    private final int value;
    
    public Base(int value) {
        this.value = value;
    }
    
    public int getValue() {
        return value;
    }
}

// Malicious or careless subclass
class Sub extends Base {
    private int shadowValue;  // Mutable field!
    
    public Sub(int value) {
        super(value);
        this.shadowValue = value;
    }
    
    @Override
    public int getValue() {
        return shadowValue;  // Returns mutable field instead!
    }
    
    // Adding mutability!
    public void setValue(int value) {
        this.shadowValue = value;
    }
}

// Client code:
public class Demo {
    static void processImmutableObject(Base ref) {
        System.out.println("Initial: " + ref.getValue());
        
        // Client assumes Base is immutable
        // But if ref is actually Sub instance...
        if (ref instanceof Sub) {
            ((Sub) ref).setValue(999);  // Mutates!
        }
        
        System.out.println("After: " + ref.getValue());  // Changed!
    }
    
    public static void main(String[] args) {
        Base b = new Sub(100);
        processImmutableObject(b);
    }
}
```

**Output:**
```
Initial: 100
After: 999    // Immutability contract violated!
```

**Line-by-Line Analysis:**

1. **Lines 2-12:** `Base` class looks immutable (final field, no setter)
2. **Problem:** Class is NOT final, can be subclassed
3. **Lines 15-30:** `Sub` class extends `Base`
4. **Line 16:** Adds mutable `shadowValue` field
5. **Lines 23-26:** Overrides `getValue()` to return mutable field
6. **Lines 29-31:** Adds `setValue()` method - introduces mutability!
7. **Line 36:** Client method expects immutable `Base` object
8. **Line 41:** Casts to `Sub` and mutates state
9. **Result:** Object behaves as mutable, violating immutability contract

### Solution: Make Base Class Final

```java
final class Base {  // Now cannot be subclassed!
    private final int value;
    
    public Base(int value) {
        this.value = value;
    }
    
    public int getValue() {
        return value;
    }
}

// class Sub extends Base { ... }  // Compilation Error!
```

**Result:** Immutability is guaranteed. No subclass can compromise it.

---

## Complete Code Examples

### Example 1: Simple Immutable Class

```java
final class Person {
    // All fields private and final
    private final String name;
    private final int age;
    
    // Initialize through constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Only getters, no setters
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    // toString for displaying
    @Override
    public String toString() {
        return "Person [name=" + name + ", age=" + age + "]";
    }
}

public class Demo1 {
    public static void main(String[] args) {
        Person p = new Person("John", 25);
        System.out.println(p);  // Person [name=John, age=25]
        
        // p.setAge(30);  // Compilation Error: no setter method
        // p.name = "Jane";  // Compilation Error: private field
        
        // Only way to "change" is to create new object
        Person p2 = new Person("Jane", 30);
        System.out.println(p2);  // Person [name=Jane, age=30]
    }
}
```

**Line-by-Line Analysis:**

1. **Line 1:** Class declared as `final` - prevents subclassing
2. **Lines 3-4:** Fields are `private final` - cannot be accessed or reassigned
3. **Lines 7-10:** Constructor - only place where fields are initialized
4. **Lines 13-19:** Only getters provided, no setters
5. **Line 28:** Create immutable object
6. **Lines 31-32:** Cannot modify (compilation errors)
7. **Line 35:** To get different values, create new object

---

### Example 2: Immutable Class with Mutable Field (WRONG WAY)

```java
import java.util.Arrays;

final class Student {
    private final String name;
    private final int[] marks;  // Array is mutable!
    
    public Student(String name, int[] marks) {
        this.name = name;
        this.marks = marks;  // Direct assignment - DANGEROUS!
    }
    
    public String getName() {
        return name;
    }
    
    public int[] getMarks() {
        return marks;  // Returning direct reference - DANGEROUS!
    }
    
    @Override
    public String toString() {
        return "Student [name=" + name + ", marks=" + Arrays.toString(marks) + "]";
    }
}

public class Demo2 {
    public static void main(String[] args) {
        int[] marks = {90, 85, 88};
        Student s = new Student("Alice", marks);
        
        System.out.println(s);  // Student [name=Alice, marks=[90, 85, 88]]
        
        // PROBLEM 1: Modifying original array after construction
        marks[0] = 0;
        System.out.println(s);  // Student [name=Alice, marks=[0, 85, 88]] - Changed!
        
        // PROBLEM 2: Modifying through getter
        int[] marksRef = s.getMarks();
        marksRef[1] = 0;
        System.out.println(s);  // Student [name=Alice, marks=[0, 0, 88]] - Changed again!
    }
}
```

**Problems Identified:**

1. **Line 9:** Direct assignment of array reference
   - Both `marks` parameter and `this.marks` point to same array
   - Modifications to parameter array affect object state
   
2. **Line 16:** Returning direct reference to array
   - Caller can modify the returned array
   - Violates immutability

**Output:**
```
Student [name=Alice, marks=[90, 85, 88]]
Student [name=Alice, marks=[0, 85, 88]]    // Immutability violated!
Student [name=Alice, marks=[0, 0, 88]]     // Violated again!
```

---

### Example 3: Immutable Class with Mutable Field (CORRECT WAY)

```java
import java.util.Arrays;

final class Student {
    private final String name;
    private final int[] marks;
    
    public Student(String name, int[] marks) {
        this.name = name;
        // Defensive copy in constructor
        this.marks = marks.clone();  // Create copy, not store reference!
    }
    
    public String getName() {
        return name;
    }
    
    public int[] getMarks() {
        // Defensive copy in getter
        return marks.clone();  // Return copy, not direct reference!
    }
    
    @Override
    public String toString() {
        return "Student [name=" + name + ", marks=" + Arrays.toString(marks) + "]";
    }
}

public class Demo3 {
    public static void main(String[] args) {
        int[] marks = {90, 85, 88};
        Student s = new Student("Alice", marks);
        
        System.out.println(s);  // Student [name=Alice, marks=[90, 85, 88]]
        
        // TRY TO MODIFY: Modifying original array after construction
        marks[0] = 0;
        System.out.println(s);  // Student [name=Alice, marks=[90, 85, 88]] - Unchanged! ✓
        
        // TRY TO MODIFY: Modifying through getter
        int[] marksRef = s.getMarks();
        marksRef[1] = 0;
        System.out.println(s);  // Student [name=Alice, marks=[90, 85, 88]] - Still unchanged! ✓
    }
}
```

**Solution Explained:**

1. **Line 10:** `this.marks = marks.clone()`
   - Creates **defensive copy** of input array
   - Object stores its own independent array
   - Modifications to parameter array don't affect object

2. **Line 19:** `return marks.clone()`
   - Returns **defensive copy** of internal array
   - Caller gets new array, not reference to internal array
   - Modifications to returned array don't affect object

**Output:**
```
Student [name=Alice, marks=[90, 85, 88]]
Student [name=Alice, marks=[90, 85, 88]]   // Unchanged! ✓
Student [name=Alice, marks=[90, 85, 88]]   // Still unchanged! ✓
```

**Key Learning:** Always use defensive copying for mutable fields in immutable classes!

---

### Example 4: Immutable Class with Nested Mutable Object

```java
class Address {  // Mutable class
    private String city;
    private String street;
    
    public Address(String city, String street) {
        this.city = city;
        this.street = street;
    }
    
    public String getCity() {
        return city;
    }
    
    public void setCity(String city) {
        this.city = city;  // Setter - makes it mutable!
    }
    
    public String getStreet() {
        return street;
    }
    
    public void setStreet(String street) {
        this.street = street;
    }
    
    @Override
    public String toString() {
        return "Address [city=" + city + ", street=" + street + "]";
    }
}

// Attempt to make immutable class with mutable field
final class Employee {
    private final String name;
    private final Address address;  // Reference to mutable object
    
    public Employee(String name, Address address) {
        this.name = name;
        // Need defensive copy, but Address doesn't support cloning!
        this.address = new Address(address.getCity(), address.getStreet());  
    }
    
    public String getName() {
        return name;
    }
    
    public Address getAddress() {
        // Return defensive copy
        return new Address(address.getCity(), address.getStreet());
    }
    
    @Override
    public String toString() {
        return "Employee [name=" + name + ", address=" + address + "]";
    }
}

public class Demo4 {
    public static void main(String[] args) {
        Address addr = new Address("Mumbai", "MG Road");
        Employee emp = new Employee("Bob", addr);
        
        System.out.println(emp);
        // Employee [name=Bob, address=Address [city=Mumbai, street=MG Road]]
        
        // Try to modify original address
        addr.setCity("Delhi");
        System.out.println(emp);  
        // Employee [name=Bob, address=Address [city=Mumbai, street=MG Road]]
        // Unchanged! ✓
        
        // Try to modify through getter
        Address empAddr = emp.getAddress();
        empAddr.setCity("Pune");
        System.out.println(emp);
        // Employee [name=Bob, address=Address [city=Mumbai, street=MG Road]]
        // Still unchanged! ✓
    }
}
```

**Solution for Nested Mutable Objects:**

1. **Line 40:** Defensive copy in constructor
   - Create new `Address` using values from parameter
   - Object has its own independent `Address` instance

2. **Lines 48-49:** Defensive copy in getter
   - Return new `Address` with copied values
   - Caller cannot modify internal `Address`

**Best Practice:** Make nested classes immutable too! If `Address` were immutable, defensive copying wouldn't be needed.

---

### Example 5: The Danger of Not Making Class Final

```java
// Base class - immutable but NOT final (MISTAKE!)
class Base {
    private final int value;
    
    public Base(int value) {
        this.value = value;
    }
    
    public int getValue() {
        return value;
    }
}

// Subclass adds mutability
class Sub extends Base {
    private int shadowValue;  // Mutable field
    
    public Sub(int value) {
        super(value);
        this.shadowValue = value;
    }
    
    @Override
    public int getValue() {
        return shadowValue;  // Returns mutable field
    }
    
    public void setValue(int value) {
        this.shadowValue = value;  // Allows modification!
    }
}

public class Demo5 {
    static void showBaseData(Base ref) {
        System.out.println("Value: " + ref.getValue());
    }
    
    public static void main(String[] args) {
        // Client expects immutable Base object
        Base b1 = new Base(100);
        showBaseData(b1);  // Value: 100
        showBaseData(b1);  // Value: 100 - unchanged ✓
        
        // But Sub violates immutability contract
        Base b2 = new Sub(200);  // Polymorphism
        showBaseData(b2);  // Value: 200
        
        ((Sub) b2).setValue(999);  // Mutate!
        showBaseData(b2);  // Value: 999 - changed! ✗
        
        // Immutability contract violated!
    }
}
```

**Output:**
```
Value: 100
Value: 100
Value: 200
Value: 999    // Immutability violated!
```

**Line-by-Line Analysis:**

1. **Line 2:** `Base` not declared final - can be subclassed
2. **Lines 14-30:** `Sub` extends `Base` and adds mutability
3. **Line 23:** Overrides `getValue()` to return mutable field
4. **Line 27:** Adds `setValue()` - introduces mutation
5. **Line 43:** `Sub` object assigned to `Base` reference (polymorphism)
6. **Line 46:** Downcasts and mutates
7. **Result:** Object initially thought to be immutable is now mutable!

**Solution:**
```java
final class Base {  // Add final keyword
    // ...
}

// class Sub extends Base { ... }  // Compilation Error!
```

---

## Handling Mutable Fields

### Types of Fields:

| Field Type | Mutability | Handling |
|------------|------------|----------|
| Primitive (`int`, `boolean`, etc.) | Immutable | Direct assignment OK |
| `String` | Immutable | Direct assignment OK |
| Wrapper classes (`Integer`, `Long`, etc.) | Immutable | Direct assignment OK |
| Arrays | **Mutable** | Defensive copy required |
| Collections (`List`, `Set`, `Map`) | **Mutable** | Defensive copy or unmodifiable wrapper |
| Date (`java.util.Date`) | **Mutable** | Defensive copy or use `LocalDate` |
| Custom objects | Depends | Defensive copy or ensure immutability |

### Defensive Copying Example for Collections:

```java
import java.util.*;

final class Team {
    private final String name;
    private final List<String> players;
    
    public Team(String name, List<String> players) {
        this.name = name;
        // Create defensive copy
        this.players = new ArrayList<>(players);  // New list with copied elements
    }
    
    public List<String> getPlayers() {
        // Return unmodifiable view
        return Collections.unmodifiableList(players);
        // OR return defensive copy:
        // return new ArrayList<>(players);
    }
}
```

---

## Best Practices

### ✅ DO:

1. **Declare class as `final`** - prevents subclass mutability
2. **Make all fields `private final`** - encapsulation + immutability
3. **Initialize all fields in constructor** - single point of initialization
4. **Provide only getters, no setters** - read-only access
5. **Use defensive copying for mutable fields** - protect internal state
6. **Prefer immutable types for fields** - `String`, `Integer`, `LocalDate`
7. **Make nested objects immutable too** - deep immutability

### ❌ DON'T:

1. **Don't forget the `final` keyword on class** - subclasses can add mutability
2. **Don't return references to mutable fields** - use defensive copying
3. **Don't directly assign mutable parameters** - clone/copy them first
4. **Don't provide any method that modifies state** - even indirectly

---

## Real-World Examples

### String Class (Immutable):

```java
String s1 = "Hello";
String s2 = s1.concat(" World");

System.out.println(s1);  // Hello (unchanged)
System.out.println(s2);  // Hello World (new object)
```

**Key Point:** String operations never modify the original string; they create new strings.

### Integer Class (Immutable):

```java
Integer i1 = 10;
Integer i2 = i1 + 5;

System.out.println(i1);  // 10 (unchanged)
System.out.println(i2);  // 15 (new object)
```

---

## Summary

### The 6 Rules of Immutability:

1. ✅ Declare class as `final`
2. ✅ Make all fields `private final`
3. ✅ Initialize all fields via constructor only
4. ✅ Provide no setter methods
5. ✅ Use defensive copying for mutable fields
6. ✅ Return defensive copies from getters for mutable fields

### Why `final` Class is Critical:

> **"Subclasses can add mutability, thereby violating the contract of the superclass. Clients will assume immutability, but will be surprised when something mutates."**

### Benefits Recap:

- **Thread-safe** without synchronization
- **Simple** and predictable behavior
- **Secure** - cannot be tampered with
- **Cacheable** - safe to reuse
- **Perfect for HashMap keys**

---

## Interview Questions

### Q1: Why should immutable classes be final?
**A:** To prevent subclasses from adding mutability and violating the immutability contract. A subclass could override methods and introduce mutable behavior, surprising clients who expect immutability.

### Q2: Can an immutable class have mutable fields?
**A:** Technically yes, but you must use defensive copying in both constructor and getters to maintain immutability. However, it's better to use only immutable fields.

### Q3: What is defensive copying?
**A:** Creating a copy of a mutable object instead of using the reference directly, to prevent external modification of internal state.

### Q4: Is `String` class immutable?
**A:** Yes. All String methods return new String objects instead of modifying the original.

### Q5: How do you make a class with an array field immutable?
**A:** Use `array.clone()` in both constructor (to copy input) and getter (to return copy).

### Q6: Can we create immutable class without final keyword?
**A:** Not safely. Without `final`, subclasses can add mutability, breaking the immutability guarantee.

---

**End of Immutable Classes Notes**
