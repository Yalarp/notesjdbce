# 08-15: Advanced JDBC Topics - Comprehensive Reference

This consolidated reference covers the remaining advanced JDBC topics from Day 1 Jakarta EE materials.

---

# 08 - Scrollable and Updatable ResultSet

## Default ResultSet Limitations

> **By default ResultSet is readonly and forward only**

**Default behavior**:
- ✅ Can only move forward (`next()`)
- ❌ Cannot move backward (`previous()`)
- ❌ Cannot jump to specific row (`absolute()`)
- ❌ Cannot modify records
-  ❌ Read-only access

---

## Scrollable and Updatable ResultSet

### Creating Advanced ResultSet

```java
Statement st = con.createStatement(
    ResultSet.TYPE_SCROLL_INSENSITIVE,  // Scrollable
    ResultSet.CONCUR_UPDATABLE          // Updatable
);
```

### ResultSet Types

| Type | Description |
|------|-------------|
| `TYPE_FORWARD_ONLY` | Default - forward only |
| `TYPE_SCROLL_INSENSITIVE` | Scrollable, doesn't reflect DB changes |
| `TYPE_SCROLL_SENSITIVE` | Scrollable, reflects DB changes |

### ResultSet Concurrency

| Concurrency | Description |
|-------------|-------------|
| `CONCUR_READ_ONLY` | Default - cannot update |
| `CONCUR_UPDATABLE` | Can update records |

---

## App7: Scrollable and Updatable Example

```java
import java.sql.*;

public class App7 {
    public static void main(String args[]) {
        String ss = "jdbc:mysql://localhost:3306/mydb";
        try(Connection con = DriverManager.getConnection(ss, "root", "root")) {
            
            Statement st = con.createStatement(
                ResultSet.TYPE_SCROLL_INSENSITIVE,
                ResultSet.CONCUR_UPDATABLE
            );
            
            ResultSet rs = st.executeQuery("select deptno,dname,loc from dept");
            
            // Jump to 5th row
            rs.absolute(5);
            rs.updateString("loc", "USA");
            rs.updateRow();  // Commit update
            
            // Move to previous row
            rs.previous();
            rs.updateString("dname", "edp");
            rs.updateRow();
            
            // Jump to 4th row
            rs.absolute(4);
            rs.updateString("loc", "england");
            rs.updateRow();
            
        }
        catch(Exception ee) {
            System.out.println(ee);
        }
    }
}
```

### Navigation Methods

| Method | Description |
|--------|-------------|
| `next()` | Move to next row |
| `previous()` | Move to previous row |
| `first()` | Move to first row |
| `last()` | Move to last row |
| `absolute(int row)` | Move to specific row (1-based) |
| `relative(int rows)` | Move relative to current position |

### Update Methods

```java
rs.updateString(String columnLabel, String value)
rs.updateInt(String columnLabel, int value)
rs.updateDouble(String columnLabel, double value)
rs.updateRow()  // Commits pending updates to database
rs.cancelRowUpdates()  // Cancels pending updates
```

---

# 09 - Transaction Management in JDBC

## Auto-Commit Concept

> **By default auto commit is 'ON'**

**Default behavior**: Every SQL statement is immediately committed.

---

## App8: Transaction with Commit/Rollback

```java
import java.sql.*;

public class App8 {
    public static void main(String args[]) throws Exception {
        String ss = "jdbc:mysql://localhost:3306/mydb";
        try(Connection con = DriverManager.getConnection(ss, "root", "root")) {
            try {
                // Disable auto-commit
                con.setAutoCommit(false);
                
                Statement st = con.createStatement();
                int a = st.executeUpdate("update dept set loc='bombay'");
                int b = st.executeUpdate("insert into dept values(10,'abc','aaa')");
                
                // Both succeeded - commit
                con.commit();
                
            } catch(Exception ee) {
                // Error - rollback all changes
                con.rollback();     
                System.out.println(ee);
            }
            
            // Re-enable auto-commit
            con.setAutoCommit(true);
        }
        catch(Exception e) {
            System.out.println(e);
        }
    }
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

# 10 - SQL Injection Attack and Prevention

## What is SQL Injection?

> **SQL Injection means passing special symbols (`--`) to SQL query to change its behavior**

### Vulnerable Code (SQL Injection App1)

``` java
Scanner sc = new Scanner(System.in);
String uname = sc.next();
String password = sc.next();

Statement st = con.createStatement();
ResultSet rs = st.executeQuery(
    "select count(*) from myaccount where uname='" + uname + 
    "' and password='" + password + "'"
);
```

**Attack**: User enters `admin'--` as username
**Resulting SQL**: 
```sql
select count(*) from myaccount where uname='admin'--' and password='...'
```
**Effect**: `--` comments out password check!

### Attack Examples

**App2**: Direct injection in code
```java
ResultSet rs = st.executeQuery(
    "select count(*) from myaccount where uname='" + uname + "'-- and password='" + password + "'"
);
// Password check bypassed!
```

**App3**: OR condition attack
```sql
select count(*) from myaccount where uname='anything' or 10=10 -- and password='...'
-- Always returns records because 10=10 is always true
```

