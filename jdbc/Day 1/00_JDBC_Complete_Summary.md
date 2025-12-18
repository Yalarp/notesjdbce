# Jakarta EE Day 1 - Complete JDBC Summary

**Quick Reference Guide for All Topics**

---

## 📑 Table of Contents

1. [Database Connectivity Overview](#1-database-connectivity-overview)
2. [JDBC Fundamentals](#2-jdbc-fundamentals)
3. [Connection Basics](#3-connection-basics)
4. [Statement Interface](#4-statement-interface)
5. [ResultSetMetaData](#5-resultsetmetadata)
6. [PreparedStatement](#6-preparedstatement)
7. [CallableStatement](#7-callablestatement)
8. [Scrollable & Updatable ResultSet](#8-scrollable--updatable-resultset)
9. [Transaction Management](#9-transaction-management)
10. [SQL Injection](#10-sql-injection)
11. [Execute Methods](#11-execute-methods)
12. [CachedRowSet](#12-cachedrowset)
13. [Properties Configuration](#13-properties-configuration)
14. [Quick Code Patterns](#14-quick-code-patterns)
15. [Best Practices](#15-best-practices)

---

## 1. Database Connectivity Overview

### JDBC vs ORM

| Aspect | JDBC | ORM (Hibernate) |
|--------|------|-----------------|
| **Approach** | SQL-based | Object-based |
| **Code Volume** | More verbose | Less code |
| **Control** | Full SQL control | Framework handles SQL |
| **Performance** | Optimized for simple queries | Overhead for simple ops |
| **Use Case** | Complex SQL, high performance | Rapid development, CRUD |

**Key Point**: JDBC for direct SQL control, ORM for object-oriented development.

---

## 2. JDBC Fundamentals

### What is JDBC?
**Java Database Connectivity** - API to connect Java applications to databases.

### JDBC Components
1. **JDBC API** - Interfaces (Connection, Statement, ResultSet)
2. **JDBC Drivers** - Database-specific implementations

### 4 Driver Types

| Type | Name | Status |
|------|------|--------|
| Type 1 | JDBC-ODBC Bridge | ❌ Obsolete |
| Type 2 | Native-API | ⚠️ Platform dependent |
| Type 3 | Network Protocol | ⚠️ Needs middleware |
| Type 4 | Pure Java | ✅ **Recommended** |

**Type 4**: 100% Java, platform-independent, direct database connection.

**MySQL Type 4 Driver**: `com.mysql.cj.jdbc.Driver`

### Key Interfaces

```java
Connection      // Database connection
DriverManager   // Get connections (class, not interface)
Statement       // Execute static SQL
PreparedStatement // Parameterized SQL
CallableStatement // Stored procedures
ResultSet       // Query results
```

### Why Interfaces?
**Loose coupling** - same code works with any database!

---

## 3. Connection Basics

### Database URL Structure

```
jdbc:mysql://localhost:3306/mydb
│    │       │         │    │
│    │       │         │    └─ Database name
│    │       │         └────── Port (3306 for MySQL)
│    │       └──────────────── Host
│    └──────────────────────── Sub-protocol
└───────────────────────────── Main protocol
```

### Connection Steps

```java
// 1. Define URL
String url = "jdbc:mysql://localhost:3306/mydb";

// 2. Get Connection (auto-loads driver in JDBC 4.0+)
Connection con = DriverManager.getConnection(url, "root", "root");

// 3. Create Statement
Statement st = con.createStatement();

// 4. Execute Query
ResultSet rs = st.executeQuery("SELECT * FROM dept");

// 5. Process Results
while(rs.next()) {
    int id = rs.getInt("deptno");
    String name = rs.getString("dname");
}

// 6. Close (automatic with try-with-resources)
```

### Try-With-Resources (ARM)

```java
try(Connection con = DriverManager.getConnection(url, user, pass)) {
    // Use connection
} // Auto-closes!
```

---

## 4. Statement Interface

### Three Execution Methods

| Method | Returns | Use For | Example |
|--------|---------|---------|---------|
| `executeQuery()` | ResultSet | SELECT | `st.executeQuery("SELECT...")` |
| `executeUpdate()` | int (rows) | INSERT/UPDATE/DELETE | `st.executeUpdate("UPDATE...")` |
| `execute()` | boolean | Any SQL | `st.execute("...")` |

### Example: SELECT

```java
Statement st = con.createStatement();
ResultSet rs = st.executeQuery("SELECT * FROM dept");

while(rs.next()) {
    int no = rs.getInt("deptno");
    String name = rs.getString("dname");
    String loc = rs.getString("loc");
}
```

### Example: UPDATE

```java
Statement st = con.createStatement();
int rows = st.executeUpdate("UPDATE dept SET loc='Mumbai'");
if(rows > 0) {
    System.out.println(rows + " rows updated");
}
```

### ResultSet Navigation

- **Initial position**: BEFORE first record
- **`rs.next()`**: Move to next row, returns true/false
- **Access by name**: `rs.getInt("deptno")`
- **Access by index**: `rs.getInt(1)` (1-based!)

---

## 5. ResultSetMetaData

### Purpose
Get information about ResultSet structure when you don't know table schema.

### Key Methods

```java
ResultSet rs = st.executeQuery("SELECT * FROM dept");
ResultSetMetaData meta = rs.getMetaData();

int colCount = meta.getColumnCount();           // Number of columns
String colName = meta.getColumnName(1);         // Column name (1-based)
int colType = meta.getColumnType(1);            // SQL type
String typeName = meta.getColumnTypeName(1);    // Type name
```

### Dynamic Query Example

```java
// Works with ANY table!
ResultSetMetaData meta = rs.getMetaData();
int cols = meta.getColumnCount();

// Print headers
for(int i = 1; i <= cols; i++) {
    System.out.print(meta.getColumnName(i) + "\t");
}

// Print data
while(rs.next()) {
    for(int i = 1; i <= cols; i++) {
        System.out.print(rs.getObject(i) + "\t");
    }
    System.out.println();
}
```

### rs.getObject()
- Returns: `Object` (works with any type)
- Use when: Type is unknown
- Alternative: Type-specific methods (`getInt()`, `getString()`)

---

## 6. PreparedStatement

### Two Main Advantages

1. **Placeholders** - Dynamic parameter values
2. **Performance** - Precompiled SQL, execution plan cached

### Performance Comparison

**Statement** (slow):
```
Execute 1: Parse → Compile → Plan → Execute
Execute 2: Parse → Compile → Plan → Execute
Execute 3: Parse → Compile → Plan → Execute
```

**PreparedStatement** (fast):
```
Prepare:   Parse → Compile → Plan (cached)
Execute 1: Execute only
Execute 2: Execute only
Execute 3: Execute only
```

### Syntax

```java
// Statement - SQL at execution
Statement st = con.createStatement();
ResultSet rs = st.executeQuery("SELECT * FROM dept WHERE id=10");

// PreparedStatement - SQL at preparation
PreparedStatement pst = con.prepareStatement("SELECT * FROM dept WHERE id=?");
pst.setInt(1, 10);
ResultSet rs = pst.executeQuery(); // No SQL parameter!
```

### Parameter Setting

```java
PreparedStatement pst = con.prepareStatement(
    "INSERT INTO dept VALUES(?, ?, ?)"
);

pst.setInt(1, 10);          // 1st placeholder
pst.setString(2, "Sales");   // 2nd placeholder
pst.setString(3, "Mumbai");  // 3rd placeholder

int rows = pst.executeUpdate();
```

**Important**: Parameter indices are **1-based** (not 0-based)!

### When to Use

✅ **Always use PreparedStatement for**:
- User input (SQL injection protection)
- Repeated queries
- INSERT/UPDATE/DELETE

✅ **Statement OK for**:
- One-time static queries
- DDL (CREATE, DROP, ALTER)

---

## 7. CallableStatement

### Purpose
Execute **stored procedures** and **functions** in database.

### Creating MySQL Procedure

```sql
DELIMITER //
CREATE PROCEDURE mypro1(
    IN dno INT,            -- Input
    OUT dname VARCHAR(20)  -- Output
)
BEGIN
    SELECT d.dname INTO dname 
    FROM dept d 
    WHERE d.deptno = dno;
END //
DELIMITER ;
```

### Calling from Java

```java
// Prepare call
CallableStatement cst = con.prepareCall("{ call mypro1(?, ?) }");

// Set IN parameter
cst.setInt(1, 3);

// Execute
cst.execute();

// Get OUT parameter
String name = cst.getString(2);
System.out.println("Department: " + name);
```

### Parameter Types

| Type | Direction | Java Code |
|------|-----------|-----------|
| **IN** | Java → DB | `cst.setInt(1, 100)` |
| **OUT** | DB → Java | `cst.registerOutParameter(2, Types.VARCHAR)`<br>`String val = cst.getString(2)` |
| **INOUT** | Both | Set + Register + Get |

### OUT Parameter Example

```java
CallableStatement cst = con.prepareCall("{ call proc(?, ?) }");
cst.setInt(1, 10);                          // IN parameter
cst.registerOutParameter(2, Types.VARCHAR); // Register OUT
cst.execute();
String result = cst.getString(2);           // Get OUT value
```

---

## 8. Scrollable & Updatable ResultSet

### Default ResultSet
- ❌ Forward-only (`next()` only)
- ❌ Read-only (cannot update)

### Advanced ResultSet

```java
Statement st = con.createStatement(
    ResultSet.TYPE_SCROLL_INSENSITIVE,  // Scrollable
    ResultSet.CONCUR_UPDATABLE          // Updatable
);
```

### Navigation Methods

```java
rs.next()           // Next row
rs.previous()       // Previous row
rs.first()          // First row
rs.last()           // Last row
rs.absolute(5)      // 5th row
rs.relative(-2)     // 2 rows back
```

### Update Methods

```java
ResultSet rs = st.executeQuery("SELECT deptno, dname, loc FROM dept");

rs.absolute(5);                    // Jump to 5th row
rs.updateString("loc", "USA");     // Modify column
rs.updateRow();                    // Commit to database

rs.previous();                     // Move to 4th row
rs.updateString("dname", "Sales");
rs.updateRow();
```

---

## 9. Transaction Management

### Auto-Commit (Default)

> **By default, auto-commit is ON** - each SQL is immediately committed.

### Manual Transaction

```java
Connection con = DriverManager.getConnection(url, user, pass);

try {
    // Disable auto-commit
    con.setAutoCommit(false);
    
    // Multiple operations
    Statement st = con.createStatement();
    st.executeUpdate("UPDATE dept SET loc='Mumbai'");
    st.executeUpdate("INSERT INTO dept VALUES(10,'Sales','Delhi')");
    
    // All succeeded - commit
    con.commit();
    
} catch(SQLException e) {
    // Error - rollback everything
    con.rollback();
    
} finally {
    // Re-enable auto-commit
    con.setAutoCommit(true);
}
```

### Transaction Methods

```java
con.setAutoCommit(false);  // Start transaction
con.commit();              // Save all changes
con.rollback();            // Undo all changes
con.setAutoCommit(true);   // Resume auto-commit
```

---

## 10. SQL Injection

### What is SQL Injection?

Passing special characters (`--`, `'`, `OR`) to alter SQL query behavior.

### Vulnerable Code

```java
// ❌ DANGER - SQL Injection possible!
String username = getUserInput();  // User enters: admin'--
String password = getUserInput();

Statement st = con.createStatement();
String sql = "SELECT * FROM users WHERE uname='" + username + 
             "' AND password='" + password + "'";
ResultSet rs = st.executeQuery(sql);
```

**Attack**: User enters `admin'--`
**Resulting SQL**: 
```sql
SELECT * FROM users WHERE uname='admin'--' AND password='...'
                                      ↑
                                   Comments out password check!
```

### Attack Variations

**Attack 1**: Comment bypass
```sql
WHERE uname='admin'-- AND password='...'
-- Everything after -- is commented out
```

**Attack 2**: OR condition
```sql
WHERE uname='anything' OR 1=1 -- AND password='...'
-- 1=1 is always true, returns all records
```

### Prevention: PreparedStatement

```java
// ✅ SAFE - SQL Injection prevented!
PreparedStatement pst = con.prepareStatement(
    "SELECT * FROM users WHERE uname=? AND password=?"
);
pst.setString(1, username);  // Values treated as DATA, not code
pst.setString(2, password);
ResultSet rs = pst.executeQuery();
```

**Why safe?**
- Special characters automatically escaped
- Values treated as data, not SQL code
- Cannot alter query structure

---

## 11. Execute Methods

### execute() Method

**Returns**: `boolean`
- `true` = Result is ResultSet (SELECT)
- `false` = Result is update count or no result

### When to Use Each

```java
// executeQuery() - SELECT only
ResultSet rs = st.executeQuery("SELECT * FROM dept");

// executeUpdate() - INSERT/UPDATE/DELETE
int rows = st.executeUpdate("UPDATE dept SET loc='Mumbai'");

// execute() - Any SQL (type unknown)
boolean hasResultSet = st.execute(sqlQuery);
if(hasResultSet) {
    ResultSet rs = st.getResultSet();
} else {
    int count = st.getUpdateCount();
}
```

---

## 12. CachedRowSet

### Disconnected Data Access

**Problem**: Keeping connection open for long time is expensive.

**Solution**: CachedRowSet - fetch data, disconnect, use data offline.

### Benefits

- ✅ No permanent connection needed
- ✅ **Serializable** (can send over network)
- ✅Scrollable and Updatable
- ✅ Efficient for large datasets

### Example

```java
import javax.sql.rowset.CachedRowSet;
import javax.sql.rowset.RowSetProvider;

CachedRowSet crs = RowSetProvider.newFactory().createCachedRowSet();

crs.setUrl("jdbc:mysql://localhost:3306/mydb");
crs.setUsername("root");
crs.setPassword("root");
crs.setCommand("SELECT * FROM dept");

crs.execute();  // Connects, fetches, DISCONNECTS

// Connection is closed, but data is still available!
while(crs.next()) {
    System.out.println(crs.getInt(1) + " " + crs.getString(2));
}
```

**Key**: After `execute()`, connection closes but data remains accessible!

---

## 13. Properties Configuration

### Why Use Properties Files?

- ✅ Externalize configuration
- ✅ Change without recompiling
- ✅ Environment-specific settings
- ✅ Security (keep credentials separate)

### myproperty.properties

```properties
url=jdbc:mysql://localhost:3306/mydb
user=root
password=root
```

### ConnectionProvider.java

```java
import java.sql.*;
import java.util.ResourceBundle;

public class ConnectionProvider {
    public static Connection getCon() {
        try {
            ResourceBundle rb = ResourceBundle.getBundle("myproperty");
            String url = rb.getString("url");
            String user = rb.getString("user");
            String password = rb.getString("password");
            
            return DriverManager.getConnection(url, user, password);
        } catch(Exception e) {
            throw new RuntimeException(e);
        }
    }
}
```

### Usage

```java
try(Connection con = ConnectionProvider.getCon()) {
    Statement st = con.createStatement();
    ResultSet rs = st.executeQuery("SELECT * FROM dept");
    // Process results
}
```

---

## 14. Quick Code Patterns

### Basic SELECT

```java
try(Connection con = DriverManager.getConnection(url, user, pass);
    Statement st = con.createStatement();
    ResultSet rs = st.executeQuery("SELECT * FROM dept")) {
    
    while(rs.next()) {
        System.out.println(rs.getInt("deptno") + " " + rs.getString("dname"));
    }
}
```

### Parameterized INSERT

```java
String sql = "INSERT INTO dept(dname, loc) VALUES(?, ?)";
try(Connection con = DriverManager.getConnection(url, user, pass);
    PreparedStatement pst = con.prepareStatement(sql)) {
    
    pst.setString(1, "Sales");
    pst.setString(2, "Mumbai");
    int rows = pst.executeUpdate();
    System.out.println(rows + " row inserted");
}
```

### Transaction

```java
try(Connection con = DriverManager.getConnection(url, user, pass)) {
    con.setAutoCommit(false);
    try {
        Statement st = con.createStatement();
        st.executeUpdate("UPDATE account SET balance=balance-1000 WHERE id=1");
        st.executeUpdate("UPDATE account SET balance=balance+1000 WHERE id=2");
        con.commit();
    } catch(Exception e) {
        con.rollback();
        throw e;
    }
}
```

### Stored Procedure

```java
try(Connection con = DriverManager.getConnection(url, user, pass);
    CallableStatement cst = con.prepareCall("{ call getDeptName(?, ?) }")) {
    
    cst.setInt(1, 10);
    cst.registerOutParameter(2, Types.VARCHAR);
    cst.execute();
    String name = cst.getString(2);
    System.out.println("Department: " + name);
}
```

---

## 15. Best Practices

### ✅ Essential Practices

1. **Always use try-with-resources** for automatic resource cleanup
2. **Use PreparedStatement** (not Statement) for user input
3. **Never concatenate user input** into SQL strings
4. **Handle SQLException** properly
5. **Use connection pooling** in production (HikariCP, C3P0)
6. **Close resources** in reverse order (ResultSet → Statement → Connection)
7. **Externalize configuration** with properties files
8. **Use transactions** for related operations
9. **Validate input** before database operations
10. **Log errors** for debugging

### ❌ Common Mistakes

1. Not closing resources (memory leaks)
2. Using Statement with user input (SQL injection)
3. Hardcoding credentials in code
4. Ignoring exceptions
5. Creating new connection for each operation (slow)
6. Not using transactions for multiple updates
7. Fetching more data than needed
8. Using SELECT * instead of specific columns

---

## 🎯 Quick Comparison Tables

### Statement Types

| Feature | Statement | PreparedStatement | CallableStatement |
|---------|-----------|-------------------|-------------------|
| **SQL** | At execution | At preparation | At preparation |
| **Parameters** | No | Yes (?) | Yes (?, IN/OUT) |
| **Performance** | Slow | Fast (cached) | Fast (cached) |
| **Security** | Vulnerable | Protected | Protected |
| **Use For** | Static SQL | Parameterized SQL | Stored procedures |

### ResultSet Types

| Type | Scrollable | Updatable | Common Use |
|------|------------|-----------|------------|
| Default | ❌ Forward only | ❌ Read-only | Most queries |
| `TYPE_SCROLL_INSENSITIVE` + `CONCUR_UPDATABLE` | ✅ Yes | ✅ Yes | Interactive editing |

### SQL Type Mapping

| SQL Type | Java Type | set Method | get Method |
|----------|-----------|------------|------------|
| INT | int | setInt() | getInt() |
| VARCHAR | String | setString() | getString() |
| DOUBLE | double | setDouble() | getDouble() |
| DATE | java.sql.Date | setDate() | getDate() |
| BOOLEAN | boolean | setBoolean() | getBoolean() |

---

## 🔑 Key Reminders

- **Column indices**: **1-based** (not 0-based!)
- **ResultSet cursor**: Starts **BEFORE** first record
- **Auto-commit**: **ON** by default
- **PreparedStatement**: execute**Query**() and execute**Update**() have **NO parameters**
- **ResourceBundle**: Looks for `.properties` file in classpath
- **SQL Injection**: **Always** use PreparedStatement for user input

---

## 📚 Interview Quick Answers

**Q: Why PreparedStatement over Statement?**  
A: Performance (precompiled), security (SQL injection prevention), cleaner code (parameters).

**Q: What is auto-commit?**  
A: Default mode where each SQL is immediately committed. Disable with `setAutoCommit(false)` for transactions.

**Q: How to prevent SQL injection?**  
A: Use PreparedStatement with parameterized queries. Never concatenate user input into SQL.

**Q: Difference between execute(), executeQuery(), executeUpdate()?**  
A: `executeQuery()` for SELECT (returns ResultSet), `executeUpdate()` for DML (returns int), `execute()` for any SQL (returns boolean).

**Q: What is ResultSetMetaData?**  
A: Interface providing metadata about ResultSet structure (column count, names, types) for dynamic processing.

---

## 🎓 Study Tips

1. **Start with basics**: Understand connection → statement → resultset flow
2. **Practice typing code**: Don't just read, type every example
3. **Understand diagrams**: Visualize the flow
4. **Complete assignments**: Hands-on practice reinforces learning
5. **Use this summary**: Quick revision before exams/interviews

---

**📖 For detailed explanations, refer to the individual topic files!**

This summary covers all essential JDBC concepts from Day 1 Jakarta EE materials. Master these concepts and you'll have a solid foundation in database programming with Java! 🚀
