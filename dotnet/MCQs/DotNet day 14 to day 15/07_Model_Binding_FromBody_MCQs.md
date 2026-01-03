# 07_Model_Binding_FromBody – MCQs

## EASY MCQs

### Q1. What attribute binds a parameter from the Request Body (JSON)?
A. `[FromQuery]`
B. `[FromBody]`
C. `[FromRoute]`
D. `[FromForm]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It tells the model binder to deserializing the request stream.
</details>

### Q2. What attribute binds a parameter from the URL path (e.g., /api/user/5)?
A. `[FromHeader]`
B. `[FromRoute]`
C. `[FromQuery]`
D. `[FromBody]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Maps tokens like `{id}` in the route template.
</details>

### Q3. Can you have multiple `[FromBody]` parameters in a single action?
A. Yes.
B. No. The request body is a stream that can only be read once.
C. Only if they are integers.
D. Yes, if separated by commas.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is a technical limitation. If you need multiple objects, wrap them in a DTO (Data Transfer Object).
</details>

### Q4. `[FromQuery]` is used to bind data from where?
A. The HTTP Headers.
B. The Query String (e.g., `?name=abc`).
C. The Database.
D. The Cookies.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Standard for optional parameters like filters, sorting, paging.
</details>

### Q5. If you use `[ApiController]`, do you need to explicitly add `[FromBody]` for complex types?
A. Yes.
B. No, it is inferred automatically for complex object types.
C. Only for GET requests.
D. Only for ints.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is one of the conveniences of the `[ApiController]` attribute.
</details>

---

## MEDIUM MCQs

### Q6. Which attribute is used to upload files?
A. `[FromBody]`
B. `[FromForm]` (binding `IFormFile`).
C. `[FromRoute]`
D. `[FromFile]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
File uploads are sent as `multipart/form-data`.
</details>

### Q7. How do you bind a custom HTTP header "X-API-KEY" to a parameter?
A. `[FromHeader(Name = "X-API-KEY")] string key`
B. `[FromRoute]`
C. `context.Headers["..."]`
D. `[FromBody]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
You can specify the exact header name in the attribute property.
</details>

### Q8. What happens if Model Binding fails (e.g. string passed for int)?
A. The parameter is null/default. If `[ApiController]` is used, a 400 Bad Request is returned automatically.
B. The server crashes.
C. It keeps the previous value.
D. It reads as 0.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Validation and binding are tightly coupled. Invalid types affect `ModelState.IsValid`.
</details>

### Q9. Can you mix `[FromRoute]` and `[FromBody]` in the same action?
A. No.
B. Yes, commonly used in PUT requests (ID from route, data from body).
C. Only in .NET 1.0.
D. Yes, but only for strings.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Put(int id, Item item)` is the classic example.
</details>

### Q10. What attribute allows injecting a service directly into an action method?
A. `[FromDI]`
B. `[FromServices]`
C. `[Inject]`
D. `[Service]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Keeps the constructor clean if a dependency is only needed for one specific edge-case action.
</details>

---

## HARD MCQs

### Q11. If a parameter is a simple type (int, string) and no attribute is present, where does `[ApiController]` infer it comes from?
A. Body.
B. Route (if matching template) or Query String.
C. Header.
D. Form.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If the name matches a route parameter, it's `FromRoute`. Otherwise, it defaults to `FromQuery`.
</details>

### Q12. Why can't `[FromBody]` bind to `GET` requests usually?
A. GET requests technically can have bodies, but it is semantically incorrect and many clients/proxies strip them.
B. GET is too fast.
C. It works perfectly fine.
D. GET bodies are encrypted.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
While HTTP spec doesn't strictly forbid it, it's widely unsupported. Binding assumes GET params come from URL.
</details>

### Q13. `public IActionResult Search([FromQuery] FilterModel filter)`: FilterModel is a class. How does this work?
A. It won't work.
B. The properties of FilterModel are matched against individual query string keys (e.g. `?Name=A&Age=10`).
C. It expects a JSON string in the URL.
D. It requires `[FromBody]`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is "Complex Type from Query". The binder creates the object and maps properties flattened from the query string.
</details>

### Q14. What happens if you forget `[FromBody]` on a parameter in a controller WITHOUT `[ApiController]`?
A. It works fine.
B. It acts as `[FromQuery]` (or Form), attempting to find fields in the URL/Form, and usually resulting in null/default object because the JSON body isn't parsed.
C. It throws an error.
D. It reads from Session.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This was a very common bug in older ASP.NET Core versions. The body content would be ignored.
</details>

### Q15. Does `[FromRoute]` support complex objects?
A. No, technically not directly capable of constructing a full object hierarchy from a customized segment effectively, usually used for simple IDs. Use `[FromQuery]` for complex flat mappings.
B. Yes, always.
C. Maybe.
D. Only if JSON.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Route segments are usually single values.
</details>
