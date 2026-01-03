# 15_Static_Classes – MCQs

## EASY MCQs

### Q1. What is the main characteristic of a `static class`?

A. It cannot optionally produce output.  
B. It cannot be instantiated (cannot create objects of it).  
C. It can only contain private members.  
D. It must inherit from `MarshalByRefObject`.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
A static class cannot be instantiated using the `new` keyword. It serves as a container for static members.
</details>

### Q2. What kind of members can a `static class` contain?

A. Only static members.  
B. Both static and instance members.  
C. Only const members.  
D. Only methods.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
The compiler enforces that a static class can ONLY contain static members (methods, fields, properties, etc.). Instance members are not allowed.
</details>

### Q3. Can a static class be inherited?

A. Yes, by other static classes.  
B. Yes, by any class.  
C. No, static classes are implicitly sealed.  
D. Yes, if marked virtual.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Static classes are implicitly `sealed`, meaning they cannot act as a base class for inheritance.
</details>

### Q4. Which of the following is an example of a built-in static class in .NET?

A. `System.String`  
B. `System.Object`  
C. `System.Math`  
D. `System.Exception`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
`System.Math` is a classic example of a static class providing utility methods (Sqrt, Abs, etc.) without requiring instantiation.
</details>

---

## MEDIUM MCQs

### Q5. Extension Methods MUST be defined in:

A. An abstract class.  
B. A sealed class.  
C. A static class.  
D. A partial class.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
C# requires that Extension Methods be defined as static methods inside a `static` class using the `this` modifier on the first parameter.
</details>

### Q6. Is it possible to define an instance constructor `Result()` in a static class `Result`?

A. Yes.  
B. No.  
C. Only if private.  
D. Only if it takes no parameters.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Since static classes cannot be instantiated, instance constructors are meaningless and strictly forbidden by the compiler.
</details>

### Q7. What happens if you try to declare `static class MyClass : BaseClass`?

A. It compiles successfully.  
B. It throws a Runtime Error.  
C. It causes a Compile Error.  
D. It creates a hybrid class.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Static classes cannot inherit from any class (except implicitly from `System.Object`). Inheritance is an OOP concept for instances; static classes do not fit this model.
</details>

### Q8. What is the primary use case for Static Classes?

A. To define data models.  
B. To create Utility/Helper libraries and Extension methods.  
C. To manage database connections.  
D. To implement interfaces.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Static classes are ideal for grouping functional utility methods that do not require maintaining state across multiple instances (e.g., `Math`, `Convert`, `Path`).
</details>

---

## HARD MCQs

### Q9. Can a static class implement an interface?

A. Yes.  
B. No.  
C. Only if the interface is also static.  
D. Only if all methods are implemented.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Interfaces define contracts for *objects* (instances). Since static classes cannot have instances, they cannot implement interfaces.
</details>

### Q10. Can a static class have a constructor?

A. No constructors allowed.  
B. Yes, a private instance constructor.  
C. Yes, a static constructor.  
D. Yes, a public static constructor.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
A static class CAN have a `static constructor` to initialize its static fields. It cannot have instance constructors. Note that static constructors cannot have access modifiers (public/private).
</details>

### Q11. Regarding the lifetime of a static class's data:

A. It is destroyed when the last method call finishes.  
B. It persists for the lifetime of the AppDomain (application execution).  
C. It is garbage collected aggressively.  
D. It relies on Main() to keep it alive.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Static fields (state) held by a static class remain in memory for the entire duration the AppDomain is loaded (basically until the app is closed or restarted).
</details>

### Q12. Compare `static class` vs `class with private constructor`. Which feature is unique to `static class`?

A. Only one instance exists.  
B. Cannot be inherited.  
C. The compiler enforces that *all* members must be static.  
D. Is thread-safe.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
A regular class with a private constructor can still contain instance members (though they might be useless if you can't create an instance, unless used internally). A `static class` keyword forces the compiler to check that *every* member is static, preventing accidental instance member declarations.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
