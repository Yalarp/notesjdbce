# 01_Polymorphism_Virtual_Methods – MCQs

## EASY MCQs

### Q1. What does the `virtual` keyword indicate in C#?
A. The method is private.  
B. The method cannot be overridden.  
C. The method can be overridden by derived classes.  
D. The method is static.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `virtual` keyword allows a method in a base class to be overridden in a derived class.
</details>

### Q2. Which keyword is used in a derived class to provide a new implementation for a virtual method?
A. `new`  
B. `override`  
C. `virtual`  
D. `static`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `override` keyword is required to extend or modify the abstract or virtual implementation of an inherited method.
</details>

### Q3. By default, methods in C# are:
A. Virtual  
B. Sealed (Non-virtual)  
C. Abstract  
D. Static  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Unlike Java, methods in C# are non-virtual (sealed) by default. You must explicitly mark them `virtual` to allow overriding.
</details>

### Q4. Can a virtual method be private?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Virtual members cannot be private because they must be accessible to derived classes to be overridden.
</details>

### Q5. What happens if you use `new` instead of `override` on a method in a derived class?
A. It overrides the method.  
B. It hides the base class method.  
C. It causes a compilation error.  
D. It makes the method abstract.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `new` keyword explicitly hides the member that is inherited from a base class. It breaks the polymorphism chain.
</details>

---

## MEDIUM MCQs

### Q6. In runtime polymorphism, what determines which method specific implementation is called?
A. The reference type.  
B. The actual object type (Instance type).  
C. The return type of the method.  
D. The namespace of the class.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
For virtual methods (overridden), the CLR determines which method to call at runtime based on the runtime type of the object, not the reference variable's type.
</details>

### Q7. Consider `Base b = new Derived();` where `Derived` overrides a method `M` of `Base`. What happens when `b.M()` is called?
A. `Base.M()` is called.  
B. `Derived.M()` is called.  
C. Compilation Error.  
D. Runtime Error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Since `b` points to a `Derived` object and `M` is overridden, the runtime calls the derived class's implementation (Polymorphism).
</details>

### Q8. True or False: You MUST override a virtual method in the derived class.
A. True  
B. False  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
False. Overriding a virtual method is optional. If you don't override it, the base class implementation is used.
</details>

### Q9. What is the output of `object o = "Hello"; Console.WriteLine(o);`?
A. Compiler Error  
B. "System.Object"  
C. "Hello"  
D. Nothing  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `String` class overrides `Object.ToString()`. Even though `o` is of type `object`, polymorphism ensures the overridden `ToString()` (which prints the string content) is called.
</details>

### Q10. Can you override a static method?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Static methods belong to the class, not an instance, and are resolved at compile time. Therefore, they cannot be virtual or overridden (though they can be hidden).
</details>

---

## HARD MCQs

### Q11. If `Class A` has `virtual void M()`, `Class B : A` has `override void M()`, and `Class C : B` has `new void M()`. `A obj = new C(); obj.M();` calls:
A. A.M()  
B. B.M()  
C. C.M()  
D. Ambiguous  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`obj` is type `A`. The runtime looks for the most derived valid override. `B` overrides `A`. `C` *hides* `B` (breaks the chain). So from `A`'s perspective, the "latest" override is in `B`.
</details>

### Q12. Can a constructor be virtual?
A. Yes  
B. No  
C. Only in abstract classes  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Constructors cannot be virtual. You are creating a specific type; polymorphism applies to behavior (methods) of an *already created* object.
</details>

### Q13. Why might you refer to a `Derived` object using a `Base` class reference?
A. To save memory.  
B. To access Derived-specific members.  
C. To write generic code that works with any class inheriting from Base (Polymorphism).  
D. It is mandatory in C#.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
This is the core purpose of polymorphism: handling different types through a unified interface (the base class).
</details>

### Q14. What happens if you call a virtual method inside a constructor?
A. It guarantees calling the base class method.  
B. It calls the overridden method in the derived class (if overridden), possibly before the derived class is initialized.  
C. Compiler Error.  
D. Runtime Exception.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
In C#, virtual calls in constructors resolves to the most derived implementation. This is dangerous because the derived class's constructor hasn't run yet, so the method might access uninitialized fields.
</details>

### Q15. Is `override` mandatory if the base method is `abstract`?
A. No, strict optional.  
B. Yes, unless the derived class is also validly abstract.  
C. Yes, always, no exceptions.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Abstract methods *must* be implemented. The only way to avoid implementing/overriding them is if the derived class itself is declared `abstract`.
</details>
