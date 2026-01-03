# 02_Downcasting_TypeConversion – MCQs

## EASY MCQs

### Q1. Casting a subclass reference to a base class reference is called:
A. Downcasting  
B. Upcasting  
C. Sidecasting  
D. Broadcasting  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Moving up the inheritance hierarchy (Child -> Parent) is called Upcasting. It is implicit and safe.
</details>

### Q2. Which casting direction can fail at runtime?
A. Upcasting  
B. Downcasting  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Downcasting (Parent -> Child) assumes the object is of a specific child type. If it's not, an `InvalidCastException` occurs (or null if using `as`).
</details>

### Q3. What operator checks if an object is compatible with a given type and returns true/false?
A. `as`  
B. `check`  
C. `is`  
D. `typeof`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `is` operator checks if the runtime type of an object is compatible with a given type and returns a boolean.
</details>

### Q4. If the `as` operator fails to cast, what does it return?
A. `false`  
B. `0`  
C. `null`  
D. Throws an exception  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `as` operator performs a safe cast. If the cast is not possible, it returns `null` instead of raising an exception.
</details>

### Q5. Can you use `as` with value types (e.g. `int`)?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `as` operator must return `null` on failure, and value types (non-nullable) cannot be null. Therefore `as` works only with reference types or nullable value types.
</details>

---

## MEDIUM MCQs

### Q6. Which exception is thrown when an explicit downcast fails?
A. `NullReferenceException`  
B. `InvalidCastException`  
C. `TypeLoadException`  
D. `ArgumentException`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
An explicit cast (e.g., `(Circle)shape`) throws `System.InvalidCastException` if the runtime type does not match the target type.
</details>

### Q7. Consider `Shape s = new Square();`. Is `((Circle)s)` valid at compile time?
A. No, compiler catches it.  
B. Yes, but fails at runtime.  
C. Yes, and logic works if they are empty classes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The compiler allows it because `Circle` inherits `Shape`, so `s` *could* theoretically be a `Circle`. It trusts you. At runtime, the check fails because `s` is actually a `Square`.
</details>

### Q8. What is the benefit of Pattern Matching with `is` (e.g., `if (o is string s)`)?
A. It runs faster than `as`.  
B. It combines the type check and assignment in one step.  
C. It allows checking multiple types simultaneously.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Introduced in C# 7, it allows `if (obj is Type variableName)`, which checks the type and casts it to `variableName` immediately if successful.
</details>

### Q9. Why would you perform a downcast?
A. To call a base class method.  
B. To access methods specific to the derived class that are not in the base class.  
C. To free memory.  
D. To convert a class to a struct.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A base reference only sees base members. To allow access to functionality unique to the subclass, you must downcast.
</details>

### Q10. What is the output? `object o = 10; string s = o as string; Console.Write(s == null);`
A. True  
B. False  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`o` holds an integer (boxed). Casting it `as string` fails because an int is not a string. `as` returns `null`. So `s == null` is true.
</details>

---

## HARD MCQs

### Q11. Upcasting is analogous to:
A. Generalization  
B. Specialization  
C. Serialization  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Upcasting treats a specific type (Dog) as a general type (Animal). This is generalization. Downcasting is specialization.
</details>

### Q12. Can you cast across sibling types? (e.g. `Square` to `Circle`, both inherit `Shape`)
A. Yes, using explicit cast.  
B. No, never.  
C. Yes, if they implement the same interface.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You can only cast up or down the inheritance chain. Siblings share a parent but have no IS-A relationship with each other, so they cannot be cast to one another directly.
</details>

### Q13. `(shape as Circle)?.FillCircle()` relies on what feature?
A. Null-coalescing operator  
B. Null-conditional operator  
C. Ternary operator  
D. Lambda expression  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `?.` syntax is the Null-conditional operator. It attempts to access the member only if the left-hand operand (`shape as Circle`) is not null.
</details>

### Q14. If `Dog` inherits `Animal`, and you have `Animal a = null;`. Is `(Dog)a` valid?
A. Throws NullReferenceException.  
B. Throws InvalidCastException.  
C. Result is `null`.  
D. Compile error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Casting `null` to any reference type results in `null`. It is a valid cast.
</details>

### Q15. Is downcasting considered a "Code Smell"?
A. No, it is standard practice.  
B. Yes, excessive downcasting suggests a violation of Liskov Substitution Principle or poor polymorphism design.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
While necessary sometimes, heavy use of `if (x is TypeA) ... else if (x is TypeB)` often indicates that polymorphic methods (virtual/abstract) should be used instead to let the object decide its own behavior.
</details>
