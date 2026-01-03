# 17_Dependency_Injection_Introduction – MCQs

## EASY MCQs

### Q1. What is the primary goal of Dependency Injection (DI)?
A. To make code run faster.  
B. To create tightly coupled classes.  
C. To remove hard-coded dependencies between classes (Loose Coupling).  
D. To eliminate the need for classes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
DI decouples a class from the creation of its dependencies, allowing implementation details to be swapped or mocked.
</details>

### Q2. Which of the following is NOT a common type of Dependency Injection?
A. Constructor Injection  
B. Setter (Property) Injection  
C. Interface Injection  
D. Loop Injection  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
Constructor, Setter, and Interface injection are the standard patterns. Loop Injection is not a term.
</details>

### Q3. What is "Tight Coupling"?
A. When two classes share the same file.  
B. When a class directly creates instances of other classes it depends on (using `new`).  
C. When code is written without spaces.  
D. When using interfaces.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Tight coupling occurs when a dependent class holds a direct reference to a concrete dependency, making it hard to change or test.
</details>

### Q4. Which pattern is generally considered an "Anti-Pattern" in modern DI comparisons?
A. Constructor Injection  
B. Service Locator  
C. Setter Injection  
D. Factory Pattern  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Service Locator hides dependencies (you can't tell what a class needs just by looking at its constructor) and makes testing harder compared to explicit DI.
</details>

### Q5. A key benefit of DI regarding testing is:
A. You don't need to write tests.  
B. It allows injecting "Mock" objects instead of real services (e.g., fake database).  
C. It automatically generates unit tests.  
D. It prevents exceptions.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Because the dependency is an interface injected from outside, unit tests can supply a fake implementation to test logic in isolation.
</details>

---

## MEDIUM MCQs

### Q6. Which principle of SOLID does Dependency Injection directly support?
A. Single Responsibility Principle.  
B. Open/Closed Principle.  
C. Dependency Inversion Principle (DIP).  
D. Liskov Substitution Principle.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
DI is the implementation technique for the Dependency Inversion Principle (High-level modules should not depend on low-level modules; both should depend on abstractions).
</details>

### Q7. Constructor Injection is best used for:
A. Optional dependencies.  
B. Required dependencies that the class cannot function without.  
C. Setting primitive values like integers.  
D. Breaking circular dependencies.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If a class necessitates a dependency to work, demanding it in the constructor ensures the object is never in an invalid state.
</details>

### Q8. Identify the Tightly Coupled code:
A. `public MyClass(IService s) { _s = s; }`  
B. `IService s = new Service();` inside the class.  
C. `public IService S { get; set; }`  
D. `void Init(IService s)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Using the `new` keyword to instantiate a specific concrete class (`Service`) creates a hard dependency on that implementation.
</details>

### Q9. Setter Injection is typically used when:
A. The dependency is mandatory.  
B. The dependency is optional or can be swapped after creation.  
C. The constructor is private.  
D. You want to make the class immutable.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Properties imply optionality. If the dependency is not set, the class usually has a default behavior or checks for null.
</details>

### Q10. In Interface Injection:
A. The dependency is passed via an interface method that the dependent class implements.  
B. The interface creates the object.  
C. Properties are used.  
D. Constructors are used.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The consumer class implements an interface (like `IInjectLogger`) which forces it to expose a method (e.g., `SetLogger(logger)`) that the injector calls.
</details>

---

## HARD MCQs

### Q11. Which is a characteristic of "Loose Coupling"?
A. Changes in one module frequently break other modules.  
B. Components interact through well-defined interfaces/abstractions.  
C. Using `static` global variables everywhere.  
D. Hardcoding connection strings in code.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Loose coupling means components know as little as necessary about each other (only the contract), minimizing ripple effects of changes.
</details>

### Q12. Why is Service Locator considered worse than Constructor Injection?
A. It is slower.  
B. It obscures dependencies (the API doesn't show what the class needs).  
C. It requires an interface.  
D. It cannot handle singletons.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
With Constructor Injection, the signature `new Car(IEngine)` clearly screams "I need an Engine". With Service Locator, `new Car()` looks empty, but might crash internally if `Locator.GetService<IEngine>()` fails.
</details>

### Q13. Can DI be implemented without a framework (like Unity, Autofac, Microsoft.Extensions.DependencyInjection)?
A. No, it is impossible.  
B. Yes, this is called "Pure DI" or "Poor Man's DI".  
C. Yes, but only for static classes.  
D. No, because of reflection.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
DI is a pattern, not a library. You can manually `new Service()` and pass it to `new Client(service)` in your Main method. This is "Pure DI".
</details>

### Q14. What does "Inversion of Control" (IoC) mean in this context?
A. The control of flow is inverted (callbacks).  
B. The control of object creation/binding is inverted from the class itself to an external container/caller.  
C. The screen is inverted.  
D. Using `if/else` in reverse.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Instead of the class controlling "I will create a Database Service", that control is taken away (inverted) and given to the caller/container ("Here is the Database Service you will use").
</details>

### Q15. DI helps achieve the "Single Responsibility Principle" because:
A. Classes perform only one task.  
B. Classes handle their own creation logic.  
C. Classes are relieved of the responsibility of resolving/creating their complex graph of dependencies.  
D. It splits classes into two.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Creation logic is distinct from execution logic. By removing creation logic (DI), the class focuses solely on its primary business function.
</details>
