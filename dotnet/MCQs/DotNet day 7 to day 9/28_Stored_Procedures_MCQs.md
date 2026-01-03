# 28_Stored_Procedures – MCQs

## EASY MCQs

### Q1. What is a Stored Procedure?
A. A backup of the database.  
B. A precompiled collection of SQL statements stored under a name and processed as a unit.  
C. A C# method.  
D. A table.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is code (SQL logic) saved physically in the database, executable by name.
</details>

### Q2. To call a stored procedure using `SqlCommand`, you must set `CommandType` to:
A. `CommandType.Text`  
B. `CommandType.TableDirect`  
C. `CommandType.StoredProcedure`  
D. `CommandType.Execute`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
This informs ADO.NET to construct the internal RPC (Remote Procedure Call) packet correctly rather than sending a "EXEC name" string.
</details>

### Q3. Stored Procedures improve performance primarily because:
A. They use less disk space.  
B. Their execution plans are precompiled and cached by SQL Server.  
C. They are written in C++.  
D. They don't use parameters.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Parsing, analyzing, and optimizing the query happens once (or infrequenty), saving CPU time on subsequent calls compared to ad-hoc SQL.
</details>

### Q4. Which direction is used for a parameter that returns a value from the SP to C#?
A. `ParameterDirection.Input`  
B. `ParameterDirection.Output`  
C. `ParameterDirection.Forward`  
D. `ParameterDirection.Left`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Output parameters allow the SP to pass data back to the caller (like C# `out` parameters).
</details>

### Q5. What is the SQL keyword to define a new procedure?
A. `NEW PROCEDURE`  
B. `CREATE PROC` (or `PROCEDURE`)  
C. `MAKE SP`  
D. `INSERT PROC`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Standard T-SQL syntax is `CREATE PROCEDURE [name] AS ...`.
</details>

---

## MEDIUM MCQs

### Q6. A "Return Value" from a Stored Procedure relies on the `RETURN` SQL statement. What type is it limited to?
A. Any object.  
B. String.  
C. Integer.  
D. Table.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
SQL Server return values are strictly 32-bit Integers, typically used for status codes (0 = Success, non-zero = Error).
</details>

### Q7. Can a stored procedure return a result set (rows/columns) AND output parameters?
A. No.  
B. Yes.  
C. Only one or the other.  
D. Only in Oracle.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
An SP can select rows to return to a DataReader, set output parameters, AND return a status integer code all in one execution.
</details>

### Q8. When retrieving an output parameter value in C#, you must accede it:
A. Before calling `ExecuteNonQuery`.  
B. After calling `ExecuteNonQuery`.  
C. During execution.  
D. You cannot.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The server processes the logic and populates the output buffer. The client can only read the resultant value after the network round-trip completes.
</details>

### Q9. Security Benefit: Granting `EXECUTE` permission on an SP allows:
A. Users to delete the database.  
B. Users to run the SP logic without having direct `SELECT/INSERT` permissions on the underlying tables.  
C. No benefit.  
D. Users to see the SP code.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This encapsulates access implementation. Code can update the table, but the user cannot bypass the code to delete rows directly.
</details>

### Q10. What is `SCOPE_IDENTITY()` used for in the example?
A. To check security.  
B. To get the last Identity ID generated in the current scope (e.g., the new Primary Key after insert).  
C. To identify the user.  
D. To find the table name.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Commonly returned via an output parameter to let the application know the ID of the record it just created.
</details>

---

## HARD MCQs

### Q11. Network Traffic reduction with SPs:
A. SPs compress data.  
B. Instead of sending a massive SQL string ("SELECT a, b, c ... FROM ... WHERE ..."), you only send the short SP name ("sp_GetData") and parameter values.  
C. False, SPs generate more traffic.  
D. SPs use UDP.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
For complex queries, sending the query text over the wire (especially repeatedly) consumes bandwidth. SP calls are compact.
</details>

### Q12. Versioning/Maintenance benefit:
A. If you change the database schema, you might only need to update the SP, not the compiled C# application (no redeploy).  
B. You must always redeploy C#.  
C. SPs cannot be changed.  
D. C# automatically updates the SP.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
If the detailed SQL logic (e.g., adding a JOIN for filtering) changes but the parameter interface stays the same, the C# app doesn't need to know. It acts as an API contract.
</details>

### Q13. `cmd.Parameters.Add(new SqlParameter { Direction = ParameterDirection.ReturnValue });` MUST be:
A. The last parameter added.  
B. The first parameter added (by convention, though modern drivers handle order, it was historically required).  
C. Named "Return".  
D. A String type.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Historically in ADO/OLEDB, the return value was arguably the 0th parameter.
</details>

### Q14. Can Stored Procedures encapsulate Transactions?
A. No.  
B. Yes, using `BEGIN TECH`, `COMMIT`.  
C. Yes, using `BEGIN TRAN`, `COMMIT`, `ROLLBACK`.  
D. Only if called from C#.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
SPs can manage their own atomic units of work internally. If one step fails, the SP can rollback everything before returning.
</details>

### Q15. Is business logic in Stored Procedures considered a "Best Practice" in modern architectures (like Microservices)?
A. Yes, always.  
B. It is debated. Logic in SPs provides performance but creates "Vendor _Lock-in" (hard to switch from SQL Server to Postgres) and splits logic between App and DB.  
C. No, never use SPs.  
D. Logic should be in JavaScript.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
While SPs are powerful tools, modern trends (Domain Driven Design) often prefer logic in the application layer for better testability and database agnosticism, using SPs mainly for performance-critical data retrieval.
</details>
