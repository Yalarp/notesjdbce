# 06_Action_Return_Types – MCQs

## EASY MCQs

### Q1. Which return type offers the most flexibility for returning different HTTP status codes?
A. `string`
B. `void`
C. `IActionResult`
D. `int`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`IActionResult` allows returning any HTTP response (Ok, NotFound, BadRequest) without being tied to a specific data type.
</details>

### Q2. What is the benefit of `ActionResult<T>` over `IActionResult`?
A. It is faster.
B. It provides Type Safety regarding the data structure returned (helpful for Swagger) while still allowing flexible status codes.
C. It allows returning multiple types.
D. It encrypts the data.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It acts as a wrapper. You can return `T` directly (implicit cast to 200 OK) or `Result` (like NotFound).
</details>

### Q3. Which helper method returns a 404 status code?
A. `return Error();`
B. `return NotFound();`
C. `return Missing();`
D. `return Null();`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Standard convenience method in `ControllerBase`.
</details>

### Q4. What does `return Ok(data)` produce?
A. 200 OK status with JSON body containing `data`.
B. 201 Created.
C. 200 OK with empty body.
D. 400 Bad Request.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The `Ok(object)` overload simplifies successful responses.
</details>

### Q5. If an action returns `void`, what is the typical HTTP status code?
A. 200 OK
B. 204 No Content
C. 404 Not Found
D. 500 Error

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The framework defaults to 204 No Content when a method returns void, implying success but no payload.
</details>

---

## MEDIUM MCQs

### Q6. Which return type is best for an asynchronous action fetching a list of books?
A. `IEnumerable<Book>`
B. `Task<ActionResult<IEnumerable<Book>>>`
C. `Task<IActionResult>`
D. `void`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is the most descriptive signature: Async (`Task`), Flexible HTTP status (`ActionResult`), and Strong Typing (`IEnumerable<Book>`).
</details>

### Q7. What is `CreatedAtAction` used for?
A. To create a new action.
B. To return a 201 Created status, including a `Location` header that points to the newly created resource's URL.
C. To redirect the user.
D. To validate the model.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It generates the URL based on the route name/values provided, ensuring HATEOAS compliance.
</details>

### Q8. Which status code represents "Forbidden" (Authenticated but not authorized)?
A. 401
B. 403
C. 404
D. 405

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
401 is "Who are you?" (Authentication). 403 is "You are known, but you can't come in here" (Authorization).
</details>

### Q9. What does `ProblemDetails` (via `return Problem()`) return?
A. A simple string.
B. A standardized JSON object (RFC 7807) containing error details like Title, Status, and TraceId.
C. An HTML page.
D. A 200 OK.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This provides a machine-readable format for specifying errors in HTTP APIs.
</details>

### Q10. If you return `T` (e.g., `Employee`) directly from a method `public Employee Get()`, what happens if the object is null?
A. Returns 200 OK with null body.
B. Returns 204 No Content.
C. Throws NullReferenceException.
D. Returns 404 Not Found.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
By default, the framework treats a null return value for a specific type as "No Content" (204).
</details>

---

## HARD MCQs

### Q11. Can `ActionResult<T>` return `NotFound()`?
A. No, it must return T.
B. Yes, because `ActionResult<T>` has an implicit conversion operator from `ActionResult`.
C. Only if T is nullable.
D. Only in GET requests.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This dual capability is its main feature. `return new NotFoundResult()` works fine in a method returning `ActionResult<T>`.
</details>

### Q12. What is the difference between `Unauthorized()` and `Forbid()`?
A. None.
B. `Unauthorized()` returns 401 (Need login). `Forbid()` returns 403 (Need permission).
C. `Forbid()` is for servers.
D. `Unauthorized()` logs the user out.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Exact mapping to HTTP semantics.
</details>

### Q13. When using `CreatedAtAction`, why do we use `nameof(GetById)` instead of the string "GetById"?
A. It looks cooler.
B. It provides compile-time safety; if the method name changes, the code won't compile, preventing broken links.
C. It is required by C#.
D. It improves performance.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Refactoring-safe code is best practice.
</details>

### Q14. `return Accepted()` corresponds to which status code and use case?
A. 200 OK.
B. 202 Accepted. Used when a request has been received for processing (e.g., long-running background job), but processing is not yet complete.
C. 201 Created.
D. 204 No Content.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Common in asynchronous processing patterns (queues).
</details>

### Q15. Why might you use `IActionResult` instead of `ActionResult<T>`?
A. If the method can return multiple incompatible data types (e.g., returns `Book` on success, but `Teacher` on partial success).
B. Because it's newer.
C. You should never use it.
D. If you hate generics.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
While rare, if the return schema varies wildly, `IActionResult` (or `object`) is the only common denominator. However, `ActionResult<T>` is preferred for documented APIs.
</details>
