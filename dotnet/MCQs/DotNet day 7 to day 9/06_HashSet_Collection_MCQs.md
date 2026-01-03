# 06_HashSet_Collection – MCQs

## EASY MCQs

### Q1. What is the primary characteristic of a `HashSet<T>`?
A. It maintains elements in sorted order.  
B. It allows duplicate elements.  
C. It stores unique elements in no particular order.  
D. It stores key-value pairs.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`HashSet<T>` is designed to store distinct elements where order is not guaranteed. Ideally, it prevents duplicates.
</details>

### Q2. Which internal data structure does `HashSet<T>` use to store elements?
A. Linked List  
B. Red-Black Tree  
C. Hash Table  
D. Dynamic Array  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`HashSet<T>` uses a hash table mechanism to achieve high-performance set operations, offering O(1) average complexity.
</details>

### Q3. What is the average time complexity for `Add`, `Remove`, and `Contains` operations in a `HashSet`?
A. O(n)  
B. O(log n)  
C. O(1)  
D. O(n log n)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Due to hashing, the average time complexity for these standard operations is constant time, O(1).
</details>

### Q4. Does `HashSet<T>` allow null values?
A. Yes, but only one null value.  
B. No, it throws an exception.  
C. Yes, multiple null values are allowed.  
D. Only for reference types, not nullable value types.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
A `HashSet` can contain null as a valid element, but since elements must be unique, it can contain at most one null value.
</details>

### Q5. Which method removes all elements from the `HashSet` that match a specific condition?
A. `RemoveAll()`  
B. `DeleteWhere()`  
C. `RemoveWhere()`  
D. `Clear()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`RemoveWhere(Predicate<T> match)` removes all elements that match the conditions defined by the specified predicate.
</details>

---

## MEDIUM MCQs

### Q6. Which method modifies the current `HashSet` to contain all elements that are present in itself, the specified collection, or both?
A. `IntersectWith`  
B. `UnionWith`  
C. `ExceptWith`  
D. `Concat`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`UnionWith` modifies the set to contain all elements that are present in the current set, in the specified collection, or in both (mathematical Union).
</details>

### Q7. If `SetA = {1, 2, 3}` and `SetB = {3, 4, 5}`, what is the result of `SetA.IntersectWith(SetB)`?
A. `{1, 2, 3, 4, 5}`  
B. `{1, 2}`  
C. `{3}`  
D. `{4, 5}`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`IntersectWith` keeps only the elements that are common to both sets. The only common element is 3.
</details>

### Q8. What does `SymmetricExceptWith` do?
A. Removes elements present in the other collection.  
B. Keeps only elements present in both collections.  
C. Modifies the set to contain elements that are present in one of the sets, but not both.  
D. Sorts the elements symmetrically.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`SymmetricExceptWith` produces the symmetric difference (XOR equivalent for sets): elements in Set A OR Set B, but NOT in both.
</details>

### Q9. When adding a duplicate value to a `HashSet` using the `Add` method, what happens?
A. An exception is thrown.  
B. The method returns `false` and the state remains unchanged.  
C. The existing value is overwritten.  
D. An exact duplicate is added to the collection.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Add` returns a boolean. If the element is already present, it returns `false` and does not modify the set.
</details>

### Q10. Compared to `List<T>`, why is `HashSet<T>` better for checking existence (`Contains`)?
A. It uses binary search.  
B. It has O(1) lookup vs O(n) for List.  
C. It allows indexing.  
D. It is thread-safe.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`List.Contains` performs a linear search (O(n)), whereas `HashSet.Contains` uses hashing (O(1)), making it significantly faster for large collections.
</details>

---

## HARD MCQs

### Q11. Which method would you use to verify if a `HashSet` is a proper subset of another collection?
A. `IsSubsetOf`  
B. `IsProperSubsetOf`  
C. `IsSupersetOf`  
D. `Overlaps`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`IsProperSubsetOf` checks if the set is a subset of the other collection but is strictly not equal to it (has fewer elements).
</details>

### Q12. Given `SetA = {1, 2}` and `SetB = {1, 2, 3}`, what does `SetA.ExceptWith(SetB)` result in?
A. `{1, 2}`  
B. `{3}`  
C. `{}` (Empty Set)  
D. `{1, 2, 3}`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`ExceptWith` removes all elements in the target set that are also in the argument collection. Since 1 and 2 are in B, they are removed from A, leaving it empty.
</details>

### Q13. `HashSet<T>` is NOT suitable when:
A. You need to enforce uniqueness.  
B. You need to access elements by index.  
C. You need fast lookups.  
D. You need to perform set operations.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`HashSet<T>` does not implement `IList<T>` and does not support indexing (e.g., `set[0]`). It is unordered.
</details>

### Q14. What happens internally when `HashSet` buckets are full?
A. It throws an `OutOfMemoryException`.  
B. It resizes the internal array (usually doubling the size) and rehashes elements.  
C. It links new elements to existing buckets (chaining) without resizing.  
D. It stops accepting new elements.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Like `Dictionary`, when the capacity is reached, `HashSet` normally grows its internal storage (often to the next prime size or power of 2) and rehashes existing entries.
</details>

### Q15. To remove only elements from `SetA` that are NOT in `SetB`, you should use:
A. `IntersectWith`  
B. `ExceptWith`  
C. `UnionWith`  
D. `RemoveWhere`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
This logic describes an Intersection. You want to keep elements that ARE in B (common), effectively removing those that are NOT in B. Thus, `IntersectWith` achieves "Remove elements from A that are not in B".
</details>
