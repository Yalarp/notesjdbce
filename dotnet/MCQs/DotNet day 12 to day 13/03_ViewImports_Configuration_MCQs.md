# 03_ViewImports_Configuration – MCQs

## EASY MCQs

### Q1. What is the main purpose of the `_ViewImports.cshtml` file?
A. To import JavaScript files.
B. To define common namespaces and directives (like `@using`, `@addTagHelper`) used across multiple razor views.
C. To define the layout HTML.
D. To configure the database connection.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It acts as a global configuration file for Razor views, so you don't have to duplicate `@using` statements in every single .cshtml file.
</details>

### Q2. Where should you place `_ViewImports.cshtml` to make it apply to ALL views in the app?
A. In the `Controllers` folder.
B. In the root `Views` folder.
C. In the `wwwroot` folder.
D. In `Program.cs`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Placing it in `Views/` ensures it is inherited by all subfolders (Home, Shared, etc.).
</details>

### Q3. Which directive enables Tag Helpers in your views?
A. `@using TagHelpers`
B. `@enableTagHelper`
C. `@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers`
D. `@tags`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The standard syntax to enable built-in ASP.NET Core Tag Helpers is `@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers`.
</details>

### Q4. Does `_ViewImports.cshtml` start with an underscore?
A. Yes, by convention for special Razor files.
B. No.
C. Optional.
D. Only on Linux.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Underscore (`_`) prefixes denote files that are not directly servable or are special system files (like `_Layout`, `_ViewStart`, `_ViewImports`).
</details>

### Q5. Can you define `@using System.Linq` in `_ViewImports.cshtml`?
A. No.
B. Yes, and it will be available in all views.
C. Yes, but it only works for C# files.
D. No, only custom namespaces allowed.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Any standard C# namespace can be imported, making those types available in Razor expressions.
</details>

---

## MEDIUM MCQs

### Q6. How does "Hierarchical Behavior" apply to `_ViewImports.cshtml`?
A. It doesn't; only the root one works.
B. You can have multiple `_ViewImports` files (e.g., one in `Views/` and one in `Views/Admin/`). The view inherits directives from BOTH (additive/override).
C. The child folder file completely replaces the root one.
D. The root one replaces the child one.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It supports inheritance. `Views/Admin/_ViewImports.cshtml` will add to (or override) what was defined in `Views/_ViewImports.cshtml` for views inside the Admin folder.
</details>

### Q7. What is the effect of `@removeTagHelper`?
A. Deletes the helper class.
B. Disables a specific Tag Helper in the scope of the views.
C. Removes HTML tags from the output.
D. None.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Useful if a Tag Helper is conflicting with standard HTML behavior or another library, allowing you to turn it off.
</details>

### Q8. Can you use `@inject` in `_ViewImports.cshtml`?
A. No, only in views.
B. Yes, this will make the injected service property available to all applicable views automatically.
C. Yes, but it crashes at runtime.
D. Only for ILogger.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
For example, `@inject IConfiguration Config` allows you to access `Config["Key"]` in every view without re-injecting it.
</details>

### Q9. Why should you avoid putting `@model MyType` in `_ViewImports.cshtml`?
A. You can't.
B. Because every view usually requires a specific/different model. Defining it globally would force all views to accept that same model type.
C. It causes a compilation error.
D. It slows down the app.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`@model` defines the single specific type for a view. Setting it globally defeats the purpose of strong typing for different pages.
</details>

### Q10. What does `@tagHelperPrefix th:` do?
A. Adds "th:" to all HTML tags.
B. Requires you to use the prefix "th:" (e.g., `<th:form ...>`) to invoke Tag Helpers, distinguishing them from standard HTML tags.
C. It is a typo.
D. It imports Thymeleaf.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is useful to avoid conflicts with standard HTML tags or to make it explicit when server-side logic is being invoked.
</details>

---

## HARD MCQs

### Q11. If `Views/_ViewImports.cshtml` has `@using NamespaceA` and `Views/Home/_ViewImports.cshtml` has `@using NamespaceB`, what namespaces does `Index.cshtml` (inside Home) see?
A. Only NamespaceB.
B. Only NamespaceA.
C. Both NamespaceA and NamespaceB.
D. Neither.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The directives are additive.
</details>

### Q12. If a Tag Helper is added in the root ViewImports but removed in a subfolder ViewImports via `@removeTagHelper`, what is the result for views in that subfolder?
A. It is enabled.
B. It is disabled (removed).
C. Error.
D. Undefined.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The nearer configuration (subfolder) takes precedence or modifies the set of directives inherited from the parent.
</details>

### Q13. Can `_ViewImports.cshtml` contain HTML markup?
A. Yes, it renders at the top of the page.
B. No, it creates a compiler error or is ignored. It supports only Razor directives.
C. Yes, but it is invisible.
D. Only comments.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is strictly for configuration directives (`using`, `addTagHelper`, etc.) and does not generate output.
</details>

### Q14. How do you resolve a type name conflict (e.g. `Date` class in two namespaces) in a View?
A. You cannot.
B. Use the fully qualified name in the View (e.g. `MyNamespace.Date`). Or use an alias in `_ViewImports.cshtml` (e.g. `@using MyDate = MyNamespace.Date`).
C. Delete one class.
D. Restart the server.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Standard C# aliasing rules work in Razor directives too.
</details>

### Q15. Is `_ViewImports.cshtml` executed for every request?
A. It is compiled into the View assembly at build/startup. Its directives are applied during the code generation of the View classes.
B. Yes, it reads the file from disk every time.
C. No, only once per user.
D. Only when `_Layout` changes.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Razor views are compiled into C# classes. The contents of `_ViewImports` are essentially merging `using` statements into the generated class file for each view.
</details>
