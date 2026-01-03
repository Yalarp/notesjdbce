# 37_CSharp10_New_Features – MCQs

## EASY MCQs

### Q1. What does `global using` do in C# 10?
A. Imports a namespace for the entire project, so you don't need to add `using` in every file.  
B. Imports a namespace from the internet.  
C. Imports a namespace for the current file only.  
D. Exports a namespace.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Defined once (usually in a `GlobalUsings.cs` or generated via `<ImplicitUsings>`), it helps reduce boilerplate import headers.
</details>

### Q2. File-Scoped Namespaces (`namespace My.App;`) aim to:
A. Increase indentation.  
B. Reduce indentation (nesting) by one level for the whole file.  
C. Create local functions.  
D. Create private classes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Instead of wrapping the entire file content in `{ }`, the semicolon indicates the namespace applies to everything following it.
</details>

### Q3. "Target-Typed New" allows you to write:
A. `List<int> list = new List<int>();`  
B. `List<int> list = new();`  
C. `var list = new();`  
D. `new list;`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If the type is explicitly defined on the left (`List<int>`), the compiler infers the type for `new()`, removing redundancy.
</details>

### Q4. Which C# version introduced "Raw String Literals"?
A. C# 7  
B. C# 8  
C. C# 11  
D. C# 1.0  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Note: The source text includes Raw String Literals in the legacy/modern context (C# 11 usually), but it's often grouped with recent features.
</details>

### Q5. A Raw String Literal starts and ends with:
A. `"`  
B. `@"`  
C. `"""` (at least 3 quotes)  
D. `$`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`""" content """`. It allows multi-line strings containing special characters (like quotes, backslashes) without any escaping.
</details>

---

## MEDIUM MCQs

### Q6. Implicit Usings (enabled in .csproj) automatically include namespaces like:
A. `System.Windows.Forms`  
B. `System`, `System.Linq`, `System.Collections.Generic` (for Console/Web apps).  
C. `System.Data.SqlClient`  
D. All installed packages.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The SDK automatically generates a global using file for common namespaces based on the project type.
</details>

### Q7. How do you interpolate variables into a Raw String Literal?
A. It is not possible.  
B. Use `$` prefix and `{var}`. But if the string contains `{`, you can use `$$` prefix and `{{var}}` to disambiguate.  
C. Use `+` operator.  
D. Use `string.Format`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The number of `$` signs determines how many braces are needed to trigger interpolation. `$$""" {{ 1 + 1 }} """` output is ` 2 `. `$$""" { 1 + 1 } """` output is ` { 1 + 1 } `.
</details>

### Q8. Natural Types for Lambdas means:
A. `var f = () => Console.Write("Hi");` is valid in C# 10.  
B. Lambda types are always object.  
C. Lambdas must be cast to `Action` explicitly.  
D. Lambdas are integers.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Before C# 10, the compiler couldn't infer a delegate type (Action/Func) for `var`. Now it attempts to infer a "natural" delegate type.
</details>

### Q9. Can a File-Scoped Namespace file contain multiple namespaces?
A. Yes.  
B. No. It enforces one namespace per file.  
C. Multiple nested namespaces are allowed.  
D. Yes, if they are classes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The syntax `namespace X;` implies "everything in this file belongs to X". You cannot switch to `namespace Y;` later in the same file.
</details>

### Q10. Target-typed new works for Field initialization?
A. No.  
B. Yes. `private Dictionary<int, string> _cache = new();`  
C. Only in methods.  
D. Only for arrays.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It works anywhere the type can be inferred from context, including fields and properties.
</details>

---

## HARD MCQs

### Q11. Can `global using` map a type alias?
A. No, only namespaces.  
B. Yes. `global using Str = System.String;`  
C. Only for static classes.  
D. Only for interfaces.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You can define global aliases, which is powerful for resolving naming conflicts or shortening common complex types project-wide.
</details>

### Q12. Default values for Lambda parameters (C# 12 preview feature often discussed with C# 10 enhancements):
A. `var f = (int x = 0) => x * 2;`  
B. Not supported.  
C. Only in local functions.  
D. Only in interfaces.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Modern C# allows lambdas to have optional parameters with default values, making them fully feature-par with methods.
</details>

### Q13. Structs in C# 10 can have:
A. Parameterless constructors `public S() { ... }`  
B. Destructors.  
C. Inheritance from classes.  
D. Virtual methods.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Previous versions forbade explicit parameterless constructors on structs (forcing zero-init). C# 10 allows them to set default state validly.
</details>

### Q14. Raw String Literals indentation rule:
A. No indentation allowed.  
B. The indentation of the closing quotes `"""` defines the "baseline". Any whitespace to the left of that baseline in the content lines is stripped.  
C. All whitespace is kept.  
D. All whitespace is removed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This smart indentation removal allows you to align the string block with your code for readability without including that indentation in the actual string value.
</details>

### Q15. `[CallerArgumentExpression]` attribute (C# 10) allows:
A. A method to capture the text source code of an expression passed as an argument.  
B. Checking for nulls.  
C. Reflection.  
D. Logging stack trace.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Used heavily in `ArgumentNullException.ThrowIfNull(arg)`. It allows the method to know the *name* of the variable passed to it automatically (e.g., "arg").
</details>
