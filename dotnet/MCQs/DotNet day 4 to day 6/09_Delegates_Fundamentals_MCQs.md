# 09_Delegates_Fundamentals – MCQs

## EASY MCQs

### Q1. What is a delegate in C#?
A. A list of classes.  
B. A type-safe function pointer.  
C. An event handler.  
D. A reference to a variable.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A delegate is an object that holds a reference to a method (or list of methods) with a specific signature, acting as a pointer to that function.
</details>

### Q2. Does a delegate signature include the return type?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
For a method to be compatible with a delegate, both the parameters and the return type must match exactly (ignoring covariance/contravariance for advanced cases).
</details>

### Q3. Can a delegate point to a static method?
A. Yes  
B. No  
C. Only if the class is static  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Delegates can point to both static methods and instance methods.
</details>

### Q4. Which keyword is used to declare a delegate?
A. `event`  
B. `pointer`  
C. `delegate`  
D. `action`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `delegate` keyword defines a delegate type, e.g., `public delegate void MyDel();`.
</details>

### Q5. What happens if you invoke a null delegate?
A. Nothing happens.  
B. `NullReferenceException`.  
C. Compiler Error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Like any reference type, if the variable is null, trying to invoke it matches calling a method on a null object, raising an exception.
</details>

---

## MEDIUM MCQs

### Q6. When a delegate points to an instance method, what does it store?
A. Only the method address.  
B. The method entry point and the target object instance.  
C. The entire object class definition.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It stores the `Target` (the object on which to invoke the method) and the `Method` (the function pointer).
</details>

### Q7. `MyDelegate d = MethodName;` is shorthand for:
A. `MyDelegate d = new MyDelegate(MethodName);`  
B. `MyDelegate d = MethodName();`  
C. `MyDelegate d = (MyDelegate)MethodName;`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
C# 2.0 introduced implicit method group conversion, allowing you to assign a method directly without the `new DelegateType(...)` syntax.
</details>

### Q8. What class do all delegates inherit from implicitly?
A. `System.Object`  
B. `System.Function`  
C. `System.MulticastDelegate`  
D. `System.Action`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
All user-defined delegates derive from `System.MulticastDelegate` (which derives from `System.Delegate`).
</details>

### Q9. Can you pass a delegate as a parameter to another method?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
This is a primary use case (Callbacks). You pass the delegate, and the receiving method calls ("calls back") the method pointed to by the delegate.
</details>

### Q10. `delegate int Op(int x);`. Is `long Method(int x)` compatible?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
No. Return types must match. An `int` is expected, but the method returns `long`. Since `long` cannot be implicitly converted *down* to `int` safely without data loss, it is incompatible (and strictly, return types usually must match exactly or be covariant for reference types).
</details>

---

## HARD MCQs

### Q11. Which property of a delegate returns the object it targets (for instance methods)?
A. `TargetObject`  
B. `Instance`  
C. `Target`  
D. `Caller`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `Target` property returns the object instance invoked by the delegate. It is null for static methods.
</details>

### Q12. Are delegates reference types or value types?
A. Value Type  
B. Reference Type  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Delegates are classes (reference types).
</details>

### Q13. Can you define a delegate inside a class?
A. Yes  
B. No, only namespace level.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Delegates can be defined inside a class (nested type) or directly in a namespace.
</details>

### Q14. What is the difference between `Action<T>` and `Func<T>`?
A. Action returns void; Func returns a value.  
B. Action takes parameters; Func does not.  
C. They are identical.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`Action` represents a method that returns void. `Func` represents a method that returns a value (the last type parameter is the return type).
</details>

### Q15. Is it possible to change the method a delegate points to after creation?
A. Yes, delegates are mutable.  
B. No, delegates are immutable.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Delegate instances are immutable. When you combine them (`a += b`) or reassign them, you are actually creating a *new* delegate instance, similar to strings.
</details>
