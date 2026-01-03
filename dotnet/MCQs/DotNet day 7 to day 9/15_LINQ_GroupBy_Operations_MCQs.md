# 15_LINQ_GroupBy_Operations – MCQs

## EASY MCQs

### Q1. What is the primary purpose of the `GroupBy` operator?
A. Sort elements.  
B. Organize elements into groups based on a key.  
C. Join two lists.  
D. Remove duplicate elements.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`GroupBy` buckets elements into groups where all elements in a group share a common key value.
</details>

### Q2. The return type of `GroupBy` is a collection of:
A. `List<T>`  
B. `Dictionary<Key, Value>`  
C. `IGrouping<TKey, TElement>`  
D. `Hashtable`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
It returns an `IEnumerable<IGrouping<Key, Element>>`. Each `IGrouping` has a `Key` property and acts as a list of items.
</details>

### Q3. How do you access the key of a group inside a loop?
A. `group.Value`  
B. `group.Index`  
C. `group.Key`  
D. `group.Name`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `IGrouping<TKey, TElement>` interface defines a `Key` property holding the value used to create that group.
</details>

### Q4. If you group Employees by Department, what does `group.Count()` return?
A. The number of departments.  
B. The number of characters in the department name.  
C. The number of employees in that specific department group.  
D. The total number of employees in the list.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Since the group itself is an Enumerable of items, calling `Count()` on the group counts the items within that bucket.
</details>

### Q5. Can you use `GroupBy` in Query Syntax?
A. No, only method syntax.  
B. Yes, using the `group ... by ...` clause.  
C. Yes, using `order by`.  
D. Yes, using `partition`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Query syntax supports grouping via `group element by key`.
</details>

---

## MEDIUM MCQs

### Q6. Which LINQ extension method allows you to group and then immediately project (transform) the results?
A. `GroupBy(...).Select(...)`  
B. `GroupJoin`  
C. `ToLookup`  
D. `Aggregate`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
A common pattern is to GroupBy a key, and then Select a new object (like a summary DTO) containing the Key and aggregates (Sum, Count) of the group.
</details>

### Q7. What is the difference between `GroupBy` and `ToLookup`?
A. No difference.  
B. `GroupBy` performs deferred execution; `ToLookup` executes immediately.  
C. `GroupBy` returns a Dictionary.  
D. `ToLookup` is slower.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`GroupBy` works lazily (deferred). `ToLookup` forces immediate iteration and creates a data structure similar to a Dictionary of Lists `ILookup<K, V>`.
</details>

### Q8. In the expression `employees.GroupBy(e => e.Department)`, what represents the key?
A. `e`  
B. `e.Department`  
C. `employees`  
D. `GroupBy`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The lambda provided `e => e.Department` is the Key Selector. The department value becomes the Key.
</details>

### Q9. How do you access the elements within a group?
A. The group object itself is enumerable/iterable.  
B. `group.GetElements()`  
C. `group.ToList()` is required.  
D. You cannot; you only get aggregates.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`IGrouping<K, E>` implements `IEnumerable<E>`. You can `foreach` over the group variable directly to get the items.
</details>

### Q10. You want to group numbers by whether they are even or odd. Key logic:
A. `n => n`  
B. `n => n % 2 == 0`  
C. `n => n / 2`  
D. `n => n * 2`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This boolean expression creates two groups: one where Key is `true` (evens) and one where Key is `false` (odds).
</details>

---

## HARD MCQs

### Q11. Using `GroupBy` with a composite key (grouping by multiple columns):
A. Not supported.  
B. Use an anonymous type `new { e.Dept, e.City }` as the key.  
C. Concatenate the strings.  
D. Use a Tuple (only in C# 9).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Anonymous types in C# automatically implement `Equals` and `GetHashCode` based on their properties, making them perfect for composite keys in grouping.
</details>

### Q12. `group by` in Query Syntax vs `GroupBy` method:
A. Query syntax creates a list of lists.  
B. Query syntax `group x by y` returns `IEnumerable<IGrouping<Y, X>>`, identical to method syntax.  
C. Query syntax does not support aggregates.  
D. Method syntax is required for grouping.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
They translate to the same IL/method calls fundamentally.
</details>

### Q13. If a group key is `null`, what happens?
A. It throws an exception.  
B. It is grouped under a `null` key (if the key type allows nulls).  
C. It is discarded.  
D. It is put in a "Default" group.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
GroupBy supports null keys. All items yielding a null key will be collected into a single group where `Key == null`.
</details>

### Q14. What corresponds to SQL `HAVING` clause in LINQ?
A. `Having()`  
B. A `Where()` clause applied *after* the `GroupBy()` (filtering the groups).  
C. A `Where()` clause applied *before* the `GroupBy()`.  
D. `TakeWhile`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
SQL `HAVING` filters results after grouping. In LINQ: `GroupBy(...) .Where(g => g.Count() > 5)` filters to keep only groups with more than 5 items.
</details>

### Q15. Can you use `Sum()` or `Max()` directly on the `grouped` variable (result of GroupBy)?
A. Yes, it sums all items in all groups.  
B. No, `grouped` is a collection of groups. You must iterate groups or Select from it first.  
C. Yes, it automatically flattens.  
D. Yes, if Key is numeric.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Use `grouped.Select(g => g.Sum(x => x.Value))` to get sums per group. Calling Sum on the top-level collection doesn't make sense without projection.
</details>
