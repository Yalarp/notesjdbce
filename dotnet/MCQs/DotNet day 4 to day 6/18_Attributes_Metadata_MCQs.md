# 18_Attributes_Metadata – MCQs

## EASY MCQs

### Q1. What is an Attribute in C#?
A. A variable inside a class.  
B. A tag that adds metadata to code elements.  
C. A database column.  
D. A graphical element.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Attributes allow you to associate declarative information (metadata) with code (classes, methods, properties), which can be retrieved at runtime.
</details>

### Q2. All custom attribute classes must inherit from:
A. `System.Object`  
B. `System.Meta`  
C. `System.Attribute`  
D. `System.Type`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
This is a compiler requirement for creating custom attributes.
</details>

### Q3. How do you apply an attribute to a class?
A. `class MyClass : AttributeName`  
B. `[AttributeName] class MyClass`  
C. `@AttributeName class MyClass`  
D. `{AttributeName} class MyClass`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Standard syntax uses square brackets `[...]` placed immediately before the element being modified.
</details>

### Q4. Which built-in attribute marks a method as deprecated?
A. `[Old]`  
B. `[Deprecated]`  
C. `[Obsolete]`  
D. `[Legacy]`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`[Obsolete("Message")]` causes the compiler to issue a warning (or error) whenever the decorated member is used.
</details>

### Q5. Can attributes accept parameters?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, they accept positional parameters (constructor arguments) and named parameters (property assignments).
</details>

---

## MEDIUM MCQs

### Q6. Which mechanism is used to read attributes at runtime?
A. Serialization  
B. Reflection  
C. Multithreading  
D. Inheritance  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Reflection (`Type.GetCustomAttributes`, etc.) is the API used to inspect compiled assemblies and discover the metadata/attributes attached to types.
</details>

### Q7. The `[AttributeUsage]` attribute is used to:
A. Use a custom attribute.  
B. Define where a custom attribute can be applied.  
C. Optimize the attribute.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is a meta-attribute applied to your custom attribute class definition to restrict usage (e.g., valid only on Classes, or only on Methods) and control inheritance/multiplicity.
</details>

### Q8. `[Conditional("DEBUG")]` causes the method call to be:
A. Executed always but logged.  
B. Removed entirely by the compiler if the symbol is not defined.  
C. Run in a background thread.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If "DEBUG" is not defined, the compiler strips out all *calls* to that method from the generated IL, ensuring zero runtime overhead in Release builds.
</details>

### Q9. Can you omit the "Attribute" suffix when using an attribute?
A. Yes, `[MyAttribute]` and `[My]` are equivalent.  
B. No, must typically use full name.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The C# compiler allows you to omit the "Attribute" suffix for convenience if the class name ends with it.
</details>

### Q10. Positional parameters in attributes correspond to:
A. Public Properties.  
B. Constructor arguments.  
C. Static fields.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Arguments that appear first without names `[Attr(123)]` must match the signature of one of the attribute class's public constructors.
</details>

---

## HARD MCQs

### Q11. `AllowMultiple = true` in AttributeUsage enables:
A. Applying the attribute to multiple classes.  
B. Applying the same attribute multiple times to the *same* element.  
C. Inheriting the attribute.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
By default, an attribute can be applied only once per element. This setting allows stacking: `[Route("/api"), Route("/home")]`.
</details>

### Q12. Named parameters in an attribute usage (e.g. `[My(Version=1)]`) map to:
A. Constructor parameters.  
B. Public read/write fields or properties.  
C. Methods.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Named arguments set the values of public properties or fields *after* the constructor has run.
</details>

### Q13. Attribute arguments must be:
A. Compile-time constants.  
B. Any variable.  
C. Runtime calculated values.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Because attributes are baked into the assembly metadata at compile time, their arguments are restricted to constant expressions (primitives, strings, type, enums, arrays of these). You cannot pass a `new Object()` or a variable.
</details>

### Q14. `[CallerMemberName]` (C# 5.0) is used to:
A. Get the name of the method calling the current method.  
B. Restrict access to specific members.  
C. Rename the member.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Helpful for INotifyPropertyChanged. The compiler automatically injects the string name of the calling property into the optional parameter.
</details>

### Q15. `Inherited = true` in AttributeUsage means:
A. The attribute class inherits from another attribute.  
B. Derived classes inherit the attribute from their base class.  
C. The attribute is public.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It controls whether reflection APIs like `GetCustomAttributes` will visually "walk up" the class hierarchy to find the attribute on base classes if it's missing on the derived class.
</details>
