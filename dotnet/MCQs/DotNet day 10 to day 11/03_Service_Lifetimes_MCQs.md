# 03_Service_Lifetimes – MCQs

## EASY MCQs

### Q1. Which service lifetime creates a new instance **every time** it is requested?
A. Singleton
B. Scoped
C. Transient
D. Static

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Transient services are lightweight and stateless. A fresh instance is created by the container every time the service is injected or requested.
</details>

### Q2. Which service lifetime creates a **single instance** that is shared across the entire application for all requests?
A. Singleton
B. Scoped
C. Transient
D. Private

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Singleton services are created the first time they are requested (or at app startup) and that same instance is reused until the application shuts down.
</details>

### Q3. Which service lifetime creates one instance per **HTTP Request**?
A. Singleton
B. Scoped
C. Transient
D. Global

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Scoped services are created once per client request (connection). All components within that single web request share the same instance, but different requests get different instances.
</details>

### Q4. `AddDbContext<T>` registers the DbContext with which default lifetime?
A. Singleton
B. Scoped
C. Transient
D. Permanent

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
EF Core DbContexts are Scoped by default. This ensures that the context tracks changes for a single unit of work (the request) and is disposed of when the request finishes.
</details>

### Q5. Which lifetime is most appropriate for a stateless helper service, like an Email Sender?
A. Singleton
B. Scoped
C. Transient
D. Database

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Transient is suitable for lightweight, stateless services that perform a specific action and don't need to maintain data between calls.
</details>

---

## MEDIUM MCQs

### Q6. What is the risk of using a **Singleton** service?
A. It consumes too much memory (if it holds large state).
B. Thread safety issues; the single instance is accessed concurrently by multiple threads (requests).
C. It is disposed too early.
D. Both A and B.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**
Since a Singleton is shared across all concurrent requests, any mutable state inside it must be protected (thread-safe). Also, if it grows indefinitely (like a cache), it persists for the whole app life.
</details>

### Q7. What is a "Captive Dependency"?
A. When a service captures an error.
B. When a service with a longer lifetime (e.g., Singleton) holds a reference to a service with a shorter lifetime (e.g., Scoped), preventing the shorter one from being disposed correctly.
C. When a Transient service holds a Singleton.
D. When a database is locked.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is a common bug. If a Singleton injects a Scoped service, the Scoped service instance is trapped inside the Singleton effectively becoming a Singleton itself, usually leading to bugs (stale data) or memory leaks (DbContext not disposing).
</details>

### Q8. What is the benefit of `AddDbContextPool` over `AddDbContext`?
A. It allows multiple databases.
B. It improves performance by reusing DbContext instances from a managed pool instead of creating/disposing them for every request.
C. It makes the DbContext Singleton.
D. It automatically applies migrations.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Context pooling resets and recycles DbContext objects. This reduces the overhead of object creation and garbage collection in high-throughput applications.
</details>

### Q9. When using `AddDbContextPool`, why must you avoid private state in your DbContext?
A. Because the pool is public.
B. Because the internal state of the Context is reset, but your custom private fields might NOT be reset, leaking data from a previous request to the next user who gets that pooled instance.
C. It throws a compiler error.
D. It prevents the database from connecting.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
EF Core recycles the object. If you stored "CurrentUser" in a private field on the Context, that field might persist when the Context is handed to the next request, causing security issues.
</details>

### Q10. A "Scoped" service in a Console Application (not Web):
A. Behaves like a Singleton.
B. Cannot be used.
C. Has a lifetime defined by a manually created `IServiceScope`.
D. Is created every time.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Outside of ASP.NET Core (where a scope = a request), you must manually create a scope using `provider.CreateScope()`. Scoped services live as long as that manually created scope exists.
</details>

---

## HARD MCQs

### Q11. Which of the following injections is SAFE and correct?
A. Injecting a Scoped service into a Singleton service.
B. Injecting a Transient service into a Singleton service.
C. Injecting a Singleton service into a Scoped service.
D. Injecting a Scoped service into the Constructor of a Middleware (which is Singleton).

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Objects can safely depend on objects that live *longer* than themselves. A Scoped service (short life) can hold a reference to a Singleton (long life). The reverse causes Captive Dependencies.
</details>

### Q12. If you inject a **Transient** service into a **Scoped** service, how long does that Transient instance effectively live?
A. It is disposed immediately after the constructor returns.
B. It lives as long as the Scoped service lives (the duration of the Request).
C. It becomes a Singleton.
D. It throws an error.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The Transient instance is created and given to the Scoped object. Since the Scoped object holds the reference, that specific Transient instance will remain alive until the Scoped object is disposed (end of request).
</details>

### Q13. How would you solve the need to use a Scoped service (like DbContext) inside a BackgroundService (which is Singleton)?
A. Change DbContext to Singleton.
B. Inject `IServiceScopeFactory`, create a scope manually (`using var scope = _factory.CreateScope()`), and resolve the Scoped service from that scope.
C. Inject DbContext directly.
D. Use a static variable.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is the standard pattern for consuming scoped dependencies in long-running background tasks. You create a temporary scope for a unit of work, do the work, and dispose the scope.
</details>

### Q14. In `AddDbContextPool`, what is the default pool size (in recent EF Core versions)?
A. Unlimited
B. 128
C. 1024
D. 10

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The default pool size was increased to 1024 (from 128 in older versions) to handle higher concurrency scenarios.
</details>

### Q15. Why is `AddTransient` generally safer for multi-threaded parallel processing within a single request?
A. Because each thread will get its own separate instance, avoiding race conditions on shared state.
B. Because it is faster.
C. Because Singleton locks the database.
D. Because Scoped cannot be used in `Parallel.ForEach`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
If you spin up multiple threads in one request and they share a Scoped instance, that instance might not be thread-safe (DbContext definitely isn't). Creating a fresh Transient instance for each parallel task avoids this collision.
</details>
