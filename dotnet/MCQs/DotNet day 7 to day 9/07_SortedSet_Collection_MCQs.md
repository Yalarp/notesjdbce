# 07_SortedSet_Collection – MCQs

## EASY MCQs

### Q1. What is the defining feature of `SortedSet<T>` compared to `HashSet<T>`?
A. It allows duplicate values.  
B. It maintains elements in a sorted order.  
C. It is faster for lookups.  
D. It accepts key-value pairs.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SortedSet<T>` stores unique elements just like `HashSet<T>`, but it maintains them in a specific sorted order (ascending by default).
</details>

### Q2. Which internal data structure does `SortedSet<T>` typically use?
A. Hash Table  
B. Dynamic Array  
C. Red-Black Tree  
D. Linked List  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`SortedSet<T>` is implemented using a self-balancing binary search tree (Red-Black Tree), which ensures O(log n) performance for operations.
</details>

### Q3. What is the time complexity for `Add`, `Remove`, and `Contains` in a `SortedSet`?
A. O(1)  
B. O(n)  
C. O(log n)  
D. O(n^2)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Because it relies on a binary search tree structure, the standard operations take O(log n) time, unlike `HashSet`'s O(1).
</details>

### Q4. If you iterate over a `SortedSet<int>` containing `{ 5, 1, 3 }`, what is the output order?
A. 5, 1, 3  
B. 1, 3, 5  
C. 5, 3, 1  
D. Random  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The set automatically sorts the elements. Integers are sorted in ascending order by default.
</details>

### Q5. Can `SortedSet<T>` contain duplicate elements?
A. Yes  
B. No  
C. Only if a custom comparer is used.  
D. Yes, but ignoring the sort order.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Like `HashSet`, `SortedSet` enforces mathematical set rules, which means all elements must be unique.
</details>

---

## MEDIUM MCQs

### Q6. Which property allows `SortedSet` to retrieve a subset of elements between two values?
A. `GetRange()`  
B. `GetViewBetween()`  
C. `SubSet()`  
D. `Slice()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `GetViewBetween(min, max)` method returns a view of the original set containing elements within the specified range.
</details>

### Q7. How can you reverse the order of elements in a `SortedSet<T>`?
A. Use `Reverse()` LINQ method creates a copy or IEnumerable, but the `SortedSet` itself has a property `Reverse()` usually via enumerator. Ideally, you use a custom `IComparer` that inverts the sort.  
B. Use `set.ReverseOrder()`.  
C. Pass a custom `IComparer<T>` to the constructor that reverses the comparison logic.  
D. It is not possible.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
You can define the sort order at creation time by passing an `IComparer<T>`. To reverse order, pass a comparer that returns the opposite comparison result.
</details>

### Q8. Which class represents the tree node internal to `SortedSet`?
A. It is not exposed publicly.  
B. `SortedSetNode`  
C. `TreeNode`  
D. `LinkedListNode`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The internal node structure is an implementation detail of the .NET Framework and is not exposed as a public API like `LinkedListNode`.
</details>

### Q9. `SortedSet<T>` operations like `UnionWith` and `IntersectWith`:
A. Are not supported.  
B. Behave identically to `HashSet<T>` but maintain sorted order.  
C. Convert the set to a List.  
D. Are slower than `List.Add`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SortedSet` supports all standard set operations defined in `ISet<T>`, and the result typically preserves the sorted nature of the container.
</details>

### Q10. What corresponds to the "minimum" element in `SortedSet`?
A. The root of the tree.  
B. The `Min` property.  
C. The element with index 0.  
D. The first element when enumerated.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SortedSet` has a `Min` property (and `Max`) that efficiently retrieves the smallest element according to the sort order. Note: `Min` is a property on `SortedSet<T>`, contrasting with LINQ's `Min()` method.
</details>

---

## HARD MCQs

### Q11. When would you prefer `SortedSet` over `SortedList` or `SortedDictionary`?
A. When you need key-value pairs.  
B. When you only need to store values (no keys) and need uniqueness + sorting.  
C. When you need O(1) access by index.  
D. When memory is the only concern.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SortedList` and `SortedDictionary` are for Key-Value pairs. `SortedSet` is for unique values only.
</details>

### Q12. Does `SortedSet<T>` support indexing (e.g., `set[i]`)?
A. Yes, it implements `IList<T>`.  
B. No, it does not provide direct index access.  
C. Yes, but it is O(n).  
D. Only via extension methods.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SortedSet` does not provide an indexer. To get the i-th element, you would have to use `ElementAt(i)` (LINQ), which iterates O(i).
</details>

### Q13. If you add an object to a `SortedSet` that does not implement `IComparable` and no `IComparer` is provided:
A. It works fine using object hash codes.  
B. It throws an `InvalidOperationException` or `ArgumentException`.  
C. It sorts by memory address.  
D. It treats all objects as equal.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SortedSet` needs a way to compare elements. If `T` does not implement `IComparable<T>` and no external comparer is given, it cannot sort them and will throw an exception at runtime when adding elements.
</details>

### Q14. What is the benefit of `GetViewBetween`?
A. It creates a deep copy of the data.  
B. It returns a dynamic view that reflects changes in the underlying set.  
C. It converts the data to an array.  
D. It is a static snapshot.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The view returned is a virtual subset. Changes to the underlying set (within range) are reflected in the view, and vice versa (if modifications are valid).
</details>

### Q15. Compared to `HashSet`, `SortedSet` uses:
A. Less memory per element.  
B. More memory per element (due to tree pointers).  
C. The same amount of memory.  
D. Contiguous memory blocks.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A Red-Black tree node typically requires references to Left Child, Right Child, and Parent (plus color bit), whereas a Hash Table entry typically needs the value and a next-bucket pointer (or similar). Tree structures generally have higher per-node overhead.
</details>
