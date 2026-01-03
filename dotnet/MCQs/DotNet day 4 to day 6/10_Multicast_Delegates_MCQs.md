# 10_Multicast_Delegates – MCQs

## EASY MCQs

### Q1. What is a multicast delegate?
A. A delegate that calls multiple methods.  
B. A delegate that takes multiple parameters.  
C. A delegate that prevents inheritance.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
A multicast delegate holds an invocation list of multiple methods. Invoking the delegate calls all methods in the list sequentially.
</details>

### Q2. Which operator adds a method to a delegate chain?
A. `+` or `+=`  
B. `&`  
C. `|`  
D. `>>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The `+=` operator is standard syntax for combining delegates (adding to the invocation list).
</details>

### Q3. Which operator removes a method from a delegate chain?
A. `-` or `-=`  
B. `delete`  
C. `remove`  
D. `~`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The `-=` operator removes the last occurrence of the specified optional delegate from the invocation list.
</details>

### Q4. In what order are methods invoked?
A. Random  
B. Reverse order of addition  
C. Order of addition (FIFO)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Methods are invoked in the order they were added to the delegate instance.
</details>

### Q5. What is the recommended return type for multicast delegates?
A. `int`  
B. `bool`  
C. `void`  
D. `object`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Because only the return value of the *last* invoked method is returned to the caller, return values from earlier methods are lost. `void` avoids this confusion.
</details>

---

## MEDIUM MCQs

### Q6. If a multicast delegate returns `int`, and invokes 3 methods returning 1, 2, and 3 respectively. What is the result?
A. 1  
B. 3  
C. 6 (Sum)  
D. Exception  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The return value of the call is the return value of the last method in the invocation list. Previous values are discarded.
</details>

### Q7. How can you get results from ALL methods in a multicast delegate?
A. You cannot.  
B. Use `GetInvocationList()` and iterate.  
C. Use `out` parameters.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`GetInvocationList()` returns an array of individual delegates. You can loop through this array and invoke them one by one to capture every result.
</details>

### Q8. If one method in the chain throws an exception:
A. It is suppressed and the next method runs.  
B. The execution stops and exception propagates.  
C. The exception is returned as a return value.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The exception propagates immediately. Subsequent methods in the invocation list are NOT called unless you manually handle the iteration with `GetInvocationList()` and try/catch blocks.
</details>

### Q9. `d -= Method;` what happens if `Method` is not in the list?
A. Throws Exception.  
B. Nothing happens.  
C. Clears the list.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is a safe operation. If the delegate is not found in the list, no change is made, and no error occurs.
</details>

### Q10. `Delegate d = d1 + d2;` Is the original `d1` modified?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Delegates are immutable. Combining them creates a new delegate instance containing the list of both. `d1` remains as it was.
</details>

---

## HARD MCQs

### Q11. Can `d += d` result in the same method being called twice?
A. Yes.  
B. No, duplicates are ignored.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, the invocation list allows duplicate entries. If you add the same method twice, it will be called twice.
</details>

### Q12. If `d1` and `d2` are multicast delegates, does `d1 == d2` check reference equality?
A. Yes.  
B. No, it checks if invocation lists are equal.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Delegate equality checks if the invocation lists have the same methods in the same order and target the same objects.
</details>

### Q13. Recursive delegation is:
A. Impossible.  
B. Adding a delegate to itself.  
C. A delegate calling a method that calls the delegate.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You can technically perform `d += d;`, which doubles the length of the invocation list. (Though C option describes recursion *using* delegates, B fits the context of "multicast operations").
</details>

### Q14. Using `out` parameters with multicast delegates:
A. Returns the value from the last method only.  
B. Is not allowed by the compiler.  
C. Aggregates all values.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Similar to return values, the `out` parameter will hold the value assigned by the last method in the chain. Earlier assignments are overwritten.
</details>

### Q15. Is multicast delegation thread-safe?
A. No.  
B. Yes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Adding/removing delegates (`+=`/`-=` usually requires checking for null or locking) is not atomic by default (though the `+=` operator on *events* usually has compiler-generated thread safety). The invocation itself is serial.
</details>
