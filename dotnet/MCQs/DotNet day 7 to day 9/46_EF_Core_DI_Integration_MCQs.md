# 46_EF_Core_DI_Integration – MCQs

## EASY MCQs

### Q1. In ASP.NET Core, `AddDbContext<T>` registers the Context as which lifetime by default?
A. Singleton  
B. Scoped  
C. Transient  
D. Static  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
"Scoped" matches the HTTP Request lifecycle. One context per request ensures thread safety and isolation.
</details>

### Q2. Why is `Singleton` lifetime bad for DbContext?
A. `DbContext` is not thread-safe. Concurrent requests using the same instance will crash/corrupt state.  
B. It is too slow.  
C. It consumes too much memory.  
D. It prevents caching.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It also causes the Change Tracker to grow infinitely (memory leak) as it tracks objects from every request ever made.
</details>

### Q3. How do you inject DbContext into a Controller?
A. Via Constructor Injection.  
B. New it up manually (`new Context()`).  
C. Use a static property.  
D. Use `Global.Context`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`public MyController(MyContext context) { ... }`. The DI container supplies the Scoped instance.
</details>

### Q4. `DbContextOptions` passed to the constructor allows:
A. Configuration of the Provider (SQL Server) and Connection String.  
B. Nothing.  
C. Setting the page title.  
D. Configuring HTML.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It decouples the Context from the hardcoded configuration.
</details>

### Q5. To read the connection string from `appsettings.json`, you typically use:
A. `IConfiguration` interface.  
B. Read text file manually.  
C. Hardcode it.  
D. Environment variable only.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`configuration.GetConnectionString("Default")`.
</details>

---

## MEDIUM MCQs

### Q6. The Repository Pattern with DI serves to:
A. Abstract away the EF Core logic/DbContext from the Business/Controller layer.  
B. Make code slower.  
C. Add more files.  
D. Increase coupling.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Makes unit testing easier (mocking the IRepository) and centralizes query logic.
</details>

### Q7. If you have a Background Service (Singleton) that needs a DbContext, what must you do?
A. Inject `IServiceScopeFactory`, create a scope, and resolve DbContext from that scope.  
B. Inject DbContext directly.  
C. Make DbContext Singleton.  
D. Do not use DB.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
You cannot inject a Scoped service into a Singleton. You must manually manage the scope: `using (var scope = _scopeFactory.CreateScope()) { var db = scope.ServiceProvider.GetRequiredService<MyContext>(); ... }`.
</details>

### Q8. `AddDbContextPool` vs `AddDbContext`:
A. Pooling recycles DbContext instances (resetting state) to reduce object allocation overhead.  
B. Pooling creates a swimming pool.  
C. Pooling is slower.  
D. AddDbContext is deprecated.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
High-performance optimization. Instead of Garbage Collecting the context object, it returns to a pool for reuse.
</details>

### Q9. `UseSqlServer` is an extension method provided by:
A. `Microsoft.EntityFrameworkCore.SqlServer` package.  
B. `System.Data`.  
C. `Newtonsoft`.  
D. `AspNetCore`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It configures the context to speak the T-SQL dialect.
</details>

### Q10. Can you use multiple DbContext types in one app?
A. Yes, register them all with `AddDbContext<T>`.  
B. No, only one allowed.  
C. Only if they share the database.  
D. Only in separate projects.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Common in modular monoliths (e.g., `CatalogContext`, `OrderContext`).
</details>

---

## HARD MCQs

### Q11. `IRepository<T>` Generic Repository Pattern often criticized because:
A. `DbContext` / `DbSet` IS already a Generic Repository and Unit of Work. Wrapping it purely for the sake of it adds necessary abstraction layers without value (YAGNI).  
B. It is too fast.  
C. It is invalid C#.  
D. It prevents testing.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Many architects prefer specific repositories (`IOrderRepository`) or using EF directly with Command/Query patterns (CQRS) over generic wrappers which hide features like `Include`/Projection logic.
</details>

### Q12. "Capturing Dependency" (in proper DI):
A. Injecting a Scoped dependency (Context) into a Singleton (Cache) captures it, keeping it alive forever and reusing it across requests (THREAD UNSAFE).  
B. Good practice.  
C. Capturing errors.  
D. Dependency injection failure.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Major bug source. The container usually throws exceptions to prevent this in Dev environment ("Scoped validation").
</details>

### Q13. `EnableRetryOnFailure()` (Resiliency):
A. Automatically retries failed DB commands (e.g., transient network glitch).  
B. Retries on logic errors.  
C. Retries forever.  
D. Reboots server.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Vital for cloud apps (Azure SQL) where transient drops happen.
</details>

### Q14. `IDesignTimeDbContextFactory<T>` is needed when:
A. Running migrations CLI, but the startup project is complex/requires args that `dotnet ef` cannot infer automatically.  
B. Always.  
C. Never.  
D. For unit testing.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Tells the tooling "Here is exactly how to create the Context" without running the full App Startup.
</details>

### Q15. Using `InMemory` database provider for Tests:
A. Is fast but behaviorally different from Relational DBs (no constraints, no transactions, case sensitivity diffs).  
B. Is exact replica of SQL Server.  
C. Is recommended for Prod.  
D. Is deprecated.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It’s good for basic logic checks but Testcontainers (Docker SQL) is preferred for true integration testing to catch SQL-specific bugs.
</details>
