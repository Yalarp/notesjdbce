# 05_SortedDictionary_Collection – MCQs

## EASY MCQs

### Q1. `SortedDictionary<K,V>` uses which internal structure?
A. Hash Table  
B. Linked List  
C. Binary Search Tree (Red-Black Tree)  
D. Dynamic Array  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
It relies on a self-balancing binary search tree to keep keys sorted while allowing O(log N) modification.
</details>

### Q2. Does `SortedDictionary` allow duplicate keys?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Like standard Dictionaries, Keys must be unique.
</details>

### Q3. Can you access `SortedDictionary` contents by index (e.g. `dict[0]`)?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Unlike `SortedList`, `SortedDictionary` does NOT support integer indexing because efficient indexing is not possible with a tree structure. You access only by Key.
</details>

### Q4. Iterating over `SortedDictionary` yields items in:
A. Insertion order.  
B. Sorted order of Key.  
C. Random order.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Traversal walks the tree in-order, guaranteeing sorted output.
</details>

### Q5. Which is faster for *Inserts*?
A. `SortedList` (Array)  
B. `SortedDictionary` (Tree)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SortedDictionary` is O(log N) for inserts. `SortedList` is O(N) because it must shift array elements.
</details>

---

## MEDIUM MCQs

### Q6. Which operation is generally faster on `SortedList` than `SortedDictionary`?
A. Insertion.  
B. Removal.  
C. Memory overhead per item.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`SortedList` uses less memory (just arrays). `SortedDictionary` encapsulates each item in a Node object with references/color bits, using significantly more heap memory.
</details>

### Q7. Time complexity for Lookup in `SortedDictionary`:
A. O(1)  
B. O(log N)  
C. O(N)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Searching a balanced binary tree takes logarithmic time.
</details>

### Q8. When would you prefer `SortedDictionary` over `Dictionary`?
A. When you need O(1) speed.  
B. When you perform many lookups but few inserts.  
C. When you need to iterate keys in order.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
If the requirement specifically asks for sorted output or range queries (e.g., get keys between A and C), `SortedDictionary` is appropriate. For raw speed, `Dictionary` is better.
</details>

### Q9. `SortedDictionary` expects the Key type to implement:
A. `IDisposable`  
B. `IComparable`  
C. `IEnumerable`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
To sort the tree, it needs to compare keys (Less than / Greater than). The keys must implement comparison logic.
</details>

### Q10. Does `SortedDictionary` re-balance itself?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It is a Red-Black tree implementation, which automatically rotates nodes to maintain balance and ensure O(log N) performance.
</details>

---

## HARD MCQs

### Q11. Can `SortedDictionary` change its comparer after creation?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The comparer is immutable. If you need a different sort order, you must create a new dictionary and copy items.
</details>

### Q12. Inserting pre-sorted data into `SortedDictionary` vs `SortedList`:
A. `SortedList` handles pre-sorted data very well (fastest case).  
B. `SortedDictionary` handles it better.  
C. No difference.  
(Note: Actually SortedList checks insertion point. If adding to *end*, it's O(1). If mixed, O(N). Tree is always O(log N)).
<br>
Let's rephrase: **Best use case for SortedDictionary vs SortedList involving modification?**
A. SortedList is better for static lookup tables. SortedDictionary is better for unsorted random inserts and deletes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
If the collection is Modified Frequently (Random inserts/removes), the Tree (SortedDictionary) wins (log N vs N). If built once and read often, Array (SortedList) wins (Compact memory, fast valid index lookup).
</details>

### Q13. Are `SortedDictionary` operations thread-safe?
A. Yes, automatically.  
B. No, reading is safe but writing requires locks.  
C. Only with `lock` keyword.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Generic collections are not thread-safe for write operations. Multi-threaded simultaneous writes (or read while writing) corrupt the tree structure.
</details>

### Q14. Populating a `SortedDictionary` from an unsorted list of N items takes:
A. O(N)  
B. O(N log N)  
C. O(N^2)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You perform N insertions. Each insertion is O(log N). Total = N * log N.
</details>

### Q15. `SortedDictionary<string, int>`. Which determines the sorting?
A. The integer values.  
B. The string keys.  
C. Both.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Sorting is always strictly based on the Key.
</details>
