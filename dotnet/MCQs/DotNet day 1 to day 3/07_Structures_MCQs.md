# 07_Structures – MCQs

## EASY MCQs

### Q1. What type of data structure is a `struct` in C#?

A. Reference Type  
B. Value Type  
C. Pointer Type  
D. Abstract Type  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
A `struct` is a Value Type, whereas a `class` is a Reference Type. This means structs are typically stored on the stack and hold their data directly.
</details>

### Q2. Which of the following is NOT true about C# structs (prior to C# 10)?

A. They can have fields and methods.  
B. They can implement interfaces.  
C. They can inherit from other structs.  
D. They can use the `new` keyword.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Structs cannot inherit from other structs or classes. They are implicitly sealed. (Note: They can only inherit from System.ValueType implicitly).
</details>

### Q3. Where are struct instances typically stored in memory?

A. Heap  
B. Stack  
C. Global Assembly Cache  
D. Registry  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
As Value Types, struct instances are typically allocated on the Stack (unless they are fields of a class, in which case they reside on the Heap within that object).
</details>

### Q4. What happens when you assign one struct variable to another (e.g., `s2 = s1`)?

A. A reference to the same memory location is copied.  
B. A full copy of the data is created.  
C. `s2` becomes a pointer to `s1`.  
D. `s2` remains null until initialized.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Assigning a struct variable to another creates a full copy of the data (values). Modifying the new copy does not affect the original.
</details>

---

## MEDIUM MCQs

### Q5. Can a struct implement an interface?

A. Yes, but only one.  
B. Yes, they can implement multiple interfaces.  
C. No, only classes can implement interfaces.  
D. No, unless the interface is also a struct.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Structs can implement interfaces just like classes can. However, they cannot inherit from base classes (other than object/ValueType).
</details>

### Q6. Consider the following struct behavior:
```csharp
struct Point { public int X; }
static void Main() {
    Point p1 = new Point();
    p1.X = 10;
    Point p2 = p1;
    p2.X = 20;
    Console.WriteLine(p1.X);
}
```
What is the output?

A. 20  
B. 10  
C. 0  
D. Null  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Because `Point` is a struct (Value Type), `p2 = p1` creates a copy. Changing `p2.X` to 20 leaves `p1.X` at 10.
</details>

### Q7. Why might you choose a struct over a class?

A. When you need inheritance.  
B. When the object needs to be very large.  
C. When you need a lightweight object to represent a single value (like a coordinate) that is short-lived.  
D. When you need a centralized identity for the object.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Structs are ideal for small, lightweight data structures that behave like primitive values, are immutable, and don't require inheritance.
</details>

### Q8. Regarding constructors in structs (in traditional C#), which rule applies?

A. You must explicitly define a parameterless constructor.  
B. You cannot define a parameterless constructor; the system provides one.  
C. You cannot define any constructors.  
D. All constructors must be private.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Traditionally (before C# 10), users could not define a parameterless constructor for a struct. The compiler always provides a default one that zeroes out all fields.
</details>

---

## HARD MCQs

### Q9. Why must all fields be initialized in a struct's parameterized constructor?

A. Because structs are stored on the Heap.  
B. Because the compiler enforces that the struct is fully defined before control is returned to the caller.  
C. It is just a suggestion, not a rule.  
D. Because structs don't support default values.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
In a struct constructor, the `this` object is considered unassigned until all fields are initialized. The compiler enforces this to ensure validity and prevent usage of uninitialized memory.
</details>

### Q10. What is the behavior of `new Point()` vs `Point p;` (without new) for a struct?

A. `new Point()` initializes fields to defaults; `Point p` leaves them unassigned (must assign before use).  
B. `Point p` creates a null reference.  
C. They are exactly the same; both initialize fields to 0.  
D. `new Point()` allocates on Heap; `Point p` allocates on Stack.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
`new Point()` calls the default constructor which zeroes out fields. `Point p;` declares the variable on the stack but leaves fields uninitialized; trying to access them before assignment causes a compile error.
</details>

### Q11. Which method signature correctly passes a struct by reference so that modifications persist?

A. `void Modify(Point p)`  
B. `void Modify(ref Point p)`  
C. `void Modify(out Point p)`  
D. Both B and C allow persistence (though semantics differ).  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** D

**Explanation:**  
`ref` passes the reference to the existing variable, allowing modification. `out` also passes by reference but requires the method to assign a value. Both allow changes to persist outside the method. `ref` is the standard way to modify an existing struct.
</details>

### Q12. Can a struct inherit from `System.ValueType` explicitly?

A. Yes, `struct MyStruct : ValueType { }` is valid.  
B. No, inheritance from `ValueType` is implicit; explicit derivation is not allowed.  
C. Yes, but only if it's abstract.  
D. No, structs inherit from `System.Object` directly.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Structs implicitly inherit from `System.ValueType` (which inherits from `System.Object`). Explicitly specifying `: System.ValueType` in code is not allowed.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
