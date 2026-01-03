# 26_Inheritance_Constructors – MCQs

## EASY MCQs

### Q1. Are constructors inherited in C#?
A. Yes, all public constructors are inherited.  
B. No, constructors are not inherited.  
C. Yes, but only the default constructor.  
D. Only if the class is abstract.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Constructors are specific to the class and are never inherited. A derived class must define its own constructors, though it can (and must) call the base class constructor.
</details>

### Q2. Which constructor executes first when creating an instance of a derived class?
A. The Derived class constructor.  
B. The Base class constructor.  
C. They execute simultaneously.  
D. It depends on the arguments passed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The Base class constructor always executes first to ensure the base part of the object is fully initialized before the Derived class adds its own initialization.
</details>

### Q3. Which keyword is used to call a constructor of the parent class?
A. `this`  
B. `parent`  
C. `super`  
D. `base`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
The `base` keyword is used in the constructor initializer list to invoke a specific constructor of the parent class (e.g., `: base(arg)`).
</details>

### Q4. If a parent class DOES NOT have a parameterless constructor, what must the child class do?
A. It cannot inherit from that class.  
B. It must manually define the parent's constructor.  
C. It must explicitly call a parameterized constructor of the base class using `base(...)`.  
D. The compiler automatically adds a default constructor.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
If the base class has no default (parameterless) constructor, the derived class is legally required to explicitly call one of the available parameterized constructors from the base.
</details>

### Q5. Can you use `this()` and `base()` in the same constructor declaration?
A. Yes, `this()` first then `base()`.  
B. Yes, `base()` first then `this()`.  
C. No, a constructor can call either another constructor of the same class (`this`) OR a base constructor (`base`), but not both directly.  
D. Only in sealed classes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
C# syntax allows only one initializer per constructor. You can chain using `this()` to another constructor which eventually calls `base()`, but you cannot invoke both directly in the same signature.
</details>

---

## MEDIUM MCQs

### Q6. What happens if the Child class constructor does not explicitly call `base()`?
A. It throws a runtime error.  
B. The compiler implicitly calls the parameterless constructor `base()`.  
C. The parent part of the object is left uninitialized.  
D. The compiler generates an error if the parent has any constructor.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If initialization is not specified, the compiler implicitly inserts a call to `base()`. This works only if the base class has a accessible parameterless constructor. If not, it's a compile error.
</details>

### Q7. In constructor chaining, if `Child(int)` calls `this()`, and `Child()` calls `base()`, what is the execution order?
A. `base()` -> `Child()` -> `Child(int)`  
B. `Child(int)` -> `Child()` -> `base()`  
C. `Child()` -> `base()` -> `Child(int)`  
D. `base()` -> `Child(int)` -> `Child()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Execution starts at the top of the chain (Base). So `base()` runs first, then the constructor it returns to (`Child()`), and finally the original called constructor (`Child(int)`).
</details>

### Q8. What is the execution order of Static Constructors in an inheritance hierarchy?
A. Parent Static -> Child Static.  
B. Child Static -> Parent Static.  
C. Random.  
D. Static constructors are not executed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
When you access the Child class, the Child static constructor runs to initialize the Child type. Because Child depends on Parent, this triggers the Parent static constructor. However, conceptually and visibly, the "Child" static init happens when the type is touched, but often the output shows Child Static -> Parent Static (or vice versa depending on exact runtime triggers), but generally, accessing the Derived type triggers its static ctor first, which may trigger the Base.
*Refinement based on standard observation:* Usually `Child` static runs, then `Parent` static.
</details>

### Q9. Can a static constructor call `base()`?
A. Yes.  
B. No.  
C. Only if the base has a static constructor.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Static constructors cannot have parameters and cannot explicitly call other constructors (neither `this` nor `base`). The runtime manages their execution.
</details>

### Q10. Why is the Base constructor executed before the Child constructor?
A. Because the compiler processes files top-down.  
B. To ensure the base class fields are initialized before the child class tries to use them.  
C. It is just a convention.  
D. Child constructors are more important.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A derived class often relies on state defined in the base class. Therefore, the base class must be fully initialized (constructed) before the derived class constructor logic runs.
</details>

---

## HARD MCQs

### Q11. If `Parent` has a private parameterless constructor and no other constructors, can `Child` inherit from it?
A. Yes, implicitly.  
B. Yes, but `Child` generally cannot be instantiated since it cannot call the base constructor.  
C. No, unless `Child` is nested inside `Parent`.  
D. Yes, `base` is not required.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
If the only constructor is private, outside classes (including derived classes) cannot access it. Thus, you effectively cannot inherit from it unless the derived class is nested within the base class (which has access to private members).
</details>

### Q12. Can you access `this` reference inside the `base(...)` call arguments?
```csharp
public Child() : base(this.SomeProperty) { }
```
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
No. The object is not yet constructed when the arguments for `base` are being evaluated. You cannot access instance members (`this`) in the initializer list.
</details>

### Q13. If a constructor throws an exception, is the finalizer called?
A. Yes, always.  
B. No, the object was never fully created.  
C. Only if `IDisposable` is implemented.  
D. Yes, if the base constructor completed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Technically, if the constructor throws, the object is not considered "fully constructed", but the finalizer (if present) IS scheduled to run for the parts that were initialized (like the base class). This is a subtle point in C# object lifetime.
*(Correction/Nuance: The Finalizer IS called if the `System.Object` constructor has run, which is practically always true for managed classes).*
</details>

### Q14. What happens if you define a constructor in a class marked `static`?
A. It works as a normal constructor.  
B. It must be private.  
C. Compilation Error.  
D. It becomes a static constructor automatically.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Instance constructors are not allowed in a `static class`. You can only have a `static` constructor (which has no access modifier). Defining `public ClassName() { }` in a static class is a compile error.
</details>

### Q15. Consider:
```csharp
class A { public A() { Print(); } public virtual void Print() { } }
class B : A { int x = 5; public override void Print() { Console.Write(x); } }
```
If `new B()` is called, what is likely printed?
A. 5  
B. 0  
C. Null  
D. Exception  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is the "calling virtual method in constructor" trap. `A`'s constructor calls `Print`. `B` overrides `Print`. The override in `B` runs. BUT, `B`'s constructor hasn't run yet (base runs first), so `x` has not been initialized to 5. It holds the default 0. output is 0.
</details>
