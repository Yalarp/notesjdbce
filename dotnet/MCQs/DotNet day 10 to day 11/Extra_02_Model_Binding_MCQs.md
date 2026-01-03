# Extra_02_Model_Binding – MCQs

## EASY MCQs

### Q1. What is "Model Binding" in ASP.NET Core?
A. Connecting to a database.
B. The process of automatically mapping data from HTTP requests (query string, form, route) to action method parameters.
C. Binding a view to a layout.
D. Creating a model class.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It saves you from manually extracting values like `Request.Form["Name"]`. The framework does it for you: `public IActionResult Save(string Name)`.
</details>

### Q2. Is Model Binding case-sensitive?
A. Yes, "id" and "ID" are different.
B. No, it is **Case-Insensitive**.
C. Only for query strings.
D. Only for JSON.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
For developer convenience, `public IActionResult Get(int id)` matches URL `?ID=5` or `?Id=5`.
</details>

### Q3. Which data source has the highest priority during standard Model Binding?
A. Query String.
B. Form Data (POST body).
C. Route Values.
D. Cookies.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Typical order: 1. Form Data, 2. Route Data, 3. Query String. Form data (body) usually overrides URL parameters.
</details>

### Q4. Model binding can map form fields to:
A. Primitive types (int, string) only.
B. Complex types (Classes) only.
C. Both Primitive types and Complex types.
D. Nothing.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
It handles simple arguments `(int age)` and complex objects `(Student student)`.
</details>

### Q5. To bind a nested property like `Student.Address.City` in a form, what `name` attribute should the input tag have?
A. `City`
B. `AddressCity`
C. `Address.City` (Dot notation)
D. `Address[City]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Dot notation is used for object traversal. `<input name="Address.City" />` maps to `student.Address.City`.
</details>

---

## MEDIUM MCQs

### Q6. What is the purpose of the `[Bind]` attribute?
A. To bind data.
B. To protect against **Over-Posting** attacks (Mass Assignment) by specifying exactly which properties to include (allowlist).
C. To validate data.
D. To rename properties.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If your model has an `IsAdmin` property, a hacker might send `IsAdmin=true` in the form. `[Bind("Name,Email")]` ensures `IsAdmin` is ignored/not updated.
</details>

### Q7. If model binding fails (e.g., sending text "abc" for an `int age` parameter), what happens?
A. An exception is thrown immediately.
B. The parameter is set to default (0), and the error is recorded in `ModelState`.
C. The controller is deleted.
D. It returns 500.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is "safe" binding. You check `ModelState.IsValid` to see if conversion succeeded.
</details>

### Q8. When would you use `FormCollection` instead of Model Binding?
A. Always.
B. When you don't have a specific model class, or you need to process dynamic form fields that are unknown at compile time.
C. For performance.
D. For security.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`FormCollection` gives you raw dictionary access: `collection["key"]`. Useful for dynamic scenarios.
</details>

### Q9. Which attribute forces binding from the Route data only?
A. `[FromQuery]`
B. `[FromGeneric]`
C. `[FromRoute]`
D. `[FromBody]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Explicit attributes guide the source. `[FromRoute] int id` ignores query/form data and looks only at the route segments.
</details>

### Q10. For a POST request with JSON body, which attribute is required on the parameter?
A. `[ToJson]`
B. `[FromBody]`
C. `[Bind]`
D. `[FromJson]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
By default, MVC tries form-data. To use the JSON formatter for the request body, you must explicitly apply `[FromBody]`.
</details>

---

## HARD MCQs

### Q11. In `public IActionResult Edit([Bind("Id, Name")] Student student)`, if the request contains `Age=20`, what will `student.Age` be?
A. 20
B. Null / Default (0).
C. An error.
D. Undefined.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Since "Age" is NOT in the Bind include list, the binder ignores that incoming value. The property remains at its default value.
</details>

### Q12. Can you bind a List/Collection?
A. No.
B. Yes, by using index notation in form fields (e.g., `students[0].Name`, `students[1].Name`).
C. Yes, but only with JSON.
D. Only Arrays.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The model binder parses indexed keys to populate lists/arrays.
</details>

### Q13. `ModelState.IsValid` checks:
A. If the database is online.
B. If Model Binding succeeded (data types converted) AND Data Validations (Attributes like Required) passed.
C. Only if Model Binding succeeded.
D. Only if Data Validations passed.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is the aggregate status of binding + validation rules.
</details>

### Q14. Can you create a **Custom Model Binder**?
A. No, you must use the built-in one.
B. Yes, by implementing `IModelBinder` and registering it. This allows custom parsing logic (e.g., parsing a complex string format into an object).
C. Yes, but only in C++.
D. Only for dates.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is an advanced extension point for specific parsing needs not covered by the default binder.
</details>

### Q15. Why is `[ValidateAntiForgeryToken]` often paired with Model Binding on POST?
A. To speed it up.
B. Security. While Model Binding maps data, AntiForgeryToken prevents CSRF (Cross-Site Request Forgery) attacks where a malicious site submits a form to your site.
C. To duplicate the data.
D. To validate emails.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Almost every state-changing POST action binding to a model should define this attribute for security.
</details>
