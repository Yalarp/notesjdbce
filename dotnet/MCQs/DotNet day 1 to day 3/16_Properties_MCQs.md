# 16_Properties – MCQs

## EASY MCQs

### Q1. What is the main purpose of a Property in C#?

A. To replace all methods.  
B. To provide controlled access (read/write) to private fields (encapsulation).  
C. To create static variables.  
D. To inherit from other classes.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Properties provide a flexible mechanism to read, write, or compute the value of a private field, promoting encapsulation and data validation.
</details>

### Q2. Which keywords are used to define the accessors of a property?

A. `read` and `write`  
B. `input` and `output`  
C. `get` and `set`  
D. `this` and `that`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The `get` accessor returns the property value, and the `set` accessor assigns a new value.
</details>

### Q3. What is an "Auto-Implemented Property"?

A. A property that runs on a separate thread.  
B. A property where the compiler automatically creates a private backing field.  
C. A property that cannot be changed.  
D. A property that validates itself.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
With auto-implemented properties (e.g., `public int Age { get; set; }`), the compiler automatically generates the private backing field for you, simplifying the syntax.
</details>

### Q4. Inside the `set` accessor, what keyword represents the new value being assigned?

A. `newVal`  
B. `this`  
C. `value`  
D. `input`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The `value` keyword is an implicit parameter in the `set` accessor that contains the data being assigned to the property.
</details>

---

## MEDIUM MCQs

### Q5. Can you have different access modifiers for `get` and `set` accessors?

A. No, they must match the property's access level.  
B. Yes, but only if the property is private.  
C. Yes, typically to make the getter public and the setter private/protected.  
D. Yes, but only in abstract classes.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
You can restrict one of the accessors (usually the setter) to be more restrictive than the property itself (e.g., `public int Score { get; private set; }`).
</details>

### Q6. What is an "Init-Only" setter (introduced in C# 9)?

A. A setter that initializes the class.  
B. A setter that can only be called during object initialization (in constructor or object initializer), making the property immutable afterwards.  
C. A setter that sets the value to 0.  
D. A static setter.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The `init` accessor allows properties to be set during object construction (including object initializers) but prevents modification once the initialization phase is complete.
</details>

### Q7. Refer to the snippet:
```csharp
public double Area => Width * Height;
```
What type of property is this?

A. Auto-implemented property.  
B. Expression-bodied read-only property (Calculated property).  
C. Static property.  
D. Write-only property.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
This syntax defines a read-only property that computes and returns the value of `Width * Height` whenever accessed. It has no backing field for `Area`.
</details>

### Q8. Which exception is commonly thrown in a setter if validation fails?

A. `NullReferenceException`  
B. `IndexOutOfRangeException`  
C. `ArgumentException` (or `ArgumentOutOfRangeException`)  
D. `SystemException`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Since the value passed to the setter is effectively an argument, `ArgumentException` implies that the provided value violates the property's validation rules.
</details>

---

## HARD MCQs

### Q9. Can a property be passed as a `ref` or `out` parameter?

A. Yes, always.  
B. Yes, if it is an auto-property.  
C. No, properties are actually methods (get/set) internally, not variables with a single memory address.  
D. Only if it is static.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
You cannot pass a property as a `ref` or `out` argument because a property is syntactic sugar for methods (`get_Name`, `set_Name`). It does not point to a single storage location like a field does.
</details>

### Q10. Is it possible to have an interface with a property signature?

A. No, interfaces only contain methods.  
B. Yes, but it must be an auto-property.  
C. Yes, you can specify whether it should have a getter, a setter, or both.  
D. Yes, but it must be static.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Interfaces can define properties. The implementation is left to the class. E.g., `int Id { get; set; }` in an interface requires the implementing class to provide both accessors.
</details>

### Q11. What is the difference between a write-only property and a readonly field?

A. They are opposites: Write-only property has only `set`; Readonly field can only be read (mostly).  
B. Readonly fields are static.  
C. Write-only properties cannot be used in constructors.  
D. There is no difference.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
A write-only property (only `set` defined) can *only* be assigned to; you cannot read its value. A `readonly` field can be read but only assigned during initialization.
</details>

### Q12. If `public int Count { get; } = 10;` is defined in a class, what does it mean?

A. It is a compilation error.  
B. It is a read-only auto-property initialized to 10.  
C. It is a static property.  
D. It returns 10 but can be changed later.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
This is a read-only auto-property with an initializer. The backing field is initialized to 10, and it cannot be changed (except inside the constructor).
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
