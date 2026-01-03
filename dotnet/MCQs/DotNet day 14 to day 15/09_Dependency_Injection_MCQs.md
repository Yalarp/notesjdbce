# 09_Dependency_Injection – MCQs

## EASY MCQs

### Q1. What is the main purpose of Dependency Injection (DI)?
A. To create objects manually using `new`.
B. To store data.
C. To decouple classes by providing their dependencies from an external container (Inversion of Control).
D. To speed up compilation.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
DIP (Dependency Inversion Principle) states high-level modules should not depend on low-level modules; both should depend on abstractions.
</details>

### Q2. Which lifetime creates a single instance for the entire application?
A. Scoped
B. Transient
C. Singleton
D. Static

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Singletons live from startup to shutdown.
</details>

### Q3. Which lifetime creates a new instance for every HTTP request?
A. Transient
B. Scoped
C. Singleton
D. Global

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
"Scoped" basically means "Request-Scoped" in ASP.NET Core web apps.
</details>

### Q4. Which lifetime creates a new instance every time the service is injected?
A. Scoped
B. Transient
C. Singleton
D. Eternal

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The lightest weight (conceptually), but can be expensive if the object is heavy to create.
</details>

### Q5. How do you inject a dependency into a Controller?
A. Property Injection.
B. Method Injection.
C. Constructor Injection (preferred).
D. Magic.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Explicitly declaring dependencies in the constructor is the standard pattern.
</details>

---

## MEDIUM MCQs

### Q6. Can you inject a Scoped service into a Singleton service?
A. Yes, easily.
B. No, this is a "Captive Dependency". The Scoped service would stay alive as long as the Singleton (forever), violating its lifecycle.
C. Yes, but it becomes Transient.
D. No, compiler error.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
By default, .NET Core attempts to detect and block this in Development mode (`ValidateScopes`), as it causes bugs (e.g., holding onto a closed DbContext).
</details>

### Q7. What is the correct way to register a DbContext?
A. `AddSingleton`
B. `AddTransient`
C. `AddScoped` (usually done via `AddDbContext`).
D. `AddStatic`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
DbContext is not thread-safe, so it cannot be Singleton. It holds connection state, so it shouldn't be Transient (too much overhead). Scoped is the correct fit.
</details>

### Q8. What does `builder.Services.AddControllers()` do?
A. Registers all controller classes in the assembly as services so they can support DI.
B. Creates the controllers.
C. Runs the controllers.
D. Deletes them.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
It registers the framework services required for Controller-based APIs.
</details>

### Q9. If `ServiceA` depends on `ServiceB`, does the DI container resolve `ServiceB` automatically when creating `ServiceA`?
A. No, you must do it manually.
B. Yes, the container resolves the dependency graph recursively.
C. Only if Singleton.
D. Only if specified in XML.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is the "Auto-Wiring" capability of containers.
</details>

### Q10. Why is Constructor Injection preferred over Property Injection?
A. It takes less code.
B. It ensures the object is fully initialized and in a valid state upon creation (dependencies are required). Properties are optional/mutable.
C. Properties are slow.
D. Constructors are faster.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Guarantees validity. You can't instantiate the class without providing its requirements.
</details>

---

## HARD MCQs

### Q11. Using `[FromServices]` injects a dependency into:
A. The Constructor.
B. A specific Action Method parameter.
C. A Property.
D. Static field.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Allows fine-grained resolution to avoid bloating the constructor if a service is used in only one method.
</details>

### Q12. If you register `builder.Services.AddTransient<IMyService, MyService>()` and inject `IMyService` twice in the *same* Controller constructor, do you get the same instance?
A. Yes.
B. No, you get two different instances.
C. Depends on the weather.
D. Yes, because it's the same request.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Transient = New instance *per resolution/injection*.
</details>

### Q13. How do you resolve a Scoped service inside a Singleton background service (e.g. `IHostedService`)?
A. Inject it directly.
B. Inject `IServiceScopeFactory`, create a scope (`CreateScope()`), and resolve the service from that scope's provider.
C. Make the background service Scoped.
D. You cannot.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is the Service Locator pattern, but permitted/necessary here to bridge lifetime mismatch.
</details>

### Q14. What is `IServiceProvider`?
A. The registered service.
B. The interface representing the DI container itself, used to resolve services.
C. The repository.
D. The configuration.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Usually hidden by Constructor Injection framework magic, but it's the engine underneath.
</details>

### Q15. `AddDbContextPool` vs `AddDbContext`. Why pool?
A. To save hard disk space.
B. To reuse DbContext instances (resetting their state) rather than creating/disposing them constantly, reducing Garbage Collection overhead in high-throughput apps.
C. To allow multiple databases.
D. To enable async.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Performance optimization.
</details>
