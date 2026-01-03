# 03_Abstract_Classes_Methods – MCQs

## EASY MCQs

### Q1. Can you create an instance of an abstract class using `new`?
A. Yes  
B. No  
C. Only if it has a constructor  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Abstract classes are incomplete blueprints and cannot be instantiated directly.
</details>

### Q2. Does an abstract method have a body?
A. Yes, a default one.  
B. No, it ends with a semicolon.  
C. Yes, but it must be empty `{}`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Abstract methods are declarations only: `public abstract void Method();`. They provide no implementation.
</details>

### Q3. Which keyword forces a derived class to implement a method?
A. `virtual`  
B. `static`  
C. `abstract`  
D. `sealed`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Marking a method as `abstract` in the base class compels any non-abstract derived class to provide an implementation override.
</details>

### Q4. Can an abstract class contain non-abstract (concrete) methods?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, abstract classes can (and often do) contain regular methods with full implementations to provide common functionality to all subclasses.
</details>

### Q5. If a class contains an abstract method, the class itself must be declared as:
A. `public`  
B. `virtual`  
C. `abstract`  
D. `static`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
If a class has even one incomplete (abstract) method, the class is incomplete and must be marked `abstract`.
</details>

---

## MEDIUM MCQs

### Q6. Which modifier is NOT allowed on an abstract method?
A. `public`  
B. `protected`  
C. `internal`  
D. `private`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
Abstract methods are meant to be overridden by derived classes. `private` members are not visible to derived classes, making overriding impossible. Default is private, so you generally use protected or public.
</details>

### Q7. Can an abstract class have a constructor?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes. While you can't `new` the abstract class, the constructor exists to be called by derived classes (using `base(...)`) to initialize fields defined in the abstract base.
</details>

### Q8. What is the difference between `virtual` and `abstract` methods?
A. Virtual requires override; Abstract is optional.  
B. Virtual has a body; Abstract does not.  
C. There is no difference.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Virtual methods provide a default implementation that *can* be overridden. Abstract methods provide NO implementation and *must* be overridden.
</details>

### Q9. Can a derived class of an abstract class also be abstract?
A. No.  
B. Yes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Yes. If the derived class does not wish to implement all abstract methods of the parent, it can also be marked as abstract, passing the burden of implementation to the next level of derivation.
</details>

### Q10. Why use an abstract class instead of an interface?
A. To support multiple inheritance.  
B. To provide default implementation and state (fields).  
C. It is faster.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Interfaces cannot have fields (state) or constructors (traditionally). Abstract classes allow defining a common identity (fields) and shared behavior (concrete methods) alongside the contract (abstract methods).
</details>

---

## HARD MCQs

### Q11. Can an abstract class implement an interface?
A. Yes, and it must implement all methods.  
B. Yes, and it can map interface methods to abstract methods.  
C. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
An abstract class can implement an interface. It can choose to provide implementations or declared those interface methods as `abstract` for its children to implement.
</details>

### Q12. Can you declare a method as `abstract static`?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`static` methods cannot be overridden (they belong to the type, not the instance v-table). `abstract` requires overriding. Thus, they are mutually exclusive concepts.
</details>

### Q13. Can an abstract method be `sealed`?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`sealed` prevents overriding. `abstract` demands overriding. They are fundamentally opposite.
</details>

### Q14. Consider: `abstract class A {}`. Is `class B : A {}` valid?
A. No, B must implement something.  
B. Yes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Since `A` has no abstract methods that require implementation, `B` can simply inherit from it without adding anything. `A` just acts as a base type that cannot be instantiated.
</details>

### Q15. Is it possible to have an abstract property?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, e.g., `public abstract int Count { get; }`. Derived classes must override the property implementation.
</details>
