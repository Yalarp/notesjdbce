# 19_Operator_Overloading – MCQs

## EASY MCQs

### Q1. What is Operator Overloading?

A. Running multiple operators at once.  
B. Redefining the behavior of built-in operators (like `+`, `==`) for custom types (classes/structs).  
C. Removing operators from the language.  
D. Creating new operator symbols.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Operator overloading allows you to define how standard operators work with your own data types (e.g., adding two `Vector` objects).
</details>

### Q2. Which modifiers are REQUIRED for an operator overloading method?

A. `public`  
B. `static`  
C. `public static`  
D. `virtual`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
All operator overloads must be declared as `public static` methods.
</details>

### Q3. Which keyword is used to declare an operator overload?

A. `overload`  
B. `operator`  
C. `op`  
D. `override`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The syntax is `public static ReturnType operator OpSymbol(...)`.
</details>

### Q4. Can you overload the assignment operator behavior (`=`)?

A. Yes.  
B. No.  
C. Only for structs.  
D. Yes, if marked unsafe.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The assignment operator `=` cannot be overloaded. Its behavior (copying reference or value) is fixed by the CLR.
</details>

---

## MEDIUM MCQs

### Q5. If you overload `==` (equality), what other operator MUST you overload?

A. `+`  
B. `=`  
C. `!=` (inequality)  
D. `<`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Comparison operators must be overloaded in pairs. If you define `==`, you must also define `!=`, otherwise the compiler throws an error.
</details>

### Q6. Which method should you override when you overload `==` to ensure consistency?

A. `ToString()`  
B. `Equals(object)` and `GetHashCode()`  
C. `CompareTo()`  
D. `Dispose()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
To prevent unexpected behavior where `a == b` is true but `a.Equals(b)` is false, you should override `Equals`. Overriding `Equals` also requires overriding `GetHashCode` to keep collections working correctly.
</details>

### Q7. Can you overload `&&` and `||` directly?

A. Yes.  
B. No, but you can enable them by overloading `&`, `|`, `true`, and `false`.  
C. No, they are reserved.  
D. Yes, for boolean types only.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
These conditional logical operators are not overloadable directly. However, they are evaluated using `&` and `|` ops along with `true` and `false` operator overloads.
</details>

### Q8. What is the difference between `implicit` and `explicit` conversion operators?

A. `Implicit` requires a cast; `Explicit` happens automatically.  
B. `Implicit` happens automatically (safe); `Explicit` requires a cast (potentially unsafe/lossy).  
C. No difference.  
D. `Implicit` is for int, `Explicit` is for double.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`implicit` is used when conversion is always safe and no data is lost (`double` <- `float`). `explicit` is used when data might be lost or the conversion is not intuitive, requiring the user to cast (`(int)double`).
</details>

---

## HARD MCQs

### Q9. Can you overload the array indexer operator `[]` using operator overloading syntax?

A. Yes, `operator []`.  
B. No, use the Indexer syntax `this[...]` instead.  
C. Yes, but only for reading.  
D. Yes, in C# 11+.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`[]` is not overloaded via `operator` keyword. It is defined using the Indexer property syntax (`public Type this[int i]`).
</details>

### Q10. When overloading a binary operator (e.g., `+`), how many parameters does the method take?

A. 0  
B. 1  
C. 2  
D. 3  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Binary operators work on two operands (left and right), so they take exactly 2 parameters. (Unary operators take 1).
</details>

### Q11. Is it valid to modify the state of the operands inside an operator overload method (e.g., modify `a` inside `operator +(a, b)`)?

A. Yes, it's recommended.  
B. No, operators should generally return a NEW instance and leave operands unchanged (immutability principle).  
C. It causes a compile error.  
D. Yes, but only for reference types.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
While syntactically allowed (if operands are reference types), it is a very bad practice. Users expect `c = a + b` to leave `a` and `b` untouched. You should return a new object.
</details>

### Q12. Can you overload `new`?

A. Yes.  
B. No.  
C. Only in factory patterns.  
D. Yes, to change memory allocation.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The `new` operator (for instantiation) cannot be overloaded. Note: The `new` *modifier* (for hiding members) is different.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
