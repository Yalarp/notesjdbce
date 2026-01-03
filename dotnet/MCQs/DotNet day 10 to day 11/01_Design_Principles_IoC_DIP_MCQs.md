# 01_Design_Principles_IoC_DIP – MCQs

## EASY MCQs

### Q1. What is the primary goal of the "Inversion of Control" (IoC) principle?
A. To create tighter coupling between classes.
B. To remove dependencies and achieve loose coupling between application classes.
C. To prevent the use of interfaces.
D. To manually manage object lifecycles in every class.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The main objective of IoC is to invert the control of object creation and management, thereby removing tight coupling between components and making the system more modular and testable.
</details>

### Q2. In the "Dependency Inversion Principle" (DIP), what should high-level modules depend on?
A. Low-level modules.
B. Concrete implementations.
C. Abstractions (interfaces or abstract classes).
D. Database connection strings.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
DIP states that high-level modules should not depend on low-level modules; both should depend on abstractions. This decoupling ensures that changes in low-level details do not affect high-level logic.
</details>

### Q3. Which of the following is a "Design Pattern" rather than a "Design Principle"?
A. Single Responsibility Principle (SRP)
B. Dependency Injection (DI)
C. Inversion of Control (IoC)
D. Dependency Inversion Principle (DIP)

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Dependency Injection is a specific Design Pattern used to implement the IoC principle. IoC, DIP, and SRP are high-level Design Principles.
</details>

### Q4. What is the role of an "IoC Container"?
A. To store database records.
B. To automatically manage the creation, injection, and lifecycle of dependencies.
C. To compile the C# code.
D. To host the web application on a server.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
An IoC Container (or DI Container) is a framework that acts as a factory, automatically creating objects and injecting their dependencies as needed, freeing the developer from manual instance management.
</details>

### Q5. Which SOLID principle does "DIP" stand for?
A. Data Injection Principle
B. Dependency Inversion Principle
C. Direct Inheritance Principle
D. Dynamic Instantiation Principle

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
DIP stands for Dependency Inversion Principle, which is the 'D' in the SOLID acronym.
</details>

---

## MEDIUM MCQs

### Q6. Consider the following code: `public class Car { private Engine _engine = new Engine(); }`. What design issue is present here?
A. It follows the Dependency Inversion Principle correctly.
B. It demonstrates loose coupling.
C. It has TIGHT COUPLING because `Car` is directly creating an instance of `Engine`.
D. It uses Constructor Injection.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
By using the `new` keyword to create `Engine` inside `Car`, the `Car` class is tightly coupled to the specific `Engine` class. It cannot easily work with a subclass of Engine or a Mock engine for testing.
</details>

### Q7. How does Dependency Injection improve "Testability"?
A. It eliminates the need for unit tests.
B. It allows real dependencies (like databases) to be swapped with Mock or Stub implementations during testing.
C. It makes the code faster, so tests run quicker.
D. It forces all methods to be public.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Because dependencies are injected (usually distinct interfaces), tests can inject fake/mock implementations instead of real services, allowing the unit under test to be verified in isolation.
</details>

### Q8. In the context of DIP, what defines a "Low-Level Module"?
A. A module that handles business policies and workflows.
B. A module that implements detailed operations like data access, file I/O, or API calls.
C. An abstract interface.
D. The `Program.cs` file.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Low-level modules handle the "details" or specific implementations (like `SqlEmployeeRepository`). High-level modules (like Controllers) contain the logic that directs these low-level operations.
</details>

### Q9. Which of the following is NOT a type of Dependency Injection?
A. Constructor Injection
B. Property (Setter) Injection
C. Method Injection
D. Inheritance Injection

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**
The three standard forms of DI are Constructor, Property, and Method injection. "Inheritance Injection" is not a standard term in this pattern.
</details>

### Q10. What is the built-in interface for the IoC container in ASP.NET Core?
A. `IUnityContainer`
B. `IServiceCollection`
C. `IContainerBuilder`
D. `IDependencyResolver`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
ASP.NET Core uses `IServiceCollection` (typically via `builder.Services`) to register services, which builds an `IServiceProvider` that acts as the container.
</details>

---

## HARD MCQs

### Q11. Why is "Constructor Injection" generally preferred over Property Injection?
A. It allows optional dependencies.
B. It ensures that the object is fully initialized with all required dependencies before it can be used (Dependencies are mandatory).
C. It allows dependencies to be changed after the object is created.
D. It is the only type supported by C#.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Constructor Injection guarantees that a class cannot be instantiated without its required dependencies, preventing the "Null Reference" issues that can occur if a property is not set. It enforces a valid state.
</details>

### Q12. The "Hollywood Principle" ("Don't call us, we'll call you") describes which aspect of IoC?
A. The flow of control is inverted; instead of the application calling libraries, the framework calls the application code.
B. The application creates all objects at startup.
C. The database calls the application.
D. Exceptions are hidden from the user.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
This is a metaphor for IoC. In traditional programming, your code drives execution. In IoC (like using a framework), the framework controls the main flow and calls into your custom code (handlers, controllers) when needed.
</details>

### Q13. If `Class A` depends on `Interface I`, and `Class B` implements `Interface I`, how does DIP affect the relationship between A and B?
A. `Class A` must depend directly on `Class B`.
B. `Class A` remains unaware of `Class B`; the connection is made via configuration/injection, adhering to the principle that "Details should depend on abstractions."
C. `Class B` must inherit from `Class A`.
D. `Class I` depends on `Class A`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
DIP ensures that the high-level module (`A`) only knows about the abstraction (`I`). It does not know or care that `B` is the implementation. `B` also depends on `I` (by implementing it).
</details>

### Q14. What is a potential downside of NOT using an IoC container in a large application with many dependencies?
A. The application will be too fast.
B. Construction of object graphs becomes complex and tightly coupled code (Manual Dependency Injection) becomes unmanageable ("Pure DI" becomes hard).
C. Compile time increases significantly.
D. You cannot use recursion.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Without a container, you must manually instantiate every dependency chain (e.g., `new Service(new Repo(new DbContext(...)))`). As the app grows, this "composition root" logic becomes extremely verbose and brittle.
</details>

### Q15. In the context of the Service Locator pattern vs. Dependency Injection, why is Service Locator generally considered an "Anti-Pattern"?
A. It is too slow.
B. It hides class dependencies (they aren't visible in the constructor), making the class harder to understand and test.
C. It cannot return null.
D. It only works with static classes.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
With DI, a class's requirements are clearly declared in its constructor signatures. With Service Locator, a class might quietly ask for a dependency internally, hiding its reliance and making it fragile if that service isn't registered.
</details>
