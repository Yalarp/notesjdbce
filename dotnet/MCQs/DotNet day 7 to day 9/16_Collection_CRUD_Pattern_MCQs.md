# 16_Collection_CRUD_Pattern – MCQs

## EASY MCQs

### Q1. What does CRUD stand for?
A. Create, Read, Update, Delete  
B. Copy, Run, Undo, Done  
C. Create, Read, Undo, Do  
D. Call, Return, Update, Destroy  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
CRUD is the standard acronym for the four basic operations of persistent storage: Create, Read, Update, and Delete.
</details>

### Q2. In the layered architecture context, what is a "POCO"?
A. Plain Old C# Object  
B. Plain Old CLR Object  
C. Private Object C# Only  
D. Public Object Common Organization  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
POCO stands for Plain Old CLR Object. It typically represents a data model (like `Employee`) with properties and no special base class or behavior logic.
</details>

### Q3. Which `List<T>` method is commonly used to find a single element based on a condition (like Id)?
A. `Select()`  
B. `Find()`  
C. `Search()`  
D. `Get()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`List.Find(predicate)` returns the first element that matches the condition or the default value if none is found.
</details>

### Q4. Why do we define an interface (e.g., `IEmpService`) before implementing the class?
A. It is required by the compiler.  
B. To enable loose coupling and make it easier to swap or mock implementations.  
C. It makes the code faster.  
D. Because classes cannot have methods without interfaces.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Interfaces define a contract. The consumer code relies on the contract (interface) rather than the concrete class, allowing for flexibility and testability.
</details>

### Q5. How is an Auto-Increment ID typically simulated in an in-memory collection?
A. Using a static variable that increments on every constructor call.  
B. Random number generation.  
C. Asking the user.  
D. Using `Guid.NewGuid()`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
A common pattern for simple in-memory demos is a `static int count` field that increments (`++count`) each time a new object is instantiated.
</details>

---

## MEDIUM MCQs

### Q6. Which method returns ALL elements matching a condition?
A. `Find()`  
B. `FindAll()`  
C. `SelectAll()`  
D. `Where().First()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`FindAll` on `List<T>` returns a valid list containing all items matching the predicate. `Where` works too but returns an `IEnumerable`.
</details>

### Q7. In the Service pattern shown, where is the data actually stored?
A. In a database.  
B. In a text file.  
C. In a `static` In-Memory List within the service class.  
D. In the `Program` class.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The example uses a `private static List<Employee> _employeeList` inside the service to simulate persistent storage across service instances (if the service is transient).
</details>

### Q8. When implementing `Delete(int id)`, what is the standard first step?
A. Call `RemoveAt(id)`.  
B. Find the object by Id to ensure it exists.  
C. Clear the list.  
D. Create a new object.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You must first locate the specific object reference (using `Find`) before you can call `Remove(obj)` safely or report that it wasn't found.
</details>

### Q9. Why might the `Add` method return the `Employee` object back?
A. It's a mistake.  
B. To confirm the operation and potentially provide the generated ID or defaulted fields.  
C. It is required by C# syntax.  
D. To duplicate the object.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Returning the added entity allows the caller to see server-generated modifications, such as the newly assigned auto-increment ID.
</details>

### Q10. If `Find(e => e.Id == 99)` finds no matching employee, what does it return?
A. Throws an exception.  
B. Returns a new empty Employee.  
C. Returns `null` (for reference types).  
D. Returns -1.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Find` returns `default(T)`. For a class (reference type), this is `null`.
</details>

---

## HARD MCQs

### Q11. Which structure best represents the "Repository/Service" separation principle?
A. Methods mixed in Program.cs.  
B. Defining interfaces for logic, implementing them in services, and keeping models (POCOs) separate.  
C. Using only static methods.  
D. Putting all logic inside the POCO class constructor.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This separation of concerns (Models hold data, Services hold logic/storage access, Interfaces define contracts) is the core of maintainable architecture.
</details>

### Q12. `JsonSerializer.Serialize(emp)` is used to:
A. Save the employee to a database.  
B. Convert the employee object into a JSON string representation.  
C. Encrypt the data.  
D. Compress the memory usage.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Serialization converts the object state into a format (JSON string) suitable for transmission, display, or storage.
</details>

### Q13. Using `List<T>` for data storage in a web application is generally:
A. The best practice for production.  
B. Only suitable for demos/prototypes because data is lost on application restart and is not thread-safe by default.  
C. Faster than any database for millions of records.  
D. Secure.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Static lists in-memory are volatile (lost on crash/restart) and have concurrency issues in multi-threaded web servers unless locked properly. Useful for learning only.
</details>

### Q14. What is Dependency Inversion in this context?
A. The Service depends on the Program.  
B. The High-level module (Program) depends on abstraction (Interface), not detail (Concrete Service).  
C. Creating objects using `new`.  
D. Using `static` classes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The Program works with `IEmpService`, not `EmployeeService` directly (except at the instantiation point). Ideally, DI removes that `new` keyword too.
</details>

### Q15. In the method `IEnumerable<Employee> GetEmployee(string name)`, why return `IEnumerable` instead of `List`?
A. To force the user to use LINQ.  
B. `List` is deprecated.  
C. To return a read-only abstraction that the caller cannot easily modify (Add/Remove) compared to casting to List.  
D. It consumes more memory.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Returning the interface `IEnumerable` (or `IReadOnlyList`) is better API design as it abstracts the underlying storage implementation and implies "query results", not "a collection you own and modify".
</details>
