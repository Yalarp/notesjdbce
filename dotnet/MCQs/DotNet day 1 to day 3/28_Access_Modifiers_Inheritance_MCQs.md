# 28_Access_Modifiers_Inheritance – MCQs

## EASY MCQs

### Q1. Which access modifier restricts access strictly to the containing class?
A. `public`  
B. `internal`  
C. `private`  
D. `protected`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`private` is the most restrictive modifier. Members marked private are not accessible outside the class body, not even to derived classes.
</details>

### Q2. Which access modifier allows access in the class and its derived classes?
A. `private`  
B. `internal`  
C. `protected`  
D. `static`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`protected` is designed specifically for inheritance, allowing subclasses to access base members while keeping them hidden from the rest of the world.
</details>

### Q3. What is the default access modifier for members of a class (if not specified)?
A. `public`  
B. `private`  
C. `internal`  
D. `protected`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If you don't specify a modifier for a field, method, or property in a class, it defaults to `private`.
</details>

### Q4. Which modifier allows access anywhere within the same assembly (project)?
A. `protected`  
B. `internal`  
C. `private`  
D. `extern`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`internal` makes the member public *within the same assembly* (DLL/EXE) but inaccessible to other assemblies referencing it.
</details>

### Q5. Can a derived class access `private` members of its base class?
A. Yes, always.  
B. No, never directly.  
C. Yes, if in the same file.  
D. Only via Reflection.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Directly in code, `private` members are invisible to the specialized class. (Option D is technically true but "B" is the standard language rule answer).
</details>

---

## MEDIUM MCQs

### Q6. What does `protected internal` mean?
A. Protected AND Internal (Intersection).  
B. Protected OR Internal (Union).  
C. Accessible only in derived classes in the same assembly.  
D. It is invalid syntax.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`protected internal` is a Union: Accessible to anyone in the same assembly (Internal) OR any derived class in any assembly (Protected).
</details>

### Q7. What creates the "Protected AND Internal" behavior (accessible only to derived classes within the same assembly)?
A. `protected internal`  
B. `internal protected`  
C. `private protected`  
D. `secret`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`private protected` (introduced in C# 7.2) restricts access to derived classes that are ALSO in the same assembly.
</details>

### Q8. Can a derived class reduce the visibility of an overridden method?
e.g. Base: `public virtual`, Derived: `protected override`
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You cannot change the access modifier when overriding. If the base is public, the override must be public to ensure the contract is maintained.
</details>

### Q9. What is the default access modifier for a top-level `class`?
A. `public`  
B. `private`  
C. `internal`  
D. `protected`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Top-level types (classes, interfaces) default to `internal`. You must explicitly mark them `public` to expose them outside the assembly.
</details>

### Q10. What is the default access modifier for interface members?
A. `private`  
B. `public`  
C. `internal`  
D. `protected`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Until C# 8.0, all interface members were implicitly public. C# 8.0 introduced private/static members, but the standard declaration remains public by default.
</details>

---

## HARD MCQs

### Q11. Can you declare a class as `protected`?
A. Yes.  
B. No.  
C. Only if it is a nested class.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Top-level classes cannot be protected (who would they be protected *from*?). However, a class nested inside another class can be marked `protected`.
</details>

### Q12. If `Assembly A` has `internal class X`, can `Assembly B` inherit from it?
A. Yes.  
B. No.  
C. Only if `Assembly A` uses `[InternalsVisibleTo("AssemblyB")]`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Normally `internal` hides the type. `InternalsVisibleTo` is a special attribute that allows specific "friend" assemblies to see internal types.
</details>

### Q13. Consider `Base` has `protected int x`. `Derived` inherits `Base`. Can `Derived` access `x` on an instance of `Base`?
```csharp
class Derived : Base {
   void Method(Base b) {
      b.x = 10; // Is this valid?
   }
}
```
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is a key protection rule. A derived class can access protected members on *itself* (or instances of ANY subclass of itself), but NOT on instances of the Base class (or other unrelated subclasses). This prevents `Derived` from messing with the internals of a potentially different implementation of `Base`.
</details>

### Q14. Can a private method be virtual?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`virtual` implies that a derived class can override it. Since derived classes cannot see private members, a private method cannot be virtual.
</details>

### Q15. Is `public` accessible outside the namespace?
A. Yes.  
B. No, only inside namespace.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`public` allows access from anywhere, across namespaces and assemblies, provided the reference is added.
</details>
