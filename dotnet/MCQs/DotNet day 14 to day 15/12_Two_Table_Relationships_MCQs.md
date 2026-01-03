# 12_Two_Table_Relationships – MCQs

## EASY MCQs

### Q1. What type of relationship exists between a `Department` and its `Employees`?
A. One-to-One
B. One-to-Many (One Department has many Employees).
C. Many-to-Many
D. None

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
One parent, multiple children.
</details>

### Q2. In the `Employee` class, what does the property `public int DepartmentId { get; set; }` represent?
A. The Primary Key.
B. The Foreign Key pointing to the Department table.
C. The Name.
D. A random number.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It holds the ID of the related parent record.
</details>

### Q3. What LINQ method is used to load related data (like fetching Department with Employee)?
A. `Join()`
B. `Include()`
C. `Select()`
D. `Attach()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Eager loading mechanism.
</details>

### Q4. What is a "Navigation Property"?
A. A property used for GPS.
B. A property on an Entity (`public Department Dept {get;set;}`) that allows you to traverse the relationship in code to access the related object.
C. A URL.
D. A map.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It automates the traversal of FK relationships.
</details>

### Q5. If you try to serialize an object graph with circular references (Parent->Child->Parent) to JSON, what happens?
A. It works fine.
B. It throws a JsonException (Cycle detected).
C. It deletes the data.
D. It returns 404.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The serializer gets stuck in an infinite loop. Use `ReferenceHandler.IgnoreCycles`.
</details>

---

## MEDIUM MCQs

### Q6. What does the `[ForeignKey("Name")]` attribute do?
A. Creates a key.
B. Explicitly specifies which property is the Foreign Key if the naming convention (e.g. `DepartmentId`) is not followed.
C. Validates the key.
D. Deletes the key.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Maps the navigation property to the underlying FK column.
</details>

### Q7. What is "Eager Loading"?
A. Loading data before it is requested.
B. Loading related entities as part of the initial query (using `Include`).
C. Loading data when accessed property (Lazy Loading).
D. Loading quickly.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Retrieves the main data and related data in a single round-trip (usually a JOIN).
</details>

### Q8. What is the N+1 problem?
A. A math problem.
B. A performance issue where 1 query fetches the list, and then N separate queries are executed to fetch related data for each item loop. `Include` solves this.
C. An error code.
D. A loop.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The database killer. Iterating `employees` and accessing `emp.Department` without checking if it was loaded.
</details>

### Q9. How do you implement Cascade Delete?
A. `OnDelete(DeleteBehavior.Cascade)` in Fluent API.
B. It happens automatically for all types.
C. Use a try-catch block.
D. Delete manually.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Ensures children are deleted when the parent is deleted.
</details>

### Q10. Why use `[JsonIgnore]` on the parent property inside the child class?
A. To hide it from the database.
B. To prevent the JSON Serializer from traversing back up to the parent, triggering a Cycle Error.
C. To delete the parent.
D. To ignore validation.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Quick fix for circular refereces in DTO-less architectures.
</details>

---

## HARD MCQs

### Q11. `ThenInclude` is used for?
A. Loading a second level of related data (e.g., Department -> Employees -> Address).
B. Including data later.
C. Loading parallel data.
D. Adding data.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Chains eager loading deeper into the graph.
</details>

### Q12. If `Employee` has `int? DepartmentId` (nullable), what does this imply?
A. The relationship is Required.
B. The relationship is Optional (Employee can exist without a Department).
C. Syntax error.
D. Department is deleted.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Nullable FK = Optional relationship. Non-nullable FK = Required relationship.
</details>

### Q13. In Fluent API, `.HasOne(...).WithMany(...)` configures what?
A. One-to-One.
B. One-to-Many relationship.
C. Many-to-Many.
D. No relationship.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Standard configuration syntax.
</details>

### Q14. What is a "Shadow Property" in EF Core?
A. A property that is dark.
B. A field that exists in the database table but is NOT defined in the C# Entity Class. EF manages it internally.
C. A private property.
D. A static property.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Useful if you don't want to pollute your domain model with FK IDs but still want the relationship.
</details>

### Q15. Lazy Loading requires what keyword on navigation properties?
A. `static`
B. `virtual`
C. `abstract`
D. `lazy`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Allows the EF proxy to override the property getter and trigger the DB load on access. (Note: standard in EF6, requires extra setup in EF Core).
</details>
