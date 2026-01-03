# 24_SqlConnection_Configuration – MCQs

## EASY MCQs

### Q1. What is the purpose of the `SqlConnection` object?
A. To execute queries.  
B. To establish a session with the SQL Server database.  
C. To hold data results.  
D. To read configuration files.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It serves as the gateway primarily used to open a communication channel with the server.
</details>

### Q2. Which method actually establishes the connection?
A. `con.Start()`  
B. `new SqlConnection()`  
C. `con.Open()`  
D. `con.Connect()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The constructor only creates the .NET object. The `Open()` method initiates the network handshake/login procedure.
</details>

### Q3. In the example, `_iconfiguration.GetConnectionString("Default")` retrieves:
A. The database name.  
B. The connection string value from the "ConnectionStrings" section of appsettings.json.  
C. The password only.  
D. The SQL driver.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is a helper method in .NET Core to simplify reading from the standard `ConnectionStrings` JSON section.
</details>

### Q4. Ideally, a `SqlConnection` should be opened:
A. The moment the application starts.  
B. As late as possible, just before executing a command.  
C. Never.  
D. In the class constructor.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
"Open Late, Close Early" is the mantra. Holding connections open wastes resources and limits scalability as the connection pool is finite.
</details>

### Q5. What does the `using` block do for `SqlConnection`?
A. It imports namespaces.  
B. It calls `Dispose()` (which calls `Close()`) automatically at the end of the block.  
C. It keeps the connection open forever.  
D. It suppresses errors.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is syntax sugar for a `try-finally` block ensuring resource cleanup.
</details>

---

## MEDIUM MCQs

### Q6. In the connection string "Data Source=(localdb)\ProjectModels", what is `Data Source`?
A. The name of the table.  
B. The name/address of the SQL Server instance.  
C. The username.  
D. The file path.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Data Source` (or `Server`) specifies the machine and instance name to connect to.
</details>

### Q7. What is `Integrated Security=True`?
A. Use the current Windows User credentials for authentication (Windows Auth).  
B. Use a specific username and password.  
C. Use SSL encryption.  
D. Use a firewall.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It avoids hardcoding passwords by trusting the OS identity of the running process/user.
</details>

### Q8. The `ConfigurationBuilder` requires `SetBasePath` to:
A. Find the database.  
B. Know where to look for the `appsettings.json` file (usually current execution directory).  
C. Create a folder.  
D. Compile the code.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Without the base path, it might look in a system directory or fail to find the relative JSON file.
</details>

### Q9. If you forget to call `con.Close()` (and don't use `using`), what happens?
A. Nothing bad.  
B. The connection remains "leased" from the pool, eventually leading to a "Connection Pool Reached Max Size" error (Connection Leak).  
C. The database crashes.  
D. The computer restarts.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Connection leaks are a common cause of production outages. The pool runs out of available connections, and new users are rejected.
</details>

### Q10. The `Initial Catalog` parameter in a connection string represents:
A. The Server Name.  
B. The Database Name.  
C. The Schema.  
D. The Table.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It specifies which database context to enter upon login.
</details>

---

## HARD MCQs

### Q11. "Connection Pooling" optimization means:
A. `con.Close()` does NOT actually close the physical TCP connection to the server.  
B. `con.Close()` terminates everything immediately.  
C. You share one `SqlConnection` object across all threads.  
D. You connect to multiple databases at once.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`Close()` just returns the connection to the driver's pool managed in the process. The physical link stays alive for a while to be reused by the next `Open()` call with the same connection string.
</details>

### Q12. Why is passing `IConfiguration` to the `ProductLayer` constructor (Dependency Injection) better than creating it inside?
A. It follows Inversion of Control / Dependency Injection principles, making `ProductLayer` testable and configuration-independent.  
B. It is slower.  
C. It writes more code.  
D. It prevents reading the file.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`ProductLayer` doesn't need to know *how* to parse JSON files; it just needs the configuration result. Creating `ConfigurationBuilder` inside binds it to the file system.
</details>

### Q13. `reloadOnChange: true` in `AddJsonFile` means:
A. The file is deleted after reading.  
B. The `IConfiguration` object will automatically update its values if the `appsettings.json` file is modified on disk while the app is running.  
C. It reloads the database.  
D. It restarts the server.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This feature allows for hot-configuration updates without restarting the application process.
</details>

### Q14. Can you construct a connection string programmatically?
A. No, must be a string literal.  
B. Yes, using `SqlConnectionStringBuilder`.  
C. Yes, using `StringBuilder` only.  
D. No, it is secure.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SqlConnectionStringBuilder` provides a strongly-typed way to build connection strings, preventing syntax errors and injection risks in the string itself.
</details>

### Q15. Security Best Practice: Where should production passwords reside?
A. `appsettings.json` committed to Git.  
B. Environment Variables or Secret Managers (like Azure Key Vault).  
C. Hardcoded source code.  
D. Stickynotes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Never commit secrets to source control. Use environment-specific overrides.
</details>
