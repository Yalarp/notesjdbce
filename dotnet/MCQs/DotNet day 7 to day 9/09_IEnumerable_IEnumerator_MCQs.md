# 09_IEnumerable_IEnumerator – MCQs

## EASY MCQs

### Q1. Which interface makes a collection usable with the `foreach` loop?
A. `IList`  
B. `ICollection`  
C. `IEnumerable` (or `IEnumerable<T>`)  
D. `IDictionary`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `foreach` statement works on any type that implements `IEnumerable` or satisfies the "duck typing" pattern for GetEnumerator.
</details>

### Q2. What represents the stateful "cursor" used to iterate over a collection?
A. `IEnumerable`  
B. `IEnumerator`  
C. `List`  
D. `Array`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`IEnumerable` is the factory; `IEnumerator` is the object that actually holds the current position and moves through the collection.
</details>

### Q3. What method initiates the iteration process in `IEnumerable`?
A. `Start()`  
B. `GetEnumerator()`  
C. `Iterate()`  
D. `MoveNext()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`GetEnumerator()` returns the `IEnumerator` object used for the loop.
</details>

### Q4. Which method advances the enumerator to the next element?
A. `Next()`  
B. `GoForward()`  
C. `MoveNext()`  
D. `Read()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`MoveNext()` advances the position index and returns `true` if successful, or `false` if the end of the collection has been passed.
</details>

### Q5. What is the `Current` property?
A. The number of elements.  
B. The element at the current position of the enumerator.  
C. The current system time.  
D. The index of the element.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Current` returns the element in the collection at the current position of the enumerator.
</details>

---

## MEDIUM MCQs

### Q6. At the start of enumeration (before the first `MoveNext` call), where is the enumerator positioned?
A. At index 0 (first element).  
B. At index -1 (before the first element).  
C. At the last element.  
D. At a random position.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The enumerator starts in an initial state positioned *before* the first element. The first call to `MoveNext()` advances it to the first element.
</details>

### Q7. The `foreach` loop is syntactic sugar for corresponding code using:
A. `for` loop with indexers.  
B. `while` loop calling `GetEnumerator` and `MoveNext`.  
C. `do-while` loop.  
D. recursive functions.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The compiler generates a `while (enumerator.MoveNext())` loop block to iterate through the items.
</details>

### Q8. What does `yield return` do in C#?
A. It returns from the method permanently.  
B. It pauses execution and provides a value to the enumerator, resuming logically next time.  
C. It throws an exception.  
D. It creates a new thread.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`yield return` is used in iterator blocks to generate elements one by one lazily, automatically building an `IEnumerable`/`IEnumerator` state machine.
</details>

### Q9. Why can't you modify a collection (e.g., `Add`/`Remove`) while iterating it with `foreach`?
A. It is physically impossible.  
B. It works fine.  
C. It throws an `InvalidOperationException`.  
D. It restarts the loop.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Most standard collections track a "version" number. If the collection is modified, the version changes, and the active enumerator detects this mismatch and throws an exception to prevent undefined behavior.
</details>

### Q10. `IEnumerator<T>` inherits from:
A. `IEnumerator` and `IDisposable`.  
B. `IEnumerable`.  
C. `ICollection`.  
D. `IComparable`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The generic `IEnumerator<T>` extends the non-generic `IEnumerator` and also `IDisposable` (because iterators might hold resources that need cleaning up).
</details>

---

## HARD MCQs

### Q11. If you manually implement `IEnumerator`, what should `Reset()` do?
A. Clear the collection.  
B. Set the position back to before the first element.  
C. Dispose the enumerator.  
D. Throw `NotSupportedException` (which is common in simple iterators but technically defined to reset).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
According to the interface contract, `Reset()` sets the enumerator to its initial position. However, many modern iterators (like generated yield return ones) throw `NotSupportedException`. Correct theoretical answer is B.
</details>

### Q12. What happens if you access `Current` before calling `MoveNext()`?
A. It returns null.  
B. It returns the first element.  
C. Valid behavior is undefined; typically throws an exception or returns default.  
D. It automatically calls MoveNext.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The state is undefined. In many implementations, it might throw an exception or return a garbage value/default because the cursor is effectively at index -1.
</details>

### Q13. `IEnumerable<T>` defines only one method. What is it?
A. `IEnumerator<T> GetEnumerator()`  
B. `List<T> ToList()`  
C. `void ForEach(Action<T>)`  
D. `bool Contains(T item)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The interface is purely a factory for the enumerator: `IEnumerator<T> GetEnumerator()`. The other methods like `ToList` are extension methods (LINQ).
</details>

### Q14. In the `using` block generated by `foreach` for a generic collection, what method is called at the end?
A. `Close()`  
B. `Stop()`  
C. `Dispose()`  
D. `Reset()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Since `IEnumerator<T>` inherits `IDisposable`, the `foreach` loop wraps usage in a `try/finally` block and calls `Dispose()` to ensure resources are released.
</details>

### Q15. Can you use `foreach` on a class that does NOT implement `IEnumerable`?
A. No, never.  
B. Yes, if it has a public `GetEnumerator` method that returns an object with `MoveNext` and `Current`.  
C. Yes, via reflection only.  
D. Yes, if it assumes it is an array.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
C# supports "duck typing" for foreach. As long as the class has a matching `GetEnumerator()` method signature returning a suitable enumerator pattern, `foreach` will compile.
</details>
