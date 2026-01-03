# 25_Inheritance_Basics – MCQs

## EASY MCQs

### Q1. Which symbol is used for inheritance in C#?
A. `extends`  
B. `:`  
C. `implements`  
D. `inherits`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
C# uses the colon `:` syntax for both class inheritance and interface implementation. e.g., `class Dog : Animal`.
</details>

### Q2. Does C# support multiple inheritance for classes?
A. Yes, using comma separation.  
B. No, a class can inherit from only one base class.  
C. Yes, but only for abstract classes.  
D. Yes, if they are in the same namespace.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
C# supports Single Inheritance for classes (one base class) but allows implementing Multiple Interfaces.
</details>

### Q3. Which keyword is used to access members of the base class from a derived class?
A. `super`  
B. `parent`  
C. `this`  
D. `base`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
The `base` keyword is used to access members (constructors, methods, properties) of the base class.
</details>

### Q4. Which access modifier makes a member accessible *only* within the same class and its derived classes?
A. `private`  
B. `public`  
C. `protected`  
D. `internal`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`protected` members are accessible in the containing class and any class that inherits from it, but not from the outside world.
</details>

### Q5. What is the relationship created by inheritance?
A. HAS-A  
B. IS-A  
C. USES-A  
D. WAS-A  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Inheritance denotes an "IS-A" relationship (e.g., Dog IS-A Animal).
</details>

---

## MEDIUM MCQs

### Q6. Are constructors inherited in C#?
A. Yes, always.  
B. No, but they can be called using `base()`.  
C. Only public constructors.  
D. Yes, but only default constructors.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Constructors are defined specifically for the type and are not inherited. However, a derived class constructor will implicitly or explicitly call a base class constructor to initialize the parent part of the object.
</details>

### Q7. Which keyword prevents a class from being inherited?
A. `static`  
B. `abstract`  
C. `sealed`  
D. `final`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `sealed` modifier prevents other classes from inheriting from the class.
</details>

### Q8. In what order are constructors executed when instantiating a derived class?
A. Derived class first, then Base class.  
B. Base class first, then Derived class.  
C. Simultaneous.  
D. Random order.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The Base class constructor runs first (to initialize the base foundation), followed by the Derived class constructor.
</details>

### Q9. Which of the following members are NOT inherited?
A. Public methods  
B. Protected fields  
C. Private members  
D. Static members  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Strictly speaking, private members are inherited (they exist in the object's memory layout) but they are NOT accessible to the derived class directly.
</details>

### Q10. What does the `protected internal` access modifier mean?
A. Accessible only in derived classes inside the same assembly.  
B. Accessible in the same assembly OR in derived classes (even in other assemblies).  
C. Accessible only in the same assembly AND derived classes.  
D. Same as public.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`protected internal` is the union of `protected` OR `internal`. It is accessible to anyone in the same assembly, AND to subclasses in other assemblies.
</details>

---

## HARD MCQs

### Q11. Can you inherit from a Struct in C#?
A. Yes.  
B. No.  
C. Only if the struct is public.  
D. Only if the struct is marked `virtual`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Structs in C# are implicitly `sealed` and do not support inheritance (though they implement interfaces). They inherit only from `System.ValueType`.
</details>

### Q12. If `Base` has only a parameterized constructor `Base(int x)`, what must the `Derived` class do?
A. Nothing special.  
B. It must also declare an empty constructor.  
C. It must effectively call `base(value)` in its constructor.  
D. It cannot inherit from such a class.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
If the base class does not have a parameterless constructor, the derived class constructor must explicitly call the available base constructor using `: base(...)`.
</details>

### Q13. What is "Name Hiding" or "Shadowing" in inheritance?
A. Using `private` to hide a member.  
B. Using the `new` keyword to define a member with the same name as a base member.  
C. Overriding a virtual method.  
D. Deleting a base member.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Shadowing occurs when a derived class defines a member with the same name as an inherited member, effectively "hiding" the base version. C# requires the `new` keyword to make this intentional and suppress warnings.
</details>

### Q14. Can a derived class access `private` members of the base class using reflection?
A. Yes.  
B. No, never.  
C. Only if `internal`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Reflection ignores access modifiers (unless restricted by security settings). While normal code cannot access private base members, Reflection can.
</details>

### Q15. `Dog d = new Animal();` (Assume Dog : Animal). Is this valid?
A. Yes, implicit casting.  
B. Yes, explicit casting required.  
C. No, compile-time error.  
D. No, runtime error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
This is invalid. A parent object is NOT a child object. An `Animal` might not be a `Dog`. You cannot assign a base instance to a derived reference implicitly or explicitly (unless the object in memory actually IS a Dog, which here it is not).
</details>
