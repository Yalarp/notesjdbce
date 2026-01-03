# 02_Dependency_Injection_ASPNETCore – MCQs

## EASY MCQs

### Q1. How does ASP.NET Core support Dependency Injection (DI)?
A. It requires installing a third-party library like Autofac.
B. It has a built-in IoC container that is an integral part of the framework.
C. It does not support DI fundamentally.
D. It only supports DI for Controllers, not Services.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
ASP.NET Core is designed from the ground up with DI in mind and includes a simple, built-in IoC container (represented by `IServiceCollection`) out of the box.
</details>

### Q2. Which interface represents the standard IoC container builder in ASP.NET Core?
A. `IBuilder`
B. `IServiceCollection`
C. `IDependencyMap`
D. `IWebContainer`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`IServiceCollection` is the interface used in `Program.cs` (via `builder.Services`) to register application and framework services before the app is built.
</details>

### Q3. What is the primary purpose of the `[FromServices]` attribute in an Action Method?
A. To inject a service into a specific action method rather than the entire controller constructor.
B. To identify a service as a Singleton.
C. To prevent the service from being disposed.
D. To read data from the HTTP Request body.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`[FromServices]` allows "Action Method Injection". This is useful if a dependency is expensive or rarely used, and you only need it for that one specific action, avoiding the overhead of creating it for every request to the controller.
</details>

### Q4. Which keyword is recommended for use with injected fields to prevent accidental reassignment?
A. `static`
B. `readonly`
C. `const`
D. `volatile`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Marking the private field required to hold the dependency as `readonly` ensures that once it is set in the constructor, it cannot be swapped out or nullified elsewhere in the class.
</details>

### Q5. In a Razor View, which directive is used to inject a service?
A. `@using`
B. `@model`
C. `@inject`
D. `@service`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The `@inject` directive (e.g., `@inject IStudentRepository rep`) allows you to resolve a service from the DI container directly inside a `.cshtml` view file.
</details>

---

## MEDIUM MCQs

### Q6. Ideally, what should a Controller depend on?
A. The concrete service class (e.g., `StudentRepository`).
B. The service interface (e.g., `IStudentRepository`).
C. The DbContext directly.
D. static Global variables.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Controllers should depend on abstractions (interfaces). This decouples the controller from the specific implementation of the data access logic, following the Dependency Inversion Principle.
</details>

### Q7. Consider `builder.Services.AddScoped<IStudentRepository, TestStudentRepository>();`. What does `IStudentRepository` represent?
A. The Implementation type.
B. The Service type (Abstraction) that checks will request.
C. The Lifetime manager.
D. The Database connection.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The first generic parameter `IStudentRepository` is the Service Type (the interface requested by consumers). The second parameter `TestStudentRepository` is the Implementation Type (the concrete class the container will provide).
</details>

### Q8. Why might you use a third-party container (like Autofac) instead of the built-in one?
A. The built-in container is too slow.
B. The built-in container lacks advanced features like property injection, convention-based registration (assembly scanning), and interception.
C. Microsoft deprecated the built-in container.
D. You cannot use Singleton with the built-in container.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The built-in container is "minimalist" and meant to serve basic needs. For complex scenarios requiring advanced capabilities like Decorators or Scanning, third-party libraries are often used.
</details>

### Q9. What happens if you try to inject a service that has NOT been registered in `Program.cs`?
A. The application works but returns null.
B. The application throws a runtime exception (`InvalidOperationException`) stating it is unable to resolve the service.
C. The compiler throws an error.
D. It automatically finds the class if the names match.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
DI containers (usually) fail fast at runtime if a requested dependency is missing. You will get a clear error message that the service `Type` has not been registered.
</details>

### Q10. Which is NOT a standard Service Lifetime in ASP.NET Core?
A. Singleton
B. Scoped
C. Transient
D. Global

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**
The three support lifetimes are Singleton, Scoped, and Transient. "Global" is not a standard term in ASP.NET Core DI terminology (Singleton effectively behaves globally, but the term is Singleton).
</details>

---

## HARD MCQs

### Q11. In the "Service Descriptor" method of registration `services.Add(new ServiceDescriptor(...))`, what is being explicitly defined?
A. Only the implementation type.
B. The Service Type, Implementation Type (or instance), and the Lifetime.
C. The SQL connection string.
D. The Middleware pipeline order.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`ServiceDescriptor` is the underlying class that describes a service. The helper methods like `AddSingleton<T>` are just wrappers around creating a `ServiceDescriptor` that defines the Interface, Implementation, and Lifetime.
</details>

### Q12. Why is "View Injection" generally discouraged for business logic?
A. It is slower than Controller logic.
B. It breaks the MVC pattern separation; Views should primarily be about display, and creating dependencies there hides logic from the Controller and makes testing the View logic harder.
C. It is not supported in the latest .NET versions.
D. You cannot inject Scoped services into Views.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Views should be "dumb" and just render the Model provided by the Controller. Injecting repositories into Views (Direct Data Access) couples the UI to the backend and bypasses the Controller's role as orchestrator.
</details>

### Q13. If you register a service using `services.AddSingleton(new MyService())`, who is responsible for creating the instance?
A. The IoC Container.
B. You (the developer) are manually created it at registration time.
C. The first HTTP Request.
D. The Garbage Collector.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If you pass a `new Instance()` directly to the registration method, you have already created it. The container simply holds onto that specific instance and returns it when requested.
</details>

### Q14. Can you use Constructor Injection in a Middleware class?
A. No, Middleware must be static.
B. Yes, but standard Middleware requires dependencies to be injected into the `Invoke` method (Method Injection) rather than the Constructor for Scoped services, unless using `IMiddleware` factory activation.
C. Yes, always, exactly like Controllers.
D. No, Middleware does not support DI.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Standard Middleware is a Singleton. Therefore, you cannot inject Scoped services into its constructor (Captive Dependency). You must inject Scoped services into the `InvokeAsync` method parameters.
</details>

### Q15. What is the execution flow when a Controller requests a dependency?
A. `Controller -> New Instance -> Database`.
B. `Request -> IoC Container (finds registration) -> Creates/Returns Instance -> Controller Constructor -> Controller Instance`.
C. `Request -> Controller -> IoC Container`.
D. `Validation -> Controller -> DI`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The framework intercepts the controller creation. It asks the Container for the required dependencies defined in the constructor, resolves them (creating if needed based on lifetime), and then instantiates the controller with them.
</details>
