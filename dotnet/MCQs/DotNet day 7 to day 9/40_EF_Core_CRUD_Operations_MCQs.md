# 40_EF_Core_CRUD_Operations – MCQs

## EASY MCQs

### Q1. To add a new record to the database, you first call:
A. `context.Add(entity)`  
B. `context.Insert(entity)`  
C. `context.Put(entity)`  
D. `context.Push(entity)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`Add()` sets the entity state to `Added`. The Insert SQL is not generated until `SaveChanges()` is called.
</details>

### Q2. Does `context.Add()` immediately hit the database?
A. Yes.  
B. No. It effectively queues the operation in memory.  
C. It throws an error.  
D. It deletes data.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
All changes are transactional and batched. Nothing happens on the server until `SaveChanges()`.
</details>

### Q3. `SaveChanges()` returns:
A. The number of rows affected/written to the database.  
B. A boolean.  
C. The data itself.  
D. Void.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Useful to verify if the operation actually did anything (e.g., return > 0).
</details>

### Q4. Which method is most efficient to retrieve an entity by Primary Key?
A. `Where(x => x.Id == id).FirstOrDefault()`  
B. `Find(id)`  
C. `Select(id)`  
D. `Get(id)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Find` checks the local context memory (cache) first. If the entity is already loaded, it returns it instantly without a database roundtrip. `Where` always queries the DB.
</details>

### Q5. To delete an entity, you use:
A. `context.Remove(entity)`  
B. `context.Delete(entity)`  
C. `context.Erase(entity)`  
D. `context.Drop(entity)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Sets state to `Deleted`. `SaveChanges` issues a `DELETE` SQL command.
</details>

---

## MEDIUM MCQs

### Q6. How do you Update an entity that you just pulled from the database in the same context?
A. Call `Update()`.  
B. Just modify the properties of the object. EF Core Change Tracking detects the difference automatically when you call `SaveChanges`.  
C. Call `Write()`.  
D. Delete and re-insert.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
In a "Connected" state, the entity is tracked using a snapshot. Any changes to properties are auto-detected as "Modified".
</details>

### Q7. `context.Entry(entity).State = EntityState.Modified;` is used when:
A. You are in a "Disconnected" scenario (e.g., receiving an object from a web request) and need to tell EF to update all columns.  
B. Always.  
C. Never.  
D. For new entities.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Since EF didn't load this object, it has no snapshot to compare. Setting state to Modified forces EF to treat it as "dirty" and generate an UPDATE statement.
</details>

### Q8. Does `Remove()` require the entity to be attached/tracked?
A. No.  
B. Yes. You typically `Find()` it first, or Create a stub with the ID, Attach it, then Remove it.  
C. It works on nulls.  
D. It works by magic.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
EF needs to know *what* to delete. It needs a tracked object with a Primary Key.
</details>

### Q9. `Include()` is used for:
A. Including libraries.  
B. Eager Loading related data (JOINs).  
C. Filtering.  
D. Sorting.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`context.Authors.Include(a => a.Books)` tells EF to fetch the Author AND their Books in the query.
</details>

### Q10. `ToListAsync()` requires:
A. `System.Linq`  
B. `Microsoft.EntityFrameworkCore` namespace.  
C. `System.Threading`  
D. SQL Server installed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is an extension method provided by EF Core, not standard LINQ-to-Objects.
</details>

---

## HARD MCQs

### Q11. Optimization: `ExecuteDelete` (EF Core 7+) allow you to:
A. `context.Users.Where(u => u.Age < 18).ExecuteDelete()`  
B. Delete entities in memory only.  
C. Delete database files.  
D. It doesn't exist.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
This performs a bulk SQL DELETE directly on the database (`DELETE FROM Users WHERE ...`) *without* loading the entities into memory first. Huge performance gain for bulk ops.
</details>

### Q12. If you attach an object graph (Author -> Books) using `Update()`, what does EF assume about the related Books?
A. It ignores them.  
B. It assumes ALL of them are Modified/Added, potentially creating duplicates if you aren't careful with IDs.  
C. It only updates the Author.  
D. It crashes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Update()` traverses the graph and marks reachable entities as Modified (or Added if no key). Handling disconnected graphs is complex in EF.
</details>

### Q13. `TryUpdateModelAsync` (in Controllers) refers to:
A. EF Core method.  
B. ASP.NET MVC/API Model Binding mechanism to update an entity from request data securely.  
C. Transaction.  
D. Validation.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It's an MVC controller helper, not strictly EF, but often used *with* EF to patch entities securely preventing over-posting.
</details>

### Q14. What happens if you call `Add()` on an entity that has an ID set (and Identity Insert is OFF)?
A. It inserts fine.  
B. It might try to insert the ID, causing a database error if the column is IDENTITY.  
C. It updates it.  
D. It ignores the ID.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
EF usually ignores the ID if it's default (0), but if you explicitly set ID=5 and try to Add, it assumes you want to force insert ID 5, which fails if Identity semantics restrict it.
</details>

### Q15. Concurrency conflicts (two users update same row) are handled by:
A. First one wins.  
B. Last one wins (default), unless a `ConcurrencyToken` / `RowVersion` is configured, then `DbUpdateConcurrencyException` is thrown.  
C. Database locks.  
D. The OS.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
By default, standard "last writer wins". Optimistic Concurrency control requires metadata configuration to detect overlaps.
</details>
