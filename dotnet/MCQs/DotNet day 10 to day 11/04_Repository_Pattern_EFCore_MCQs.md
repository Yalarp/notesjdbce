# 04_Repository_Pattern_EFCore – MCQs

## EASY MCQs

### Q1. What is the main purpose of the Repository Pattern?
A. To make the database faster.
B. To create an abstraction layer between the business logic and the data access layer.
C. To replace SQL Server.
D. To generate Views automatically.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The Repository Pattern acts as a mediator, hiding the details of data access (EF Core commands) from the rest of the application. This allows business logic to focus on rules rather than SQL queries.
</details>

### Q2. Which entity/class in EF Core acts as the "Unit of Work"?
A. `DbSet`
B. `DbContext`
C. `Entity`
D. `Migration`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The `DbContext` manages database connections and holds the "Change Tracker". It coordinates writing all changes (transactionally) to the database when `SaveChanges()` is called.
</details>

### Q3. In the code `context.Entry(emp).State = EntityState.Modified;`, what does this instruction do?
A. It deletes the record.
B. It tells EF Core to treat the entire entity as "Changed" so it will generate an UPDATE statement for all columns.
C. It inserts a new record.
D. It validates the model.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This explicitly marks the entity as modified. EF Core will effectively assume every property has changed and update all mapped columns in the database.
</details>

### Q4. Which command is used to apply Migrations to the database?
A. `Add-Migration`
B. `Update-Database`
C. `Remove-Migration`
D. `Generate-SQL`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Add-Migration` creates the code files for the change. `Update-Database` actually executes the generated SQL against the target database to bring the schema up to date.
</details>

### Q5. What does the `[Required]` attribute do in a Model class?
A. It forces the database column to be NOT NULL.
B. It makes the property private.
C. It generates a primary key.
D. It encrypts the data.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`[Required]` is a Data Annotation that serves two purposes: validaton in the UI (cannot be empty) and schema generation (create a non-nullable column in the DB).
</details>

---

## MEDIUM MCQs

### Q6. Why do we typically inject the Repository Interface into the Controller instead of the Concrete Class?
A. To make the code compile.
B. To adhere to Dependency Inversion and allow for easier unit testing (mocking).
C. Because Interfaces are faster.
D. Concrete classes cannot be injected.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
By depending on `IEmployeeRepository`, the Controller doesn't care if the data comes from SQL, a text file, or a mock object. This makes testing the controller logic simple.
</details>

### Q7. What is the difference between `Display` and `DisplayName` attributes?
A. They are identical.
B. `DisplayName` is from `System.ComponentModel` (older), while `Display(Name=...)` is from `System.ComponentModel.DataAnnotations` (newer, more features).
C. `Display` is only for dates.
D. `DisplayName` is for Controllers.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Both are used to friendly names for UI labels. `[Display(Name="...")]` is generally preferred in modern Data Annotations as it supports localization resources, but `[DisplayName]` is often seen in simpler scenarios.
</details>

### Q8. In the repository implementation: `context.Employee.Include(e => e.Department).FirstOrDefault(...)`; What does `Include` do?
A. It filters the results.
B. It performs Eager Loading, generating a SQL JOIN to fetch the related Department data along with the Employee.
C. It includes a file.
D. It sorts the data.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Without `Include`, the `Department` navigation property on the returned Employee object would be null (unless lazy loading is enabled). Include forces the related data to be retrieved in the same query.
</details>

### Q9. When implementing the Update method, why might one use `context.Update(entity)` instead of attaching and setting state manually?
A. It is the only way to update.
B. `context.Update(entity)` automatically marks the entity as Modified. If the entity is a graph (has child objects), it might also mark them as Modified/Added depending on tracking.
C. It is slower.
D. It creates a new record.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Update()` is a convenience method that sets the state to Modified. It's useful for disconnected scenarios where you receive an object ensuring it gets saved.
</details>

### Q10. What is the purpose of `ReferenceHandler.IgnoreCycles` in Program.cs JSON options?
A. To make the JSON prettier.
B. To prevent "System.Text.Json.JsonException: A possible object cycle was detected" exceptions when serializing related entities (e.g., Employee -> Department -> Employees list).
C. To ignore null values.
D. To encrypt the JSON.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
EF Core navigation properties are bidirectional (Employee has Dept, Dept has List<Employee>). Default serializers get stuck in an infinite loop trying to serialize this. `IgnoreCycles` tells the serializer to stop when it sees an object it has already processed.
</details>

---

## HARD MCQs

### Q11. Why is the Repository Pattern sometimes considered "redundant" with EF Core?
A. EF Core is broken.
B. EF Core's `DbContext` and `DbSet` are already an implementation of the Repository and Unit of Work patterns. Adding another layer can be seen as over-abstraction.
C. Repositories are security risks.
D. Microsoft advised against it.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`DbSet` acts like a repository (collection of objects). `DbContext` is the Unit of Work. Some developers prefer using `DbContext` directly to avoid "wrapping a wrapper," while others prefer Repositories to decouple from EF Core specifically.
</details>

### Q12. How does `AsNoTracking()` affect the Repository's read performance?
A. It makes it slower because it skips caching.
B. It improves performance by telling EF Core NOT to snapshot the data or track changes for these entities (useful for Read-Only scenarios).
C. It prevents data from being loaded.
D. It enables Lazy Loading.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Change tracking involves overhead (memory and CPU). If you are just fetching data to display in a list (Read-Only), disabling tracking via `AsNoTracking()` significantly optimizes the query.
</details>

### Q13. In a Generic Repository `IRepository<T>`, what constraint is usually applied to T?
A. `where T : class`
B. `where T : struct`
C. `where T : new()`
D. `where T : DbContext`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Usage is typically `public interface IRepository<T> where T : class`. This ensures that T is a reference type, which is required for it to be an EF Core Entity mapped to a table.
</details>

### Q14. What happens if you forget to call `SaveChanges()` after `context.Add(emp)`?
A. The data is saved automatically when the request ends.
B. The data is kept in memory in the Change Tracker but is NEVER written to the database. It is lost when the context is disposed.
C. An exception is thrown.
D. The database locks.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
EF Core operations are transactional in memory. Nothing hits the database until `SaveChanges()` is explicitly called.
</details>

### Q15. Using `AddDbContextPool` changes the lifetime of the **DbContext internal state**. How does this impact your Repository implementation?
A. You must make your repository Static.
B. You should not store any state specific to a request (like 'TenantId') in the DbContext instance itself, because that instance might be wiped and reused by a different user in a subsequent request.
C. It requires the Repository to be Transient.
D. No impact at all.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Since the object is recycled, any private fields you added to your custom `AppDbContext` are NOT automatically reset (unless you override `ResetState` in newer versions or manage it manually). This can lead to data leaking between requests.
</details>
