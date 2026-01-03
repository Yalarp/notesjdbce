# 09_Model_Binding – MCQs

## EASY MCQs

### Q1. What involves "Model Binding" in ASP.NET Core?
A. Binding a book.
B. Automatically mapping data from an HTTP request (Form, URL, etc.) to controller action parameters.
C. Connecting to SQL.
D. Linking CSS files.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It automates the tedious task of reading `Request.Form` or `Request.QueryString` and converting types.
</details>

### Q2. Which attribute specifies that a parameter should be bound from the Query String?
A. `[FromRoute]`
B. `[FromForm]`
C. `[FromQuery]`
D. `[FromBody]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Forces the binder to look only at URL parameters (e.g. `?id=5`).
</details>

### Q3. By default, what is the order of data sources checked?
A. Route -> Query -> Form
B. Form -> Route -> Query
C. Query -> Route -> Form
D. Random

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Form data (most specific/secure) -> Route Values -> Query String (least specific).
</details>

### Q4. Can Model Binding bind complex objects (like `Student` class)?
A. No, only int and string.
B. Yes, by matching request parameter names to the object property names.
C. Only if the class is static.
D. Only with XML.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It recursively traverses the graph. `Student.Address.City` binds to `<input name="Address.City" />`.
</details>

### Q5. What happens if binding fails for an integer parameter (e.g. user sends "abc")?
A. Application crashes.
B. The parameter is set to default (0), and `ModelState.IsValid` becomes false.
C. The parameter is null.
D. It returns 404.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It provides a safe failure mechanism. You must check `ModelState` to detect the error.
</details>

---

## MEDIUM MCQs

### Q6. Which attribute is used to inject a service into an Action Method via Dependency Injection, rather than binding from the request?
A. `[FromServices]`
B. `[Inject]`
C. `[Service]`
D. `[Bind]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`public IActionResult Index([FromServices] ILogger log)` allows method-level injection.
</details>

### Q7. What is the purpose of the `[Bind("Name, Email")]` attribute on an action parameter?
A. To rename properties.
B. To protect against **Over-Posting** (Mass Assignment) by specifying an inclusion list of allowed properties.
C. To bind everything.
D. To validate data.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It prevents a distinct security vulnerability where a malicious user adds extra fields (e.g. `IsAdmin=true`) to the POST request.
</details>

### Q8. When using `[FromBody]`, what Media Type is typically expected?
A. `application/x-www-form-urlencoded`
B. `application/json`
C. `text/plain`
D. `image/png`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
 `[FromBody]` uses configured Input Formatters (usually JSON) to read the raw request stream. It differs from Form binding.
</details>

### Q9. Why is `IFormCollection` generally discouraged?
A. It is deprecated.
B. It is not type-safe, hard to test, and requires manual string parsing, defeating the purpose of MVC's automatic binding.
C. It is slower.
D. It exposes passwords.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Model binding is cleaner and preferred. `IFormCollection` is a low-level fallback.
</details>

### Q10. Does Model Binding perform validation?
A. No.
B. Yes, implicit validation (type conversion) happens during binding. Explicit validation (Data Annotations) happens immediately after binding. Both contribute to `ModelState`.
C. Only type checking.
D. Only regex.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Binding and Validation are two steps of the same pipeline phase.
</details>

---

## HARD MCQs

### Q11. Which attribute prevents a specific property from EVER being bound?
A. `[BindNever]`
B. `[NoBind]`
C. `[Ignore]`
D. `[ReadOnly]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Placed on the Model property (e.g. `public int Id { get; set; }`) to ensure it is ignored by the binder even if data is sent.
</details>

### Q12. If you have an action `public IActionResult Edit(int id)` and the request URL is `/Edit/5?id=10`, which value is bound to `id`?
A. 5 (from Route), assuming default routing `{action}/{id}`.
B. 10 (from Query).
C. Error.
D. 15.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Route values have higher priority than Query String values.
</details>

### Q13. Can `[FromBody]` be applied to multiple parameters in a single action method?
A. Yes.
B. No. The request body is a stream that can typically be read only once.
C. Only for GET requests.
D. Yes, if they are strings.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
 Generally, you can only bind one parameter from the body unless buffering is enabled, but standard design allows only one object from JSON body.
</details>

### Q14. What is a "Custom Model Binder"?
A. A binder for books.
B. A class implementing `IModelBinder` used to handle complex parsing logic not supported by the default binder (e.g. parsing a pipe-separated string into a List).
C. A standard feature.
D. A database tool.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You can override standard binding behavior globally or per-type/parameter.
</details>

### Q15. How does Model Binding handle Lists/Arrays in a Form POST?
A. It cannot.
B. It expects keys like `items[0]`, `items[1]`, etc. (Sequential indices).
C. It uses comma-separated strings.
D. It requires JSON.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The underlying format for binding collections from form-data uses index notation.
</details>
