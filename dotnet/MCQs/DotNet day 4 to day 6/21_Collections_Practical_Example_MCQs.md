# 21_Collections_Practical_Example – MCQs

## EASY MCQs

### Q1. In the Employee Management System example, `IEmpService` is:
A. A Class  
B. An Interface  
C. A Struct  
D. An Abstract Class  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`IEmpService` defines the contract (signature of methods) that any employee service implementation must fulfill.
</details>

### Q2. Why do we implement an interface (`IEmpService`) instead of using the class directly?
A. To make the code slower.  
B. To allow Dependency Injection and loose coupling.  
C. Interfaces are mandatory in C#.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Using interfaces allows switching implementations (e.g., from InMemoryService to DatabaseService) without changing the client code and facilitates unit testing.
</details>

### Q3. Which method is used to add an employee to the list?
A. `.Insert()`  
B. `.Append()`  
C. `.Add()`  
D. `.Push()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `List<T>.Add(item)` method appends an object to the end of the list.
</details>

### Q4. Defensive copying in `GetAllEmployees` refers to:
A. Checking for nulls.  
B. Returning `new List<Employee>(_employees)` instead of `_employees`.  
C. Encrypting the data.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Returning a copy prevents external callers from adding/removing items directly from the service's internal private storage, protecting data integrity.
</details>

### Q5. What happens if you try to add an employee that is null?
A. It is added to the list.  
B. `ArgumentNullException` is thrown.  
C. The program crashes silently.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `Add` method explicitly checks `if (emp == null)` and throws `ArgumentNullException` to effectively guard against bad data.
</details>

---

## MEDIUM MCQs

### Q6. To find all employees in the "IT" department, which List method is best?
A. `.Find()`  
B. `.FindAll()`  
C. `.Contains()`  
D. `.BinarySearch()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`FindAll` accepts a predicate and returns a *new list* containing all elements that match the condition. `Find` allows retrieving only the first match.
</details>

### Q7. The predicate `e => e.Id == id` is used to:
A. Transform the employee to an ID.  
B. Sort the employees by ID.  
C. Check if an employee's ID matches the search ID.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
This lambda expression returns `true` for the employee whose `Id` property matches the `id` variable, identifying the specific record.
</details>

### Q8. To delete an employee safely, the service first:
A. Calls `_employees.RemoveAt(0)`.  
B. Finds the employee; if found, calls `_employees.Remove()`.  
C. Clears the list.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `Delete` method typically verifies existence first (`Find`) to ensure we are deleting the correct object and to handle the "Not Found" case gracefully (e.g., throwing exception).
</details>

### Q9. `StringComparison.OrdinalIgnoreCase` is used to:
A. Sort strings alphabetically.  
B. Compare strings ignoring case (e.g., "IT" == "it").  
C. Improve memory usage.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It ensures robust string matching regardless of capitalization, which is standard practice for user input or business keys like department names.
</details>

### Q10. `JsonSerializerOptions { WriteIndented = true }` produces:
A. Compact JSON  
B. Human-readable (formatted) JSON  
C. XML output  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This option adds line breaks and indentation to the JSON string, making it easier for developers to read (pretty-printing).
</details>

---

## HARD MCQs

### Q11. If `_employees.Find(e => e.Id == 99)` returns null, what does access `emp.Name` do?
A. Returns "Unknown".  
B. Throws `NullReferenceException`.  
C. Returns empty string.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Accessing members of a null reference is a runtime error. This highlights the importance of null checks after lookup operations.
</details>

### Q12. The `Employee` class provides a parameterless constructor because:
A. It is required for creating instances manually.  
B. Serialization libraries often require it to instantiate the object before setting properties.  
C. It improves performance.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Many serializers (older XmlSerializer, and System.Text.Json in some configs) rely on `new Employee()` (param-less) to create the object before populating properties via setters.
</details>

### Q13. Implementing `Delete(int id)` using `_employees.Remove(new Employee { Id = id })` would fail because:
A. Removing by object reference works only if it's the *same* instance (unless Equals is overridden).  
B. The ID is wrong.  
C. Arguments are invalid.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`List.Remove(item)` uses the default equality comparer. For classes, this is reference equality. A `new Employee` instance has a different memory address than the existing one, so nothing would be removed unless `Equals()` is overridden to check IDs.
</details>

### Q14. In the `Program.cs`, Dependency Injection is simulated by:
A. `IEmpService service = new EmployeeService();`  
B. `new List<Employee>()`  
C. `static void Main`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Assigning the concrete implementation `new EmployeeService()` to the interface variable `IEmpService` is the simplest form of dependency injection (Manual Injection/Composition Root), allowing the rest of the code to rely only on the abstraction.
</details>

### Q15. `_employees.Exists(e => e.Id == emp.Id)` is functionally equivalent to:
A. `_employees.Count > 0`  
B. `_employees.Find(e => e.Id == emp.Id) != null`  
C. `_employees.Contains(emp)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Exists` returns true if any element matches the predicate. This is semantically identical to checking if `Find` returns a non-null result (but `Exists` returns bool directly).
</details>
