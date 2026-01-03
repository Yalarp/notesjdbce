# 19_Generic_NonGeneric_Delegates – MCQs

## EASY MCQs

### Q1. Which generic delegate returns a value?
A. `Action<T>`  
B. `Func<T>`  
C. `Predicate<T>`  
D. `Reference<T>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Func` delegates *always* return a value. The last type parameter specifies the return type.
</details>

### Q2. Which generic delegate returns `void`?
A. `Func`  
B. `Action`  
C. `Predicate`  
D. `Task`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Action` delegates encapsulate a method that has parameters (0 to 16) and does not return a value.
</details>

### Q3. `Predicate<T>` always returns:
A. `int`  
B. `string`  
C. `bool`  
D. `void`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
A Predicate represents a set of criteria to check if the object T meets a condition, inherently returning true or false.
</details>

### Q4. `Func<int, string, bool>` takes how many inputs?
A. 1  
B. 2  
C. 3  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Format is `Func<Input1, Input2, ReturnType>`. So inputs are `int` and `string`. `bool` is the return type.
</details>

### Q5. Can `Action` delegates take arguments?
A. No.  
B. Yes, up to 16.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Yes, `Action<T1, T2...>` allows passing input parameters.
</details>

---

## MEDIUM MCQs

### Q6. Which delegate is semantically equivalent to `Func<T, bool>`?
A. `Action<T>`  
B. `Predicate<T>`  
C. `Check<T>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Predicate<T>` is effectively a specialized wrapper for `delegate bool Predicate(T obj)`. It matches the signature of `Func<T, bool>`.
</details>

### Q7. Generic delegates are primarily defined in which namespace?
A. `System`  
B. `System.Generics`  
C. `System.Delegates`  
D. `System.Collections`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The `Action` and `Func` types reside directly in the root `System` namespace.
</details>

### Q8. Non-generic delegates (from early C# versions) require:
A. Explicit declaration of a delegate type.  
B. Using `var`.  
C. Nothing special.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Before generics, you had to define `public delegate int MyOperation(int x);`. Generic `Func<int, int>` removed that boilerplate necessity.
</details>

### Q9. `foreach` on a `List<T>` traditionally accepts which delegate?
A. `Func<T>`  
B. `Action<T>`  
C. `Predicate<T>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`List.ForEach` performs an operation on each element. This maps to `Action<T>` (do something with item T).
</details>

### Q10. `List.FindAll` expects which delegate?
A. `Action<T>`  
B. `Func<T, T>`  
C. `Predicate<T>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
It needs to test each element to see if it belongs in the result list, so it asks for a `Predicate<T>`.
</details>

---

## HARD MCQs

### Q11. Is `Func<int, bool>` type-compatible with `Predicate<int>`?
A. Yes, they are interchangeable.  
B. No, they are distinct types even if signatures match.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
In C#, delegate types are nominal, not structural. Even though they have the same method signature, you cannot assign a `Func<T, bool>` variable directly to a `Predicate<T>` variable without constructing a new delegate (e.g. `new Predicate<int>(func)`).
</details>

### Q12. `Action` (non-generic) corresponds to:
A. `void Method()`  
B. `void Method(object o)`  
C. `object Method()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The base `Action` delegate takes 0 arguments and returns void.
</details>

### Q13. `public delegate void EventHandler(object sender, EventArgs e)` is:
A. A generic delegate.  
B. A non-generic delegate.  
C. An attribute.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is the classic non-generic declaration. The modern generic replacement would be `EventHandler<TEventArgs>`.
</details>

### Q14. Can generic delegates be used with covariance/contravariance?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, `Func<out TResult>` is covariant in its return type. `Action<in T>` is contravariant in its parameter type.
</details>

### Q15. Does `Func<T>` support `ref` or `out` parameters?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The standard built-in `Func` and `Action` delegates do not support `ref` or `out` parameters. If you need those, you must declare a custom delegate type.
</details>
