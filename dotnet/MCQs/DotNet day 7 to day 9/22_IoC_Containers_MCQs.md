# 22_IoC_Containers – MCQs

## EASY MCQs

### Q1. What does IoC stand for?
A. Input of Code  
B. Inversion of Control  
C. Interface of Classes  
D. Integer of Count  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
IoC is a design principle where the flow of control is inverted compared to traditional procedural programming.
</details>

### Q2. What is the main purpose of an IoC Container?
A. To compile code.  
B. To manage the creation and lifetime of objects (dependencies) automatically.  
C. To store database records.  
D. To run unit tests.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
An IoC container (or DI Container) is a framework that knows how to create objects based on configuration and inject their dependencies.
</details>

### Q3. Which is the built-in DI container in .NET Core?
A. Autofac  
B. Ninject  
C. Microsoft.Extensions.DependencyInjection  
D. Unity  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Microsoft provided a lightweight, built-in container compliant with `IServiceProvider` starting with .NET Core.
</details>

### Q4. Which lifetime creates a NEW instance every time it is requested?
A. Singleton  
B. Scoped  
C. Transient  
D. Static  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Transient services are lightweight and stateless; a fresh instance is created by the container for every injection.
</details>

### Q5. Which lifetime creates ONE instance per HTTP request?
A. Singleton  
B. Scoped  
C. Transient  
D. Global  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Scoped services are created once per client request (connection) within a scope usage.
</details>

---

## MEDIUM MCQs

### Q6. According to the Dependency Inversion Principle (DIP):
A. High-level modules should depend on details.  
B. Low-level modules should depend on high-level modules.  
C. Both should depend on abstractions (interfaces).  
D. Abstractions should depend on details.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
DIP states: Depend on abstractions, not concretions. This decouples the layers.
</details>

### Q7. `services.AddSingleton<ILogger, FileLogger>();` means:
A. Whenever `ILogger` is requested, provide a `FileLogger`.  
B. Whenever `FileLogger` is requested, provide `ILogger`.  
C. Create a new `FileLogger` every time.  
D. Create a file named Logger.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
This registration maps the service type `ILogger` (Interface) to the implementation type `FileLogger` (Concrete Class) with Singleton lifetime.
</details>

### Q8. What happens if you try to inject a Scoped service into a Singleton service?
A. It works perfectly.  
B. It causes a "Captive Dependency" problem (The scoped service becomes a singleton).  
C. It causes a runtime exception in .NET Core (if validation is enabled).  
D. Both B and C.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
A Singleton lives forever. If it holds a reference to a Scoped service, that "Scoped" service is now trapped inside the Singleton and won't be disposed at the end of the request, effectively becoming a Singleton itself. .NET Core defaults check for this in Development 
mode.
</details>

### Q9. Which method is used to finalize the registration and create the container?
A. `services.Start()`  
B. `services.BuildServiceProvider()`  
C. `services.Run()`  
D. `services.Inject()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`BuildServiceProvider` compiles registrations into the `IServiceProvider` (the container) that can resolve services.
</details>

### Q10. "Auto-wiring" in containers refers to:
A. Connecting cables.  
B. The container automatically inspecting the constructor, resolving required dependencies recursively, and instantiating the object.  
C. Writing code automatically.  
D. Connecting to the internet.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You don't need to tell the container `new Service(new Repo(new Db()))`. It figures out the chain automatically.
</details>

---

## HARD MCQs

### Q11. Why is `AddSingleton` appropriate for a Cache Service but not for a User Session?
A. Cache is shared data; Session is user-specific.  
B. Cache is small; Session is large.  
C. Singleton is faster.  
D. Session is transient.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The Singleton instance is shared across ALL requests. You want a shared cache, but you certainly don't want User A's session data appearing for User B.
</details>

### Q12. The `IServiceCollection` is essentially:
A. The container itself.  
B. The list of service descriptors (configuration) before building the container.  
C. A database connection.  
D. A garbage collector.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is a collection of `ServiceDescriptor` objects. It is the "blueprint" or "recipe book". The `IServiceProvider` is the "kitchen" that cooks (creates) the objects.
</details>

### Q13. If you register multiple implementations for the same interface (e.g., `AddTransient<IService, A>` then `AddTransient<IService, B>`), what happens when you request `IEnumerable<IService>`?
A. Error.  
B. You get only the last one (B).  
C. You get all of them (A and B).  
D. You get the first one (A).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
This is a feature. Injecting `IEnumerable<T>` gives you all registered implementations. Injecting just `T` gives you the *last* registered one.
</details>

### Q14. Autofac, Ninject, and Castle Windsor are examples of:
A. Third-party IoC Containers.  
B. Microsoft Libraries.  
C. Operating Systems.  
D. Databases.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
These are mature, feature-rich containers that have existed long before .NET Core's built-in DI. They offer advanced features like property injection, interception (AOP), and convention-based scanning.
</details>

### Q15. Is it good practice to call `provider.GetService<T>()` explicitly in your business logic?
A. Yes.  
B. No, that is the Service Locator anti-pattern.  
C. Sometimes.  
D. Only in controllers.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You should rarely touch the container directly. Let the framework (ASP.NET Core) resolve your controllers and inject dependencies via constructor.
</details>
