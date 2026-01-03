# 03_Data_Types_And_Identifiers – MCQs

## EASY MCQs

### Q1. Which of the following is a valid C# identifier?

A. `1stValue`  
B. `class`  
C. `_salary`  
D. `first name`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Identifiers can contain letters, digits, and underscores but must start with a letter or underscore. They cannot contain spaces or be reserved keywords. `_salary` is valid.
</details>

### Q2. According to C# naming conventions, which case should be used for public properties and methods?

A. camelCase  
B. PascalCase  
C. UPPER_CASE  
D. snake_case  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
PascalCase (first letter of each word uppercase) is used for Classes, Methods, Properties, Namespaces, and Public Members.
</details>

### Q3. Where are Value Types stored in the .NET memory model?

A. Heap  
B. Stack  
C. Hard Drive  
D. Constant Pool  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Value types (like `int`, `float`, `struct`) are stored on the Stack and directly contain their data.
</details>

### Q4. Which suffix is mandatory when declaring a `decimal` literal?

A. F  
B. D  
C. L  
D. M  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** D

**Explanation:**  
The 'M' or 'm' suffix is mandatory for `decimal` literals (e.g., `10.5M`). Without it, a decimal number is treated as a `double`.
</details>

---

## MEDIUM MCQs

### Q5. Which of the following statements about the `var` keyword is FALSE?

A. `var` variables must be initialized at declaration.  
B. `var` can be used for class-level fields.  
C. The type of a `var` variable is inferred by the compiler.  
D. Once referenced, the type of a `var` variable cannot change.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`var` cannot be used for class-level fields (member variables). It is only for implicitly typed local variables within methods.
</details>

### Q6. What is the .NET Framework type equivalent for the C# `float` alias?

A. System.Double  
B. System.Int32  
C. System.Single  
D. System.Decimal  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
`float` is an alias for the .NET type `System.Single`. `double` is `System.Double`.
</details>

### Q7. Consider the following code:
```csharp
int a = 10;
int b = a;
b = 20;
```
What will be the value of `a` after execution?

A. 20  
B. 10  
C. Null  
D. 0  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Since `int` is a Value Type, assigning `a` to `b` creates a copy of the value. Changing `b` does not affect `a`. Therefore, `a` remains 10.
</details>

### Q8. Which of the following variable declarations is INVALID?

A. `var x = 10;`  
B. `var str = "Hello";`  
C. `var n = null;`  
D. `var obj = new object();`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
`var` requires the compiler to infer the type from the initialization. `null` does not have a specific type, so `var n = null;` causes a compile-time error. You must cast null (e.g., `var n = (string)null;`).
</details>

---

## HARD MCQs

### Q9. When you use the `new` keyword with a Value Type (e.g., `int x = new int();`), what happens?

A. It allocates memory on the Heap and initializes it to 0.  
B. It causes a compilation error because Value Types cannot use `new`.  
C. It allocates memory on the Stack and initializes it to the default value (0).  
D. It creates a null reference.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Value types can use `new`. It calls the default constructor, which allocates memory on the Stack (not Heap) and initializes the variable to its default value (0 for int).
</details>

### Q10. Regarding Reference Types, what happens when you assign one reference variable to another (e.g., `ref1 = ref2`)?

A. A deep copy of the object is created on the Heap.  
B. The data from the Heap is moved to the Stack.  
C. Only the address (reference) is copied; both variables point to the same object.  
D. The original object is garbage collected immediately.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
For Reference Types, assignment copies the reference (memory address), not the actual object. Both variables will point to the same object on the Heap.
</details>

### Q11. What is the base type of `int` in the .NET type hierarchy?

A. System.Object -> System.ValueType -> System.Int32  
B. System.Object -> System.Int32  
C. System.ValueType -> System.Object -> System.Int32  
D. System.Int32 has no base type because it is a primitive.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
`int` (System.Int32) inherits from `System.ValueType`, which in turn inherits from `System.Object`.
</details>

### Q12. Which statement correctly describes the `char` type in C#?

A. It is an 8-bit signed integer.  
B. It is a Reference Type representing a single character.  
C. It is a 16-bit struct representing a Unicode character.  
D. It behaves exactly like `string` but for one letter.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
`char` (System.Char) is a Value Type (struct) that represents a single 16-bit Unicode character. It is not a reference type.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
