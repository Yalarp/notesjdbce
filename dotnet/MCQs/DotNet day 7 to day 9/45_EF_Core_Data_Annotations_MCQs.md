# 45_EF_Core_Data_Annotations – MCQs

## EASY MCQs

### Q1. Which namespace contains standard Data Annotations like `[Key]`?
A. `System.ComponentModel.DataAnnotations`  
B. `System.Data`  
C. `System.EF`  
D. `System.Xml`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Generic validation and metadata namespace used by EF, MVC, and others.
</details>

### Q2. `[Table("MyUsers")]` attribute does what?
A. Maps the class to a DB table named "MyUsers" (instead of the default name "Users").  
B. Creates a table in UI.  
C. Deletes the table.  
D. Renames the class.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Overrides the default convention (which usually uses DbSet name).
</details>

### Q3. `[NotMapped]` attribute:
A. Prevents the property/entity from being mapped to a Database column/table.  
B. Maps it to null.  
C. Shows an error.  
D. Hides it from Intellisense.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Useful for computed properties (`FullName`) or runtime-only state.
</details>

### Q4. `[Column("col_name")]` allows you to:
A. Specify the exact column name in the database.  
B. Add a column.  
C. Delete a column.  
D. Create new table.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Decouples your C# Property Name (`FirstName`) from legacy DB naming (`first_name_vch`).
</details>

### Q5. `[Required]` is used for:
A. Validation (Not Null).  
B. Authentication.  
C. Authorization.  
D. Encryption.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Enforces a bit of business rule and creates a `NOT NULL` DB constraint.
</details>

---

## MEDIUM MCQs

### Q6. `[InverseProperty("PropName")]` helps resolve:
A. Ambiguous relationships (e.g., when there are multiple FKs between the same two entities).  
B. Inverse matrix.  
C. Property duplications.  
D. The order of columns.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
If `Flight` has `DepartureCity` and `ArrivalCity` (both referencing `City`), EF needs help knowing which collection on `City` corresponds to which property on `Flight`.
</details>

### Q7. `[DatabaseGenerated(DatabaseGeneratedOption.Identity)]` means:
A. The database generates the value on Insert (e.g., Auto-Increment / Identity / Serial).  
B. The application generates it.  
C. It is random.  
D. The value is constant.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Common for integer Primary Keys.
</details>

### Q8. `[Index(nameof(Prop), IsUnique=true)]`:
A. Creates a Unique Index on the column in the database.  
B. Sorts the array.  
C. Finds items faster in List.  
D. Does nothing.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Introduced in EF Core 5. Allows defining indexes directly on the model via attributes (previously Fluent-only).
</details>

### Q9. `[StringLength(50)]` vs `[MaxLength(50)]`.
A. Functionally very similar for DB generation (varchar(50)). `StringLength` comes from Validation namespace and supports MinimumLength logic for UI/API validation.  
B. They are incompatible.  
C. MaxLength is only for arrays.  
D. StringLength is deprecated.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Usually `MaxLength` is preferred for pure EF usage, `StringLength` for shared Validation usage.
</details>

### Q10. `[Timestamp]` maps to:
A. `DateTime`.  
B. `rowversion` / `byte[]` in SQL Server (concurrency token).  
C. `TimeSpan`.  
D. String.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Used for Optimistic Concurrency control. DB updates this byte array automatically on every write.
</details>

---

## HARD MCQs

### Q11. Which attribute sets the "Schema" of a table?
A. `[Table("Name", Schema="dbo")]`  
B. `[Schema("dbo")]`  
C. `[Namespace]`  
D. Not possible with attributes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The Table attribute has a named parameter for schema.
</details>

### Q12. Can Data Annotations configure "Cascade Delete"?
A. No. You must use Fluent API (`OnDelete`).  
B. Yes, `[CascadeDelete]`.  
C. Yes, `[Required]` implies it.  
D. Yes, `[Delete]`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Annotations are limited. Structural behaviors like Cascade rules usually require Fluent API. (Though `[Required]` on a dependent often implies Cascade Delete by convention, explicit control requires Fluent).
</details>

### Q13. `[ConcurrencyCheck]` attribute:
A. Marks a property to be included in the `WHERE` clause of Update/Delete commands to check for concurrency conflicts.  
B. Locks the row.  
C. Checks performance.  
D. Validates time.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Prevents "Lost Updates". `UPDATE ... WHERE Id=1 AND Name='OldName'`. If 0 rows affected, someone else changed Name in between.
</details>

### Q14. `[ComplexType]` (EF6) equivalent in EF Core?
A. `[Owned]`  
B. `[Complex]`  
C. `[Struct]`  
D. `[Embed]`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Used for Owned Entity Types (Value Objects) that are embedded in the same table.
</details>

### Q15. Order of precedence: Fluent API vs Data Annotations.
A. Fluent API wins (overrides annotations).  
B. Annotations win.  
C. They throw exception if conflicting.  
D. Random.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Fluent API is the ultimate source of truth. Annotations are applied first, then Fluent overrides them.
</details>
