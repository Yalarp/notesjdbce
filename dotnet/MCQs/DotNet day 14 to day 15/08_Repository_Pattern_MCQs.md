# 08_Repository_Pattern – MCQs

## EASY MCQs

### Q1. What is the main goal of the Repository Pattern?
A. To make code slower.
B. To abstract data access logic behind an interface, decoupling the business logic (Controller) from the data access implementation (Database).
C. To replace SQL with C#.
D. To delete data.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It acts as a Mediator between the domain and data mapping layers.
</details>

### Q2. In the pattern, what calls the Repository?
A. The Database.
B. The Controller (or Service layer).
C. The View.
D. The Browser.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The Controller requests data from the Repository to prepare the response.
</details>

### Q3. Why use an Interface (`IMembers`)?
A. It allows multiple implementations and easier unit testing (mocking).
B. It is required by C#.
C. It looks professional.
D. It improves database speed.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Contracts (Interfaces) allow you to swap the real database repository with a fake one during testing.
</details>

### Q4. Where do you typically register the Repository in .NET Core?
A. `Program.cs` (DI Container).
B. `Controller`.
C. `Index.cshtml`.
D. `appsettings.json`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`builder.Services.AddScoped<IInterface, Implementation>()`.
</details>

### Q5. Should the Controller know about the `DbContext` directly when using this pattern?
A. Yes.
B. No. The Controller should only depend on the Repository Interface.
C. Maybe.
D. Only for DELETE.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Direct dependencies on DbContext inside Controller violate the pattern (Leaky Abstraction).
</details>

---

## MEDIUM MCQs

### Q6. Which CRUD operation is associated with `Add`?
A. SELECT
B. INSERT
C. UPDATE
D. DELETE

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Adding an entity to the repository equates to inserting a record.
</details>

### Q7. If you switch from SQL Server to MongoDB, what code needs to change?
A. Everything.
B. The Controller code.
C. Only the Repository Implementation and the DI registration. The Interface and Controller remain unchanged.
D. The Model.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
This is the power of Loose Coupling.
</details>

### Q8. What is "Hard Coding" dependencies (e.g., `repo = new MemberRepository()`) and why is it bad?
A. It prevents Dependency Injection and makes testing difficult because you can't substitute the dependency.
B. It is good practice.
C. It is faster.
D. It saves memory.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Tight coupling ("New is Glue").
</details>

### Q9. What does `IEnumerable<T>` return type imply for a Read operation?
A. A single item.
B. A collection of items that can be iterated over.
C. A boolean.
D. An integer.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Standard for "GetAll" methods.
</details>

### Q10. In the Repository implementation, how is the `DbContext` accessed?
A. `new DbContext()`
B. Constructor Injection into the Repository class.
C. Global static variable.
D. `ViewBag`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Repositories themselves should resolve their dependencies (like DbContext) via DI.
</details>

---

## HARD MCQs

### Q11. Is strict Repository Pattern always necessary with EF Core?
A. Yes, always.
B. No. EF Core's `DbContext` is already an implementation of the Repository/Unit-of-Work pattern. For simple apps, using DbContext directly in Controllers is acceptable, though it couples you to EF Core.
C. No, never use it.
D. Only in Java.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is a debated topic. The pattern is useful for testing/abstraction, but DbContext is already a powerful repository abstraction itself. Architecture decisions depend on complexity.
</details>

### Q12. How does the Repository Pattern facilitate Unit Testing?
A. It connects to the real DB.
B. You can create a `MockMemberRepository` that implements `IMembers` but uses a simple `List<Member>` in memory. You inject this into the Controller to test logic without a database.
C. It automates tests.
D. It checks syntax.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Mocks eliminate the slow, fragile dependency on external databases during unit tests.
</details>

### Q13. Should a Repository return `IQueryable<T>` or `IEnumerable<T>`/`List<T>`?
A. `IQueryable<T>` allows the Controller to add more filters (leaking logic). `IEnumerable<T>` returns materialized data, enforcing that query logic stays in the Repository.
B. `IQueryable` is safer.
C. `List` is faster.
D. No difference.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Purists argue Repositories should return List/IEnumerable to encapsulate data access fully. Returning IQueryable leaks data access details (SQL evaluation happens in controller), reducing the pattern's benefits.
</details>

### Q14. What is the "Unit of Work" pattern often used with Repository?
A. It manages the transaction. It ensures that multiple repository operations share the same database context and are committed as one atomic transaction.
B. It counts hours.
C. It is a class.
D. It is a testing tool.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Ensures `repo1.Add()` and `repo2.Update()` succeed or fail together (DbContext usually acts as the UoW).
</details>

### Q15. A generic repository `IRepository<T>` handles standard CRUD. Where does custom logic (e.g. `GetMembersByActiveStatus`) go?
A. Nowhere.
B. In a specialized repository `IMemberRepository : IRepository<Member>`.
C. In the Controller.
D. In the View.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Mix generic base repositories for boilerplate with specific derived repositories for domain-specific queries.
</details>
