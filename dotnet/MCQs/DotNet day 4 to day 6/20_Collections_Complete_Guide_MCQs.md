# 20_Collections_Complete_Guide – MCQs

## EASY MCQs

### Q1. Which collection type stores Key-Value pairs?
A. `List<T>`  
B. `Dictionary<TKey, TValue>`  
C. `Queue<T>`  
D. `Stack<T>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Dictionaries map unique keys to values, providing efficient lookup.
</details>

### Q2. Which collection works on First-In-First-Out (FIFO) principle?
A. `Stack`  
B. `Queue`  
C. `List`  
D. `HashSet`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Queue` adds to the back (`Enqueue`) and removes from the front (`Dequeue`).
</details>

### Q3. Which collection ensures all elements are unique?
A. `List<T>`  
B. `HashSet<T>`  
C. `Queue<T>`  
D. `Array`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`HashSet` is designed strictly for unique membership. Adding a duplicate has no effect (returns false).
</details>

### Q4. `ArrayList` belongs to which namespace?
A. `System.Collections.Generic`  
B. `System.Collections`  
C. `System.IO`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`ArrayList` is the legacy non-generic collection, prone to boxing/unboxing. It resides in `System.Collections`.
</details>

### Q5. How do you access an element in a List by position?
A. `.Get(index)`  
B. `[index]`  
C. `.ElementAt(index)`  
D. `.Pull(index)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Lists support standard indexer syntax `list[0]`, making them behave like dynamic arrays.
</details>

---

## MEDIUM MCQs

### Q6. Accessing a Dictionary key that does not exist using `[]`:
A. Returns null.  
B. Throws `KeyNotFoundException`.  
C. Returns default value.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The indexer `dict[key]` is strict. If you want a safe lookup, use `msg.TryGetValue(key, out val)`.
</details>

### Q7. `SortedList` stores elements:
A. In order of insertion.  
B. Sorted by Key.  
C. Sorted by Value.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It maintains the internal array such that keys are always sorted, allowing for binary search lookups (though insertion prevents O(1) speed).
</details>

### Q8. Cost of `Contains` in a `HashSet` vs `List`:
A. Both are O(N).  
B. HashSet is O(1), List is O(N).  
C. HashSet is O(N), List is O(1).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
HashSet uses hashing to find items instantly (O(1)). List must scan the entire array linearly (O(N)).
</details>

### Q9. `Stack` works on which principle?
A. FIFO  
B. LIFO  
C. Random Access  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Last-In-First-Out. `Push` on top, `Pop` from top.
</details>

### Q10. `LinkedList<T>` in C# is a:
A. Singly linked list.  
B. Doubly linked list.  
C. Circular buffer.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`System.Collections.Generic.LinkedList<T>` is a standard doubly-linked list implementation (each node points to Next and Previous).
</details>

---

## HARD MCQs

### Q11. Difference between `SortedList` and `SortedDictionary`:
A. Implementation (Array vs Tree).  
B. SortedList allows duplicates.  
C. No difference.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`SortedList` uses 2 arrays (keys/values) - faster memory, faster lookup, slower insertion (array copy). `SortedDictionary` uses a Red-Black Tree - faster insertion/removal O(logN), slightly more memory overhead.
</details>

### Q12. Modifying a collection while iterating it with `foreach`:
A. Works fine.  
B. Throws `InvalidOperationException`.  
C. Skips the modified item.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The enumerator detects that the "version" of the collection changed and throws immediately to prevent undefined behavior.
</details>

### Q13. `ObservableCollection<T>` is special because:
A. It is faster.  
B. It provides notifications (events) when items are added/removed.  
C. It is thread-safe.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Used heavily in UI frameworks (WPF/MAUI). It implements `INotifyCollectionChanged`, allowing UI to update automatically when the list changes.
</details>

### Q14. Can `Dictionary` keys be null?
A. Yes, always.  
B. No, never for generic Dictionary (refs).  
C. Yes for reference types, but only one null key allowed (Wait, actually standard Dictionary disallows null keys).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Standard `Dictionary<TKey, TValue>` throws ArgumentNullException if you try to add a null key. (Note: `Hashtable` allowed nulls, but generic Dictionary does not).
</details>

### Q15. Initial selection capacity of a `List<T>` impacts:
A. Correctness.  
B. Performance (re-allocation resizing).  
C. Thread safety.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If you know you will hold 10000 items, `new List<int>(10000)` prevents the internal array from resizing (doubling and copying) multiple times as you add items.
</details>
