# 21_Interview_Questions – MCQs

## EASY MCQs

### Q1. Ideally, what is the nature of a RESTful service?
A. Stateful
B. Stateless
C. Connected
D. Session-based

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
REST services are stateless; no client context is stored on the server between requests. Each request must contain all necessary info.
</details>

### Q2. Which HTTP method is NOT idempotent?
A. GET
B. PUT
C. DELETE
D. POST

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**
Posting the same data multiple times creates multiple resources. GET, PUT (replace), and DELETE (remove) result in the same state if repeated.
</details>

### Q3. What is the main difference between `Controller` and `ControllerBase`?
A. `Controller` has View support; `ControllerBase` does not.
B. `ControllerBase` is for MVC.
C. `Controller` is faster.
D. There is no difference.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`Controller` adds support for Views (`View()`, `PartialView()`), which Web APIs generally don't need.
</details>

### Q4. Which status code indicates "Unauthorized" (Authentication failed)?
A. 403
B. 401
C. 404
D. 500

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
401 = "I don't know who you are". 403 = "I know who you are, but you aren't allowed here".
</details>

### Q5. Why do we prioritize `async/await` in Web application code?
A. To make single requests process faster.
B. To improve thread utilization and scalability under load.
C. To write less code.
D. To fix bugs.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It prevents blocking threads, allowing the server to handle more concurrent requests.
</details>

---

## MEDIUM MCQs

### Q6. What is the "N+1 Problem" in EF Core?
A. An error when adding numbers.
B. Executing 1 query for the main list and then N additional queries for related data for each item.
C. A compilation error.
D. A variable naming convention.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This performance issue occurs when lazy loading or looping executes a DB query per iteration. Solved by Eager Loading (`Include`).
</details>

### Q7. What is the difference between Authentication and Authorization?
A. They are synonyms.
B. AuthN verifies Identity; AuthZ verifies Permissions.
C. AuthN is for database; AuthZ is for frontend.
D. AuthZ comes before AuthN.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Authentication answers "Who are you?"; Authorization answers "What can you do?".
</details>

### Q8. Which DI lifetime creates a single instance for the entire application's life?
A. Scoped
B. Transient
C. Singleton
D. Static

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Singleton services are created the first time they are requested and reused everywhere.
</details>

### Q9. What is a "Captive Dependency"?
A. When a controller depends on a view.
B. When a service with a longer lifetime (e.g., Singleton) holds a reference to a service with a shorter lifetime (e.g., Scoped).
C. When a database is locked.
D. When nuget packages are missing.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This effectively promotes the shorter-lived service to the longer lifetime, potentially causing memory leaks or bugs (e.g., using a closed DbContext).
</details>

### Q10. What is the purpose of an API Gateway?
A. To generate documentation.
B. To act as a single entry point for a system of microservices, handling routing, aggregation, and cross-cutting concerns.
C. To store the database.
D. To run the frontend.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It decouples the client from individual microservices and provides a unified interface.
</details>

---

## HARD MCQs

### Q11. Why shouldn't you use `[DataType(DataType.EmailAddress)]` for validation?
A. It causes a runtime error.
B. It is only for UI formatting/hints and does not perform actual server-side validation.
C. It is deprecated.
D. It conflicts with EF Core.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You should use the `[EmailAddress]` validation attribute for actual logic checks.
</details>

### Q12. Explain the order of execution: Middleware vs Filters.
A. Filters run before Middleware.
B. Middleware runs before Routing; Filters run within the MVC Action Invocation pipeline (after Routing and before/after Action).
C. They run in parallel.
D. Filters run only on startup.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Middleware wraps the entire request pipeline. Filters (ActionFilters, etc.) are part of the MVC/Controller subsystem and run only when a controller action is matched and invoked.
</details>

### Q13. `Task` vs `void` in asynchronous programming: Why is `async void` discouraged?
A. It cannot be awaited, and exceptions thrown within it crashes the process (cannot be caught by standard try-catch blocks outside the method).
B. It is too slow.
C. It returns null.
D. It requires more memory.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`async void` is intended only for event handlers. In all other cases, return `Task` so the caller can handle completion and errors.
</details>

### Q14. How does `[ApiController]` influence detailed error reporting?
A. It disables it.
B. It automatically transforms validation errors into a `ProblemDetails` response.
C. It sends an email to the admin.
D. It redirects to the home page.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is one of the "opinionated" features of the attribute, responding with a standardized 400 Bad Request payload containing field-level errors.
</details>

### Q15. In REST, which method applies a Partial Update?
A. PUT
B. POST
C. PATCH
D. UPDATE

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
PUT replaces the target resource entirely. PATCH applies a delta (only the changes).
</details>
