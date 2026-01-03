# 12_Private_Constructor_Singleton – MCQs

## EASY MCQs

### Q1. What is the primary effect of declaring a constructor as `private`?

A. It makes the class static.  
B. It prevents the class from being instantiated from outside the class.  
C. It allows only subclasses to instantiate the class.  
D. It hides the class from the Solution Explorer.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
A private constructor means that instances of the class cannot be created using the `new` keyword from outside the class itself.
</details>

### Q2. Which Design Pattern commonly uses a private constructor?

A. Observer Pattern  
B. Repository Pattern  
C. Singleton Pattern  
D. MVC Pattern  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The Singleton Pattern uses a private constructor to ensure that only the class itself can create the single instance allowed.
</details>

### Q3. How do you access the instance of a Singleton class?

A. `new Singleton()`  
B. `Singleton.Create()`  
C. Through a public static property or method (e.g., `Singleton.Instance`).  
D. `Singleton.GetCopy()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Since the constructor is private, a public static member (commonly named `Instance`) is provided to return the single shared instance.
</details>

### Q4. What is "Lazy Initialization" in the context of Singleton?

A. The instance is created immediately when the program starts.  
B. The instance is created only when it is accessed for the first time.  
C. The instance is created by a background thread.  
D. The instance is deleted automatically.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Lazy initialization means delaying the creation of the object until the point where it is actually needed (first access), improving startup performance.
</details>

---

## MEDIUM MCQs

### Q5. Why is the basic Singleton implementation (checking `if instance == null`) NOT thread-safe?

A. Because the garbage collector might delete the instance.  
B. Because two threads could pass the null check simultaneously and create two separate instances.  
C. Because static members cannot be accessed by multiple threads.  
D. Because private constructors are not thread-safe.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
In a multi-threaded environment, a "race condition" can occur where two threads check `_instance == null` at the same time, find it true, and both proceed to create a new instance, violating the Singleton pattern.
</details>

### Q6. Which keyword is often used to ensure thread safety in Singleton implementation?

A. `sealed`  
B. `lock`  
C. `safe`  
D. `atomic`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The `lock` statement is used to ensure that only one thread can execute the critical section (creating the instance) at a time.
</details>

### Q7. Apart from Singleton, when would you use a private constructor?

A. For abstract classes.  
B. For utility classes that contain only static members (to prevent instantiation).  
C. For data transfer objects (DTOs).  
D. For structs.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
If a class is purely a utility class (like `System.Math`) containing only static methods, a private constructor is used to prevent consumers from creating meaningless instances (e.g., `new Math()`).
</details>

### Q8. What is the role of the `Double-Check Locking` pattern?

A. To create two instances for backup.  
B. To optimize performance by avoiding the lock overhead once the instance is initialized.  
C. To lock the instance twice for extra security.  
D. To prevent inheritance.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Double-Check Locking first checks if the instance is null without locking (fast). If it is null, it acquires the lock and checks again (safe) before creating. This prevents the performance penalty of locking on every single access after initialization.
</details>

---

## HARD MCQs

### Q9. Which modern .NET class provides a built-in, thread-safe, and lazy way to implement Singleton?

A. `Task<T>`  
B. `Lazy<T>`  
C. `WeakReference`  
D. `ThreadLocal<T>`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`Lazy<T>` guarantees thread-safe, lazy initialization. `private static readonly Lazy<Singleton> _lazy = ...` is the recommended modern approach.
</details>

### Q10. Can a class with a private constructor be inherited?

A. Yes, always.  
B. No, because the derived class cannot call the base class constructor.  
C. Yes, if the derived class is nested within the base class.  
D. Yes, if the derived class defines its own public constructor.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Generally no, because constructors are not inherited but must be accessible to be called. Since a derived class constructor must call a base constructor, and the only one is private, inheritance is blocked. Exception: A nested class *inside* the parent class has access to private members, so it *can* inherit.
</details>

### Q11. Compare Factory Pattern vs. Singleton. Which statement is TRUE?

A. Both strictly enforce a single instance.  
B. Factory Pattern creates new instances as needed (or pools them), while Singleton enforces exactly one shared instance.  
C. Singleton allows parameters in `GetInstance`, Factory does not.  
D. Factory Pattern requires a private constructor.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The key distinction is cardinality. Singleton = 1 instance exists for the app lifetime. Factory = Creates instances on demand (could be 1, could be many, often creates new ones).
</details>

### Q12. In the "Static Initialization" approach for Singleton (static readonly field), when is the instance created?

A. Whenever the compiler decides.  
B. Before the `run_command` tool is called.  
C. When the class is first loaded or a static member is accessed (thread-safe by CLR).  
D. Explicitly via a method call.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Static initializers are thread-safe and run automatically by the CLR when the class is first accessed or loaded.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
