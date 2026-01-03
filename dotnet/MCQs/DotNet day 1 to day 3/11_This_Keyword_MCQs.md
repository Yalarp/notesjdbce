# 11_This_Keyword – MCQs

## EASY MCQs

### Q1. What does the `this` keyword refer to in C#?

A. The previous class.  
B. The current instance of the class.  
C. The base class.  
D. The static members of the class.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The `this` keyword is a reference to the current instance of the class in which it is used.
</details>

### Q2. Which of the following is a valid use of `this`?

A. To access private members of another class.  
B. To distinguish between class fields and method parameters with the same name.  
C. To access static methods.  
D. To import namespaces.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
One of the most common uses of `this` is to resolve ambiguity when a parameter name shadows an instance field (e.g., `this.name = name`).
</details>

### Q3. Can `this` be used in a static method?

A. Yes, always.  
B. Yes, but only for static variables.  
C. No, because static methods differ from instance methods and do not belong to a specific object instance.  
D. Only if the method is private.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Static methods belong to the class itself, not to any specific instance. Therefore, there is no "current object" for `this` to refer to.
</details>

### Q4. How is `this` used in constructor chaining?

A. `public Class() : base(this) { }`  
B. `public Class() : this(params) { }`  
C. `this.Class(params)` inside the body.  
D. `return this;`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Constructor chaining is achieved using the syntax `: this(...)` before the constructor body to call another constructor in the same class.
</details>

---

## MEDIUM MCQs

### Q5. Consider the following code:
```csharp
public class Demo {
    public Demo GetInstance() {
        return this;
    }
}
```
What does `GetInstance()` return?

A. A new copy of the object.  
B. The reference to the calling object itself.  
C. Null.  
D. The parent class object.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Returning `this` returns the reference to the current object on which the method was called. This pattern is often used for method chaining (Fluent Interface).
</details>

### Q6. Can you modify the value of `this` itself (e.g., `this = new MyClass();`)?

A. Yes, inside a constructor.  
B. Yes, inside any instance method.  
C. No, `this` is read-only.  
D. Only in unsafe code.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The `this` reference is read-only; you cannot assign a new value or object to `this` within an instance method or constructor.
</details>

### Q7. In an Extension Method, what does the `this` keyword before the first parameter signify?

A. It passes the current instance to the method.  
B. It marks the method as private.  
C. It indicates the type that the method extends.  
D. It forces the method to be static.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
In an extension method assignment (e.g., `public static void Ext(this string str)`), the `this` keyword modifies the first parameter to specify which type (in this case, `string`) the method operates on.
</details>

### Q8. Refer to the code:
```csharp
class Point {
    int x, y;
    public Point(int x, int y) {
        x = x;
        y = y;
    }
}
```
What happens here?

A. The fields `x` and `y` are initialized correctly.  
B. A compile-time error occurs.  
C. The parameters assign values to themselves; fields remain uninitialized (0).  
D. The compiler automatically fixes the ambiguity.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Without `this.`, the code `x = x` assigns the parameter `x` to itself due to shadowing. The instance fields `x` and `y` are never assigned and remain at their default values (0).
</details>

---

## HARD MCQs

### Q9. When passing `this` to another method (e.g., `Process(this)`), what is effectively passed?

A. A deep copy of the object.  
B. The memory address (reference) of the current object on the Heap.  
C. The type information of the class.  
D. The static members of the class.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`this` holds the reference (pointer/address) to the current object on the Heap. Passing it passes that reference by value (so the called method works on the same object instance).
</details>

### Q10. Why is `this` generally optional when accessing class members within the class?

A. Because members are public by default.  
B. Because the compiler implicitly treats member access (like `name`) as `this.name` if there is no local variable shadowing it.  
C. Because C# doesn't support explicit `this`.  
D. It is only optional in static methods.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The compiler automatically scopes identifiers to the class members if no local variable or parameter blocks (shadows) that name. Explicit `this` is only required to resolve ambiguity.
</details>

### Q11. Which scenario absolutely REQUIRES the use of `this`?

A. Accessing a public property.  
B. Calling a private method.  
C. Creating an indexer.  
D. Declaring a static variable.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
When declaring an indexer, the syntax is `public type this[int index] { ... }`. The `this` keyword is syntactically required here to define the indexer.
</details>

### Q12. If a constructor calls another constructor using `: this()`, when does the body of the *called* constructor execute relative to the *calling* constructor?

A. After the calling constructor body.  
B. Before the calling constructor body.  
C. In parallel.  
D. It depends on the operating system.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
In constructor chaining, the chained constructor (the one called via `: this()`) executes fully *before* the body of the constructor that initiated the call.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
