# 08_Interfaces_CSharp8_Features – MCQs

## EASY MCQs

### Q1. Which major feature was added to interfaces in C# 8.0?
A. Private fields  
B. Default Interface Implementations  
C. Constructors  
D. Destructors  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
C# 8.0 allows interfaces to provide a body (implementation) for methods, making them "default methods".
</details>

### Q2. Can interfaces now have static members (methods/fields)?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, C# 8+ allows static methods and fields in interfaces, often used for utility methods related to the interface.
</details>

### Q3. If a class implements an interface but does not implement a default method, what happens?
A. Compile Error.  
B. It uses the default implementation defined in the interface.  
C. Runtime Error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is the primary benefit: you can add new methods to an interface with default implementations without breaking existing classes that implement that interface.
</details>

### Q4. Can a default interface method be overridden?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
A class can facilitate its own implementation of the method, which effectively overrides the interface's default logic.
</details>

### Q5. To access a default interface method, you must use:
A. The class instance directly.  
B. An interface reference.  
C. A static call.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Default implementations are not added to the class's public API directly. You must cast the object to the interface type to invoke the default method.
</details>

---

## MEDIUM MCQs

### Q6. Can interfaces have `private` methods in C# 8+?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, private methods are allowed to help structure the code of default implementations (e.g., helper methods used by the public default methods).
</details>

### Q7. What is the "Diamond Problem" resolution in C# interfaces?
A. It is not allowed; compile error.  
B. The compiler picks the first one.  
C. The class must explicitly implement the method to resolve ambiguity.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
If a class inherits from two interfaces that both provide a default implementation for the same method name/signature, the compiler requires the class to implement that method itself to clarify which behavior is desired.
</details>

### Q8. Are default interface methods `virtual` by default?
A. Yes  
B. No, they are sealed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
They are effectively virtual because implementing classes are allowed to override them.
</details>

### Q9. Can you mark a default interface method as `sealed`?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, if you want to prevent implementing classes (or derived interfaces) from overriding the default behavior.
</details>

### Q10. Accessing a static field in an interface requires:
A. An instance of an implementing class.  
B. The Interface type name.  
C. Reflection.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Like static members in classes, they belong to the type. Access them via `InterfaceName.FieldName`.
</details>

---

## HARD MCQs

### Q11. Which framework version is required for Default Interface Methods?
A. .NET Framework 4.7  
B. .NET Core 2.0  
C. .NET Core 3.0 or .NET 5+  
D. .NET Standard 2.0  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The runtime support for default interface methods was added in the .NET Core 3.0 runtime. It is not supported on the legacy .NET Framework.
</details>

### Q12. Can a default interface method access `this`?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, `this` refers to the instance of the class (or struct) that is implementing the interface. This allows default methods to call other methods on the interface.
</details>

### Q13. `interface I { void M() => ... }` class `C : I { }`. Is `new C().M()` valid?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
No. `M()` is not a member of class `C`. It is a member of interface `I`. You must use `((I)new C()).M()`.
</details>

### Q14. Can an interface provide a default implementation for a property?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, interfaces can provide default implementations for property getters and setters using the same syntax as methods.
</details>

### Q15. Why might you prefer an Abstract Class over Interface Defaults?
A. To support multiple inheritance.  
B. To define instance fields (state).  
C. To allow private members.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Interfaces still cannot hold instance state (fields). If your base type needs to manage variable data/state directly, an abstract class is still the correct choice.
</details>
