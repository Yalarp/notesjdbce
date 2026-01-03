# 20_Strings_And_StringBuilder – MCQs

## EASY MCQs

### Q1. Strings in C# are:

A. Mutable (Changeable)  
B. Immutable (Unchangeable)  
C. Value Types  
D. Pointers  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Strings are immutable reference types. Once created, their content cannot be modified. Any modification creates a new string object.
</details>

### Q2. Which class is recommended for heavy string manipulation (e.g., inside loops)?

A. `String`  
B. `StringBuilder`  
C. `StringWriter`  
D. `StringBuffer`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`StringBuilder` (in `System.Text`) is mutable and designed for efficient string modification (appending, replacing) without creating intermediate objects.
</details>

### Q3. What is the syntax for String Interpolation?

A. `String.Format("...", arg)`  
B. `$"Hello {name}"`  
C. `@""`  
D. `#""`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The `$` prefix enables string interpolation, allowing variables to be embedded directly in the string within braces `{}`.
</details>

### Q4. What does the `@` symbol do before a string literal (e.g., `@"C:\Path"`)?

A. Encrypts the string.  
B. Makes it a Verbatim string (ignores escape characters like `\`).  
C. Makes it mutable.  
D. Formats it as currency.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The `@` creates a verbatim string literal, where backslashes are treated as literal characters rather than escape codes. This is useful for file paths.
</details>

---

## MEDIUM MCQs

### Q5. What is "String Interning"?

A. Compressing strings to save space.  
B. The process where the CLR stores only one copy of duplicate string literals to optimize memory.  
C. Converting string to char array.  
D. Encrypting strings in memory.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The CLR maintains an "intern pool". If a string literal is used multiple times, they all reference the same memory location to save space.
</details>

### Q6. Comparisons using `==` on strings check for:

A. Reference equality (Memory Address).  
B. Value equality (Content).  
C. Length equality.  
D. Type equality.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Although String is a reference type, the `==` operator is overloaded to compare the *values* (content) of the strings, not their references (unless cast to `object`).
</details>

### Q7. How does `StringBuilder` minimize performance overhead?

A. It uses the GPU.  
B. It modifies an internal character buffer in-place instead of creating new objects for every change.  
C. It compresses text.  
D. It runs on a separate thread.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`StringBuilder` uses a resizeable buffer. Appending data writes to this buffer. New memory is allocated only when the buffer is full (capacity is exceeded).
</details>

### Q8. Identify the valid Raw String Literal (C# 11+).

A. `$"..."`  
B. `@"..."`  
C. `"""..."""` (Triple quotes)  
D. `r"..."`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Raw string literals start and end with at least three double quotes (`"""`). They allow multi-line strings that ignore indentation whitespace.
</details>

---

## HARD MCQs

### Q9. What happens if you modify a string variable (`s = s + "a"`) that was pointing to an Interned string?

A. The interned string in the pool is modified, affecting all other variables using it.  
B. A new string is created on the heap; the interned string remains untouched.  
C. An exception is thrown.  
D. It converts to StringBuilder automatically.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Due to immutability, you cannot modify the interned string. The operation results in a NEW string object being created and assigned to `s`. The original string in the pool stays exactly as it was.
</details>

### Q10. Is `StringBuilder` thread-safe?

A. Yes, fully thread-safe.  
B. No, it is not thread-safe.  
C. Only if initialized with `true`.  
D. Yes, unlike String which is unsafe.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`StringBuilder` is not thread-safe. Concurrent modifications from multiple threads can corrupt its state. (Strings are thread-safe for reading because they are immutable).
</details>

### Q11. Consider `string s = new string("Hello".ToCharArray());`. Is `s` interned automatically?

A. Yes.  
B. No.  
C. Only in Release mode.  
D. Only if it is static.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Strings created dynamically (like using `new string(...)` or runtime concatenation) are NOT automatically added to the intern pool. Use `string.Intern(s)` to add them manually if needed.
</details>

### Q12. What does `StringBuilder.Capacity` represent vs `StringBuilder.Length`?

A. They are the same.  
B. `Length` is current characters; `Capacity` is allocated memory size before resizing is needed.  
C. `Length` is max size; `Capacity` is current size.  
D. `Capacity` is disk space.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`Length` is the actual number of characters currently held. `Capacity` is the size of the internal buffer. When Length > Capacity, the Capacity is automatically doubled (usually).
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
