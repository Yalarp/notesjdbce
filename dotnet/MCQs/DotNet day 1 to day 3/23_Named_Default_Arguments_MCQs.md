# 23_Named_Default_Arguments – MCQs

## EASY MCQs

### Q1. What is the correct syntax for defining a default argument?
A. `void Method(int x default 0)`  
B. `void Method(int x = 0)`  
C. `void Method(optional int x)`  
D. `void Method(int x : 0)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Default arguments are defined by assigning a constant value to the parameter in the method signature, e.g., `int x = 0`.
</details>

### Q2. Where must optional parameters (default arguments) be placed in the parameter list?
A. At the beginning.  
B. In the middle.  
C. At the end, after all required parameters.  
D. Anywhere.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Parameters with default values must come after all required parameters (except for `params` arrays) to avoid ambiguity in positional calls.
</details>

### Q3. Which syntax allows you to pass arguments in any order by specifying the parameter name?
A. `Method(value -> paramName)`  
B. `Method(paramName: value)`  
C. `Method(paramName = value)`  
D. `Method(value as paramName)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Named arguments use the syntax `parameterName: value`, enabling you to pass arguments out of order or skip optional ones.
</details>

### Q4. Can you mix positional arguments and named arguments in a single call?
A. No.  
B. Yes, but positional arguments must come first.  
C. Yes, but named arguments must come first.  
D. Yes, in any mixed order indiscriminately.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You can use both, but positional arguments must precede named arguments. Once you start using named arguments, you typically continue using them for the rest of the list (though C# 7.2 relaxed this slightly if the positions are correct, the general rule is positional result first).
</details>

### Q5. What kind of value is required for a default parameter?
A. Any variable.  
B. A database call result.  
C. A compile-time constant.  
D. A `new` object instantiation.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Default values must be compile-time constants (strings, numbers, null, enums, consts) because the compiler bakes this value into the calling code.
</details>

---

## MEDIUM MCQs

### Q6. Why must you be careful when changing the default value of a parameter in a public library?
A. It causes a syntax error.  
B. The old value is "baked into" existing compiled client code until they recompile.  
C. It resets the version number of the assembly.  
D. Default values cannot be changed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The default value is substituted at the *call site* during compilation. If the library changes the default but the client application isn't recompiled, the client will continue passing the *old* default value.
</details>

### Q7. How can named arguments improve readability for boolean parameters?
A. You can avoid booleans entirely.  
B. `Method(true)` is clearer than `Method(isRecursive: true)`.  
C. `Method(isRecursive: true)` clearly states what `true` stands for.  
D. Named arguments make the code run faster.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Passing a bare `true` or `false` is often confusing ("Blind Bool"). Named arguments clarify the intent: `Save(force: true)`.
</details>

### Q8. Which attribute allows the compiler to automatically pass the file path of the caller?
A. `[CallerMemberName]`  
B. `[CallerFilePath]`  
C. `[CallerLineNumber]`  
D. `[SourcePath]`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`[CallerFilePath]` is an attribute applied to an optional parameter. The compiler injects the full path of the source file calling the method.
</details>

### Q9. Can you use `DateTime.Now` as a default parameter value?
A. Yes.  
B. No.  
C. Only if it is static.  
D. Only in async methods.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`DateTime.Now` is evaluated at runtime, not compile time. Default parameters require compile-time constants. You must use `null` or a specific structure strategy to handle runtime defaults.
</details>

### Q10. What is the benefit of using Named Arguments when dealing with many optional parameters?
A. You can skip the ones in the middle you don't care about.  
B. You can declare new variables in the call.  
C. It allows dynamic typing.  
D. It prevents method overloading.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
If a method has 5 optional parameters and you only want to set the 4th one, named arguments let you specify just that one (`param4: value`), leaving the others at their defaults. Use of positional arguments would require you to provide values for 1, 2, and 3 as well.
</details>

---

## HARD MCQs

### Q11. Is the following call valid?
```csharp
void Test(int a, int b = 5, int c = 10) {}
// Call:
Test(1, c: 20);
```
A. No, you must provide `b`.  
B. Yes, `a` is 1, `b` takes default 5, `c` becomes 20.  
C. No, named arguments cannot follow positional ones.  
D. Yes, but `c` ends up being 5.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is a primary use case. You provide required positional args, skip the middle optional arg (`b`), and specify the last one (`c`) by name.
</details>

### Q12. If a method overload conflict occurs between a method with default parameters and a method with exact parameters, which does the compiler prefer?
A. The one with default parameters.  
B. The one with exact parameters (no optional expansion needed).  
C. It throws an ambiguity error.  
D. The one defined first in the class.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The compiler generally prefers an exact signature match over one that requires filling in optional parameters. However, poor design can still lead to ambiguity.
</details>

### Q13. Can attributes like `[CallerMemberName]` be used on parameters without default values?
A. Yes.  
B. No.  
  
<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
These attributes rely on the parameter being optional. The compiler "fills in" the default value with the specific info (member name, line number). If you don't provide a default value (e.g., `string name = ""`), the compiler cannot treat it as optional.
</details>

### Q14. What happens if you try to use a named argument that refers to a parameter that doesn't exist?
A. It is ignored.  
B. Compiler references a global variable.  
C. Compilation Error.  
D. Runtime Error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Named arguments are validated at compile time. If the name doesn't match a parameter in the method, it is an error.
</details>

### Q15. In what order are arguments evaluated if named arguments are used to reorder them?
```csharp
Method(b: GetB(), a: GetA()); 
```
A. `GetB()` then `GetA()` (Source order).  
B. `GetA()` then `GetB()` (Target method parameter order).  
C. Undefined.  
D. Parallel.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Arguments are evaluated in the order they appear at the call site (left to right), even if they correspond to different parameter indices in the target method.
</details>
