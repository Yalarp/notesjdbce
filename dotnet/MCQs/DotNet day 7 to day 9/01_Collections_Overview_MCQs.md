# 01_Collections_Overview – MCQs

## EASY MCQs

### Q1. Which namespace contains the recommended generic collections?
A. `System.Collections`  
B. `System.Collections.Generic`  
C. `System.Data`  
D. `System.IO`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`System.Collections.Generic` (List<T>, Dictionary<K,V>) provides type safety and performance, unlike the older non-generic `System.Collections` (ArrayList, Hashtable).
</details>

### Q2. What is a primary limitation of standard Arrays in C#?
A. They are slow.  
B. They cannot store integers.  
C. They have a fixed size after creation.  
D. They are not indexable.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Arrays (`int[]`) must have their size defined at initialization and cannot grow dynamically. Collections like `List<T>` solve this by resizing automatically.
</details>

### Q3. Which collection type effectively prevents Duplicate elements?
A. `List<T>`  
B. `HashSet<T>`  
C. `ArrayList`  
D. `Stack<T>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`HashSet<T>` is designed to store only unique elements. Trying to add a duplicate value returns false and does not add it.
</details>

### Q4. Which collection stores data as Key-Value pairs?
A. `List<T>`  
B. `Dictionary<K,V>`  
C. `Queue<T>`  
D. `HashSet<T>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Dictionaries map a unique Key to a Value, allowing fast retrieval by Key.
</details>

### Q5. What is "Boxing"?
A. Converting a reference type to a value type.  
B. Converting a value type to a reference type (Object).  
C. Compressing a file.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Boxing occurs when a value type (like `int`) is wrapped inside an Object. This happens in non-generic collections like `ArrayList` and incurs a performance penalty.
</details>

---

## MEDIUM MCQs

### Q6. `SortedList<K,V>` is implemented internally using:
A. A Hash Table.  
B. A Linked List.  
C. Two Arrays (Keys and Values).  
D. A Red-Black Tree.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`SortedList` uses two internal arrays to maintain elements in sorted order. This allows O(1) indexed access but makes insertions O(N) due to shifting.
</details>

### Q7. If you need fast O(1) lookups by Key and order does not matter, use:
A. `SortedDictionary`  
B. `Dictionary`  
C. `List`  
D. `Stack`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Dictionary<K,V>` uses a Hash Table algorithm, providing the fastest average lookup time (constant time) but does not guarantee any specific order.
</details>

### Q8. Which interface is the base for all generic collections?
A. `IList`  
B. `IEnumerable<T>`  
C. `IDictionary`  
D. `IClonable`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`IEnumerable<T>` is the fundamental interface that allows a collection to be iterated over using `foreach`. `ICollection<T>` extends it.
</details>

### Q9. `ArrayList list = new ArrayList(); list.Add(1); list.Add("Two");`
A. Compile-time Error.  
B. Runtime Error.  
C. Allowed but dangerous (no type safety).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`ArrayList` stores `object`, so it accepts mixed types. This often leads to `InvalidCastException` at runtime when you try to retrieve items.
</details>

### Q10. What happens if you add a duplicate key to a Dictionary?
A. It over-writes the old value.  
B. It ignores the new value.  
C. It throws an `ArgumentException`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `.Add()` method strictly checks for duplicates. To overwrite/update, you must use the indexer: `dict[key] = newValue`.
</details>

---

## HARD MCQs

### Q11. Which collection maintains sorting using a Red-Black Tree?
A. `SortedList`  
B. `SortedDictionary`  
C. `List`  
D. `HashTable`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`SortedDictionary<K,V>` uses a balanced binary search tree (Red-Black tree) structure, ensuring O(log N) performance for insertions/deletions while keeping keys sorted.
</details>

### Q12. `SortedSet<T>` vs `HashSet<T>`:
A. `SortedSet` allows duplicates.  
B. `HashSet` is sorted.  
C. `SortedSet` is slower (O(log N)) but ordered; `HashSet` is faster (O(1)) but unordered.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`HashSet` is a pure Hash Table (speed). `SortedSet` maintains order using a Tree structure (order), sacrificing some speed on inserts/lookups.
</details>

### Q13. Can `List<T>` have null values?
A. No.  
B. Yes, if T is a reference type or Nullable value type.  
C. Only one null value allowed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`List<T>` allows duplicates and nulls (checking valid types). E.g., `List<string>` can contain multiple `null` entries.
</details>

### Q14. Access complexity for `SortedList<K,V>` by index `sl.Values[0]`:
A. O(1)  
B. O(N)  
C. O(log N)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Since `SortedList` is backed by arrays, accessing an element by its integer index is an instantaneous direct array access. access by *Key* is O(log N).
</details>

### Q15. When to use `ICollection<T>` parameter vs `IEnumerable<T>`?
A. `ICollection` when you need Count or Add/Remove capabilities.  
B. `IEnumerable` when you need to modify the list.  
C. No difference.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`IEnumerable` is read-only forward iteration. `ICollection` adds properties like `.Count` and methods like `.Add()`, `.Remove()`. Use the most specific interface needed.
</details>
