# 14_Const_And_Readonly – MCQs

## EASY MCQs

### Q1. What is the main difference between `const` and `readonly` regarding initialization?

A. `const` can be initialized in constructor; `readonly` cannot.  
B. `const` must be initialized at declaration; `readonly` can be initialized at declaration or in a constructor.  
C. They are identical.  
D. `readonly` is for static members only.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`const` is a compile-time constant and must be assigned when declared. `readonly` can be assigned either at declaration OR inside a constructor (allowing for runtime determination).
</details>

### Q2. Is a `const` field implicitly static?

A. Yes.  
B. No, it is instance-based.  
C. Only if marked static.  
D. No, it is dynamic.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
`const` members are implicitly static. You access them via the Class Name (e.g., `Math.PI`), not via an instance.
</details>

### Q3. Which types are allowed to be `const`?

A. All types.  
B. Only primitive types (int, double, etc.), enums, and strings.  
C. Only reference types.  
D. Only integers.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`const` fields must be values that can be fully evaluated at compile time. This limits them to primitives (numbers, bool, char), enums, and string literals.
</details>

### Q4. Can you modify a `readonly` field after the constructor has finished execution?

A. Yes, using reflection.  
B. No.  
C. Yes, if it is public.  
D. Yes, in the destructor.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
For normal usage, a `readonly` field is immutable after the constructor completes. (Reflection is an exception, but functionally the answer is No).
</details>

---

## MEDIUM MCQs

### Q5. When is the value of a `const` field evaluated?

A. At Runtime.  
B. At Compile Time.  
C. Just-In-Time.  
D. When accessed.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The compiler replaces all usages of a `const` variable with the literal value itself during compilation (embedding the value).
</details>

### Q6. Refer to the code:
```csharp
class Demo {
    public readonly int val;
    public Demo(int v) { val = v; }
}
```
Is this valid?

A. No, `readonly` must be assigned at declaration.  
B. No, `val` must be static.  
C. Yes, `readonly` fields can be assigned in the constructor.  
D. Yes, but only if `v` is a literal.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
This is the primary use case for `readonly`: allowing a value to be immutable but determined at runtime (via constructor parameters).
</details>

### Q7. If `Library.dll` defines `public const int Ver = 1;` and your app uses it. Later, `Library.dll` changes `one` to `2` and is recompiled, but your app is NOT recompiled. What value does your app see?

A. 1  
B. 2  
C. 0  
D. Runtime Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
Because `const` values are embedded directly into the *calling* assembly's IL code at compile time, your app effectively has "1" hardcoded into it. You must recompile the app to see the change.
</details>

### Q8. Can a `readonly` field be static?

A. No.  
B. Yes (`static readonly`).  
C. Yes, but it becomes `const`.  
D. Only in abstract classes.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Yes, `static readonly` is commonly used for values that are constant for the whole app but need to be calculated at runtime (e.g., loading config).
</details>

---

## HARD MCQs

### Q9. Consider a `readonly` reference type field: `public readonly List<int> Numbers;`. What is immutable?

A. The list content (you cannot add items).  
B. The reference `Numbers` (you cannot assign a new List object to it).  
C. Both reference and content.  
D. Neither.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`readonly` on a reference type prevents reassignment of the variable (the pointer). However, the object pointed to is still mutable. You can call `Numbers.Add(1)` perfectly fine.
</details>

### Q10. Which is faster to access: `const` or `static readonly`?

A. `static readonly` because it's cached.  
B. `const` because the value is embedded directly in the instruction (no memory lookup).  
C. Identical performance.  
D. `static readonly` because it is heap-based.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`const` is slightly faster because the value is hardcoded into the IL instructions (like a literal), whereas `readonly` requires a field lookup (memory access) at runtime.
</details>

### Q11. Can you use a `const` variable in a case label of a switch statement?

A. Yes.  
B. No.  
C. Only if it is private.  
D. Only if it is an integer.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
Since `const` values are known at compile time, they act just like literals and are valid (and common) in switch case labels.
</details>

### Q12. Why can't you write `public const DateTime Time = DateTime.Now;`?

A. Because DateTime is a struct.  
B. Because `DateTime.Now` is calculated at runtime, and `const` requires a compile-time value.  
C. Because it is missing `new`.  
D. You can, this is valid.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`const` values must be deterministic at compile time. `DateTime.Now` relies on execution time, so it must be stored in a `readonly` (or `static readonly`) field, not `const`.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
