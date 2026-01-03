# 22_Method_Parameters – MCQs

## EASY MCQs

### Q1. What is the default parameter passing mechanism in C#?
A. Pass by Reference  
B. Pass by Value  
C. Pass by Pointer  
D. Pass by Output  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
By default, arguments in C# are passed by value. A copy of the data is passed to the method.
</details>

### Q2. Which keyword requires the variable to be initialized BEFORE passing it to the method?
A. `out`  
B. `ref`  
C. `params`  
D. `this`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `ref` keyword requires the variable to be assigned a value before it is passed to the method.
</details>

### Q3. Which keyword allows a method to return multiple values via parameters?
A. `return`  
B. `void`  
C. `out`  
D. `new`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `out` keyword allows a method to assign values to parameters that are reflected back in the caller, effectively returning multiple results.
</details>

### Q4. Where must the `params` parameter be placed in a method signature?
A. It must be the first parameter.  
B. It can be anywhere.  
C. It must be the last parameter.  
D. It depends on the return type.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
If a method uses `params` to accept a variable number of arguments, it must be the last parameter in the list.
</details>

### Q5. What is the primary purpose of the `in` parameter modifier?
A. To allow modification of the argument.  
B. To pass arguments by reference but prevent modification (Read-Only).  
C. To force the argument to be initialized inside the method.  
D. To allow null values.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`in` passes the argument by reference (efficient for large structs) but ensures it cannot be modified by the called method (read-only).
</details>

---

## MEDIUM MCQs

### Q6. Can you have multiple `params` arrays in a single method definition?
A. Yes, as many as needed.  
B. No, only one `params` array is allowed.  
C. Yes, provided they are different types.  
D. Yes, if they are optional.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A method can have only one `params` keyword, and it must be the final parameter.
</details>

### Q7. What happens if a method with an `out` parameter returns without assigning a value to that parameter?
A. The parameter gets a default value.  
B. The compiler throws an error.  
C. It runs effectively but the value is null.  
D. It throws a Runtime Exception.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is a compile-time requirement that any `out` parameter MUST be assigned a value within the method before it returns.
</details>

### Q8. Which statement is true about `ref` and `out` concerning method overloading?
A. `ref` and `out` are treated as different signatures; you can overload based on them.  
B. You cannot overload a method solely based on the difference between `ref` and `out`.  
C. You can overload them only if the return types are different.  
D. `ref` cannot be overloaded at all.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
At the CLR level, `ref` and `out` are implemented similarly. Therefore, C# does not allow overloading methods if the only difference is `ref` vs `out`.
</details>

### Q9. When passing a Reference Type (like a class) by value, what is copied?
A. The entire object is deep copied.  
B. The reference (pointer) to the object is copied.  
C. Nothing is copied.  
D. The properties are copied to a new object.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Passing a reference type by value copies the reference. Both the caller and the method point to the same object on the heap, but if the method reassigns the parameter to a `new` object, the caller's variable is NOT affected.
</details>

### Q10. What data type is the parameter marked with `params` treated as inside the method?
A. A List  
B. An Array  
C. A Dictionary  
D. A String  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Inside the method, the `params` parameter behaves exactly like a single-dimensional array of the specified type.
</details>

---

## HARD MCQs

### Q11. Which of the following allows a method to return a reference to a variable storage slot (Ref Return)?
```csharp
public ref int GetCounter() { ... }
```
A. Yes, C# 7.0+ supports ref returns.  
B. No, methods can only return values.  
C. Only if the method is static.  
D. Only for struct types.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
C# supports `ref` returns, allowing a method to return a reference to a variable (like an array element or field) rather than a copy of its value, allowing the caller to modify it.
</details>

### Q12. Why would you use `in` for a large `struct`?
A. To make it mutable.  
B. To avoid the performance cost of copying the large struct while ensuring safety (immutability).  
C. To allow the struct to be null.  
D. `in` is only for classes, not structs.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Structs are value types and are copied by default. For large structs, this copying is expensive. `in` passes by reference (no copy) but strictly prevents modification, offering both performance and safety.
</details>

### Q13. Consider the following code. What is the output?
```csharp
void Change(ref int x) { x = 20; }
int a = 10;
Change(ref a);
Console.WriteLine(a);
```
A. 10  
B. 20  
C. 0  
D. Compilation Error  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`ref` passes the reference to the actual variable `a`. The modification inside `Change` directly updates `a`.
</details>

### Q14. Can you use the `params` keyword with a multi-dimensional array like `int[,]`?
A. Yes.  
B. No, only single-dimensional arrays (`int[]`) are supported.  
C. Yes, but only for jagged arrays.  
D. Only in unsafe context.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `params` keyword only works with single-dimensional arrays.
</details>

### Q15. Is the `in` keyword required at the call site?
```csharp
void Print(in int x) { ... }
int n = 5;
Print(n); // Is this valid?
```
A. No, it is optional at the call site.  
B. Yes, you must write `Print(in n)`.  
C. Yes, but only if `n` is a constant.  
D. No, `in` parameters cannot be called with variables.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Unlike `ref` and `out`, specifying `in` at the call site is generally optional, though it can be included for clarity or to resolve ambiguity.
</details>
