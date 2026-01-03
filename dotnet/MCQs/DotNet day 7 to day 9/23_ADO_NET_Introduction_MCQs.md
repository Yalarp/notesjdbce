# 23_ADO_NET_Introduction – MCQs

## EASY MCQs

### Q1. What does ADO.NET stand for?
A. Active Data Objects .NET  
B. ActiveX Data Objects .NET  
C. Application Data Objects .NET  
D. Advanced Data Objects .NET  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is the successor to the older ActiveX Data Objects (ADO) technology, adapted for the .NET Framework.
</details>

### Q2. Which namespace contains the core ADO.NET classes for SQL Server?
A. `System.Data.Oracle`  
B. `System.Data.SqlClient` (or `Microsoft.Data.SqlClient`)  
C. `System.IO`  
D. `System.Net`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The specific provider for Microsoft SQL Server is historically in `System.Data.SqlClient`, though newer .NET Core apps prefer `Microsoft.Data.SqlClient`.
</details>

### Q3. ADO.NET supports two main architectures. What are they?
A. Connected and Disconnected  
B. Online and Offline  
C. Stateful and Stateless  
D. TCP and UDP  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The Connected architecture (DataReader) keeps the link open while reading. The Disconnected architecture (DataSet) fetches data, closes connection, and works in memory.
</details>

### Q4. Which object is used to establish a session with the database?
A. `SqlCommand`  
B. `SqlConnection`  
C. `SqlDataReader`  
D. `SqlAdapter`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SqlConnection` represents an open connection to a SQL Server database.
</details>

### Q5. Where is the recommended place to store Connection Strings in .NET Core?
A. Hardcoded in C# file.  
B. In a text file on desktop.  
C. In `appsettings.json`.  
D. In Registry.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
External configuration files (`appsettings.json`) allow changing database targets without recompiling the code.
</details>

---

## MEDIUM MCQs

### Q6. Which object provides a forward-only, read-only stream of rows from a database?
A. `DataSet`  
B. `SqlDataReader`  
C. `DataTable`  
D. `SqlDataAdapter`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SqlDataReader` is the most efficient way to read data sequentially. It requires an open connection.
</details>

### Q7. The Disconnected Architecture typically uses which pair of objects?
A. `SqlCommand` and `SqlDataReader`  
B. `SqlDataAdapter` and `DataSet`  
C. `SqlConnection` and `String`  
D. `Reader` and `Writer`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `SqlDataAdapter` acts as a bridge to fill a `DataSet` (in-memory cache) and update changes back to the database.
</details>

### Q8. What is a `DataSet`?
A. A single row of data.  
B. An in-memory representation of data, capable of holding multiple tables, relationships, and constraints.  
C. A database file on disk.  
D. A connection string.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Think of `DataSet` as a mini-database in your RAM. It is database-agnostic.
</details>

### Q9. Which package is required for `IConfiguration` to read JSON files?
A. `System.Text`  
B. `Microsoft.Extensions.Configuration.Json`  
C. `System.Data`  
D. `System.Xml`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The configuration system is modular. You need the JSON provider extension to parse `appsettings.json`.
</details>

### Q10. Why is `using` statement critical for `SqlConnection`?
A. It speeds up the query.  
B. It ensures the connection is closed and returned to the pool, even if an exception occurs.  
C. It encrypts the connection.  
D. It is mandatory syntax.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SqlConnection` implements `IDisposable`. The `using` block ensures `Dispose()` is called, which closes the physical connection properly.
</details>

---

## HARD MCQs

### Q11. Comparing Connected vs Disconnected: Which consumes less memory for large datasets?
A. Disconnected (DataSet).  
B. Connected (DataReader).  
C. Both are same.  
D. None.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SqlDataReader` streams one row at a time. `DataSet` loads the *entire* result into memory. For millions of rows, `DataSet` will crash your app (OutOfMemory).
</details>

### Q12. Connection Pooling:
A. ADO.NET opens a new physical connection for every specific `new SqlConnection()` call.  
B. ADO.NET reuses physical connections from a pool if the connection string matches exactly.  
C. Is disabled by default.  
D. Only works with Oracle.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Opening physical connections is expensive. ADO.NET maintains a pool. `Open()` effectively grabs one from the pool, and `Close()` returns it to the pool.
</details>

### Q13. `System.Data.Common` namespace contains:
A. SQL Server specific classes.  
B. Base classes (DbConnection, DbCommand) that allow writing provider-independent code.  
C. Configuration logic.  
D. Nothing.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Ideally, you can write code against `DbConnection` abstractions, allowing you to switch between SQL Server, Oracle, or MySQL just by changing the factory.
</details>

### Q14. What is the role of `SqlDataAdapter.Fill()`?
A. To fill a glass with water.  
B. Opens connection, executes SelectCommand, retrieves data, populates DataSet, and closes connection.  
C. Only executes query.  
D. Saves data to database.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It handles the entire lifecycle of the connection automatically (Open -> Fetch -> Close) to populate the disconnected cache.
</details>

### Q15. In a high-concurrency web API, which approach is preferred for ready-only data?
A. Disconnected (DataSet).  
B. Connected (DataReader) or Dapper (which uses DataReader internally).  
C. Static variables.  
D. XML files.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
DataReader is faster and lighter. DataSet adds significant overhead (memory and object creation) which is unnecessary if you are just reading data to send as JSON.
</details>
