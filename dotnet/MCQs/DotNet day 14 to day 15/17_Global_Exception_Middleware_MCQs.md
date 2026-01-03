# 17_Global_Exception_Middleware – MCQs

## EASY MCQs

### Q1. What is the primary purpose of Middleware in ASP.NET Core?
A. To define database schemas.
B. To handle HTTP requests and responses in a pipeline.
C. To write unit tests for the application.
D. To generate frontend HTML code.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Middleware components are assembled into an application pipeline to handle requests and responses. They can process requests, pass them to the next component, or short-circuit the pipeline.
</details>

### Q2. In the middleware pipeline, where should the Exception Handler middleware be placed?
A. At the very end of the pipeline.
B. In the middle, after Authentication.
C. At the beginning (or very near the beginning) of the pipeline.
D. It doesn't matter.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
It should be placed early in the pipeline (usually first) so that it can catch exceptions thrown by any subsequent middleware (like Routing, Auth, Controllers).
</details>

### Q3. Which method is used to register a global exception handler in the request pipeline?
A. `app.UseRouting()`
B. `app.UseExceptionHandler()`
C. `app.UseStaticFiles()`
D. `app.UseCors()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`UseExceptionHandler` adds a middleware to the pipeline that will catch exceptions, log them, and re-execute the request for an error handling path.
</details>

### Q4. What is the standard RFC format used by ASP.NET Core to return machine-readable error details?
A. SOAP Faults
B. Problem Details (RFC 7807)
C. XML Error Report
D. Custom Text Format

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
ASP.NET Core uses the Problem Details standard (RFC 7807) to define a standardized JSON format for API errors (containing details like title, status, and traceId).
</details>

### Q5. Why should you use `UseDeveloperExceptionPage()` only in the Development environment?
A. It is too slow for production.
B. It requires a paid license for production.
C. It reveals sensitive information like stack traces which is a security risk in production.
D. It only works with IIS.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The developer exception page shows detailed stack traces and code snippets, which helps debugging but exposes internal application details that attackers could exploit.
</details>

---

## MEDIUM MCQs

### Q6. In a custom middleware `InvokeAsync` method, what does calling `await _next(context);` do?
A. It restarts the pipeline.
B. It passes control to the next middleware component in the pipeline.
C. It stops the request processing immediately.
D. It logs the request to a file.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`_next` is a `RequestDelegate`. Invoking it passes the `HttpContext` to the subsequent middleware in the chain.
</details>

### Q7. How can you access the exception details inside an error handling controller (e.g., mapped to `/error`)?
A. `HttpContext.Request.Body`
B. `HttpContext.Features.Get<IExceptionHandlerFeature>()`
C. `HttpContext.Session`
D. `Request.Query["error"]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The `IExceptionHandlerFeature` interface allows retrieving the exception that occurred during request processing when using the built-in exception handler.
</details>

### Q8. When creating custom exception middleware, why do we wrap `_next(context)` in a `try-catch` block?
A. To validate the request headers.
B. To measure the performance of the request.
C. To catch any unhandled exceptions thrown by downstream middleware or controllers.
D. To modify the response status code for successful requests.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The middleware sits "around" the rest of the pipeline. The `try` block executes the downstream logic. If anything throws, the `catch` block handles it efficiently in one central place.
</details>

### Q9. Which of the following is a key benefit of using Global Exception Middleware over individual try-catch blocks in every controller action?
A. It improves database performance.
B. It reduces code duplication (DRY principle) and ensures consistent error responses.
C. It allows using XML instead of JSON.
D. It automatically fixes the bugs.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Instead of repeating error handling logic in every method, global middleware handles it once for the entire application, ensuring a uniform response structure.
</details>

### Q10. What HTTP status code is most appropriate for a `NotFoundException`?
A. 500 Internal Server Error
B. 400 Bad Request
C. 404 Not Found
D. 401 Unauthorized

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
A custom `NotFoundException` usually implies a specific resource was requested but does not exist, mapping directly to the standard HTTP 404 status.
</details>

---

## HARD MCQs

### Q11. In the context of the RequestDelegate pattern, what is the type of the `_next` parameter injected into a custom middleware constructor?
A. `Action<HttpContext>`
B. `Func<Task>`
C. `RequestDelegate`
D. `IServiceProvider`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The signature for a middleware constructor typically accepts a `RequestDelegate next`, which represents the next component in the pipeline. `RequestDelegate` is a delegate defined as `Task RequestDelegate(HttpContext context)`.
</details>

### Q12. If `app.UseExceptionHandler("/error")` is placed AFTER `app.MapControllers()`, what happens if a controller throws an exception?
A. The exception handler catches it successfully.
B. The exception handler will NOT catch it because the request has already been handled (or the stack has unwound past the handler).
C. The application crashes immediately.
D. The browser receives a 200 OK.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Middleware forms a stack (Last-In, First-Out for execution, but First-In, Last-Out for the return path). However, for `UseExceptionHandler` to catch an exception, it must surround the execution of the component that throws. If it is registered *after* `MapControllers`, it is effectively "downstream" or not in the call stack when the controller executes, so it cannot catch the exception. (Correct order: ExceptionHandler first).
</details>

### Q13. How does `IApplicationBuilder.UseMiddleware<T>()` resolve the middleware class dependencies?
A. It only supports parameterless constructors.
B. It uses the DI container to resolve dependencies injected into the constructor, except for `RequestDelegate` which is passed explicitly by the framework.
C. It requires all dependencies to be static.
D. It creates a new instance using `Activator.CreateInstance` ignoring DI.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Middleware is instantiated once (if standard middleware) or per-request (if `IMiddleware`). For standard convention-based middleware, `RequestDelegate` comes from the pipeline build process, and other services (usually Singleton, or sometimes Transient depending on scope) are injected via DI. Note: Scoped services usually shouldn't be injected into the constructor of a standard Singleton-lifetime middleware.
</details>

### Q14. What is the risk of logging `exception.ToString()` directly to an external logging sink without sanitization?
A. It consumes too much disk space.
B. It provides too little information.
C. It might leak sensitive ecosystem data (connection strings, passwords in memory dumps, PII) included in the exception message or stack trace.
D. It causes a compilation error.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Security best practice. Raw stack traces or exception messages might contain sensitive data. While logging full details is helpful for devs, it must be secured. `exception.ToString()` is generally safe*r* for logs than for user output, but one must still be wary of PII. The primary incorrect answer context implies "why not show to user," but for logging, the risk is persistent storage of sensitive data.
</details>

### Q15. When implementing a custom `GlobalExceptionMiddleware`, why do we need to set `context.Response.ContentType = "application/json"` before writing the response?
A. Because the default is `text/html`, and the client expects JSON.
B. It is required by the C# compiler.
C. The middleware will throw an exception otherwise.
D. It automatically formats the string as JSON.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
When writing directly to `context.Response.WriteAsync`, the framework doesn't automatically set the Content-Type. You must explicitly set it so the client (browser/Postman) knows how to parse the response body.
</details>
