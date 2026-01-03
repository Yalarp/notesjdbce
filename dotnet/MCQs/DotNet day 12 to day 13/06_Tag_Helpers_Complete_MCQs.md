# 06_Tag_Helpers_Complete – MCQs

## EASY MCQs

### Q1. What is the main syntax difference between Tag Helpers and HTML Helpers?
A. Tag Helpers use C# method calls (e.g., `@Html.TextBoxFor`).
B. Tag Helpers look like standard HTML tags with special `asp-` attributes (e.g., `<input asp-for="...">`).
C. Tag Helpers use XML syntax.
D. Tag Helpers are deprecated.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Tag Helpers flow naturally with HTML, making them more readable and designer-friendly compared to the context-switching C# syntax of HTML Helpers.
</details>

### Q2. Which attribute on the `<a>` tag specifies the target controller?
A. `controller`
B. `data-controller`
C. `asp-controller`
D. `target-controller`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The `asp-controller` attribute is processed by the AnchorTagHelper to generate the correct href URL.
</details>

### Q3. What does the `asp-for` attribute do on an `<input>` element?
A. It styles the input.
B. It binds the input to a model property, automatically setting `name`, `id`, `value`, and validation attributes.
C. It loops through a list.
D. It validates the password.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is the primary way to achieve two-way binding and model integration in views.
</details>

### Q4. Which directive is required in `_ViewImports.cshtml` to enable Tag Helpers?
A. `@enableTagHelpers`
B. `@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers`
C. `@using TagHelpers`
D. `@import TagHelpers`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This wildcard directive imports all built-in Tag Helpers from the MVC assembly.
</details>

### Q5. What is the purpose of `asp-append-version="true"` on an `<img>` tag?
A. To rotate the image.
B. To perform "Cache Busting" by appending a unique hash of the file content to the URL.
C. To resize the image.
D. To fallback to a CDN.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If the image file changes on the server, the hash changes, forcing the browser to download the new version instead of using a stale cached copy.
</details>

---

## MEDIUM MCQs

### Q6. How do you generate a dropdown list using Tag Helpers?
A. `<dropdown list="items" />`
B. `<select asp-for="Property" asp-items="ListSource"></select>`
C. `<input type="select" />`
D. `@Html.DropDownList`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The `asp-items` attribute accepts an `IEnumerable<SelectListItem>`, often passed via ViewBag or a ViewModel property.
</details>

### Q7. When using `[DataType(DataType.Password)]` on a model property, what HTML does `<input asp-for="Password" />` generate?
A. `<input type="text" ... />`
B. `<input type="password" ... />`
C. `<input type="hidden" ... />`
D. `<password ... />`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The InputTagHelper respects DataAnnotations and infers the correct HTML `type` attribute.
</details>

### Q8. What does `asp-validation-summary="ModelOnly"` display?
A. All errors including property-level errors.
B. Only errors associated with the Model itself (e.g., business logic failures added via `ModelState.AddModelError("", "Global Error")`), excluding individual property validation errors.
C. No errors.
D. Only successful messages.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is useful for displaying top-level form errors, while property-specific errors are usually shown next to the fields using `asp-validation-for`.
</details>

### Q9. Which attribute automatically generates an Anti-Forgery Token inside a `<form>`?
A. `asp-antiforgery="true"` (Default behavior for FormTagHelper).
B. `@Html.Token()`
C. `secure="true"`
D. It must be added manually.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The FormTagHelper automatically generates the hidden `__RequestVerificationToken` input for POST forms unless explicitly disabled.
</details>

### Q10. What happens if you use `asp-route-id="5"` on an anchor tag?
A. It adds `?id=5` to the URL query string OR adds `/5` to the URL path, depending on the route configuration.
B. It creates a variable named id.
C. It navigates to ID 5 immediately.
D. It fails if the route doesn't have an ID.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Tag Helpers use the routing system. If the route pattern is `{controller}/{action}/{id}`, it generates a path segment. If not, it generates a query string parameter.
</details>

---

## HARD MCQs

### Q11. If you want to use an **Enum** to populate a Select lists, which helper method is commonly used?
A. `Enum.GetValues()`
B. `Html.GetEnumSelectList<TEnum>()`
C. `ViewBag.Enum`
D. `TagHelper.Enum`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Calls `Html.GetEnumSelectList<MyEnum>()` inside `asp-items` to automatically generate `SelectListItem`s for each enum member.
</details>

### Q12. Can you create **Custom Tag Helpers**?
A. No.
B. Yes, by creating a class inheriting from `TagHelper` and overriding the `Process` or `ProcessAsync` method.
C. Yes, by writing JavaScript.
D. Only by modifying the ASP.NET source code.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Custom Tag Helpers allow you to create reusable UI components (e.g., `<my-modal title="...">`) that encapsulate complex HTML/C# logic.
</details>

### Q13. How does the `LabelTagHelper` determine the text to display?
A. It only uses the property name.
B. It checks `[Display(Name="...")]` or `[DisplayName("...")]`. If absent, it falls back to the property name.
C. It checks the database.
D. It is always empty.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It introspects the model metadata to provide user-friendly labels automatically.
</details>

### Q14. What does the `asp-all-route-data` attribute accept?
A. A string.
B. A Dictionary (Key-Value pairs) representing multiple route values.
C. A JSON object.
D. An Array.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Useful when you have a dynamic set of query parameters to add to a link, instead of hardcoding `asp-route-param1`, `asp-route-param2`, etc.
</details>

### Q15. Why might you use `<!` (bang symbol) with a Tag Helper?
A. To comment it out.
B. To force it to be treated as a standard HTML tag, ignoring the Tag Helper processing (Opt-out).
C. To treat it as high priority.
D. It is a syntax error.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Using `<!span>` prevents the SpanTagHelper from processing that element. (Though the syntax is rare, typically you just don't use the `asp-` attributes if you don't want processing). *Note: The actual opt-out character is `!` before the tag name, e.g. `<!form ...>`.
</details>
