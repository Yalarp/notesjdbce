# 24_Method_Overloading – MCQs

## EASY MCQs

### Q1. What is Method Overloading?
A. Replacing a method in a derived class.  
B. Defining multiple methods with the same name but different signatures.  
C. Hiding a private method.  
D. Calling a method recursively.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Method overloading is the ability to define multiple methods in the same class with the same name, provided they have different parameter lists.
</details>

### Q2. Which of the following is NOT a valid way to overload a method?
A. Changing the number of parameters.  
B. Changing the data type of parameters.  
C. Changing the order of parameter types.  
D. Changing only the return type.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
The return type alone is not part of the method signature for overloading purposes. You cannot have two methods differing *only* by return type.
</details>

### Q3. Can constructors be overloaded?
A. Yes.  
B. No.  
C. Only in abstract classes.  
D. Only static constructors.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Constructors are commonly overloaded to provide different ways to initialize an object (e.g., empty constructor vs. constructor with arguments).
</details>

### Q4. Is `void Foo(int x)` and `void Foo(ref int x)` a valid overload?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes. `int` and `ref int` are different signatures. The call site syntax (`Foo(a)` vs `Foo(ref a)`) distinguishes them clear enough for the compiler.
</details>

### Q5. Is `void Foo(ref int x)` and `void Foo(out int x)` a valid overload?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
No. At the CLR level (IL), `ref` and `out` are identical. They cannot coexist as overloads in the same class.
</details>

---

## MEDIUM MCQs

### Q6. How does the compiler resolve which overloaded method to call?
A. It picks the one declared last.  
B. It picks the one declared first.  
C. It attempts to find an exact match, then tries implicit conversions.  
D. It picks the one with the fewest parameters.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The compiler looks for the "best match". An exact type matches first. If none, it checks for compatible implicit conversions (e.g., `int` -> `long`).
</details>

### Q7. What happens if you pass `null` to an overloaded method `void Print(string s)` and `void Print(MyClass c)`?
A. It calls `Print(string)`.  
B. It calls `Print(MyClass)`.  
C. It throws a NullReferenceException.  
D. It causes an "Ambiguous call" compile error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
Since `null` is valid for both `string` and `MyClass` (both are reference types), the compiler cannot decide which one strictly applies, triggering an ambiguity error. You must cast the null: `Print((string)null)`.
</details>

### Q8. Does method overloading support inheritance?
A. No, overloading only works in a single class.  
B. Yes, a derived class can overload a method defined in the base class.  
C. No, that is called overriding.  
D. Only if the method is static.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A derived class can introduce a *new* overload of a method that shares the same name as a base method. Use normally requires resolving which one is intended, but they coexist.
</details>

### Q9. Which keyword is associated with Method Overriding, NOT Overloading?
A. `overload`  
B. `override`  
C. `new`  
D. `static`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`virtual` and `override` are used for runtime polymorphism (Overriding). Overloading is compile-time polymorphism and needs no special keyword (other than just defining the methods).
</details>

### Q10. If you have `Foo(int x)` and `Foo(double x)`, and you call `Foo(5)`, which one is called?
A. `Foo(int)`  
B. `Foo(double)`  
C. Ambiguous error.  
D. Both.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`5` is an `int` literal. `Foo(int)` is an exact match. `Foo(double)` would require an implicit conversion. The exact match wins.
</details>

---

## HARD MCQs

### Q11. Consider `void M(object o)` and `void M(string s)`. If you call `M("hello")`, which is called?
A. `M(object)`  
B. `M(string)`  
C. Ambiguous.  
D. Runtime error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Standard overload resolution rule: "More specific is better". `string` is more specific than `object`, so `M(string)` is chosen.
</details>

### Q12. You have `Foo(int x, double y)` and `Foo(double x, int y)`. You call `Foo(1, 1)`. What happens?
A. `Foo(int, double)` is called.  
B. `Foo(double, int)` is called.  
C. Compile Error: Ambiguous invocation.  
D. It depends on the return type.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
For `Foo(int, double)`, the second arg needs conversion. For `Foo(double, int)`, the first arg needs conversion. Neither is strictly "better" (one conversion each), so it is ambiguous.
</details>

### Q13. Can `params` parameter methods be overloaded with regular arrays?
e.g. `Foo(params int[] x)` vs `Foo(int[] x)`
A. Yes.  
B. No, they are considered duplicate signatures.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`params` is syntactic sugar for the caller. Inside the method, it is just `int[]`. Thus, the signature is effectively `Foo(int[] x)` for both, causing a collision.
</details>

### Q14. What is the interaction between Optional Parameters and Overloading?
A. They work perfectly together.  
B. They can easily lead to "Betterness" ambiguity warnings or errors.  
C. Optional parameters disable overloading.  
D. Overloading disables optional parameters.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If you have `Foo(int x)` and `Foo(int x, int y = 0)`, calling `Foo(5)` is valid for BOTH. This creates ambiguity or tricky resolution rules. It is generally advised to avoid mixing extensive overloading with optional parameters.
</details>

### Q15. Is Method Overloading compile-time or runtime polymorphism?
A. Runtime.  
B. Compile-time.  
C. Both.  
D. Neither.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Overloading is resolved by the compiler (Static Binding). The compiler decides exactly which method to jump to based on the argument types known at compile time. Overriding is runtime (Dynamic Binding).
</details>
