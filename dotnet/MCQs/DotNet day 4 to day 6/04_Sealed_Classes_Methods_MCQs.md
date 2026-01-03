# 04_Sealed_Classes_Methods – MCQs

## EASY MCQs

### Q1. What does the `sealed` keyword prevent when applied to a class?
A. Instantiation  
B. Inheritance  
C. Method overloading  
D. Private access  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A `sealed` class cannot be used as a base class. It ends the inheritance chain.
</details>

### Q2. Can you instantiate a sealed class?
A. Yes  
B. No  
C. Only via reflection  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Sealed classes are fully functional concrete classes; you can create objects of them using `new`. You just can't inherit from them.
</details>

### Q3. Which keyword is the opposite of `sealed` (conceptually)?
A. `static`  
B. `abstract`  
C. `private`  
D. `void`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`abstract` implies "must be inherited to be useful." `sealed` implies "cannot be inherited." They are opposites.
</details>

### Q4. Can a sealed class contain abstract methods?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Abstract methods require a derived class to implement them. Since a sealed class cannot have derived classes, having abstract methods would be a paradox (and is a compile error).
</details>

### Q5. Can you use `sealed` on a normal (non-overridden) method?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You can only seal a method that is an `override` of a virtual/abstract method. You cannot "seal" a standard method because standard methods are already non-virtual (not overridable) by default.
</details>

---

## MEDIUM MCQs

### Q6. Which famous .NET class is sealed?
A. `System.Object`  
B. `System.String`  
C. `System.Exception`  
D. `System.Collections.ArrayList`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `String` class is sealed for security, performance, and immutability reasons. You cannot inherit from String.
</details>

### Q7. Why would you seal a virtual method override?
A. To allow further overriding.  
B. To prevent further overriding in subsequent derived classes.  
C. To hide it.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If a class overrides a method but wants to stop the polymorphism chain there (ensuring no further subclasses change this specific behavior), it uses `sealed override`.
</details>

### Q8. Does `sealed` improve performance?
A. Yes, slightly.  
B. No, it's purely for design.  
C. It decreases performance.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The compiler (JIT) can sometimes optimize calls to sealed members or classes (e.g., removing virtual table lookups/inlining) because it knows there are no other possible overrides.
</details>

### Q9. `sealed class A : B`. Is this valid?
A. No, sealed classes cannot inherit.  
B. Yes, sealed classes can inherit from others.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A sealed class can act as a child (inherit from B), it just cannot act as a parent.
</details>

### Q10. Can you use `new` on a method in a subclass of a sealed class?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You cannot create a subclass of a sealed class AT ALL. So the question is moot—this code wouldn't exist.
</details>

---

## HARD MCQs

### Q11. Which access modifier is effectively implied if a class is sealed?
A. Method overrides become effectively sealed.  
B. All members become private.  
C. All members become static.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Since you cannot derive from the class, any `virtual` methods it might define or `override` essentially behave as if they are sealed for the future, as no subclasses can exist to override them.
</details>

### Q12. Can a `private` method be sealed?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`private` methods cannot be virtual/overridden anyway. `sealed` applies to overrides. Thus, they don't combine.
</details>

### Q13. Can `structs` be inherited from?
A. Yes.  
B. No, structs are implicitly sealed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
In C#, structs are value types and are implicitly sealed. You cannot inherit from a struct (though they can implement interfaces).
</details>

### Q14. Is it possible to have `protected` members in a `sealed` class?
A. Yes, but it generates a compiler warning.  
B. No, compiler error.  
C. Yes, and it is useful.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The compiler warns (CS0628) because `protected` implies "accessible to derived classes". Since a sealed class cannot have derived classes, `protected` is functionally equivalent to `private`, likely indicating a mistake in logic.
</details>

### Q15. Can extension methods be applied to sealed classes?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Extension methods are often the *only* way to "add" functionality to a sealed class (like `string`), since inheritance is blocked.
</details>
