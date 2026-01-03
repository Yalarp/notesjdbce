# 07_Interfaces_Fundamentals – MCQs

## EASY MCQs

### Q1. Can an interface contain fields?
A. Yes  
B. No  
C. Only static fields  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Interfaces define behavior (methods, properties, events), not state. They cannot contain instance fields (variables).
</details>

### Q2. By default, interface members are:
A. `private`  
B. `public`  
C. `protected`  
D. `internal`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Interface members are implicitly public because the purpose of an interface is to be exposed by the implementing class.
</details>

### Q3. Can a class implement multiple interfaces?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
C# supports multiple inheritance for interfaces (a class can implement many), unlike classes (which only support single inheritance).
</details>

### Q4. Can you create an instance of an interface?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Like abstract classes, interfaces are contracts and cannot be instantiated directly with `new`. You instantiate the class that *implements* the interface.
</details>

### Q5. A class implementing an interface must:
A. Implement all interface members.  
B. Implement at least one member.  
C. Be abstract.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Unless the class is abstract, it is contractually obligated to provide implementations for ALL members defined in the interface.
</details>

---

## MEDIUM MCQs

### Q6. Which interface is used for cloning objects?
A. `ICopyable`  
B. `IClonable`  
C. `ICloneable`  
D. `IDuplicatable`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`ICloneable` is the standard .NET interface that defines the `Clone()` method.
</details>

### Q7. Implicit interface implementation requires the method to be:
A. `public`  
B. `private`  
C. `protected`  
D. `virtual`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
When implementing an interface normally (implicitly), the method must be `public` to satisfy the interface contract.
</details>

### Q8. Explicit interface implementation is useful when:
A. You want to make the method public.  
B. Multiple interfaces have methods with the same name/signature.  
C. You want to override a base method.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Explicit implementation (`void I1.Method()`) resolves name collisions by allowing the class to distinct implementations for `I1.Method` vs `I2.Method`.
</details>

### Q9. Can an interface inherit from another interface?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, interfaces can inherit from other interfaces. The implementing class must then implement members from *both* interfaces.
</details>

### Q10. `MemberwiseClone()` performs a:
A. Deep Copy  
B. Shallow Copy  
C. Reference Copy  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It copies the non-static fields of the current object to the new object. If a field is a value type, a bit-by-bit copy is performed. If a field is a reference type, the reference is copied (shallow copy).
</details>

---

## HARD MCQs

### Q11. Can you access an explicitly implemented interface member through a class instance?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Explicit implementations are private to the class instance. They are ONLY accessible via a reference to the Interface type (e.g., `((IFace)obj).Method()`).
</details>

### Q12. If a base class implements an interface method but not virtually, can a derived class re-implement the interface?
A. Yes, using `new`.  
B. Yes, by adding the interface to its declaration again.  
C. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is called "Interface Re-implementation". If `Derived : Base, IInterface`, the Derived class can provide a new implementation for the interface methods, effectively ignoring the Base class's implementation for interface calls on the Derived instance.
</details>

### Q13. Which access modifier is allowed on explicitly implemented interface methods?
A. `public`  
B. `private`  
C. None  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
You cannot specify an access modifier (not even public). They are inherently private to the class scope and public to the interface scope.
</details>

### Q14. Can an interface have a constructor?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Attempting to define a constructor in an interface results in a compile-time error "Interfaces cannot contain instance constructors".
</details>

### Q15. Does an abstract class implementing an interface have to implement all methods?
A. Yes.  
B. No, it can mark them abstract.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
An abstract class can choose to map interface methods to abstract methods, forcing the concrete derived classes to provide the actual implementation.
</details>
