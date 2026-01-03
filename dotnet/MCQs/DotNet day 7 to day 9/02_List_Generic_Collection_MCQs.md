# 02_List_Generic_Collection – MCQs

## EASY MCQs

### Q1. `List<T>` uses what internal data structure?
A. Linked List  
B. Array  
C. Tree  
D. Hash Table  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`List<T>` manages a dynamic internal array (`T[]`). When it fills up, it creates a larger array and copies elements over.
</details>

### Q2. What property tells you how many slots are currently allocated in memory for the List?
A. `Count`  
B. `Size`  
C. `Capacity`  
D. `Length`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Capacity` is the size of the internal array. `Count` is how many items you have actually added. `Capacity` >= `Count`.
</details>

### Q3. How do you add multiple items to a List at once?
A. `.AddMany()`  
B. `.AddRange()`  
C. `.AppendAll()`  
D. `.InsertAll()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`AddRange(IEnumerable<T>)` adds an entire collection of items to the end of the list efficiently.
</details>

### Q4. Accessing `list[0]` is an operation with complexity:
A. O(1)  
B. O(N)  
C. O(log N)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Indexer access maps directly to array index usage, which is constant time O(1).
</details>

### Q5. What happens if you access an invalid index (e.g., `list[5]` when Count is 3)?
A. Returns null.  
B. Returns 0.  
C. Throws `ArgumentOutOfRangeException`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The indexer validates that the index is >= 0 and < Count. If not, it throws an exception.
</details>

---

## MEDIUM MCQs

### Q6. Which method removes the specific object `obj` from the list?
A. `RemoveAt(obj)`  
B. `Delete(obj)`  
C. `Remove(obj)`  
D. `Erase(obj)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Remove(item)` searches for the first occurrence of the item (using Equals) and removes it. `RemoveAt` takes an integer index.
</details>

### Q7. When `List<T>` exceeds its Capacity, it typically resizes by:
A. Adding 1 slot.  
B. Adding 10 slots.  
C. Doubling the capacity.  
D. Squaring the capacity.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The standard growth strategy is doubling (4 -> 8 -> 16...) to achieve amortized O(1) performance for Add operations.
</details>

### Q8. The `Find` method expects a parameter of type:
A. `Func<T, bool>`  
B. `Predicate<T>`  
C. `Action<T>`  
D. `Expression<T>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Find(Predicate<T> match)` uses a delegate returning truthy/falsy to identify the item.
</details>

### Q9. `TrimExcess()` is used to:
A. Remove the last element.  
B. Reduce Capacity to match Count.  
C. Delete duplicate items.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If a list grew large (e.g. 1000) and you removed most items (down to 10), `Capacity` stays 1000. `TrimExcess` frees the unused memory by shrinking the internal array.
</details>

### Q10. `FindAll()` returns:
A. The first matching item.  
B. A `List<T>` containing all matching items.  
C. An array of matching items.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It iterates the entire list and collects all logical matches into a new List instance.
</details>

---

## HARD MCQs

### Q11. Removing an item from index 0 of a List (`RemoveAt(0)`) has complexity:
A. O(1)  
B. O(N)  
C. O(log N)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Because it is an array, removing the first element requires shifting ALL subsequent elements down by one spot to fill the gap. This is expensive for large lists.
</details>

### Q12. `TrueForAll` checks:
A. If any element matches.  
B. If every element matches the condition.  
C. If the list is not empty.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It returns `true` only if the predicate returns `true` for *every* element in the list.
</details>

### Q13. `List<int> l = new List<int>(); l.Add(1);` Does this cause boxing?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`List<int>` is generic. The internal array is `int[]`. The value 1 is stored directly as a 32-bit integer. No object wrapper (boxing) is created.
</details>

### Q14. Can you use `Sort()` on `List<Employee>` without arguments?
A. Yes, if Employee implements `IComparable<Employee>`.  
B. Yes, it sorts by memory address.  
C. No, it throws an exception if no comparer is provided and Employee doesn't implement IComparable.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The default `Sort()` relies on the default comparer. If the type does not implement `IComparable`, it cannot know how to order the objects (Runtime Error: InvalidOperationException).
</details>

### Q15. `BinarySearch` on a List requires:
A. The list to be sorted.  
B. The list to be empty.  
C. Unique elements.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Binary search algorithm only works on sorted collections. If the list is unsorted, the result is undefined (usually negative number indicating not found, even if it exists).
</details>
