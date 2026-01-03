# 15_Nullable_Partial_Classes – MCQs

## EASY MCQs

### Q1. What does `int?` represent in C#?
A. An integer that cannot change.  
B. A nullable integer (System.Nullable<int>).  
C. A pointer to an integer.  
D. A dynamic integer.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `?` suffix is syntactic sugar for `System.Nullable<T>`, allowing value types to accept the value `null`.
</details>

### Q2. `HasValue` property returns true if:
A. The variable is null.  
B. The variable contains a valid non-null value.  
C. The variable is zero.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If a `Nullable<T>` has been assigned a value, `HasValue` is true. If it is null, `HasValue` is false.
</details>

### Q3. Which keyword allows splitting a class definition into multiple files?
A. `split`  
B. `partial`  
C. `abstract`  
D. `static`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `partial` keyword tells the compiler to merge multiple file definitions into one single class at compile time.
</details>

### Q4. The `??` operator is called:
A. The Elvis operator.  
B. The Null-Coalescing operator.  
C. The Ternary operator.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It returns the left-hand operand if it is not null; otherwise it returns the right-hand operand. `a ?? b`.
</details>

### Q5. Can you have a nullable `bool` (`bool?`)?
A. No.  
B. Yes, it has 3 states: true, false, null.  
C. Yes, but it only holds true/false.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`bool?` is often used in databases (Tristate boolean) to represent True, False, or Unknown (null).
</details>

---

## MEDIUM MCQs

### Q6. Accessing `.Value` on a nullable type that is currently `null` causes:
A. Return 0.  
B. `NullReferenceException`.  
C. `InvalidOperationException`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Unlike reference types throwing NullReference, accessing the Value property of a null `Nullable<T>` explicitly throws `InvalidOperationException`.
</details>

### Q7. Partial methods must implicitly be:
A. `public`  
B. `private`  
C. `internal`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Partial methods are implementation details used to inject logic into generated code. They are private and cannot have access modifiers explicitly (prior to C# 9).
</details>

### Q8. If a partial method is defined but not implemented:
A. Compiler error.  
B. Runtime error.  
C. The compiler removes the call and the definition completely.  
D. It throws NotImplementedException.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
This is a feature for code generators. If the user doesn't care to hook into the event (implement the method), the compiler strips the call out entirely for zero performance cost.
</details>

### Q9. `int? a = null; int b = a.GetValueOrDefault();` What is `b`?
A. null  
B. 0  
C. Exception  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`GetValueOrDefault()` returns the underlying default value for the type (0 for int) if the container is null.
</details>

### Q10. Can different parts of a partial class implement different interfaces?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, the final compiled class implements the union of all interfaces listed on all partial definitions.
</details>

---

## HARD MCQs

### Q11. Can `Nullable<T>` be used with reference types (e.g. `Nullable<string>`)?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`System.Nullable<T>` applies generic constraint `where T : struct`. Reference types are already nullable by nature, so wrapping them in a struct wrapper is invalid. (Note: C# 8 "Nullable Reference Types" is a compiler analysis feature, not the same runtime type as `Nullable<T>`).
</details>

### Q12. `int? x = 5; int y = x;` Is this valid?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
No. You cannot implicitly convert a nullable type to a non-nullable type (possibility of null). You must use an explicit cast `(int)x` or `.Value`.
</details>

### Q13. Can a partial class span across different assemblies (DLLs)?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Partial classes are a compile-time feature. All parts must be available during the single compilation step for the assembly. You cannot extend a class from a compiled DLL using `partial`.
</details>

### Q14. What is the type of `null`?
A. `object`  
B. `void`  
C. It has no type.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The null literal itself doesn't have a type, but it is convertible to any reference type or nullable value type.
</details>

### Q15. `int? a = null; int? b = 10; Console.WriteLine(a < b);` Output?
A. True  
B. False  
C. null  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
In C#, comparison operators with nulls usually return false (`a > b` is false, `a < b` is false). (Lifted operators logic: if one operand is null, result is false/null depending on context, but boolean usage results in false).
</details>
