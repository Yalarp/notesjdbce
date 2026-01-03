# 38_Entity_Framework_Introduction – MCQs

## EASY MCQs

### Q1. What does "ORM" stand for?
A. Object-Relational Mapper  
B. Only Relational Model  
C. Object Role Model  
D. Oracle Resource Manager  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It bridges the gap between Object-Oriented C# code and Relational SQL tables.
</details>

### Q2. Which NuGet package is the Core EF library?
A. `System.Data.SqlClient`  
B. `Microsoft.EntityFrameworkCore`  
C. `Newtonsoft.Json`  
D. `Microsoft.AspNet.Mvc`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This package contains the base core functionality. You also need a provider (like SqlServer) and Tools.
</details>

### Q3. "Code First" approach means:
A. You write SQL first.  
B. You write C# classes/entities first, and EF generates the database.  
C. You write code in Python.  
D. You query data first.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It emphasizes define-model-in-code. Migrations then sync the DB schema to match the code.
</details>

### Q4. "Database First" approach means:
A. You start with an existing Database, and EF scaffolds/generates the C# classes from it.  
B. You create database manually for every change.  
C. Database is more important than code.  
D. You use stored procedures only.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Useful for legacy systems where the DB schema is the source of truth.
</details>

### Q5. What is `DbContext`?
A. A table.  
B. The session/gateway between your C# code and the database.  
C. A column.  
D. A query language.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It manages connections, configuration, and caching (change tracking) for a unit of work.
</details>

---

## MEDIUM MCQs

### Q6. Which command creates a Migration?
A. `dotnet run`  
B. `dotnet ef migrations add <Name>`  
C. `dotnet build`  
D. `git commit`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This CLI command compares your current code model with the last migration snapshot and generates a new migration plan.
</details>

### Q7. Which command applies the pending migrations to the actual database?
A. `dotnet switch`  
B. `dotnet ef database update`  
C. `dotnet ef update`  
D. `Update-Database` (PowerShell only)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This executes the SQL required to bring the database schema up to date with the latest migration.
</details>

### Q8. EF Core supports which databases?
A. SQL Server only.  
B. Many, via Providers (SQL Server, SQLite, PostgreSQL, MySQL, InMemory, etc.).  
C. No databases.  
D. Only Azure.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Its provider model allows it to work with almost any relational (and some non-relational like CosmosDB) stores.
</details>

### Q9. Why is LINQ used with EF Core?
A. To draw graphics.  
B. To write strongly-typed queries in C# (`.Where(x => x.Id > 5)`) which EF translates to SQL.  
C. To connect to internet.  
D. To format strings.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
LINQ provides compile-time safety for queries, preventing syntax errors common in raw SQL strings.
</details>

### Q10. What is "Scaffolding"?
A. Building a UI.  
B. Reverse engineering an existing database execution to create C# Entity classes (Database First).  
C. Deleting the database.  
D. Testing code.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `scaffold` command reads the DB schema and outputs the corresponding Code First classes.
</details>

---

## HARD MCQs

### Q11. Can you run EF Core in strict "Disconnected" mode (e.g., Web API)?
A. No.  
B. Yes. You receive DTOs/Entities, attach them to a fresh DbContext, set their State (Modified/Added), and SaveChanges.  
C. Yes, but it never tracks changes.  
D. Only with sessions.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Web apps are stateless. The DbContext that queried the data is disposed of when the request ended. The update request comes in with data but no tracking info, so you must explicitly tell EF the state.
</details>

### Q12. "Change Tracking" impacts performance. How do you disable it for read-only queries?
A. `AsNoTracking()`  
B. `StopTracking()`  
C. `ReadOnly()`  
D. `Fast()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`context.Authors.AsNoTracking().ToList()` is faster because EF skips setting up the change tracking snapshots for the returned objects.
</details>

### Q13. Does EF Core migration automatically handle data migration (e.g., split a column "Name" into "First" and "Last")?
A. Yes, perfectly.  
B. No. It handles Schema changes. Data transformations usually require writing custom SQL in the `Up()` method of the migration.  
C. It deletes data.  
D. It guesses.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Auto-migrations only see structure. Logic to preserve/transform data during structural changes must be code-injected manually.
</details>

### Q14. What is the `Microsoft.EntityFrameworkCore.Tools` package used for?
A. Runtime execution.  
B. PowerShell/CLI commands (`Add-Migration`, `Scaffold-DbContext`) inside Visual Studio.  
C. SQL Server connection.  
D. Nothing.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It contains the design-time logic to analyze your code and generate migration files.
</details>

### Q15. "Shadow Properties" in EF Core are:
A. Properties that exist in the Database table but are NOT defined in the C# Entity class.  
B. Properties that cast shadows.  
C. Private properties.  
D. Deleted properties.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Useful for auditing columns (CreatedDate, UpdatedBy) or Foreign Keys that you don't want polluting your domain model classes. EF tracks them internally.
</details>
