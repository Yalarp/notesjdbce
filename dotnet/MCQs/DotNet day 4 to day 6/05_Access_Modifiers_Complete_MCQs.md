# 05_Access_Modifiers_Complete – MCQs

## EASY MCQs

### Q1. Which modifier allows a member to be accessed from anywhere?
A. `private`  
B. `internal`  
C. `public`  
D. `protected`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`public` is the least restrictive access modifier, allowing access from any class in any assembly.
</details>

### Q2. `private` members are accessible:
A. Within the same file.  
B. Within the same class only.  
C. Within the same assembly.  
D. Within derived classes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`private` restricts access strictly to the body of the containing class.
</details>

### Q3. Which modifier limits access to the current assembly (project)?
A. `protected`  
B. `internal`  
C. `public`  
D. `static`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`internal` allows all classes within the same compiled assembly (DLL/EXE) to access the member, but blocks external assemblies.
</details>

### Q4. `protected` members are accessible in:
A. The defining class and its derived classes.  
B. The defining class only.  
C. The entire world.  
D. Any class in the same namespace.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`protected` is meant for inheritance, granting access to subclasses (even in different assemblies) while keeping the member hidden from the general public.
</details>

### Q5. What is the default access modifier for a class member (field/method) if none is specified?
A. `public`  
B. `internal`  
C. `private`  
D. `protected`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Members default to the most restrictive level, `private`.
</details>

---

## MEDIUM MCQs

### Q6. What does `protected internal` mean?
A. Accessible only to derived classes inside the same assembly.  
B. Accessible to everyone in the same assembly OR derived classes in other assemblies.  
C. Accessible to everyone in the same assembly AND derived classes in other assemblies.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is a Union (OR). Internal (Same Assembly) + Protected (Derived classes anywhere). This is less restrictive than either individual modifier.
</details>

### Q7. What creates the "Accessible to derived classes ONLY if they are in the same assembly" condition?
A. `protected internal`  
B. `private protected`  
C. `internal private`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`private protected` (C# 7.2+) is an Intersection (AND). It must be Internal (Same Assembly) AND Protected (Derived).
</details>

### Q8. What is the default access modifier for a top-level Class (not nested)?
A. `public`  
B. `private`  
C. `internal`  
D. `protected`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Top-level types default to `internal`. You must explicitly mark them `public` if you want them exposed to other assemblies.
</details>

### Q9. Can a derived class in a different assembly access an `internal` member of the base?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
No. `internal` is strictly bounded by the assembly. Derivation does not override the assembly boundary for `internal` members.
</details>

### Q10. Can you declare a top-level class as `private`?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A top-level class cannot be private because it would be inaccessible to anything (including the startup code), rendering it useless. Nested classes can be private.
</details>

---

## HARD MCQs

### Q11. Which is more restrictive: `protected internal` or `private protected`?
A. `protected internal`  
B. `private protected`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`private protected` is more restrictive (Intersection/AND). `protected internal` is very broad (Union/OR).
</details>

### Q12. Can an overridden method change the access modifier?
A. Yes, to be more permissive.  
B. Yes, to be more restrictive.  
C. No, it must match exactly.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The override must match the signature exactly, including accessibility. You cannot widen or narrow the access.
</details>

### Q13. `public class A { private class B {} }`. Can you access `B` from `A`?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, the outer class has access to all members of its nested classes, even private ones (and vice versa).
</details>

### Q14. What are the interface member access modifiers by default (C# 7 and below)?
A. `private`  
B. `public`  
C. `internal`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Interface members are implicitly public.
</details>

### Q15. If a class is `internal`, can it have `public` members?
A. No.  
B. Yes, but they are effectively internal.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The members can be marked public, but since the class itself is internal, nobody outside the assembly can see the class, so they effectively cannot access the public members either.
</details>
