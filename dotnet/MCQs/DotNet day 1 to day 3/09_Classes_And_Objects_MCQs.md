# 09_Classes_And_Objects – MCQs

## EASY MCQs

### Q1. What is a Class in C#?

A. An instance of an object.  
B. A built-in data type for numbers.  
C. A user-defined reference type that acts as a blueprint for objects.  
D. A variable stored on the Stack.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
A class is a user-defined reference type that encapsulates data (fields) and behavior (methods), serving as a template or blueprint for creating objects.
</details>

### Q2. Which keyword is used to create an instance (object) of a class?

A. `create`  
B. `new`  
C. `init`  
D. `make`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The `new` keyword is used to allocate memory on the heap and call the constructor to instantiate an object of a class.
</details>

### Q3. Where is the actual object data stored in memory?

A. Stack  
B. Heap  
C. Registry  
D. Cache  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
While the reference variable is stored on the Stack, the actual object data (the instance) is stored on the Heap.
</details>

### Q4. What is the default access modifier for members of a class (fields, methods) if not specified?

A. `public`  
B. `internal`  
C. `private`  
D. `protected`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The default access modifier for class members is `private`, meaning they are only accessible within the class definition.
</details>

---

## MEDIUM MCQs

### Q5. Consider the code: `Student s1 = new Student();`. What does `s1` hold?

A. The entire object data.  
B. The memory address (reference) of the object on the Heap.  
C. Null.  
D. The first field of the object.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`s1` is a reference variable allocated on the Stack. It holds the memory address of the actual Student object, which resides on the Heap.
</details>

### Q6. Which class do all C# classes implicitly inherit from?

A. `System.Object`  
B. `System.Root`  
C. `System.Class`  
D. `System.Base`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
All classes in C# implicitly inherit from `System.Object`, which provides fundamental methods like `ToString()`, `Equals()`, and `GetType()`.
</details>

### Q7. What happens when you do a reference assignment like `ref2 = ref1` for a class type?

A. A deep copy (clone) of the object is created.  
B. `ref2` gets a copy of the reference from `ref1`, so both point to the same object.  
C. The object data is moved from `ref1` to `ref2`.  
D. `ref1` becomes null.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
For reference types, assignment copies the reference (address), not the object itself. This results in a shallow copy where both variables point to the exact same object instance.
</details>

### Q8. What is the default value for a field of type `bool` in a class?

A. `true`  
B. `false`  
C. `null`  
D. -1  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The default value for boolean fields is `false`. (Numeric fields default to 0, reference types to null).
</details>

---

## HARD MCQs

### Q9. Which access modifier restricts access to the "current assembly" only?

A. `private`  
B. `protected`  
C. `internal`  
D. `public`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The `internal` access modifier allows access to any code within the same assembly (compilation unit, like a .dll or .exe) but restricts access from other assemblies.
</details>

### Q10. What is the difference between `private protected` and `protected internal`?

A. They are the same.  
B. `protected internal` means "protected OR internal" (anywhere in assembly OR derived classes). `private protected` means "protected AND internal" (derived classes ONLY within same assembly).  
C. `protected internal` is more restrictive than `private protected`.  
D. `private protected` is accessible in any derived class globally.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`protected internal` is the union (Assembly OR Subclass). `private protected` is the intersection (Assembly AND Subclass). Thus, `private protected` is more restrictive; it allows access only to subclasses that are inside the *same* assembly.
</details>

### Q11. If `Student s1;` is declared but not initialized with `new`, what value does `s1` have (assuming it's a field)?

A. An arbitrary garbage address.  
B. An empty object.  
C. `null`.  
D. A compiler error upon declaration.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Unless initialized, a field of a reference type defaults to `null`, meaning it points to no object on the Heap.
</details>

### Q12. Regarding memory, what happens when `new Account()` is executed?

A. Only Stack memory is allocated for the reference.  
B. Only Heap memory is allocated for the data.  
C. A reference is created on the Stack AND memory is allocated on the Heap for the object data.  
D. The constructor is called, but no memory is allocated.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Object creation involves two parts: a reference variable is created on the Stack (to hold the address), and the `new` keyword allocates memory on the Heap for the actual object data and calls the constructor.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
