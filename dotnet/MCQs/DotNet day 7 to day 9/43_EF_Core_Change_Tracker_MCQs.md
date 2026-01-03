# 43_EF_Core_Change_Tracker – MCQs

## EASY MCQs

### Q1. What component of `DbContext` is responsible for detecting changes?
A. `Database`  
B. `ChangeTracker`  
C. `ModelBuilder`  
D. `LINQ`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It maintains the state manager for all attached entity instances.
</details>

### Q2. `EntityState.Unchanged` means:
A. The entity has been modified.  
B. The entity was loaded from DB and matches the snapshot (no edits yet).  
C. The entity is new.  
D. The entity is deleted.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Default state after a query (unless `AsNoTracking`).
</details>

### Q3. `EntityState.Added` forces EF to generate which SQL?
A. `UPDATE`  
B. `DELETE`  
C. `INSERT`  
D. `SELECT`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
New rows are created for Added entities.
</details>

### Q4. `AsNoTracking()` improves performance because:
A. It doesn't query the database.  
B. It specifically tells EF NOT to take a "snapshot" or track the returned entities.  
C. It uses multiple threads.  
D. It caches data significantly.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Skipping the overhead of setting up tracking data reduces memory and CPU usage for read-only scenarios.
</details>

### Q5. If you modify a tracked entity's property (`user.Name = "New"`), the state becomes:
A. `Modified`  
B. `Added`  
C. `Deleted`  
D. `Broken`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
EF detects the difference between the current value "New" and the original snapshot value.
</details>

---

## MEDIUM MCQs

### Q6. `context.Entry(entity).CurrentValues.SetValues(dto)` serves what purpose?
A. It copies property values from a DTO/Source object onto the Tracked Entity, automatically marking changed properties as Modified.  
B. It validates data.  
C. It inserts data.  
D. It deletes the entity.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Powerful technique for partial updates. `SetValues` matches properties by name and copies the new data in one method call.
</details>

### Q7. `EntityState.Detached` means:
A. The object exists in memory (C#), but the Context is not watching it at all.  
B. The object is deleted.  
C. The object is being saved.  
D. The object is null.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Objects created with `new` are detached. Objects returned from `AsNoTracking` queries are detached.
</details>

### Q8. Does `ChangeTracker` store the "Original Value" of a property?
A. No.  
B. Yes, to perform the comparison against "Current Value" during SaveChanges.  
C. Only for INTs.  
D. Only if configured.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is how EF knows *exactly* which columns changed, generating optimized SQL like `UPDATE ... SET Name=@p WHERE ...` (skipping Age if Age didn't change).
</details>

### Q9. `context.Attach(entity)` usually sets the state to:
A. `Modified`  
B. `Unchanged`  
C. `Added`  
D. `Deleted`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It assumes the entity matches what is in the DB currently. You typically Modify it *after* attaching.
</details>

### Q10. What is `HasChanges()`?
A. A method on `ChangeTracker` returning true if any tracked entity is Added/Modified/Deleted.  
B. A Linq method.  
C. A database trigger.  
D. A variable.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Useful UI check ("Do you want to save your changes?").
</details>

---

## HARD MCQs

### Q11. "Graph Diff" or updating a complex graph (Parent + Children) in Disconnected scenarios:
A. Is automatic and easy.  
B. Is notoriously difficult in EF Core. You often have to manually figure out which children were added, deleted, or modified compared to the DB.  
C. Is impossible.  
D. Use `Add()`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Because EF didn't track the changes happening on the client (browser), receiving a list of children back requires work to reconcile which ones remain.
</details>

### Q12. `DebugView` (e.g., `context.ChangeTracker.DebugView.LongView`):
A. A powerful debugging string dump showing all tracked entities and their current states/values.  
B. A UI tool.  
C. A logging level.  
D. An error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Inspect this property in the debugger watch window to understand exactly what EF thinks is going on.
</details>

### Q13. `DetectChanges()` method:
A. Is called automatically by `SaveChanges()`. It scans all tracked POCOs to update their States based on properties.  
B. Never needs to be called.  
C. Is slow.  
D. Deletes data.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
You generally don't call it manually. But in tight loops with thousands of items, disabling AutoDetectChanges and calling it once manually can boost performance.
</details>

### Q14. Can you track the same Entity Key twice in one Context instance?
A. Yes, perfectly fine.  
B. No. `InvalidOperationException`: The instance of entity type 'User' cannot be tracked because another instance with the same key value for {'Id'} is already being tracked.  
C. Yes, but it overwrites.  
D. Only if `AsNoTracking`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Identity Map pattern ensures only ONE object instance represents Row #1 in memory per Context to avoid conflicting states.
</details>

### Q15. `PropertyEntry.IsModified` allows you to:
A. Manually flag a single property as dirty/modified, ensuring it gets updated in SQL.  
B. Check if a property is public.  
C. Delete the property.  
D. Read only.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`context.Entry(user).Property(u => u.Name).IsModified = true;` allows surgical updates without retrieving the record first.
</details>
