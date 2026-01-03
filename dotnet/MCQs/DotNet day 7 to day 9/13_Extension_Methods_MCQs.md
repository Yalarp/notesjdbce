# 13_Extension_Methods – MCQs

## EASY MCQs

### Q1. What is the main purpose of Extension Methods in C#?
A. To create subclasses easily.  
B. To add methods to existing types without modifying the source code or using inheritance.  
C. To access private members of a class.  
D. To override virtual methods.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Extension methods allow you to "extend" a type (like `String` or `List`) with new instance-like methods, even if you don't own the source code for that type.
</details>

### Q2. Which keyword is required on the first parameter of an extension method?
A. `ref`  
B. `out`  
C. `this`  
D. `extends`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `this` modifier before the first parameter type indicates that the method extends that specific type.
</details>

### Q3. Where must extension methods be defined?
A. In any class.  
B. In a `static` class.  
C. In an `abstract` class.  
D. In a `struct`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Extension methods must be defined as `static` methods inside a top-level `static` class.
</details>

### Q4. How do you call an extension method `Reverse` defined for `string` on a variable `str`?
A. `Reverse(str)`  
B. `str.Reverse()`  
C. `String.Reverse(str)`  
D. `Extension.Reverse(str)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Although they are static methods, code consumes them using instance method syntax: `objectInstance.Method()`.
</details>

### Q5. Can extension methods access private fields of the extended class?
A. Yes, always.  
B. No, never.  
C. Only if the class is sealed.  
D. Only via Reflection.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Extension methods are just static methods in a separate class. They respond to the public API of the type they accept as `this` parameter; they have no special privileges.
</details>

---

## MEDIUM MCQs

### Q6. What happens if a class defines an instance method with the same name and signature as an extension method?
A. The extension method overrides the instance method.  
B. The compiler throws an "Ambiguous call" error.  
C. The instance method takes precedence; the extension method is ignored.  
D. Both are called.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Instance methods always win. If `str.ToString()` exists, an extension method `ToString(this string s)` will never be called via method syntax.
</details>

### Q7. To use an extension method defined in a namespace `MyExtensions`, you must:
A. Inherit from the namespace.  
B. Add a `using MyExtensions;` directive (or the containing namespace).  
C. Copy the code file.  
D. Use the `extends` keyword.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Extension methods are only brought into scope if you import the namespace containing the static class.
</details>

### Q8. Method Chaining (e.g., `text.Reverse().ToUpper()`) works because:
A. The compiler merges the methods.  
B. Each extension method returns an object/value that the next method is then called upon.  
C. C# is a functional language.  
D. It uses reflection.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Standard fluent interface pattern: The output of the first call becomes the `this` input of the second call.
</details>

### Q9. Can you write an extension method for an Interface (e.g., `IEnumerable<T>`)?
A. No, only for classes.  
B. Yes, and it effectively adds that method to all classes implementing the interface.  
C. Yes, but only for abstract classes.  
D. No, interfaces cannot have implementation.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is extremely powerful (and how LINQ works). Extending `IEnumerable<T>` makes the method available on `List<T>`, `Array`, `Dictionary`, etc.
</details>

### Q10. Is the object instance passed to `this` allowed to be null in an extension method?
A. No, it throws NullReferenceException automatically before the call.  
B. Yes, execution enters the static method, and you can check for null manually.  
C. Yes, but you cannot access any members.  
D. No, the compiler prevents it.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Unlike instance methods which crash if called on null, extension methods are just `StaticClass.Method(potentialNull)`. You can write `str.IsNullOrEmpty()` where `str` is null, provided the method handles it.
</details>

---

## HARD MCQs

### Q11. Can extension methods be overrides for virtual methods?
A. Yes.  
B. No.  
C. Only in abstract classes.  
D. Only in sealed classes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Extension methods are static and resolved at compile-time. They are not polymorphic and cannot participate in virtual method dispatch/overriding.
</details>

### Q12. If `NamespaceA` and `NamespaceB` both define an extension method `DoWork()` for String, and you import both namespaces:
A. The code works fine.  
B. The compiler picks the first one.  
C. Result is an ambiguous call error if you try to use `DoWork()`.  
D. It uses the one in the global namespace.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The compiler cannot decide which one you meant, so you must either remove one using directive or call the method as a static method explicitly (`ClassA.DoWork(str)`).
</details>

### Q13. LINQ is primarily implemented using:
A. Inheritance.  
B. Extension Methods on `IEnumerable<T>` and `IQueryable<T>`.  
C. Operator Overloading.  
D. Java Native Interface.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Methods like `.Where`, `.Select`, `.OrderBy` are all extension methods defined in the `System.Linq.Enumerable` (or `Queryable`) class.
</details>

### Q14. Can you create an extension property?
A. Yes.  
B. No.  
C. Only mostly read-only.  
D. Only in C# 10+.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
C# only supports extension *methods*. It does not support extension properties, events, or fields.
</details>

### Q15. Using extension methods to "add" methods to `System.Object`:
A. Is impossible.  
B. Is possible but generally discouraged as it pollutes IntelliSense for every single object in the project.  
C. Is the standard way to implement logging.  
D. Causes helper classes to fail.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`public static void Foo(this object o)` is valid, but now every single variable `x.Foo()` appears in the IDE, cluttering the API surface.
</details>
