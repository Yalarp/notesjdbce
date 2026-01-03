# 41_EF_Core_Relationships – MCQs

## EASY MCQs

### Q1. Which property type represents a "One-to-Many" relationship end in the class?
A. `public int Id { get; set; }`  
B. `public Author Author { get; set; }`  
C. `public ICollection<Book> Books { get; set; }`  
D. `public string Name { get; set; }`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
A collection property (`List`, `ICollection`, `IEnumerable`) indicates that the entity can hold multiple related entities.
</details>

### Q2. What does `[ForeignKey("AuthorId")]` attribute do?
A. It creates a Primary Key.  
B. It explicitly designates a property as the foreign key for a specific navigation property.  
C. It deletes the key.  
D. It connects to the internet.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Useful when the foreign key property name (`AuthorFK`) doesn't match the convention (`AuthorId`).
</details>

### Q3. In a "One-to-One" relationship:
A. Both sides have a Collection.  
B. Both sides have a single reference property to each other.  
C. One side has a collection, the other has a reference.  
D. No properties are needed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`User.Profile` (one) <-> `Profile.User` (one). The foreign key is usually on the dependent side.
</details>

### Q4. "Many-to-Many" (M:N) relationships usually require:
A. A single table.  
B. A Junction (or Join) Table in the database containing FKs to both sides.  
C. No tables.  
D. Files.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Student` <-> `StudentCourses` <-> `Course`. EF Core 5+ can hide this join table if it contains no extra payload data, but it still exists in DB.
</details>

### Q5. What is the default delete behavior for required relationships (non-nullable FK)?
A. NoAction.  
B. SetNull.  
C. Cascade (Delete).  
D. Restrict.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
If a Book *requires* an Author, and you delete the Author, the Book cannot exist (orphaned), so EF deletes the Book too by default.
</details>

---

## MEDIUM MCQs

### Q6. How do you configure a Composite Key in EF Core?
A. `[Key]` on multiple properties.  
B. `modelBuilder.Entity<T>().HasKey(x => new { x.Part1, x.Part2 });`  
C. It is impossible.  
D. Use `[Composite]`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Data Annotations don't support composite keys in Core. You must use Fluent API.
</details>

### Q7. Eager Loading is achieved using:
A. `Load()`  
B. `Fetch()`  
C. `Include()`  
D. `Join()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`context.Authors.Include(a => a.Books)` tells EF to generate a SQL JOIN and populate the `Books` collection property.
</details>

### Q8. To configure a Self-Referencing relationship (e.g., Employee Manager):
A. `public Employee Manager { get; set; }` and `public ICollection<Employee> Subordinates { get; set; }` inside `Employee` class.  
B. You need two classes.  
C. Not supported.  
D. Recursive loop error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
EF detects the typematch. An Employee points to another instance of Employee.
</details>

### Q9. `DeleteBehavior.ClientSetNull` means:
A. The database sets null.  
B. EF Core sets the FK to null in memory for tracked entities, but the Database is not configured with ON DELETE SET NULL.  
C. The client deletes the row.  
D. Nothing happens.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is default for optional relationships. EF fixes up the graph in memory, assuming the DB might throw if you actually try to save an orphan (unless DB also allows nulls).
</details>

### Q10. A "Shadow Property" FK is created when:
A. You define a navigation property but NO corresponding foreign key property in the class.  
B. You use `[Shadow]`.  
C. Never.  
D. You hide the class.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
If `Book` has `Author` nav prop but no `int AuthorId`, EF creates `AuthorId` column in DB anyway to make the relationship work, tracking it internally.
</details>

---

## HARD MCQs

### Q11. Can you filter inside `Include()`? (EF Core 5+)
A. No, you must load all children.  
B. Yes. `.Include(a => a.Books.Where(b => b.Price > 10))`  
C. Yes, but only with raw SQL.  
D. Only with 3rd party libs.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
"Filtered Include" is a powerful feature allowing you to eagerly load only a subset of related data.
</details>

### Q12. "Split Queries" (`AsSplitQuery()`) are used to:
A. Avoid "Cartesian Explosion" performance issues when including multiple collections in a single query.  
B. Split database tables.  
C. Hack the database.  
D. Run queries in parallel.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Instead of one giant JOIN returning redundant data, EF runs separate SELECTs for the main entity and each collection, then stitches them in memory.
</details>

### Q13. `HasOne().WithMany()` without parameters:
A. Throws error.  
B. Infers the navigation properties from context/generics if they adhere to convention.  
C. Deletes the relationship.  
D. Creates M:N.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Often standard conventions work without explicit configuration, but Fluent API allows being explicit `HasOne(x => x.A).WithMany(y => y.Bs)`.
</details>

### Q14. Relationship Fix-up:
A. EF Core automatically populates navigation properties if the related entities are already loaded in the Context (Local), even without Include.  
B. A bug fix.  
C. Repairing broken DB constraints.  
D. Manual process only.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
If you load all Authors, then load all Books separately, EF sees the FK matches and automatically adds the Books to the Author.Books collections in memory.
</details>

### Q15. `DeleteBehavior.Restrict` vs `DeleteBehavior.NoAction` (SQL Server Specific):
A. They are identical.  
B. `Restrict` happens usually after triggers; `NoAction` causes the delete to fail immediately (FK error) without running triggers. (Though implementation details vary by provider).  
C. `NoAction` deletes the data.  
D. `Restrict` allows delete.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Historically confusing in EF. In SQL Server specifically, `NoAction` is the standard "Foreign Key Error" response.
</details>
