# 13_Static_Members – MCQs

## EASY MCQs

### Q1. What does it mean for a member to be `static` in a class?

A. It cannot be changed (constant).  
B. It belongs to the class itself, not to specific instances.  
C. It is private to the class.  
D. It is stored on the Stack.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Static members differ from instance members in that they are shared by all instances and belong to the type (class) rather than any individual object.
</details>

### Q2. How do you access a public static method `Add` in class `MathHelper`?

A. `new MathHelper().Add()`  
B. `MathHelper.Add()`  
C. `this.Add()`  
D. `Add()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Static members are accessed using the class name itself, e.g., `ClassName.MemberName`.
</details>

### Q3. Can a static method access non-static (instance) members directly?

A. Yes, always.  
B. No.  
C. Only if they are public.  
D. Only inside a constructor.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Static methods do not have a `this` reference, so they cannot directly access instance fields or methods. They can only access other static members directly.
</details>

### Q4. How many copies of a static variable exist in memory?

A. One for each object created.  
B. Exactly one, shared by all instances.  
C. Zero until initialized.  
D. It depends on the number of threads.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
There is only one copy of a static variable for the entire application domain, regardless of how many objects of the class are created.
</details>

---

## MEDIUM MCQs

### Q5. When is a Static Constructor called?

A. Every time an object is created.  
B. Only once, automatically, before the first instance is created or any static member is referenced.  
C. Manually by the programmer.  
D. When the application exits.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The static constructor is called automatically by the CLR to initialize the class before its first use (instance creation or static member access). It runs exactly once.
</details>

### Q6. Which of the following is true about Static Constructors?

A. They can take parameters.  
B. They can have access modifiers (public/private).  
C. They cannot be overloaded.  
D. You can call them explicitly using `new`.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Since their execution is controlled by the CLR, static constructors cannot take parameters (how would you pass them?), cannot have access modifiers, and cannot be overloaded.
</details>

### Q7. Consider the output:
```csharp
class Demo {
    static int i = 10;
    public Demo() { i++; }
    public int GetI() { return i; }
}
// Main:
Demo d1 = new Demo();
Demo d2 = new Demo();
Console.WriteLine(d2.GetI());
```
What is printed?

A. 10  
B. 11  
C. 12  
D. 2  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
`i` starts at 10. `d1` constructor increments to 11. `d2` constructor increments the *shared* variable to 12. Both `d1` and `d2` see 12.
</details>

### Q8. Where are static variables stored in memory?

A. On the Stack.  
B. Inside each object on the Heap.  
C. In a special area of the Heap (often called High Frequency Heap or Method Area) associated with the Type.  
D. CPU Registers.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Static variables are stored in the memory area associated with the Type definition itself (available for the life of the AppDomain), not within individual instance objects.
</details>

---

## HARD MCQs

### Q9. What is the execution order of constructors/initializers?

A. Instance Ctor -> Static Ctor -> Field Initializers  
B. Static Field Initializers -> Static Ctor -> Instance Field Initializers -> Instance Ctor  
C. Instance Field Initializers -> Instance Ctor -> Static Ctor  
D. All parallel.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
When a class is first used: Static fields are initialized -> Static constructor runs. Then, when an object is created: Instance fields are initialized -> Instance constructor runs.
</details>

### Q10. Can you use `this` keyword inside a static method?

A. Yes, if you pass an object parameter.  
B. No, `this` refers to the current instance, which relies on a specific object context that static methods lack.  
C. Yes, to access static variables.  
D. Only in extension methods.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
See previous explanation. `this` implies an instance context. Static methods operate in a class context. Note: In extension methods, `this` is a parameter modifier, not the context reference *inside* the static method logic itself in the traditional sense.
</details>

### Q11. If a static constructor throws an unhandled exception, what happens?

A. The exception is swallowed.  
B. The application crashes immediately.  
C. A `TypeInitializationException` is thrown, and the class becomes unusable for the life of the AppDomain.  
D. The constructor tries to run again.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
If a static constructor fails, the CLR wraps the exception in a `TypeInitializationException`. The type fails to load, and any subsequent attempt to access the class will throw the same exception.
</details>

### Q12. Why creates a "Warning" when accessing a static member through an instance variable (in some IDEs/Languages, though C# allows it typically via class name only)?

A. It is illegal in C#; you MUST use ClassName.  
B. It implies the member belongs to the instance, which is misleading.  
C. It causes a runtime error.  
D. It creates a duplicate copy.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
Actually, in C#, accessing a static member via an instance variable (e.g., `obj.StaticMethod()`) is a **Compiler Error**, not just a warning (unlike Java). You *must* use the class name. (Note: Only extension methods appear to be called on instances).
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
