# 33_CSharp7_Out_Variables – MCQs

## EASY MCQs

### Q1. Before C# 7, how did you have to handle `out` parameters?
A. Declare the variable *before* calling the method.  
B. Declare the variable inside the method call.  
C. Use `var`.  
D. You didn't need them.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`int result; Method(out result);` was the required syntax, which was verbose and leaked the variable scope.
</details>

### Q2. What is the C# 7 Syntax for inline out variables?
A. `Method(out int result)`  
B. `Method(int result)`  
C. `Method(ref result)`  
D. `Method(new result)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
You can declare the type and name right inside the argument list: `int.TryParse(s, out int result)`.
</details>

### Q3. Can you use `var` with inline out variables?
A. No.  
B. Yes, e.g., `out var result`.  
C. Only with strings.  
D. Only with arrays.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Type inference works perfectly: `out var result` infers the type from the method signature.
</details>

### Q4. What is a "Discard" in C#?
A. A variable you delete.  
B. A special variable `_` (underscore) used when you don't care about the return value/out parameter.  
C. A deleted file.  
D. A trash can.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Example: `int.TryParse(s, out _)` checks if the parsing is valid but ignores the actual number result.
</details>

### Q5. A Tuple in C# 7 allows you to:
A. Return multiple values from a method easily.  
B. Create a database.  
C. Throw multiple exceptions.  
D. Run parallel threads.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Lightweight grouping of values `(string Name, int Age)` without defining a separate class.
</details>

---

## MEDIUM MCQs

### Q6. What is the syntax for a "Named Tuple"?
A. `Tuple<int, string>`  
B. `(int Id, string Name)`  
C. `Tuple(int Id, string Name)`  
D. `[int Id, string Name]`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The parenthesis syntax `(Type name, Type name)` creates a ValueTuple with semantic names.
</details>

### Q7. How do you "Deconstruct" a tuple?
A. `var (x, y) = GetTuple();`  
B. `var tuple = GetTuple();`  
C. `x = tuple.Item1;`  
D. `Deconstruct(tuple);`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Deconstruction splits the tuple elements immediately into separate local variables `x` and `y`.
</details>

### Q8. Are ValueTuples (`(int, int)`) Reference Types or Value Types?
A. Reference Types (class).  
B. Value Types (struct).  
C. Interface.  
D. Dynamic.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
They are `System.ValueTuple` structs, allocating on the stack (unlike the old `System.Tuple` which was a class/heap object). This improves performance.
</details>

### Q9. What happens if you compare two tuples `(1, 2) == (1, 2)`?
A. False (reference mismatch).  
B. True (structured value equality).  
C. Compilation Error.  
D. Runtime Exception.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
C# 7.3+ supports `==` checking for tuples, comparing them element-by-element.
</details>

### Q10. What is the scope of an inline out variable declared in an `if` condition?
A. Only inside the `if` block.  
B. The outer scope surrounding the `if` statement.  
C. Global.  
D. No scope.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Wait! This is tricky. `if (Try(out int x)) { ... } return x;` IS VALID. The variable leaks into the enclosing block scope.
</details>

---

## HARD MCQs

### Q11. "System.Tuple" (old) vs "System.ValueTuple" (new C# 7).
A. Use System.Tuple always.  
B. Use System.ValueTuple (parenthesis syntax) for lightweight returns; use Class for public APIs.  
C. They are the same.  
D. ValueTuple is slower.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
ValueTuples are mutable structs with better performance characteristics for simple temporary grouping.
</details>

### Q12. Can you define extension methods for Tuples?
A. No.  
B. Yes, just like any other type.  
C. Only inside `System` namespace.  
D. Only for `Item1`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You can extend `(int, int)` directly. `public static void Print(this (int, int) t) ...`
</details>

### Q13. If you have a class `Point` with a `Deconstruct` method, what can you do?
A. Destroy it.  
B. Use positional pattern matching `var (x, y) = point`.  
C. Delete it from memory.  
D. Serialize it.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The compiler looks for `public void Deconstruct(out T1 x, out T2 y)` to enable tuple-like syntax unpacking for custom objects.
</details>

### Q14. What if tuple field names mismatch in assignment? `(int A, int B) t1 = (C: 1, D: 2);`
A. Error.  
B. It works. The names on the right side are ignored; only types and position matter.  
C. Warning.  
D. Runtime error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Tuple names are fundamentally compiler syntactic sugar metadata. The underlying types are just `int, int`.
</details>

### Q15. Why use `TryParse` pattern over `Parse`?
A. `TryParse` avoids Exceptions for invalid input, which is much faster/cleaner for user input flow.  
B. `Parse` is faster.  
C. `TryParse` throws exceptions.  
D. `Parse` handles nulls.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Handling exceptions for control flow is an anti-pattern (slow). `TryParse` returns bool(false) instead of `throw`, utilizing the `out` param for the result.
</details>
