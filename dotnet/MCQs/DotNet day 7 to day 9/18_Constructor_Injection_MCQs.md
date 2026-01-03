# 18_Constructor_Injection – MCQs

## EASY MCQs

### Q1. In Constructor Injection, how is the dependency provided to the class?
A. Through a public property.  
B. Through a parameter in the class constructor.  
C. Through a dedicated method.  
D. Through a global variable.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The dependencies are declared as arguments in the constructor signature.
</details>

### Q2. What is a key advantage of Constructor Injection regarding object state?
A. It allows the object to be created in an invalid state.  
B. It ensures the dependency is present immediately upon creation (Object is valid).  
C. It allows changing the dependency later.  
D. It is optional.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Since constructors must run to create the object, you guarantee that the object receives its required dependencies before anyone can use it.
</details>

### Q3. How do you typically store the injected dependency inside the class?
A. In a `static` variable.  
B. In a `private` (often `readonly`) field.  
C. In a local variable.  
D. In a temporary file.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The dependency is assigned to a private field so it can be used by other methods in the class throughout its lifetime.
</details>

### Q4. Which keyword is associated with the field holding the dependency to prevent accidental replacement?
A. `static`  
B. `const`  
C. `readonly`  
D. `sealed`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `readonly` keyword ensures the field is only assigned during initialization (constructor), preserving the integrity of the dependency graph.
</details>

### Q5. If you have a class `Client(IService s)`, can you instantiate `Client` without passing an `IService`?
A. Yes, it will use a default.  
B. No, the compiler enforces the constructor signature.  
C. Yes, if you pass `null` (syntax allows, but risky).  
D. Both B and C (You must pass an argument, even if it is null).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
You strictly cannot call `new Client()` (assuming no other constructors). You MUST pass an argument. However, you *could* pass `null`, but proper DI frameworks or guard clauses (`ArgumentNullException`) prevent this.
</details>

---

## MEDIUM MCQs

### Q6. Referencing the provided code: `BusinessLogicImplementation(IService client)`. Who is responsible for creating the concrete `ClaimService`?
A. The `BusinessLogicImplementation` class.  
B. The `IService` interface.  
C. The caller (e.g., `Program.Main` or an IoC Container).  
D. The `ClaimService` itself.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The caller instantiates the specific service (`new ClaimService()`) and passes it into the BusinessLogic constructor.
</details>

### Q7. If a class requires 5 different dependencies, Constructor Injection can lead to:
A. Constructor Over-injection (or "Constructor Bloat").  
B. Faster execution.  
C. Better memory management.  
D. No issues.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Having too many parameters is a code smell (Constructor Bloat), suggesting the class might be doing too much (violating Single Responsibility Principle).
</details>

### Q8. Comparatively, Constructor Injection is preferred over Setter Injection for:
A. Optional dependencies.  
B. Required dependencies.  
C. Circular dependencies.  
D. Value types.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Mandatory dependencies should go in the constructor to enforce the contract that "this object needs these things to work".
</details>

### Q9. Steps to implement manual Constructor Injection:
1. Define Interface
2. Implement Interface
3. Define Consumer with Interface field
4. ???
5. Inject from Main

What is step 4?
A. Create default constructor.  
B. Create parameterized constructor assigning argument to field.  
C. Create a Set method.  
D. Create a static instance.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The consumer need a constructor accepting the interface to wire the field.
</details>

### Q10. Does Constructor Injection support runtime swapping of implementation?
A. No, it is fixed at compile time.  
B. Yes, but only if you recreate the object with a different dependency.  
C. Yes, the field changes automatically.  
D. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Once the object is created with Dependency A, it usually holds A for life (especially if readonly). To "swap", you instantiate a new consumer with Dependency B.
</details>

---

## HARD MCQs

### Q11. Can Constructor Injection function with inheritance?
A. No.  
B. Yes, the derived class constructor must accept the dependency and pass it to the base constructor (`: base(dependency)`).  
C. Yes, base classes inject themselves automatically.  
D. No, constructors are not inherited.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If the base class requires a dependency, the derived class must request it (or create it) and bubble it up via the `base()` chaining mechanism.
</details>

### Q12. How does Constructor Injection facilitate Unit Testing?
A. It doesn't.  
B. You can pass `new MockService()` into the constructor during the test setup.  
C. You can inspect private fields.  
D. It prevents compilation errors.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Since the constructor accepts the interface, the test framework can simply instantiate the class under test passing a dummy/mock implementation of that interface.
</details>

### Q13. Circular Dependencies (A needs B, B needs A) in Constructor Injection:
A. Are handled automatically.  
B. Cause a StackOverflowException (or instantiation failure) because neither can be created first.  
C. Are valid.  
D. Are resolved by the compiler.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is a fatal flaw in constructor injection. You cannot create A without B, but you cannot create B without A. Refactoring (e.g., using Property injection for one, or extracting a third service) is required.
</details>

### Q14. Immutability favors multithreading. Does Constructor Injection support immutability?
A. Yes, perfectly.  
B. No.  
C. Only for structs.  
D. Only for strings.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Since dependencies are set once at creation (and can be readonly), the internal state regarding dependencies doesn't change, making the object thread-safe regarding its configuration.
</details>

### Q15. In strict Dependency Injection, the `Main` method (or Composition Root):
A. Should contain business logic.  
B. Should be the dirty place where all objects are wired together.  
C. Should not use `new`.  
D. Should be empty.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The "Composition Root" is the centralized location where the object graph is constructed (where the `new` keywords live) before starting the application logic.
</details>
