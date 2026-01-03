# 39_DbContext_DbSet – MCQs

## EASY MCQs

### Q1. What does a `DbSet<T>` represent?
A. A single row.  
B. A table (or view) in the database corresponding to Entity T.  
C. A database connection.  
D. A configuration file.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`DbSet<Author>` acts as the repository collection for all Author records in the DB.
</details>

### Q2. Where do you typically configure the database connection string?
A. `OnConfiguring` method or via Dependency Injection options.  
B. In the `Main` method only.  
C. In `OnModelCreating`.  
D. In the entity class.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`optionsBuilder.UseSqlServer("...")` connects the context to a physical store.
</details>

### Q3. Which attribute marks a property as the Primary Key?
A. `[Primary]`  
B. `[Key]`  
C. `[Id]`  
D. `[Unique]`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
From `System.ComponentModel.DataAnnotations`.
</details>

### Q4. A "Navigation Property" (e.g., `author.Books`) allows you to:
A. Navigate the internet.  
B. Access related data (traverse relationships) in the object graph.  
C. Does nothing.  
D. Opens a map.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It represents the Foreign Key relationship in an object-oriented way.
</details>

### Q5. `[Required]` attribute maps to what in SQL?
A. `NULL`  
B. `NOT NULL`  
C. `DEFAULT`  
D. `UNIQUE`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Ensures the column must have a value.
</details>

---

## MEDIUM MCQs

### Q6. `OnModelCreating` is used for:
A. Connecting to DB.  
B. Fluent API configuration of the entity model (mappings, relationships, constraints).  
C. Creating the class files.  
D. Logging.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It provides a more powerful and flexible alternative to Data Attributes for configuring the model.
</details>

### Q7. How does EF Core handle `public int Id { get; set; }` by convention?
A. It ignores it.  
B. It automatically treats it as the Primary Key (Identity column).  
C. It treats it as a foreign key.  
D. It treats it as an integer column called "Id".  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Properties named `Id` or `<ClassName>Id` are conventionally assumed to be PKs.
</details>

### Q8. Dependency Injection of DbContext usually uses which lifetime?
A. Singleton.  
B. Scoped (per request).  
C. Transient.  
D. Static.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`DbContext` is not thread-safe and holds state (Change Tracking). It should be fresh for every HTTP request but shared within that request.
</details>

### Q9. `[ForeignKey("AuthorId")]` attribute lies on:
A. The `Author` class.  
B. The `Book` class (the dependent side).  
C. The DbContext.  
D. The connection string.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It tells EF that the property `AuthorId` is the FK for the navigation property it decorates (`Author`).
</details>

### Q10. If you do not provide a constructor taking `DbContextOptions` in your Context class:
A. DI won't work standardly.  
B. It works fine.  
C. It is faster.  
D. The database is locked.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The standard `AddDbContext<T>` in Startup.cs expects to pass options into your context via constructor injection.
</details>

---

## HARD MCQs

### Q11. "Fluent API" overrides "Data Annotations". True or False?
A. True.  
B. False.  
C. They merge perfectly.  
D. It depends on order.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Fluent API (`OnModelCreating`) has the highest precedence. If attribute says MaxLength(50) and Fluent says MaxLength(100), it will be 100.
</details>

### Q12. A "Composite Key" (multi-column PK) can be defined using:
A. `[Key]` attribute on both properties.  
B. Only via Fluent API: `modelBuilder.Entity<T>().HasKey(x => new { x.A, x.B });`  
C. SQL only.  
D. It is not supported.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
EF Core Data Annotations do not support composite keys (unlike EF6). You MUST use Fluent API.
</details>

### Q13. `ChangeTracker` property of DbContext allows you to:
A. Track GPS location.  
B. Inspect the state (Added, Modified, Deleted) of all attached entities.  
C. Change the password.  
D. See logic history.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Useful for debugging or overriding methods like `SaveChanges` to implement auditing (finding all modified entries and setting UpdatedDate).
</details>

### Q14. What happens if you define a DbSet for `Book` but NOT for `Author`, but `Book` has a navigation property to `Author`?
A. Error.  
B. `Author` is explicitly excluded from DB.  
C. `Author` is included in the model by convention (since it is reachable), but you just don't have a top-level collection for it.  
D. `Book` is ignored.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
EF discovers reachable entities. You can still save Authors by adding them to `Book.Author`, but you can't allow `context.Authors` directly without the DbSet property (or `context.Set<Author>()`).
</details>

### Q15. `HasData()` in `OnModelCreating` is used for:
A. Seeding initial data (Model Seeding) into the database via migrations.  
B. Checking if data exists.  
C. Validating data.  
D. Hiding data.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It generates explicit `INSERT` statements in the migration file to ensure specific rows (like lookup tables or admin user) exist.
</details>
