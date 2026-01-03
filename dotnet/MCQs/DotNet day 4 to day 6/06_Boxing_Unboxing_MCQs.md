# 06_Boxing_Unboxing – MCQs

## EASY MCQs

### Q1. Converting a value type to a reference type is called:
A. Boxing  
B. Unboxing  
C. Casting  
D. Serialization  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Boxing is the implicit process of wrapping a value type (like int, struct) inside a System.Object on the heap.
</details>

### Q2. Where are value types stored typically?
A. Heap  
B. Stack  
C. Queue  
D. Global Memory  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Value types (local variables) are typically stored on the Stack (unless part of a class), whereas reference types are stored on the Heap.
</details>

### Q3. Unboxing requires which type of cast?
A. Implicit  
B. Explicit  
C. None  
D. Safe  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Unboxing extracts the value type from the object. Because this operation is risky (type mismatch possible), C# requires an explicit cast `(int)obj`.
</details>

### Q4. Which operation is generally faster?
A. Boxing  
B. Using generics (`List<int>`)  
C. Unboxing  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Generics avoid boxing/unboxing entirely, preserving type safety and performance, making them significantly faster than boxing operations.
</details>

### Q5. What is the base class for all value types?
A. `System.Object`  
B. `System.ValueType`  
C. `System.Type`  
D. `System.Struct`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
All value types inherit from `System.ValueType`, which overrides methods like `Equals` to use value equality instead of reference equality.
</details>

---

## MEDIUM MCQs

### Q6. `object o = 10; long x = (long)o;` What happens?
A. `x` becomes 10.  
B. `InvalidCastException`.  
C. Compiler Error.  
D. `x` becomes 0.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Unboxing must be to the *exact* original type. The object contains reduced `Int32`, not `Int64`. You must unbox to `int` first: `(long)(int)o`.
</details>

### Q7. When a value type is boxed, where is the object created?
A. Stack  
B. Heap  
C. CPU Cache  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Boxing allocates a new object on the Heap and copies the value from the Stack into that new heap object.
</details>

### Q8. Does `ArrayList` use boxing when storing integers?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`ArrayList` stores items as `object`. Adding a value type (like `int`) forces it to be boxed.
</details>

### Q9. `int x = 5; object o = x; x = 10;` What is the value inside `o`?
A. 5  
B. 10  
C. Null  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Boxing creates a *copy* of the value. Changing the original stack variable `x` has no effect on the independent boxed copy on the heap.
</details>

### Q10. Is boxing implicit or explicit?
A. Implicit  
B. Explicit  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Boxing is implicit (e.g., `object o = 5;`). No cast is needed because treating a specific type as `object` (base type) is always safe.
</details>

---

## HARD MCQs

### Q11. Can you unbox `null`?
A. Yes, it becomes 0.  
B. No, it throws `NullReferenceException`.  
C. Yes, it becomes default value.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Trying to unbox a null object typically throws `NullReferenceException` because there is no value type inside to extract.
</details>

### Q12. `int i = 10; IComparable c = i;` Does boxing occur?
A. No.  
B. Yes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Yes. Interfaces are reference types. Assigning a value type to an interface variable causes boxing (the value is wrapped in an object that implements the interface).
</details>

### Q13. Are all structs boxed when passed to a method accepting `object`?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Since `struct` is a value type, passing it to a parameter of type `object` requires conversion to a reference type, triggering boxing.
</details>

### Q14. Modifying a field of a boxed struct (via cast):
A. Updates the boxed struct on the heap.  
B. Is impossible in C# directly without unboxing first.  
C. Updates a temporary stack copy, leaving the box unchanged.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`( (Point)box ).X = 10;` unboxes `box` to a temporary stack copy, modifies the copy, and discards it. The original boxed object remains unchanged. To modify the boxed value, you must use an interface or unbox-modify-rebox.
</details>

### Q15. Does `Console.WriteLine(3)` cause boxing?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Overloads exist: `Console.WriteLine(int value)`. This specific overload takes an `int`, so no conversion to `object` is needed. However, `Console.WriteLine("Val: {0}", 3)` *would* cause boxing for the params object array.
</details>