---

## Prevention with PreparedStatement

### SQL Injection App4: Safe Code

```java
PreparedStatement pst = con.prepareStatement(
    "select count(*) from myaccount where uname=? and password=?"
);
pst.setString(1, uname);
pst.setString(2, password);
ResultSet rs = pst.executeQuery();
```

**Why safe?**
- Values treated as **data**, not SQL code
- Special characters automatically escaped
- Cannot alter query structure

### SQL Injection App5: Even with `--`

```java
PreparedStatement pst = con.prepareStatement(
    "select count(*) from myaccount where uname=? -- and password=?"
);
pst.setString(1, uname);
pst.setString(2, password);  // ERROR: 2 setXXX but only 1 placeholder!
```

**Protection**: PreparedStatement requires values for ALL placeholders!

---

# 11 - Execute Method Variations

## execute() Method

**Returns**: `boolean`
- `true` - Result is ResultSet (SELECT query)
- `false` - Result is update count or no result

### When to Use

- Dynamic SQL where type is unknown at compile time
- Stored procedures that may return multiple results
- DDL statements (CREATE, DROP, ALTER)

### Example: execute() for SELECT

```java
boolean b = st.execute("select * from dept");
if(b) {
    ResultSet rs = st.getResultSet();
    while(rs.next()) {
        // Process results
    }
}
```

### Example: execute() for UPDATE

```java
boolean c = pst.execute();  // UPDATE statement

if(!c) {  // false means update count
    int mod = pst.getUpdateCount();
    if(mod > 0) {
        System.out.println("Records updated");
    }
}
```

### Summary

| Method | Returns | Use For |
|--------|---------|---------|
| `executeQuery()` | ResultSet | SELECT only |
| `executeUpdate()` | int (rows affected) | INSERT/UPDATE/DELETE |
| `execute()` | boolean | Any SQL, unknown type |

---

# 12 - CachedRowSet (Disconnected Data)

## Disconnected Environment

> **Connection required only at retrieval, then connection closes**

**Benefits**:
- No permanent connection needed
- Scalable for thousands of records
- CachedRowSet is **serializable** (can send over network)
- ResultSet is **NOT serializable**

---

## CachedRowSet Example

```java
import javax.sql.rowset.CachedRowSet;
import javax.sql.rowset.RowSetProvider;

public class App1 {
    public static void main(String args[]) {
        try(CachedRowSet crs = RowSetProvider.newFactory().createCachedRowSet()) {
            
            crs.setUsername("root");
            crs.setPassword("root");
            crs.setUrl("jdbc:mysql://localhost:3306/mydb");
            crs.setCommand("select * from dept");
            crs.execute();  // Connects, fetches data, disconnects
            
            System.out.println("Even after connection closed with ARM");
            
            while(crs.next()) {  // Data available offline!
                int a = crs.getInt(1);
                String b = crs.getString(2);
                String c = crs.getString(3);
                System.out.println(a + "\t" + b + "\t" + c);
            }
            
        } catch(Exception ee) {
            ee.printStackTrace();
        }
    }
}
```

**Key Point**: After `execute()`, connection is closed but data remains accessible!

---

# 13 - Properties-Based Configuration

## Why Use Properties Files?

- ✅ Externalize configuration
- ✅ Easy to modify without recompiling
- ✅ Sensitive data separation
- ✅ Environment-specific settings

---

## myproperty.properties

```properties
url=jdbc:mysql://localhost:3306/mydb
user=root
password=root
```

---

## ConnectionProvider.java

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.util.ResourceBundle;

public class ConnectionProvider {
    static Connection con;
    
    public static Connection getCon() {
        try {
            String url, user, password;
            
            ResourceBundle rb = ResourceBundle.getBundle("myproperty");
            url = rb.getString("url");
            user = rb.getString("user");
            password = rb.getString("password");
            
            con = DriverManager.getConnection(url, user, password);
            
        } catch(Exception ee) {
            System.out.println(ee);
        }
        return con;
    }
}
```

---

## MyClass.java (Usage)

```java
import java.sql.*;

public class MyClass {
    public static void main(String[] args) {
        try(Connection con = ConnectionProvider.getCon()) {
            
            Statement st = con.createStatement();
            ResultSet rs = st.executeQuery("select * from dept");
            
            while(rs.next()) {
                System.out.println(rs.getInt(1));
                System.out.println(rs.getString(2));
                System.out.println(rs.getString(3));
            }
            
        } catch(Exception ee) {
            System.out.println(ee);
        }
    }
}
```

---

# 14 - JDBC Assignments and Practice

## Assignment 1: Student Table

**Table**:
```sql
CREATE TABLE Student (
    rollno INT PRIMARY KEY,
    name VARCHAR(50),
    age INT
);
```

**Task**: Accept rollno, name, age from user and insert. Then view all records.

---

## Assignment 2: Employee Designation Query

**Table**:
```sql
CREATE TABLE Employee (
    empid INT PRIMARY KEY,
    empname VARCHAR(50),
    desig VARCHAR(30)
);

