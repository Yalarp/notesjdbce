# 05_CRUD_Operations_MVC – MCQs

## EASY MCQs

### Q1. In the MVC Controller, what attribute is used to handle form submissions?
A. `[HttpGet]`
B. `[HttpPost]`
C. `[HttpPut]`
D. `[ServiceFilter]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`[HttpPost]` action methods are invoked when a user submits a form (Post request). This distinguishes the processing action from the display action (GET).
</details>

### Q2. What is the purpose of `ModelState.IsValid`?
A. To check if the database is online.
B. To check if the incoming model data satisfies the validation rules (Data Annotations like `[Required]`) defined in the class.
C. To check if the user is logged in.
D. To validate the HTML syntax.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Before saving data, the controller checks `ModelState.IsValid`. If false, it means the user's input violated validation rules (e.g., left a required field empty), and the form should be re-displayed with errors.
</details>

### Q3. What does `RedirectToAction("Index")` do?
A. It returns the Index View directly.
B. It sends a HTTP 302 Found response to the browser, telling it to make a new GET request to the Index action.
C. It deletes the Index.
D. It throws an error.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Redirecting follows the Post-Redirect-Get (PRG) pattern. It prevents the user from accidentally re-submitting the form if they refresh the page after a successful save.
</details>

### Q4. Which Tag Helper is used to bind an input element to a model property?
A. `asp-controller`
B. `asp-action`
C. `asp-for`
D. `asp-validation`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`asp-for="PropertyName"` automatically generates the `id`, `name`, and `value` attributes for the HTML input tag based on the Model property, ensuring correct data binding.
</details>

### Q5. What does the `[ValidateAntiForgeryToken]` attribute prevent?
A. SQL Injection
B. Cross-Site Request Forgery (CSRF) attacks
C. Cross-Site Scripting (XSS)
D. Denial of Service (DoS)

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
CSRF adds a hidden token to the form. This attribute validates that the token in the incoming POST request matches the one generated for the user's session, ensuring the request originated from your application's form.
</details>

---

## MEDIUM MCQs

### Q6. Why do we often have two Action Methods for "Create" (e.g., `public ActionResult Create()` and `public ActionResult Create(Employee emp)`)?
A. It is a mistake.
B. One is for the GET request (to display the empty form) and the other is for the POST request (to process the submitted data).
C. One is for admins, one is for users.
D. One is for creation, one is for update.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is standard practice. The HttpGet method prepares the view (e.g., populating dropdowns). The HttpPost method (overloaded) accepts the bound model and attempts to save it.
</details>

### Q7. In the Edit(Post) action, if `ModelState.IsValid` is false, what should you return?
A. `RedirectToAction("Index")`
B. `View(emp)`
C. `NotFound()`
D. `Content("Error")`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You should return the View passing back the submitted model object (`emp`). This preserves user input so they don't have to Retype it, and allows Tag Helpers to display the validation error messages.
</details>

### Q8. What is the purpose of `ViewData["DepartmentId"] = new SelectList(...)`?
A. To create a new table.
B. To prepare the key-value pairs needed to render a `<select>` dropdown list in the View.
C. To validate the Department Id.
D. To filter the database.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`SelectList` is a helper class holding the collection of items, the data value field (Id), and the data text field (Name). The view uses this to render the `<option>` elements.
</details>

### Q9. What happens if you delete an entity that has related child records (e.g., deleting a Department with Employees) without Cascade Delete configuration?
A. It works fine.
B. The database triggers a referential integrity constraint violation error (Foreign Key conflict).
C. The children are automatically deleted.
D. The children are moved to another department.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
By default, SQL Server enforces FK constraints. You cannot delete a parent if children exist. You must either enable Cascade Delete (in EF config) or handle deletions manually.
</details>

### Q10. What does `asp-validation-summary="ModelOnly"` display?
A. Errors for individual fields.
B. Global errors (Model-level) that are not associated with a specific property key.
C. All errors including field errors.
D. No errors.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Field-specific errors are usually shown next to the input using `asp-validation-for`. "ModelOnly" summary is for general errors like "Invalid login attempt" or complex cross-property validation failures.
</details>

---

## HARD MCQs

### Q11. How does Model Binding work in the Create(POST) method?
A. You manually read `Request.Form`.
B. The framework uses the names of the form fields (generated by `asp-for`) to match and populate the properties of the `Employee` parameter automatically.
C. It uses Reflection to guess the data.
D. It downloads the data from the cloud.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The Model Binder looks at form data, route data, and query strings. It matches keys (e.g., "Name", "Email") to the properties of the action method argument object and converts types (string to int/date) automatically.
</details>

### Q12. In the `Delete` action, why do we need `[ActionName("Delete")]` on the POST method `DeleteConfirmed`?
A. It is optional.
B. Because C# does not allow two methods with the precise same signature (`Delete(int id)` for GET and `Delete(int id)` for POST). We name the C# method `DeleteConfirmed` but map it to the "Delete" URL action name.
C. To make it secure.
D. To delete faster.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Method overloading requires different parameters. Since both Delete GET and Delete POST typically take just `int id`, we must change the C# method name. The attribute aliases it back to "Delete" for routing purposes.
</details>

### Q13. What is the difference between `IEnumerable` and `IQueryable` when passing models to Views?
A. No difference.
B. `IQueryable` executes in the database; `IEnumerable` executes in memory. Passing `IQueryable` to a view is dangerous because the View might trigger additional SQL queries (Lazy Loading / N+1 problem) during iteration.
C. `IEnumerable` is for SQL.
D. `IQueryable` is read-only.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Ideally, Controllers should materialize the data (call ToList()) before passing to the View. Passing an unexecuted `IQueryable` risks the View logic accidentally changing the SQL query or causing performance issues.
</details>

### Q14. What does the `[Bind("Id,Name,Email")]` attribute do in a controller action parameter?
A. It binds only the specified properties, protecting against "Overposting" (Mass Assignment) attacks.
B. It binds everything except those properties.
C. It validates the properties.
D. It is deprecated.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
If a hacker adds an input `<input name="IsAdmin" value="true" />` to the form, the default binder might overwrite your IsAdmin property. `[Bind]` whitelists strictly which properties are allowed to be updated.
</details>

### Q15. Why use `await Html.RenderPartialAsync(...)` instead of `@Html.Partial(...)`?
A. Partial is deprecated.
B. `RenderPartialAsync` writes directly to the response stream, which is more performant effectively than buffering the partial result into a String (HtmlString) like `@Html.Partial` does.
C. It looks cooler.
D. It allows JavaScript.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The Async Render methods are preferred in Core for performance reasons, avoiding large string allocations for partial views.
</details>
