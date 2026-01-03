# 04_Dictionary_Collection – MCQs

## EASY MCQs

### Q1. `Dictionary<K,V>` uses which algorithm for storage?
A. Binary Tree  
B. Linear Search  
C. Hashing (Hash Table)  
D. Bubble Sort  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
It uses the Key's `GetHashCode()` to calculate a bucket index, allowing direct access.
</details>

### Q2. Does `Dictionary` guarantee the order of items?
A. Yes, sorted by key.  
B. Yes, by insertion order.  
C. No, order is undefined.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
While implementation details might sometimes look ordered, the spec guarantees NO order. Resizing the dictionary usually scrambles the order entirely.
</details>

### Q3. Average time complexity for `Add`, `Remove`, `ContainsKey`:
A. O(1)  
B. O(N)  
C. O(log N)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
This is the main strength of Hash Tables. Operations are constant time regardless of size (ignoring collisions/resizing).
</details>

### Q4. `dict["key"] = value` will:
A. Add the item if "key" doesn't exist.  
B. Update the item if "key" exists.  
C. Both A and B.  
D. Throw exception if "key" exists.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The indexer functions as an "Upsert" (Update or Insert) operation.
</details>

### Q5. Can a Dictionary have a null Key?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`GetHashCode` cannot be called on null. `Dictionary` actively forbids null keys (ArgumentNullException).
</details>

---

## MEDIUM MCQs

### Q6. `TryAdd` (in newer .NET versions) returns:
A. Void.  
B. Boolean (true if added, false if already exists).  
C. The existing value.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It allows adding without checking `ContainsKey` first, returning false instead of throwing if the key is already present.
</details>

### Q7. What happens when a Hash Collision occurs (two keys generate same hash)?
A. The old item is overwritten.  
B. An exception is thrown.  
C. Chaining / Bucket list is used to store both.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The dictionary handles collisions internally (usually via chaining/linked lists in the same bucket) so both items are preserved and retrievable.
</details>

### Q8. To iterate only over the values of a dictionary:
A. `foreach (var val in dict.Values)`  
B. `foreach (var val in dict)`  
C. `dict.GetAllValues()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The `.Values` property returns a collection of just the value types.
</details>

### Q9. `Dictionary<string, int>`. Which defines the Key type?
A. string  
B. int  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Format is `<TKey, TValue>`. First param is key.
</details>

### Q10. Why is Dictionary preferred over Hashtable?
A. Hashtable is abstract.  
B. Dictionary is generic (type-safe, faster/no boxing).  
C. Hashtable only allows 10 items.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Hashtable` (old) uses `object`. `Dictionary` (new) is generic, avoiding boxing overhead for value types and ensuring type safety.
</details>

---

## HARD MCQs

### Q11. Using a mutable object (where `GetHashCode` changes) as a Dictionary Key is:
A. Recommended.  
B. Dangerous/Bad Practice.  
C. Impossible.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If the key object changes such that its hash code changes *after* being added, you will likely never find it again (lookup will check the *new* hash bucket, but the item is in the *old* one). Keys should be immutable.
</details>

### Q12. Complexity of `ContainsValue`:
A. O(1)  
B. O(N)  
C. O(log N)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The hash map is organized by Key, not Value. To find a value, the dictionary must iterate through every single item (Linear Search).
</details>

### Q13. `Load Factor` in a dictionary refers to:
A. The weight of the data.  
B. The ratio of items to number of buckets.  
C. CPU usage.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
When the load factor exceeds a threshold (e.g. buckets are getting full), the dictionary performs a "Resize/Rehash" (creates larger bucket array) to maintain O(1) performance.
</details>

### Q14. `Clear()` operation on Dictionary:
A. O(1) (instant).  
B. O(N) (touches buckets).  
C. Deletes the variable.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It must iterate the bucket array to zero-out references so the GC can claim the objects. (Complexity is proportional to Capacity).
</details>

### Q15. Initializing dictionary with capacity `new Dictionary<int,int>(1000)`:
A. Wastes memory.  
B. Is an optimization if you know you have ~1000 items.  
C. Limits the dictionary to max 1000 items.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It pre-allocates buckets, preventing multiple resize/rehash operations as you add the first 1000 items. It does NOT limit the max size; it will still grow if needed.
</details>
