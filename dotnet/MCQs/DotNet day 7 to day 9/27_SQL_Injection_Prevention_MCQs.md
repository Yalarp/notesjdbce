# 27_SQL_Injection_Prevention – MCQs

## EASY MCQs

### Q1. What is the root cause of SQL Injection?
A. Weak passwords.  
B. Concatenating untrusted user input directly into dynamic SQL strings.  
C. Using SQL Server.  
D. Using Open Source software.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
When user input acts as code (changing the query structure) rather than data, injection occurs.
</details>

### Q2. What is the most effective defense against SQL Injection?
A. Using `string.Replace("'", "")`.  
B. Using Stored Procedures or Parameterized Queries.  
C. Using Firewall.  
D. Encrypting the database.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Parameterization separates code from data at the database engine level.
</details>

### Q3. In the attack payload `" ' OR '1'='1 "`, what is the goal?
A. To crash the server.  
B. To create a tautology (always true condition), often bypassing authentication or listing all records.  
C. To format the disk.  
D. To encrypt data.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`WHERE Id = 'input'` becomes `WHERE Id = '' OR '1'='1'`. Since 1=1 is always true, the query returns everything.
</details>

### Q4. Is `AddWithValue` safe against SQL Injection?
A. No.  
B. Yes, absolutely.  
C. Only for integers.  
D. Only for dates.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Yes, it creates a parameter. The value is sent as data, same as explicitly creating a `SqlParameter`. (Though it has other minor performance/type downsides, it IS secure).
</details>

### Q5. A successful SQL Injection attack can result in:
A. Data theft.  
B. Data deletion.  
C. Bypassing login.  
D. All of the above.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
Depending on the permissions of the database user, an attacker can do anything that user can do.
</details>

---

## MEDIUM MCQs

### Q6. How does a Parameterized Query treat input containing a single quote `'`?
A. It terminates the string.  
B. It treats it as a literal character part of the data value.  
C. It throws an error.  
D. It deletes the quote.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The engine knows "This parameter is a string value". If the value is `It's`, the engine stores `It's`. It doesn't confuse the quote with the query delimiter.
</details>

### Q7. Why is `EXEC` or `sp_executesql` inside a stored procedure potentially dangerous?
A. It isn't.  
B. If you concatenate parameters inside the dynamic SQL string *within* the SP, you are still vulnerable to injection.  
C. Stored procedures are slow.  
D. It deletes the procedure.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Simply "Using a Stored Procedure" is not magic. If the SP logic concatenates strings (`SET @sql = 'SELECT * FROM ' + @table`), it is vulnerable.
</details>

### Q8. Identify the SAFE code:
A. `cmd.CommandText = "SELECT * FROM User WHERE Name = '" + name + "'";`  
B. `cmd.CommandText = $"SELECT * FROM User WHERE Name = '{name}'";`  
C. `cmd.CommandText = "SELECT * FROM User WHERE Name = @n"; cmd.Parameters.AddWithValue("@n", name);`  
D. `cmd.CommandText = string.Format("SELECT * FROM User WHERE Name = '{0}'", name);`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Only Option C uses parameters. All others use string concatenation/formatting, which is vulnerable.
</details>

### Q9. Least Privilege Principle in database security means:
A. Use the `sa` or `admin` account for the web application connection.  
B. The application's database user should only have permissions strictly necessary (e.g., SELECT, INSERT, EXECUTE) and nothing more.  
C. No password.  
D. Give access to everyone.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If injection happens, limiting the user's rights limits the potential damage (e.g., preventing DROP TABLE).
</details>

### Q10. Does Entity Framework Core protect against SQL Injection?
A. No.  
B. Yes, because it uses parameterized queries by default for LINQ queries.  
C. Only if you configure it.  
D. Only for SQL Server.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`context.Users.Where(u => u.Name == name)` generates parameterized SQL automatically. (Note: `FromSqlRaw` can still be vulnerable if used improperly).
</details>

---

## HARD MCQs

### Q11. Can SQL Injection occur in an `ORDER BY` clause?
A. No, never.  
B. Yes, because parameters cannot typically be used for identifiers (table/column names).  
C. Yes, but parameters fix it easily.  
D. No, SQL Server blocks it.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You cannot say `SELECT * FROM T ORDER BY @col`. You must validate the input against a whitelist (e.g., only allow "Price" or "Name") before concatenating it, or use a CASE statement.
</details>

### Q12. Client-side validation (JavaScript) is:
A. Sufficient for security.  
B. Useless for security (can be bypassed), but good for UX.  
C. Better than server-side.  
D. Mandatory.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Attackers use tools (Postman, curl) to send raw requests, bypassing browser-based JavaScript checks completely.
</details>

### Q13. Blind SQL Injection is:
A. Attacking without a monitor.  
B. An attack where the application doesn't return data errors, so the attacker infers data by asking true/false questions (e.g., causing time delays).  
C. Very fast.  
D. Only for MySQL.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Even if you hide errors, attackers can check "Does page load in 5 seconds?" (WAITFOR DELAY) to confirm "Is the first letter of password 'A'?".
</details>

### Q14. `SqlParameter` property `SqlDbType` vs `AddWithValue` type inference collision.
A. `AddWithValue` might assume string when you needed a specific varchar length or an Xml type, causing performance ( implicit conversion) or logic issues.  
B. They are identical.  
C. `AddWithValue` is faster.  
D. `SqlDbType` is deprecated.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Explicitly defining the type avoids cached plan mismatches (e.g., sending NVARCHAR causing index scan on VARCHAR column).
</details>

### Q15. Sanitization (removing dangerous characters) vs Parameterization.
A. Sanitization is better.  
B. Parameterization is the primary defense; Sanitization is a secondary (and harder to get right) defense.  
C. They are the same.  
D. Replace `'` with `''` is perfect security.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is notoriously difficult to blacklist ALL dangerous characters. Parameterization solves the problem structurally.
</details>
