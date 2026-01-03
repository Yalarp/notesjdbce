# 35_CSharp7_Ref_Returns – MCQs

## EASY MCQs

### Q1. What does a "Ref Return" (`ref return`) allow a method to do?
A. Return a value copy.  
B. Return a reference (pointer-like alias) to a storage location (variable/field/array slot) rather than the value itself.  
C. Return an error.  
D. Return void.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It allows the caller to get a reference to the data and potentially modify it directly.
</details>

### Q2. How do you accept a ref return result?
A. `int y = GetRef();`  
B. `ref int y = ref GetRef();`  
C. `var y = GetRef();`  
D. `pointer y = GetRef();`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You must use `ref` local variable declaration to maintain the reference connection. If you just say `int y`, you get a copy.
</details>

### Q3. "Local Functions" are:
A. Functions defined inside a namespace.  
B. Functions declared inside another method body.  
C. Functions that only run locally on the machine.  
D. Private methods.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
They are private helpers scoped strictly to the containing method.
</details>

### Q4. Can a Local Function access variables from the containing method?
A. No.  
B. Yes (Closure).  
C. Only static variables.  
D. Only constants.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
They capture the context, making them very convenient for small helpers that need access to local state without passing arguments.
</details>

### Q5. Why use Ref Returns?
A. Syntax sugar.  
B. Performance optimization (avoiding copying large structs) and allowing modification of collection internals.  
C. Encryption.  
D. Database access.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If a `struct` is 100 bytes, returning it by value copies 100 bytes. Returning by ref copies 4/8 bytes (address).
</details>

---

## MEDIUM MCQs

### Q6. Can you return a reference to a local variable declared inside the method?
A. Yes.  
B. No.  
C. Only if it is int.  
D. Only on weekends.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
SAFETY RULE: You cannot return a ref to the stack frame that is about to pop (die). You can only return refs to fields, array elements, or incoming ref settings that live *longer* than the method.
</details>

### Q7. Local Functions vs Lambdas (`Func<>`). Which is generally more performant?
A. Lambdas.  
B. Local Functions.  
C. They are identical.  
D. Lambdas are allocated on stack.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Lambdas require instantiating a Delegate object (heap allocation). Local Functions compiled structurally (often just a jump code or private method) avoid this delegate overhead.
</details>

### Q8. Ref Locals: `ref int x = ref array[0]; x = 99;` What happens to `array[0]`?
A. Nothing.  
B. It becomes 99.  
C. Error.  
D. Arrays are immutable.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`x` IS an alias for the memory slot `array[0]`. Writing to `x` writes to the array.
</details>

### Q9. Where is the best place to define a recursive helper function?
A. Private method in class.  
B. Local Function inside the method that needs it.  
C. Global public method.  
D. Lambda.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Keeps validity scope tight (Encapsulation) and handles recursion more cleanly (and performantly) than lambdas.
</details>

### Q10. `static` Local Functions (C# 8) ensure:
A. They run faster.  
B. They cannot capture local variables (state) from the enclosing method.  
C. They are public.  
D. They are singletons.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Adding `static` prevents accidental closure capture, ensuring the function is pure/isolated, which can save allocation of the closure class.
</details>

---

## HARD MCQs

### Q11. Can `ref` returns be used with Properties?
A. No.  
B. Yes, `ref` returns properties.  
C. Only getters.  
D. Only setters.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`public ref int Value => ref _storage;` allows the caller to assign values via the property! `obj.Value = 5;` (if it returns ref).
</details>

### Q12. `ref readonly` return:
A. Returns a reference (fast, no copy) but prevents modification.  
B. Returns a copy.  
C. Returns nothing.  
D. Error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Crucial for large readonly structs (like strict Data structures) where you want performance of passing by reference but immutability safety.
</details>

### Q13. Local functions can be generic?
A. No.  
B. Yes. `void Helper<T>(T item) { ... }`  
C. Only if the outer method is generic.  
D. Only integers.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
They support full method capabilities including generics, params, etc.
</details>

### Q14. Can you use `yield return` (Iterators) inside a Local Function?
A. No.  
B. Yes.  
C. Only in Lambdas.  
D. Only in Main.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Yes. This is often used to valid arguments eagerly in the outer method, then return the iterator from the local function deferredly.
</details>

### Q15. "Ref Conditional Operator": `ref (cond ? ref a : ref b)`
A. Syntax error.  
B. Valid in newer C#. Returns reference to either variable.  
C. Returns value.  
D. Illegal logic.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Supported in C# 7.2+. Allows conditional reference logic.
</details>
