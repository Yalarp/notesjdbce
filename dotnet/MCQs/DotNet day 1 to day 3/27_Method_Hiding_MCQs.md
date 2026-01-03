# 27_Method_Hiding – MCQs

## EASY MCQs

### Q1. Which keyword is used to hide a base class method in a derived class?
A. `override`  
B. `abstract`  
C. `new`  
D. `hide`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `new` keyword explicitly tells the compiler that you intend to hide the inherited member with a new implementation.
</details>

### Q2. Does method hiding allow polymorphism?
A. Yes, full polymorphism.  
B. No, the method called depends on the reference type, not the runtime object.  
C. Yes, if the method is private.  
D. Only if `base` is called.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Method hiding (using `new`) breaks the polymorphic chain. If you access the object via a Base reference, the Base method is called, not the Derived one.
</details>

### Q3. What is the keyword pair required for Method Overriding?
A. `virtual` and `new`  
B. `static` and `void`  
C. `virtual` and `override`  
D. `abstract` and `new`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
To override a method (enable polymorphism), the base method must be marked `virtual` (or abstract) and the derived method must use `override`.
</details>

### Q4. What happens if you hide a method without using the `new` keyword?
A. Compilation Error.  
B. It becomes an override automatically.  
C. Compiler Warning (but it compiles and hides).  
D. Runtime Exception.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The compiler assumes you intended to hide it but warns you that you should be explicit by adding the `new` keyword. The behavior is exactly that of hiding.
</details>

### Q5. Can you hide a static method?
A. Yes.  
B. No.  
C. Only if it is private.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, static members can be hidden in a derived class using `new`. They cannot be overridden (logic doesn't apply to instances), but hiding works.
</details>

---

## MEDIUM MCQs

### Q6. Which reference type determines the method call in Method Hiding?
A. The variable's declared type (Reference Type).  
B. The actual object's type (Runtime Type).  
C. The first interface it implements.  
D. It is random.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
With hiding (`new`), the compiler binds the call based on the variable's type (Static Binding). If `Base b = new Derived()`, `b.Method()` calls `Base.Method`.
</details>

### Q7. Can you override a method that was marked `new` (hidden) in the parent?
A. No, `new` breaks the virtual chain.  
B. Yes, if the `new` method is also marked `virtual`.  
C. Yes, always.  
D. No, never.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You can start a *new* polymorphic hierarchy. The method `public new virtual void Method()` hides the old one but allows further derivation to override THIS new version.
</details>

### Q8. How do you call a hidden base method from the derived class?
A. `this.Method()`  
B. `parent.Method()`  
C. `base.Method()`  
D. `super.Method()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `base` keyword allows access to the immediate parent's members, bypassing the hiding in the current class.
</details>

### Q9. Can fields (variables) be hidden?
A. Yes, using `new`.  
B. No, fields cannot be same name.  
C. Yes, using `override`.  
D. Only static fields.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Fields cannot be overridden (virtual properties can be, but not fields), but they CAN be hidden using the `new` keyword.
</details>

### Q10. What does `sealed override` do?
A. Hides the method.  
B. Overrides the base method but prevents further derived classes from overriding it again.  
C. Prevents the method from being called.  
D. compile error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It continues the polymorphism from the parent but stops it for any future children.
</details>

---

## HARD MCQs

### Q11. Consider `Class A { virtual M() }`, `Class B : A { override M() }`, `Class C : B { new M() }`.
If `A obj = new C(); obj.M();` is called, what executes?
A. A.M()  
B. B.M()  
C. C.M()  
D. Ambiguous.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`obj` is of type `A`. `A.M` is virtual. The runtime looks for the *most derived override*. `B` overrides it. `C` *hides* it (disconnects). So the polymorphism chain stops at `B`. Thus `B.M()` is called.
</details>

### Q12. Difference between `new` vs `override` regarding ABI (Application Binary Interface)?
A. No difference.  
B. `new` creates a new slot in the vtable; `override` reuses/updates the existing slot.  
C. `new` is faster.  
D. `override` is static.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is the technical underpinning. Overriding updates the Virtual Method Table (vtable) entry so all calls go to the new code. Hiding creates a completely separate entry, leaving the old slot pointing to the old code.
</details>

### Q13. Can you hide a method that is not `virtual`?
A. Yes.  
B. No, only virtual methods can be hidden.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes. You can hide *any* inherited member (virtual or not) using `new`. It simply declares "For this class and its children, this name means something else."
</details>

### Q14. If `Child` hides `Parent.Method` but casts itself to `Parent`, can it access the hidden method?
```csharp
((Parent)child).Method();
```
A. Yes, it calls the Parent Method.  
B. No, it calls the Child Method.  
C. Runtime Error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
This is a standard way to bypass hiding. Casting to the Base type forces the compiler to bind to the Base method (since it's not overridden).
</details>

### Q15. Why use Method Hiding usually?
A. To fix bugs in base class.  
B. To perform versioning (e.g. Base adds a method that clashes with your existing method names).  
C. To improve performance.  
D. To implement Interface logic.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Hiding is often a result of API evolution—e.g., you have a `Run()` method, and the library you inherit from later adds a `Run()` method. Using `new` preserves your existing behavior while acknowledging the collision.
</details>
