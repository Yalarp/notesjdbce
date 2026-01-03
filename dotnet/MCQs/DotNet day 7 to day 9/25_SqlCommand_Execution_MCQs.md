# 25_SqlCommand_Execution – MCQs

## EASY MCQs

### Q1. Which method should you use for an `INSERT` statement?
A. `ExecuteReader`  
B. `ExecuteNonQuery`  
C. `ExecuteScalar`  
D. `ExecuteXmlReader`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
INSERT, UPDATE, and DELETE modify data but do not return rows. `ExecuteNonQuery` is designed for this.
</details>

### Q2. Which method should you use for `SELECT COUNT(*) FROM Table`?
A. `ExecuteReader`  
B. `ExecuteNonQuery`  
C. `ExecuteScalar`  
D. `ExecuteVoid`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
You expect a single value (scalar result). `ExecuteScalar` returns the first column of the first row efficiently.
</details>

### Q3. What does `ExecuteReader()` return?
A. An integer count.  
B. An implementation of `SqlDataReader`.  
C. A `DataSet`.  
D. A String.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It returns a `SqlDataReader` object used to iterate over the results row by row.
</details>

### Q4. To execute a command, the associated `SqlConnection` must be:
A. Any state.  
B. New.  
C. Open.  
D. Closed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The connection must be explicitly opened (`con.Open()`) before calling any `Execute` method.
</details>

### Q5. What does `ExecuteNonQuery()` return?
A. The data inserted.  
B. The primary key.  
C. The number of rows affected (int).  
D. True/False.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
For standard DML statements, it returns the row count.
</details>

---

## MEDIUM MCQs

### Q6. In the code `SqlCommand cmd = new SqlCommand(sql, con);`, what happens if `sql` is null?
A. No error.  
B. An Exception is thrown when creating the command or executing it.  
C. It deletes the table.  
D. It acts as SELECT *.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The command text cannot be null.
</details>

### Q7. How do you check if a `SqlDataReader` contains any results before reading?
A. `rdr.Read()`  
B. `rdr.HasRows`  
C. `rdr.Count > 0`  
D. `rdr.NextResult()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`HasRows` is a boolean property indicating if the result set is non-empty.
</details>

### Q8. What does `rdr.Read()` do?
A. Reads all data into array.  
B. Advances the cursor to the next row and returns `true` if a row exists.  
C. Opens the file.  
D. Returns the first column.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It moves the pointer forward. `DataReader` starts *before* the first row. You must call `Read()` at least once to get data.
</details>

### Q9. In the snippet: `"INSERT... VALUES (" + id + ...`, what is the major security flaw?
A. Memory Leak.  
B. SQL Injection.  
C. Deadlock.  
D. Performance issue.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Concatenating strings to build SQL queries allows malicious users to manipulate the query logic (e.g., `' OR '1'='1'`). Always use Parameters!
</details>

### Q10. If `ExecuteScalar` returns `DBNull.Value`, what does it mean?
A. The query failed.  
B. The result in the database cell is NULL.  
C. There were no rows.  
D. The connection dropped.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`DBNull` represents a database NULL. It is distinct from C# `null`. If the result is simply empty (no rows), `ExecuteScalar` typically returns `null`.
</details>

---

## HARD MCQs

### Q11. Can `SqlCommand` execute multiple SQL statements in one go?
A. No.  
B. Yes, if separated by semicolons (e.g., "INSERT...; SELECT...").  
C. Yes, but only in multiple threads.  
D. No, it requires multiple commands.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Batch execution is possible. `ExecuteReader` creates a reader where you can use `NextResult()` to move to the second query's result set.
</details>

### Q12. Difference between `cmd.ExecuteReader()` and `cmd.ExecuteReader(CommandBehavior.CloseConnection)`?
A. No difference.  
B. With `CommandBehavior.CloseConnection`, closing the Reader automatically closes the underlying Connection.  
C. It closes the connection immediately.  
D. It prevents reading.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Useful when returning a Reader out of a method. Since the caller owns the reader but not the connection variable, this flag ensures the connection is cleaned up when the caller is done with the reader.
</details>

### Q13. `SqlCommand` can also execute Stored Procedures. How?
A. `cmd.CommandType = CommandType.StoredProcedure` and set `CommandText` to proc name.  
B. Write "EXEC procName" in text.  
C. Both A and B work, but A is preferred.  
D. It is not supported.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Setting the `CommandType` explicitly to `StoredProcedure` is the cleaner, RPC-optimized way.
</details>

### Q14. Why is `ExecuteScalar` generally more efficient than `ExecuteReader` for obtaining a single value?
A. It isn't.  
B. It skips the overhead of creating a complex `SqlDataReader` caching structure just for one value.  
C. It runs on GPU.  
D. It caches results.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is optimized for that specific use case (fetching 1x1 cell), discarding extra metadata handling required for streams.
</details>

### Q15. If an Exception occurs inside the `using (SqlConnection...)` block during `ExecuteNonQuery`:
A. The connection stays OPEN indefinitely.  
B. The transaction commits.  
C. `Dispose()` is called as stack unwinds, closing the connection safely.  
D. The app ignores it.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
This is the main safety feature of the `using` block. Even with exceptions, cleanup code runs.
</details>
