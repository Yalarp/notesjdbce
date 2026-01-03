# 10_Entity_Framework_Core – MCQs

## EASY MCQs

### Q1. What is Entity Framework Core?
A. A database.
B. An ORM (Object-Relational Mapper) for .NET that maps C# classes to database tables.
C. A frontend framework.
D. A server.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It automates the translation of object operations to SQL queries.
</details>

### Q2. Which class represents the Database Session and Unit of Work?
A. `DbTable`
B. `DbContext`
C. `DbConnection`
D. `DbSession`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`DbContext` is the heart of EF Core.
</details>

### Q3. Which property represents a table in the DbContext?
A. `List<T>`
B. `DbSet<T>`
C. `Table<T>`
D. `Collection<T>`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`DbSet<Employee>` maps to the Employees table.
</details>

### Q4. How do you persist changes (Add/Update/Delete) to the database?
A. `context.Write()`
B. `context.SaveChanges()` (or `SaveChangesAsync()`)
C. `context.Go()`
D. `context.Persist()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Until `SaveChanges` is called, changes exist only in the context's memory.
</details>

### Q5. What is the attribute to mark a property as the Primary Key?
A. `[Primary]`
B. `[Key]`
C. `[Id]`
D. `[PK]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`System.ComponentModel.DataAnnotations.KeyAttribute`.
</details>

---

## MEDIUM MCQs

### Q6. Which LINQ method is used for "Eager Loading" related data (Joins)?
A. `Join()`
B. `Include()`
C. `Load()`
D. `Fetch()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`context.Employees.Include(e => e.Department)` loads the department details with the employee. without it, `Department` would be null.
</details>

### Q7. What does `Find(id)` do differently from `FirstOrDefault(x => x.Id == id)`?
A. Nothing.
B. `Find` checks the local context memory (cache) first to see if the entity is already loaded. `FirstOrDefault` always sends a query to the database.
C. `Find` is slower.
D. `Find` works on Name column.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Find` is optimized for PK lookups.
</details>

### Q8. What is "Code-First" approach?
A. You write SQL first.
B. You write C# classes (Entities) first, and EF generates/updates the database schema from them (Migrations).
C. You write HTML first.
D. You write tests first.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The predominant workflow in modern .NET dev.
</details>

### Q9. What does `[JsonIgnore]` do on a navigation property?
A. Deletes it from DB.
B. Prevents the serializer from including this property in the JSON response, often used to prevent Circular Reference loops (Parent -> Child -> Parent...).
C. Ignores validation.
D. Makes it null.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Critical for bi-directional relationships in APIs.
</details>

### Q10. How do you map a One-to-Many relationship?
A. Parent has `List<Child>`, Child has `ParentId` and `Parent` object.
B. Both have `List`.
C. Both have IDs only.
D. Using arrays.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Navigation properties define the graph structure.
</details>

---

## HARD MCQs

### Q11. What is the `EntityState` of an object after you call `context.Add(obj)` but before `SaveChanges`?
A. Unchanged
B. Added
C. Modified
D. Detached

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The Context tracks it as "New", preparing to generate an INSERT statement.
</details>

### Q12. Why should you use `AsNoTracking()` for read-only queries?
A. It isn't useful.
B. It improves performance by instructing EF NOT to attach returned entities to the Change Tracker. Since you won't update them, tracking is wasted overhead.
C. It allows writing.
D. It deletes data.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Best practice for GET requests returning lists where no modification happens.
</details>

### Q13. Explain "Overposting" or "Mass Assignment" vulnerability.
A. Posting too much data.
B. When a user sends JSON including properties they shouldn't edit (like `IsAdmin: true`), and the API automatically binds it to the Entity and saves it. Prevention: Use DTOs instead of Entities.
C. Posting twice.
D. Posting invalid JSON.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Always separate API contracts (DTOs) from Database Entities for security.
</details>

### Q14. What does `OnModelCreating` method do?
A. Creates the class.
B. Provides a place to configure the model using Fluent API (relationships, constraints, table names) instead of Attributes.
C. Runs on every request.
D. Connects to SQL.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The Fluent API is more powerful than Data Annotations.
</details>

### Q15. Is `DbContext` thread-safe?
A. Yes, use it everywhere.
B. No. A `DbContext` instance must NOT be shared across threads. In web apps, `Scoped` lifetime ensures one instance per request (one thread at a time usually), which is safe.
C. Only in Release mode.
D. Yes, if singleton.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Trying to run two parallel queries on the same context instance throws an exception.
</details>
