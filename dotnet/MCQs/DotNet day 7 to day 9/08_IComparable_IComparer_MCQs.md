# 08_IComparable_IComparer – MCQs

## EASY MCQs

### Q1. Which interface contains the `CompareTo` method?
A. `IComparer<T>`  
B. `IComparable<T>`  
C. `IEquatable<T>`  
D. `IEnumerator`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`IComparable<T>` defines the `CompareTo` method, used to define the "natural" sort order of a class.
</details>

### Q2. Which interface would you implement to define an external or alternate sort order for a class?
A. `IComparable<T>`  
B. `IComparer<T>`  
C. `ISortable`  
D. `IOrder`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`IComparer<T>` is implemented in a separate helper class to provide custom or multiple comparison logics (e.g., sort by name, then sort by age).
</details>

### Q3. If `A.CompareTo(B)` returns a value less than 0, it means:
A. A comes after B.  
B. A is equal to B.  
C. A comes before B.  
D. An error occurred.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
A negative return value (e.g., -1) indicates that the current instance (A) precedes the object being compared to (B) in the sort order.
</details>

### Q4. Which method signature belongs to `IComparer<T>`?
A. `int CompareTo(T other)`  
B. `bool Equals(T x, T y)`  
C. `int Compare(T x, T y)`  
D. `void Sort(T x, T y)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`IComparer<T>` requires the implementation of `int Compare(T x, T y)`, taking two arguments to compare.
</details>

### Q5. When calling `List.Sort()` on a list of objects that implement `IComparable`, what happens?
A. It throws an exception.  
B. It uses the class's `CompareTo` method to sort the list.  
C. It sorts by memory address.  
D. It requires an `IComparer` to be passed explicitly.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The parameterless `Sort()` method relies on the default comparer, which checks if the type implements `IComparable` and uses it.
</details>

---

## MEDIUM MCQs

### Q6. To sort a `List<Student>` by Name and then by Id, which approach is best?
A. Modify `Student` to implement multiple `IComparable` interfaces.  
B. Create a custom `IComparer<Student>` that checks names, and if equal, checks Ids.  
C. Call `Sort()` twice.  
D. Use `Array.Sort`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Creating a specific implementation of `IComparer` captures this compound logic clearly without polluting the `Student` class's natural order.
</details>

### Q7. What is the return value of `CompareTo` if the current instance and the argument are equal in sort order?
A. 1  
B. -1  
C. 0  
D. null  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
A return value of 0 indicates equality in terms of ordering.
</details>

### Q8. Identify the correct implementation logic for `CompareTo` for standard integer comparison of a field `Age`:
A. `return this.Age - other.Age;` (handling overflow carefully or using .CompareTo)  
B. `return this.Age > other.Age ? -1 : 1;`  
C. `return 0;`  
D. `return other.Age.CompareTo(this.Age);`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Delegate to the field's own `CompareTo`: `return this.Age.CompareTo(other.Age);`. Or, subtraction can work if ranges are safe, but `CompareTo` is safer. Option A implies the standard ascending logic.
</details>

### Q9. Can a class implement `IComparable<T>` and also be sorted using an `IComparer<T>`?
A. No, they are mutually exclusive.  
B. Yes, `List.Sort()` will prioritize `IComparable`.  
C. Yes, you can choose `List.Sort()` (uses IComparable) or `List.Sort(comparer)` (uses IComparer).  
D. Yes, but it causes compile-time warnings.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
This is a standard pattern. A class has a default natural order (IComparable), but you can override it ad-hoc using specific Comparers.
</details>

### Q10. When implementing `IComparer<T>`, where is the logic typically placed?
A. Inside the class being sorted.  
B. In a separate helper class or nested class.  
C. Inside the `Main` method only.  
D. In the `Global.asax`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Since `IComparer` is often a distinct strategy, it's placed in its own class (e.g., `StudentNameSorter`) or a static property/nested class.
</details>

---

## HARD MCQs

### Q11. Which method would you use to sort an array `T[]` using a Comparison delegate instead of an interface?
A. `Array.Sort(arr, (x, y) => ...)`  
B. `arr.Sort(delegate)`  
C. `Collections.Sort(arr)`  
D. `Array.Order(arr)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`Array.Sort` and `List.Sort` both accept a `Comparison<T>` delegate (lambda) as an overload, avoiding the need for a full class implementation.
</details>

### Q12. If `Compare(x, y)` returns a positive number, what does `List.Sort` do?
A. Places `x` before `y`.  
B. Places `x` after `y`.  
C. Treats them as equal.  
D. Moves `x` to the start of the list.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Positive means `x` is "greater than" `y`, so for ascending sort, `x` should come after `y`.
</details>

### Q13. Handling `null` in `CompareTo`:
A. Throw `NullReferenceException`.  
B. By convention, a null reference compares less than any non-null reference.  
C. By convention, a null reference compares greater than any non-null reference.  
D. Nulls are ignored.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
In .NET sorting conventions, `null` is usually considered "less than" everything else (creates `null, null, A, B`), but strictly speaking, `obj.CompareTo(null)` should return a positive number (current instance > null). Wait—standard rule: "Any instance is greater than null". So `CompareTo(null)` returns 1. If both are null (not possible in instance method), they are equal.
</details>

### Q14. What is the main disadvantage of `IComparable` compared to `IComparer`?
A. It is slower.  
B. It couples the sorting logic to the domain class and allows only one sort order.  
C. It cannot handle integers.  
D. It is deprecated.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`IComparable` defines "the" sort order. If you need multiple ways to sort (by Date, by Price, etc.), you have to modify the class or switch to `IComparer`.
</details>

### Q15. `Comparer<T>.Default` does what?
A. Returns a null comparer.  
B. Returns a comparer that uses the type `T`'s `IComparable` implementation.  
C. Returns a random sorter.  
D. Throws an exception if `T` is custom.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Comparer<T>.Default` smarty checks if `T` implements `IComparable<T>` (or nongeneric `IComparable`) and returns a comparer that delegates to it.
</details>
