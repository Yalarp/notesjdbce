# 10_Constructors – MCQs

## EASY MCQs

### Q1. What is the return type of a Constructor?

A. `void`  
B. `int`  
C. The class type itself.  
D. It has no return type.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** D

**Explanation:**  
Constructors are special methods that do not have a return type, not even `void`. They implicitly return the instance being created, but syntactically, no return type is specified.
</details>

### Q2. When is a constructor called?

A. When the class is declared.  
B. When an object is created using `new`.  
C. When the program terminates.  
D. When a method is called.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Instance constructors are called automatically when an instance of the class is created using the `new` keyword.
</details>

### Q3. If you define a parameterized constructor in a class, what happens to the default parameterless constructor?

A. It remains available.  
B. It is automatically removed/hidden by the compiler.  
C. It becomes private.  
D. It must be manually deleted.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Wait, once you define *any* constructor explicitly, the compiler stops providing the automatic default parameterless constructor. If you still need it, you must define it manually.
</details>

### Q4. Which keyword is used to refer to the current instance of the class within a constructor?

A. `base`  
B. `self`  
C. `this`  
D. `me`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The `this` keyword refers to the current instance (object) and is often used to distinguish between class fields and constructor parameters with the same name.
</details>

---

## MEDIUM MCQs

### Q5. What is Constructor Chaining?

A. Creating multiple objects in a loop.  
B. A constructor calling another constructor of the same class or base class.  
C. Inheriting constructors from a parent class.  
D. Defining constructors with different names.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Constructor chaining is the technique of having one constructor call another (using `: this(...)`) to reuse initialization logic and avoid code duplication.
</details>

### Q6. Which syntax correctly implements constructor chaining to call the default constructor from a parameterized one?

A. `public MyClass(int x) { this(); ... }`  
B. `public MyClass(int x) : this() { ... }`  
C. `public MyClass(int x) : base() { ... }`  
D. `public MyClass(int x) -> MyClass() { ... }`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The correct syntax uses the colon `:` followed by `this()` (for same class) or `base()` (for parent class) *before* the constructor body.
</details>

### Q7. What represents the correct execution order for a class with both static and instance constructors?

A. Instance Constructor -> Static Constructor  
B. Static Constructor -> Instance Constructor  
C. They run in parallel.  
D. Instance fields -> Instance Constructor -> Static Constructor  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The static constructor is called automatically before the first instance is created or any static members are referenced. Thus, it runs *before* the instance constructor.
</details>

### Q8. What is the primary purpose of a Private Constructor?

A. To prevent the class from being instantiated.  
B. To hide the class from other assemblies.  
C. To create a secure object.  
D. To allow only subclasses to create instances.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
A private constructor prevents any code outside the class (including derived classes) from creating instances of that class. This is common in utility classes (containing only static members) or Singleton patterns.
</details>

---

## HARD MCQs

### Q9. Consider the following code:
```csharp
class Student {
    public string Name;
    public Student(Student other) {
        this.Name = other.Name;
    }
}
```
What kind of constructor is this?

A. Static Constructor  
B. Copy Constructor  
C. Default Constructor  
D. Private Constructor  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
A Copy Constructor takes an instance of the same class as a parameter and initializes the new instance by copying values from the argument object.
</details>

### Q10. Why is the `this` keyword necessary in the following snippet?
```csharp
public Student(string name) {
    this.name = name;
}
```
A. To make the variable public.  
B. To differentiate the field `name` from the parameter `name` (handling shadowing).  
C. To call the base class constructor.  
D. It is not necessary; `name = name` works fine.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Without `this.`, `name = name` would assign the parameter to itself (shadowing), leaving the class field unchanged. `this.name` explicitly targets the instance field.
</details>

### Q11. Which statement about Static Constructors is FALSE?

A. They cannot take parameters.  
B. They cannot have access modifiers (like public/private).  
C. They are called explicitly by the user code.  
D. They are used to initialize static data.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Static constructors are called automatically by the CLR (runtime), not by user code. You cannot call them explicitly, nor can you control exactly when they run (other than "before first use").
</details>

### Q12. In the context of inheritance (though technically C# constructors don't inherit), if a derived class constructor does not explicitly call a base constructor, what happens?

A. The code fails to compile.  
B. The compiler inserts a call to the base class's default parameterless constructor `base()`.  
C. No base constructor is called.  
D. The base class must have a static constructor.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
If not specified, the compiler implicitly adds `: base()` to the derived constructor, calling the default parameterless constructor of the base class. If the base class does not have a parameterless constructor, this causes a compile error unless an explicit call is made.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
