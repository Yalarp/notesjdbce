# 44_EF_Core_Logging – MCQs

## EASY MCQs

### Q1. To quickly see SQL queries in the Console during development, use:
A. `.LogTo(Console.WriteLine)` in `OnConfiguring`.  
B. Use a proxy tool.  
C. `Console.WriteSQL()`  
D. Breakpoints.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Simple API (EF Core 5+) to pipe internal logs to a delegate (string action).
</details>

### Q2. `EnableSensitiveDataLogging()` is risky because:
A. It is slow.  
B. It logs actual parameter values (like user passwords, credit card numbers, PII) into the log output.  
C. It crashes the app.  
D. It deletes data.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Strictly for debugging logic errors (why did this query return 0 rows? oh, I passed 'Jon' instead of 'John'). NEVER in Production.
</details>

### Q3. By default, EF Core Logging integrates with:
A. Windows Event Log.  
B. The standard .NET `Microsoft.Extensions.Logging` (ILogger) system if using `AddDbContext`.  
C. Text files.  
D. Nothing.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If you are in ASP.NET Core, EF logs flow to the same destination as your other app logs (Console, Debug, ApplicationInsights).
</details>

### Q4. `DbLoggerCategory.Database.Command` refers to:
A. The logging category specific to executed SQL commands.  
B. Connection errors.  
C. Migration logic.  
D. Compiler warnings.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Filtering on this category allows you to see only the SQL output, reducing noise.
</details>

### Q5. Why should you filter `LogLevel`?
A. To reduce performance overhead and noise (ignoring verbose debug info).  
B. You cannot filter.  
C. Everything must be logged.  
D. To delete logs.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
EF Core can be very chatty. Typically `Information` or `Warning` is used in Prod, `Debug` in Dev.
</details>

---

## MEDIUM MCQs

### Q6. `EnableDetailedErrors()` helps by:
A. Adding more specific context (like stack traces or entity values) to Exceptions.  
B. Solving the error automatically.  
C. Logging to a file.  
D. Ignoring errors.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
E.g., adds details about which entity caused the validation failure during SaveChanges. Adds slight overhead.
</details>

### Q7. How to log to a file specifically from EF (without global logger)?
A. `.LogTo(message => File.AppendAllText("log.txt", message))`  
B. Not possible.  
C. Use SQL Profiler.  
D. Use `Trace.Write`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Since `LogTo` accepts any `Action<string>`, you can route it to a custom file writer easily.
</details>

### Q8. The `Query` category logs:
A. LINQ translation events (compiling the query plan).  
B. The results.  
C. The connection string.  
D. User input.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Useful to see if a query is successfully using the cache or being recompiled effectively.
</details>

### Q9. Configuring logging in `appsettings.json` works if:
A. You use `AddDbContext` (DI) which respects the standard `Logging` configuration section.  
B. Only if you use `LogTo`.  
C. Only in WebForms.  
D. Automatically always.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Standard ASP.NET Core pattern. You can set `"Microsoft.EntityFrameworkCore": "Warning"` in the JSON config.
</details>

### Q10. `CommandTimeout` log indicates:
A. The query took too long and was aborted.  
B. The command was successful.  
C. The network is fast.  
D. A syntax error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Important operational log to monitor for performance degradation.
</details>

---

## HARD MCQs

### Q11. Using `TagWith("MyQueryName")` in LINQ:
A. Adds a SQL Comment (`-- MyQueryName`) to the generated SQL, making it easily identifiable in logs/profiler.  
B. Tags the result object.  
C. Does nothing.  
D. Is invalid.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Extremely useful for correlating a specific LINQ block in codebase with the SQL seen in production logs.
</details>

### Q12. "Client vs Server Evaluation" warnings (in older EF Core) or Runtime Errors (EF Core 3+):
A. Occur when LINQ cannot translate a C# method to SQL.  
B. Are ignored.  
C. Are features.  
D. Are database errors.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
EF logs allow you to catch implicit client-eval (pulling all data then filtering in memory), which is a huge performance killer.
</details>

### Q13. Can you use `ILoggerFactory` explicitly in `OnConfiguring`?
A. Yes, `options.UseLoggerFactory(...)`.  
B. No.  
C. Only for Azure.  
D. Only for SQLite.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
This binds a specific logger implementation to the Context, bypassing the ServiceProvider if needed (e.g. Console App without Host).
</details>

### Q14. What is `DbContextLoggerOptions.SingleLine`?
A. Formats the log message as a single line (instead of multi-line pretty print).  
B. Logs only one error.  
C. Logs only one query.  
D. Disables logging.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Useful for dense log files or Splunk/ELK ingestion where multi-line messages break parsing.
</details>

### Q15. Is Logging enabled by default in Release builds?
A. Yes, usually at `Information` level unless overridden in config.  
B. No, it is removed by compiler.  
C. Only Errors.  
D. Only Critical.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It depends on your `appsettings.Production.json`. Typically explicit SQL logging is turned off (Warning/Error only) to save disk/IO, but the capability remains.
</details>
