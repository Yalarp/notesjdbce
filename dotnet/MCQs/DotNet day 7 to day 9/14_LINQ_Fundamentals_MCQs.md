# 14_LINQ_Fundamentals – MCQs

## EASY MCQs

### Q1. What does LINQ stand for?
A. List Integrated Query  
B. Language Integrated Query  
C. Linked In-Memory Query  
D. Linear Integrated Queue  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
LINQ (Language Integrated Query) provides standard query capabilities directly into the C# language.
</details>

### Q2. Which namespace is required to use LINQ extension methods?
A. `System.Text`  
B. `System.Collections.Generic`  
C. `System.Linq`  
D. `System.Data`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `System.Linq` namespace must be imported to access extension methods like `Where`, `Select`, etc.
</details>

### Q3. Which method is used to filter elements in a sequence?
A. `Select`  
B. `Filter`  
C. `Where`  
D. `Take`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `Where` operator filters the collection based on a predicate function.
</details>

### Q4. Which syntax looks like SQL?
A. Method Syntax  
B. Query Syntax  
C. Lambda Syntax  
D. Fluent Syntax  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Query syntax uses keywords like `from`, `where`, `select` and syntactically resembles SQL.
</details>

### Q5. What does the `Select` operator do?
A. Filters the data.  
B. Sorts the data.  
C. Projects or transforms each element of a sequence into a new form.  
D. Groups the data.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Select` is a projection operator. It maps inputs to outputs (e.g., selecting just the Name from an Employee object).
</details>

---

## MEDIUM MCQs

### Q6. "Deferred Execution" in LINQ means:
A. The query executes in a background thread.  
B. The query is not executed when it is defined, but when the variable is iterated over (e.g., `foreach`).  
C. The query execution is delayed by 5 seconds.  
D. The query runs immediately but returns a Promise.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Operators like `Where` and `Select` return an iterator. No data is processed until you actually pull data from it (using foreach, ToList, etc.).
</details>

### Q7. To force immediate execution of a LINQ query and store results, you can call:
A. `Execute()`  
B. `Run()`  
C. `ToList()` or `ToArray()`  
D. `Commit()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Methods like `ToList()`, `ToArray()`, `Count()`, `First()` trigger immediate iteration of the source.
</details>

### Q8. Identify the correct lambda syntax to filter numbers greater than 10:
A. `.Where(n => n > 10)`  
B. `.Select(n => n > 10)`  
C. `.Filter(n > 10)`  
D. `.Having(n => n > 10)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`Where` takes a `Func<T, bool>` predicate.
</details>

### Q9. Which operator is used to sort data in ascending order?
A. `Sort`  
B. `Order`  
C. `OrderBy`  
D. `Ascending`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`OrderBy` sorts ascending. `OrderByDescending` sorts descending.
</details>

### Q10. What type does `Select` return if you create an anonymous type `new { Name = e.Name }`?
A. `List<Employee>`  
B. `IEnumerable<Employee>`  
C. `IEnumerable<'a>` (IEnumerable of generic anonymous type)  
D. `Object`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
It returns an `IEnumerable<T>` where T is the compiler-generated anonymous class type.
</details>

---

## HARD MCQs

### Q11. Difference between `First()` and `FirstOrDefault()`:
A. `First()` returns the first element or throws exception if empty; `FirstOrDefault()` returns default value (null) if empty.  
B. `FirstOrDefault()` returns the first element or throws exception.  
C. No difference.  
D. `First()` is faster.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`First()` expects at least one element. `FirstOrDefault()` handles empty sequences gracefully by returning `null` (for reference types) or `0`.
</details>

### Q12. How do you sort by multiple criteria (e.g., Name, then Age)?
A. `.OrderBy(x => x.Name).OrderBy(x => x.Age)`  
B. `.OrderBy(x => x.Name).ThenBy(x => x.Age)`  
C. `.OrderBy(x => x.Name, x.Age)`  
D. `.Sort(x => x.Name).Sort(x => x.Age)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Using `.OrderBy` twice resets the sort. `ThenBy` (or `ThenByDescending`) performs a secondary sort on the sorted sequence (`IOrderedEnumerable`).
</details>

### Q13. `Func<T, bool>` is a delegate signature typically used for:
A. `Select`  
B. `Where` (Predicate)  
C. `OrderBy`  
D. `Join`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A function taking T and returning bool is a Predicate, used to test whether an element should be included in `Where`.
</details>

### Q14. In Query syntax, the `select` or `group` clause must:
A. Appear first.  
B. Appear last.  
C. Be optional.  
D. Appear in the middle.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Standard LINQ Query Syntax (from ... where ...) must end with a `select` or `group` clause.
</details>

### Q15. `IEnumerable<T>` vs `IQueryable<T>`:
A. `IQueryable` is faster for objects.  
B. `IEnumerable` runs in-memory; `IQueryable` is for remote/database sources (allows expression tree translation to SQL).  
C. `IEnumerable` supports SQL injection.  
D. `IQueryable` is a base class of `IEnumerable`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`IEnumerable` executes delegates (compiled code). `IQueryable` stores Expression Trees that providers (like Entity Framework) can parse and translate into SQL queries.
</details>
