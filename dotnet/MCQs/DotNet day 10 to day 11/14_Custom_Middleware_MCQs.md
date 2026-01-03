# 14_Custom_Middleware – MCQs

## EASY MCQs

### Q1. What are the two main approaches to creating custom middleware in ASP.NET Core?
A. IMiddleware Interface and Convention-based
B. Class-based and Function-based
C. Static and Dynamic
D. Global and Local

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The two supported patterns are: 1) Implementing `IMiddleware` interface (Factory-based), and 2) Writing a POCO class following specific naming conventions (Convention-based).
</details>

### Q2. Convention-based middleware MUST have which method?
A. `ExecuteAsync`
B. `Invoke` or `InvokeAsync`
C. `ProcessRequest`
D. `Handle`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The framework uses reflection to find a method named `Invoke` or `InvokeAsync` that returns a `Task` and accepts `HttpContext`.
</details>

### Q3. For Convention-based middleware, what must the Constructor accept?
A. `HttpContext`
B. `IApplicationBuilder`
C. `RequestDelegate` (next)
D. `Configuration`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The middleware must capture the `next` delegate in its constructor so it knows who to call after it finishes its work.
</details>

### Q4. Which approach requires registering the middleware class in the DI container (Program.cs)?
A. Convention-based
B. `IMiddleware` implementation
C. Both
D. Neither

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Factory-activated middleware (`IMiddleware`) is resolved from the DI container for each request (or based on lifetime), so it MUST be added to services (e.g., `services.AddTransient<MyMiddleware>()`). Convention middleware instances are created once by the pipeline builder.
</details>

### Q5. What is the standard way to expose your middleware to consumers?
A. Instructing them to specific `UseMiddleware<T>`.
B. Creating an Extension Method on `IApplicationBuilder` (e.g., `app.UseMyMiddleware()`).
C. Using attributes.
D. Using config files.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
While `UseMiddleware<T>` works, usually developers wrap it in an extension method like `app.UseAuthentication()` or `app.UseMyCustomLogic()` for valid readable syntax.
</details>

---

## MEDIUM MCQs

### Q6. In Convention-based middleware, how are "Scoped" dependencies (like DbContext) injected?
A. In the Constructor.
B. In the `InvokeAsync` method parameters.
C. They cannot be injected.
D. Via a property.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Convention middleware is instantiated as a Singleton (once per app lifetime). Constructor injection only allows Singleton dependencies. To use Scoped services (per-request), you must accept them as arguments in the `InvokeAsync` method.
</details>

### Q7. Why can't you inject a Scoped service into the **Constructor** of a Convention-based middleware?
A. It causes a runtime error.
B. It causes a "Captive Dependency" - the Scoped service would be trapped inside the Singleton middleware and never disposed/renewed for new requests.
C. The compiler allows it but it's slow.
D. Scoped services are not supported.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Since the middleware instance is created only once (Singleton behavior), any dependency injected into the constructor is also held for the lifetime of the app. This breaks the behavior of Scoped services (which should die after the request).
</details>

### Q8. Does `IMiddleware`-based middleware solve the Scoped dependency issue?
A. Yes, because it is factory-activated. If you register it as Transient/Scoped, a fresh instance is created when needed, allowing constructor injection of Scoped services.
B. No, it is the same.
C. No, it makes it worse.
D. Yes, but it is slower.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`IMiddleware` is fully integrated with DI. You typically register it as `AddTransient<MyMiddleware>`. The factory creates a new instance for every request, so safe constructor injection of Scoped dependencies is allowed.
</details>

### Q9. Which statement is proper for saving the `next` delegate in convention middleware?
A. `public RequestDelegate Next { get; set; }`
B. `private readonly RequestDelegate _next;` (initialized in constructor)
C. `static RequestDelegate _next;`
D. `var next = new RequestDelegate();`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It should be an immutable, private field set once during construction.
</details>

### Q10. What does `builder.UseMiddleware<MyMiddleware>()` do?
A. It compiles the middleware.
B. It adds the middleware type to the pipeline. The framework will then inspect it (if convention) or resolve it (if factory) when building the pipeline.
C. It runs the middleware immediately.
D. It registers it in DI.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It registers the middleware *type* into the pipeline definition.
</details>

---

## HARD MCQs

### Q11. Which is easier to Unit Test?
A. Convention-based.
B. `IMiddleware` implementation.
C. No difference.
D. Neither.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`IMiddleware` defines a strict interface (`InvokeAsync`), making it straightforward to mock and test. Convention-based relies on reflection and "magic" method signatures which can be slightly more brittle or harder to mock interactions for in strict isolation.
</details>

### Q12. If your middleware modifies the response body (e.g., encryption/compression), when should you do it?
A. Before `next()` is called.
B. After `next()` returns.
C. Response body cannot be modified.
D. In the constructor.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You capture the response (often by swapping the Response.Body stream with a memory stream before `next`, letting downstream write to it, and then engaging logic *after* `next` returns to read/modify/write back to the original stream).
</details>

### Q13. In convention-based middleware, can `InvokeAsync` have additional parameters besides `HttpContext`?
A. No.
B. Yes, any additional parameters are resolved from Dependency Injection (Method Injection).
C. Yes, but they must be integers.
D. Yes, but they must be strings.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is how you get Scoped dependencies. `InvokeAsync(HttpContext context, IMyScopedService service)` works because the framework invokes this method per-request using the request's service scope.
</details>

### Q14. Can you use `Invoke` (synchronous) instead of `InvokeAsync`?
A. Yes, but it's discouraged in modern async pipelines as it blocks threads.
B. No, it must be Async.
C. Yes, it is preferred.
D. Only in Console apps.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The framework supports `Invoke` for backward compatibility or simple sync logic, but mixing blocking code in an async pipeline (Kestrel) hurts scalability. `Task InvokeAsync` is best practice.
</details>

### Q15. Is custom middleware "Thread Safe"?
A. Convention-based middleware must be written to be thread-safe (stateless) because it is a Singleton shared by concurrent requests.
B. No, it is single threaded.
C. Yes, the framework locks it.
D. No need to worry about threads.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Since one instance handles all requests concurrently (Convention-based), you should not store request-specific data in class-level fields. Use `HttpContext` for request data.
</details>
