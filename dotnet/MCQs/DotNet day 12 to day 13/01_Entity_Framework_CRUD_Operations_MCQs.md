# 01_Entity_Framework_CRUD_Operations – MCQs

## EASY MCQs

### Q1. What does "POCO" stand for in the context of Entity Framework?
A. Plain Old CLR Object
B. Public Object Class Organization
C. Private Object Core Operation
D. Persistent Object Code Organization

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
POCO (Plain Old CLR Object) refers to simple classes that do not depend on any framework-specific base classes or interfaces, making them lightweight and easy to test.
</details>

### Q2. Which class in EF Core represents a session with the database?
A. `DbSet`
B. `DbContext`
C. `DbConnection`
D. `DbCommand`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`DbContext` is the primary class that manages the connection to the database and coordinates entity operations (querying, saving, etc.).
</details>

### Q3. What is the purpose of `DbSet<T>` in a DbContext?
A. It represents a single row in a table.
B. It represents a collection of entities that map to a database table.
C. It defines the database connection string.
D. It is used for migrations only.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`DbSet<T>` properties on the DbContext correspond to tables in the database, allowing you to query and save instances of `T`.
</details>

### Q4. Which method is used to persist tracked changes to the database?
A. `Add()`
B. `Update()`
C. `SaveChanges()`
D. `Commit()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`SaveChanges()` pushes all changes made to tracked entities (Added, Modified, Deleted) to the database in a single transaction.
</details>

### Q5. What is the default lifetime of a DbContext when registered using `AddDbContextPool` or `AddDbContext` in ASP.NET Core?
A. Singleton
B. Transient
C. Scoped
D. Static

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
DbContext is typically registered as Scoped, meaning a new instance is created for each HTTP request and disposed of when the request finishes.
</details>

---

## MEDIUM MCQs

### Q6. In the code `context.Employee.Add(employee)`, what is the state of the entity immediately after execution?
A. Unchanged
B. Added
C. Modified
D. Saved

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The `Add()` method attaches the entity to the context and sets its state to `Added`. The data is not sent to the database until `SaveChanges()` is called.
</details>

### Q7. Consider the following code:
```csharp
context.Entry(emp).State = EntityState.Modified;
context.SaveChanges();
```
What type of SQL operation does this trigger?
A. INSERT
B. UPDATE
C. DELETE
D. SELECT

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Setting the state to `Modified` tells EF Core that the entity exists but has changed. `SaveChanges()` will generate an UPDATE statement.
</details>

### Q8. Why is `AddDbContextPool` preferred over `AddDbContext` for performance?
A. It bypasses the connection string.
B. It keeps the database connection open forever.
C. It reuses DbContext instances from a pool, reducing the overhead of object creation and garbage collection.
D. It caches query results automatically.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`AddDbContextPool` maintains a pool of reusable DbContext instances. When a request needs one, it takes it from the pool instead of creating a new one, which is more efficient for high-throughput apps.
</details>

### Q9. What does the `[Include("Department")]` (or `.Include(e => e.Department)`) method do in a LINQ query?
A. It filters the results by Department.
B. It performs Eager Loading, retrieving the related Department data along with the Employee data in a single query (using JOIN).
C. It validates the Department ID.
D. It creates a new Department.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Include()` is used for Eager Loading, ensuring that navigation properties are populated to avoid NullReferenceExceptions or N+1 query problems.
</details>

### Q10. What happens if you try to serialize an object graph with circular references (e.g., Employee -> Department -> Employees) to JSON without configuration?
A. It works perfectly.
B. It throws a `JsonException` (cycle detected).
C. It returns null.
D. It ignores the circular part automatically.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The default JSON serializer detects the cycle and throws an exception. You must configure `ReferenceHandler.IgnoreCycles` or use `[JsonIgnore]` to handle this.
</details>

---

## HARD MCQs

### Q11. If you use `context.Employee.Remove(emp)` but forget to call `context.SaveChanges()`, what happens to the database?
A. The record is deleted immediately.
B. The record is marked as deleted in memory, but the database remains unchanged.
C. The database throws a constraint violation.
D. The transaction is rolled back automatically.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
EF Core operates in a disconnected/unit-of-work manner. Changes are only applied to the database when `SaveChanges()` is explicitly called.
</details>

### Q12. Difference between `Find(id)` and `FirstOrDefault(x => x.Id == id)`:
A. `Find` is faster because it checks the local cache (ChangeTracker) first before hitting the database; `FirstOrDefault` always queries the database.
B. `Find` allows including related data, `FirstOrDefault` does not.
C. `Find` is for async only.
D. They are identical.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`Find` is optimized to look up entities by primary key in the context's local memory first. If found, it returns the instance without a DB query. `FirstOrDefault` builds and executes a SQL query every time.
</details>

### Q13. When implementing the Repository Pattern with EF Core, why is it typically better to return `IEnumerable<T>` or `IQueryable<T>` from the repository?
A. `IEnumerable` executes the query immediately (client-side evaluation), while `IQueryable` allows the query to be extended (e.g., filtered/sorted) before execution (server-side evaluation).
B. `IEnumerable` is faster.
C. `IQueryable` is deprecated.
D. There is no difference.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
If you expose `IQueryable`, the caller can add `.Where()` clauses that become part of the SQL. If you return `IEnumerable` (usually via `.ToList()`), the data is fetched into memory first, and subsequent filtering happens in the app server (less efficient for large datasets). Note: The service layer often returns specific DTOs or Lists to encapsulate logic.
</details>

### Q14. What is the "N+1 query problem" in the context of `GetAllEmployee()`?
A. When you fetch N employees, then iterate and make 1 additional query for each employee (Total N+1 queries) to fetch related data (e.g., Department) because Lazy Loading is used or Eager Loading was skipped.
B. When you have N+1 columns.
C. When the query fails N+1 times.
D. When you have too many connections.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
This happens if you load a list of employees and then access `emp.Department` inside a loop without having used `.Include()`. It causes a significant performance hit.
</details>

### Q15. In the `Update()` method, `context.Entry(employeeChanges).State = EntityState.Modified;` is used. Why might this be preferred over `context.Update(employeeChanges)` in some scenarios?
A. It is the only way to update.
B. `context.Update()` marks ALL properties as modified, potentially updating columns that haven't changed. Setting specific properties or using `Attach` allows more granular control (though setting State=Modified on the Entry also marks all props).
C. `Update()` throws an error on detached entities.
D. It is faster.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Actually, `context.Update(entity)` marks the entire entity as Modified. If you want to update only specific fields, you would Attach the entity and then set `IsModified` on specific properties. However, in disconnected scenarios (web apps), `Update()` or setting State=Modified is the standard way to handle full object updates.
</details>
