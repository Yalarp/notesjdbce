# 03_SortedList_Collection – MCQs

## EASY MCQs

### Q1. `SortedList<K,V>` automatically sorts elements by:
A. Value  
B. Key  
C. Insertion Order  
D. Randomly  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It maintains keys in sorted order (based on IComparer or default sort) at all times so that binary search can be used.
</details>

### Q2. Can you access elements in a `SortedList` by integer index?
A. Yes, e.g., `list.Values[0]`.  
B. No, only by Key.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
A unique feature of `SortedList` (vs Dictionary) is that it exposes `Keys` and `Values` as indexable lists `IList`. You can get the "smallest key" using index 0.
</details>

### Q3. Attempting to add a duplicate Key to a `SortedList` results in:
A. Updating the value.  
B. Ignoring the addition.  
C. Throwing `ArgumentException`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Keys must be unique. To update, use the indexer `list[key] = val`. `Add()` throws on duplicates.
</details>

### Q4. Adding an item to `SortedList` is generally:
A. Faster than Dictionary.  
B. Slower than Dictionary.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is slower O(N) because it must find the correct spot (binary search) and then *shift* all subsequent elements in the array to make room. Dictionary Add is O(1).
</details>

### Q5. Can Keys in `SortedList` be null?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Keys must be comparable to determine order. Comparison with null is generally invalid for sorting purposes, so null keys are forbidden.
</details>

---

## MEDIUM MCQs

### Q6. Which method allows you to check for a key safely without throwing exceptions?
A. `HasKey()`  
B. `ContainsKey()`  
C. `CheckKey()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`ContainsKey` returns boolean true/false. Accessing specific key via indexer throws if missing.
</details>

### Q7. `SortedList` implementation uses:
A. Linked List.  
B. Hash Table.  
C. Two internal arrays.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
One array for Keys, one for Values. They are kept synchronized.
</details>

### Q8. What does `IndexOfKey("abc")` return if "abc" is not found?
A. 0  
B. -1  
C. null  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Standard .NET convention for "Index Of" methods is to return -1 when the item is missing.
</details>

### Q9. Iterating a `SortedList` with `foreach` yields items of type:
A. `DictionaryEntry`  
B. `KeyValuePair<K,V>`  
C. `Tuple<K,V>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Standard for generic dictionary-like collections.
</details>

### Q10. `SortedList` is best suited for:
A. Massive datasets with frequent writes.  
B. Small/Static datasets where memory matters and sorted access is needed.  
C. Unordered data.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It uses less memory than Dictionary or SortedDictionary (no node/bucket overhead). But insertions are expensive. Ideal for lookup tables loaded once.
</details>

---

## HARD MCQs

### Q11. Using the indexer `sl["key"]` involves complexity:
A. O(1)  
B. O(N)  
C. O(log N)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
It performs a Binary Search on the keys array to find the index, then retrieves the value from that index. Binary Search is O(log N).
</details>

### Q12. `TryGetValue` vs indexer `[]` for missing keys:
A. `TryGetValue` returns false; `[]` throws KeyNotFoundException.  
B. `TryGetValue` throws; `[]` returns null.  
C. Both throw.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`TryGetValue` is the standard safe pattern to avoid try-catch blocks for control flow.
</details>

### Q13. `SortedList` vs `SortedDictionary` memory usage:
A. `SortedList` uses less memory.  
B. `SortedDictionary` uses less memory.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`SortedList` is just arrays (dense compact storage). `SortedDictionary` is a tree of Node objects (Key, Value, LeftPtr, RightPtr, Color), resulting in significant per-item overhead.
</details>

### Q14. If you modify a Value in `SortedList` (`sl["A"] = 5`), is re-sorting required?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Sorting relies on Keys. Values do not affect the order. Updating a value is an O(log N) lookup then O(1) write.
</details>

### Q15. Can `SortedList` contain duplicate Values?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Uniqueness constraint applies only to Keys. Multiple keys can map to the same value (e.g., "Bob" -> 50, "Alice" -> 50).
</details>
