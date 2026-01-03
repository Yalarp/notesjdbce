# 26_SqlDataReader – MCQs

## EASY MCQs

### Q1. What is the primary characteristic of `SqlDataReader`?
A. Connects to the internet.  
B. It provides a forward-only, read-only stream of rows.  
C. It allows updating rows while reading.  
D. It stores all data in memory.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SqlDataReader` is designed for high-performance reading, streaming data sequentially without caching the entire result set.
</details>

### Q2. How do you advance the reader to the next row?
A. `rdr.Next()`  
B. `rdr.Read()`  
C. `rdr.Move()`  
D. `rdr.Go()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `Read()` method moves the internal cursor to the next record. It returns `true` if a row exists, otherwise `false`.
</details>

### Q3. Does `SqlDataReader` contain data when first returned by `ExecuteReader()`?
A. Yes, it points to the first row.  
B. No, the cursor is positioned BEFORE the first row.  
C. Yes, it contains all rows.  
D. No, it is null.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You strictly MUST call `Read()` at least once to position it on the first valid row of data.
</details>

### Q4. Which property checks if the result set is empty?
A. `rdr.Count`  
B. `rdr.HasRows`  
C. `rdr.IsEmpty`  
D. `rdr.Length`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`HasRows` returns a boolean indicating whether the returned result set contains one or more rows.
</details>

### Q5. While the `SqlDataReader` is open, what is the state of the `SqlConnection`?
A. It is free to be used by other commands.  
B. It is busy serving the reader.  
C. It is closed.  
D. It is disconnected.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The connection is "busy" streaming data. You cannot execute other commands on the same connection until the reader is closed.
</details>

---

## MEDIUM MCQs

### Q6. Which method offers the best performance and type safety for retrieving an integer column?
A. `(int)rdr["Age"]`  
B. `Convert.ToInt32(rdr[0])`  
C. `rdr.GetInt32(0)`  
D. `int.Parse(rdr["Age"].ToString())`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`GetInt32(ordinal)` retrieves the native 32-bit integer directly from the stream without boxing/unboxing or string parsing overhead.
</details>

### Q7. If you try to read a column value that is `NULL` in the database using `GetString()`, what happens?
A. It returns empty string.  
B. It returns `null`.  
C. It throws an `InvalidCastException` (or `SqlNullValueException`).  
D. It returns "NULL".  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The typed accessor methods (`GetInt32`, `GetString`) cannot handle `DBNull` automatically. You must check `IsDBNull()` first.
</details>

### Q8. What is the recommended way to get the ordinal (index) of a column by its name?
A. Loop through all columns.  
B. Guess the number.  
C. `rdr.GetOrdinal("ColumnName")`  
D. Use a Dictionary.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`GetOrdinal` performs a lookup to find the integer index corresponding to the column name, which can then be reused for performance.
</details>

### Q9. `rdr["Price"]` returns which C# type?
A. `decimal`  
B. `double`  
C. `object`  
D. `string`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The indexer returns `object`. You must cast it `(decimal)rdr["Price"]` or convert it to use it as a specific type.
</details>

### Q10. Why is `Select *` bad when using `GetInt32(index)`?
A. It isn't.  
B. If the table schema changes (columns reordered or added), the index `0, 1, 2` might point to the wrong data, breaking the code.  
C. It causes a syntax error.  
D. It is slower.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Positional access depends strictly on the order of columns in the query. Using `SELECT *` makes this order fragile.
</details>

---

## HARD MCQs

### Q11. Can `SqlDataReader` read multiple result sets (e.g., from a batch query "SELECT * FROM A; SELECT * FROM B")?
A. No.  
B. Yes, using `rdr.NextResult()`.  
C. Yes, using `rdr.NextRow()`.  
D. Yes, automatically.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Read()` iterates rows in the *current* result set. `NextResult()` advances the reader to the *next* result set in the batch.
</details>

### Q12. What is a "DTO" (Data Transfer Object) in this context?
A. The `SqlConnection` object.  
B. A simple class (like `Employee` or `Product`) used to hold the data read from the database, decoupled from logic.  
C. A database table.  
D. A query tool.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
We read raw data from the reader and "map" it into strongly-typed DTOs/POCOs to pass around the application.
</details>

### Q13. `CommandBehavior.SequentialAccess` mode:
A. Allows reading columns in random order.  
B. Forces you to read columns sequentially (0, then 1, then 2).  
C. Reads all rows at once.  
D. Is default.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It optimizes reading large binary data (BLOBs) by streaming data without buffering the entire row. The trade-off is you cannot go back to column 0 if you are at column 5.
</details>

### Q14. If `rdr.Read()` returns `false`, and you call `rdr.Read()` again:
A. It moves to the first row.  
B. It throws an Exception.  
C. It continues to return `false`.  
D. It crashes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Once the stream is exhausted, subsequent calls indicate no more data is available.
</details>

### Q15. Best practice for checking NULLs on nullable integers:
A. `int? val = rdr["Col"] as int?;`  
B. `int? val = rdr.IsDBNull(i) ? (int?)null : rdr.GetInt32(i);`  
C. `int val = (int)rdr["Col"];` // hope for the best  
D. `try-catch` block.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Option B is the explicit, safe, and performant way to handle nullable value types without depending on `object` casting nuances or exceptions.
</details>