INSERT INTO Employee VALUES
(1, 'John', 'Manager'),
(2, 'Jane', 'Developer'),
(3, 'Bob', 'Developer'),
(4, 'Alice', 'Tester'),
(5, 'Charlie', 'Manager');
```

**Task**: Accept designation from user, retrieve all employees with that designation.

---

## Assignment 3: Object Persistence

**Table**:
```sql
CREATE TABLE Product (
    pid INT PRIMARY KEY,
    qty INT,
    cost DECIMAL(10,2),
    pname VARCHAR(50)
);
```

**Java Class**:
```java
class Product {
    private int pid, qty;
    private double cost;
    private String pname;
    
    // Constructor, getters, setters, toString()
}
```

**Tasks**:
1. Create Product instance
2. Display it
3. Insert into database
4. Set instance = null (eligible for GC)
5. Retrieve from database
6. Create new Product from retrieved data
7. Display it

---

# 15 - JDBC Quick Reference Guide

## Core Interfaces

### Connection
```java
Connection con = DriverManager.getConnection(url, user, pass);
Statement st = con.createStatement();
PreparedStatement pst = con.prepareStatement(sql);
CallableStatement cst = con.prepareCall("{call proc(?,?)}");
con.setAutoCommit(false);
con.commit();
con.rollback();
con.close();
```

### Statement
```java
ResultSet rs = st.executeQuery("SELECT...");
int rows = st.executeUpdate("UPDATE...");
boolean result = st.execute("...");
```

### PreparedStatement
```java
PreparedStatement pst = con.prepareStatement("SELECT * FROM dept WHERE id=?");
pst.setInt(1, 10);
ResultSet rs = pst.executeQuery();
```

### CallableStatement
```java
CallableStatement cst = con.prepareCall("{call proc(?,?)}");
cst.setInt(1, 100);
cst.registerOutParameter(2, Types.VARCHAR);
cst.execute();
String result = cst.getString(2);
```

### ResultSet
```java
while(rs.next()) {
    int id = rs.getInt("id");
    String name = rs.getString("name");
}
```

---

## Common Patterns

### Basic Query
```java
try(Connection con = DriverManager.getConnection(url, user, pass);
    Statement st = con.createStatement();
    ResultSet rs = st.executeQuery("SELECT * FROM table")) {
    
    while(rs.next()) {
        // Process
    }
}
```

### Parameterized Query
```java
String sql = "INSERT INTO table VALUES(?,?,?)";
try(Connection con = DriverManager.getConnection(url, user, pass);
    PreparedStatement pst = con.prepareStatement(sql)) {
    
    pst.setInt(1, 100);
    pst.setString(2, "Name");
    pst.setDouble(3, 50.0);
    int rows = pst.executeUpdate();
}
```

### Transaction
```java
try(Connection con = DriverManager.getConnection(url, user, pass)) {
    con.setAutoCommit(false);
    try {
        // Multiple operations
        con.commit();
    } catch(Exception e) {
        con.rollback();
    }
}
```

---

## Best Practices

1. ✅ **Always use try-with-resources**
2. ✅ **Use PreparedStatement for user input**
3. ✅ **Never concatenate user input into SQL**
4. ✅ **Close resources in reverse order**
5. ✅ **Handle SQLException properly**
6. ✅ **Use connection pooling in production**
7. ✅ **Externalize configuration**
8. ✅ **Use transactions for multiple related operations**

---

## MySQL Connection String

```
jdbc:mysql://localhost:3306/database?params
```

**Common parameters**:
- `useSSL=false`
- `serverTimezone=UTC`
- `autoReconnect=true`

---

## SQL Type Mapping

| SQL Type | Java Type | PreparedStatement | ResultSet |
|----------|-----------|-------------------|-----------|
| INT | int | setInt() | getInt() |
| VARCHAR | String | setString() | getString() |
| DOUBLE | double | setDouble() | getDouble() |
| DATE | java.sql.Date | setDate() | getDate() |
| BOOLEAN | boolean | setBoolean() | getBoolean() |
| BLOB | byte[] | setBytes() | getBytes() |

---

## Interview Questions

### 1. Statement vs PreparedStatement?
**Answer**: PreparedStatement is precompiled, faster for repeated execution, protects against SQL injection, supports parameters.

### 2. What is ResultSetMetaData?
**Answer**: Provides metadata about ResultSet structure (column count, names, types) for dynamic query processing.

### 3. How to prevent SQL injection?
**Answer**: Use PreparedStatement with parameterized queries. Never concatenate user input into SQL strings.

### 4. What is auto-commit?
**Answer**: Default JDBC behavior where each SQL statement is automatically committed. Can be disabled for transactions with setAutoCommit(false).

### 5. Difference between execute(), executeQuery(), and executeUpdate()?
**Answer**: 
- executeQuery() - SELECT, returns ResultSet
- executeUpdate() - INSERT/UPDATE/DELETE, returns int
- execute() - Any SQL, returns boolean

---

**Congratulations!** You've completed all Jakarta EE Day 1 JDBC topics! 🎉

These notes cover everything from basic connections to advanced topics like transactions, stored procedures, and security. Practice the assignments to reinforce your learning!
