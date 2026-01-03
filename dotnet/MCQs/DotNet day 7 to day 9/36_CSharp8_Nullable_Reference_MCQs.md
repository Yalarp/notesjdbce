# 36_CSharp8_Nullable_Reference – MCQs

## EASY MCQs

### Q1. What is the primary purpose of "Nullable Reference Types" in C# 8?
A. To allow value types to be null.  
B. To help developers avoid `NullReferenceException` by making nullability explicit in code and compiler warnings.  
C. To prevent the use of null completely.  
D. To optimize memory.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The feature doesn't change the runtime (strings can still be null), but the compiler strictly analyzes flow to warn if you access a possibly-null variable without checking.
</details>

### Q2. How do you declare a `string` variable that allows nulls in C# 8+?
A. `string s`  
B. `string? s`  
C. `Nullable<string> s`  
D. `string* s`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `?` suffix (e.g., `string?`, `Person?`) indicates that the variable *intends* to hold nulls. `string` (without ?) implies it should never be null.
</details>

### Q3. What is the "Null-Forgiving Operator"?
A. `?`  
B. `!`  
C. `??`  
D. `?:`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The postfix `!` operator (e.g., `variable!.Member`) tells the compiler "Trust me, I know this isn't null here", suppressing the warning.
</details>

### Q4. "Records" (C# 9) are primarily designed for:
A. Mutable data.  
B. Immutable data models with value-based equality.  
C. Static utility classes.  
D. Database connection strings.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Records provide built-in immutability features, concise syntax, and value semantics (two records with same data are equal), making them ideal for DTOs.
</details>

### Q5. What does the `init` accessor do?
A. Allows setting the property only in the constructor or object initializer.  
B. Allows setting the property anytime.  
C. Makes the property private.  
D. Initializes the property to null.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`public int Age { get; init; }` makes the property immutable after the object initialization phase completes.
</details>

---

## MEDIUM MCQs

### Q6. If you have `string name` (non-nullable) in a class, what must the constructor do?
A. Nothing.  
B. It *must* initialize `name` to a non-null value; otherwise, the compiler warns.  
C. It can leave it null.  
D. It must set it to empty string.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The compiler ensures strictness. If you declare it non-nullable, you must ensure it has a value upon creation.
</details>

### Q7. The `with` expression is used for:
A. Modifying a record in place.  
B. Creating a non-destructive copy of a record with specific properties modified.  
C. Inheritance.  
D. Pattern matching.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`var p2 = p1 with { Age = 31 };` creates a new record `p2` that is identical to `p1` except for the `Age`. `p1` remains unchanged.
</details>

### Q8. Are Records Reference Types or Value Types?
A. Always Value Types.  
B. Always Reference Types (by default).  
C. They are Pointers.  
D. Neither.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A `record` (or `record class`) is a reference type. C# 10 introduced `record struct` for value type records.
</details>

### Q9. Value Equality in Records means:
A. `r1 == r2` returns true if they refer to the same memory address.  
B. `r1 == r2` returns true if all their property values are equal, even if they are different objects.  
C. Records cannot be compared.  
D. `r1` is larger than `r2`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Records override `Equals` and `GetHashCode` automatically to perform field-by-field comparison.
</details>

### Q10. How do you enable Nullable Reference Types?
A. It is on by default in .NET Framework 4.8.  
B. Use `<Nullable>enable</Nullable>` in the .csproj file or `#nullable enable` directive in code.  
C. Use `using System.Nullable;`.  
D. You cannot.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is an opt-in feature (default in new .NET 6+ projects) because it causes many warnings in legacy code.
</details>

---

## HARD MCQs

### Q11. Can `structs` use `init` properties?
A. No.  
B. Yes.  
C. Only if readonly.  
D. Only in C# 7.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Yes, `init` works for structs too, allowing immutable struct design compatible with object initializers.
</details>

### Q12. Positional Records: `public record Person(string Name, int Age);`
A. Use fields instead of properties.  
B. Auto-generate `Init` properties, a Constructor, and a Deconstruct method.  
C. Are private.  
D. Are mutable by default.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This concise syntax creates a fully functional immutable data type with constructor `new Person("Bob", 20)` and deconstruction `var (name, age) = p;`.
</details>

### Q13. `null` vs `default` in Generic Constraints where `T : notnull`.
A. T Can be int?.  
B. T MUST be a non-nullable type (value or reference). `int?` or `string?` are disallowed.  
C. T must be a class.  
D. T is void.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `notnull` constraint enforces that the type argument cannot be nullable.
</details>

### Q14. In a nullable context, what is `string?[]?`?
A. Syntax error.  
B. A nullable array of nullable strings. (The array itself can be null, and elements inside can be null).  
C. A text file.  
D. A 2D array.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Outer `?` = array reference can be null. Inner `?` = elements can be null.
</details>

### Q15. Does the `!` operator change runtime behavior?
A. Yes, it creates an object.  
B. No, it is purely a compile-time signal to silence warnings. If the value IS null at runtime, you will still get a `NullReferenceException`.  
C. Yes, it throws exception.  
D. No, it converts null to empty string.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is effectively a "Shut up, Compiler" operator. It fixes build warnings, not runtime bugs.
</details>
