# 05_HTTP_Methods_CRUD – MCQs

## EASY MCQs

### Q1. Which HTTP method is used to READ data?
A. POST
B. GET
C. PUT
D. DELETE

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
GET retrieves data and should have no side effects.
</details>

### Q2. Which HTTP method is used to DELETE data?
A. REMOVE
B. DELETE
C. CLEAR
D. DROP

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The standard HTTP verb for removal is DELETE.
</details>

### Q3. Which HTTP method is typically used to CREATE new data?
A. GET
B. POST
C. PUT
D. HEAD

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
POST submits an entity to the specified resource, often resulting in a state change or side effects on the server (creation).
</details>

### Q4. Which return type is best for an ASYNC action?
A. `ActionResult`
B. `Task<IActionResult>` or `Task<ActionResult<T>>`
C. `void`
D. `string`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Use `Task<T>` to leverage asynchronous execution (await) which frees up threads while waiting for I/O.
</details>

### Q5. What status code is returned by `CreatedAtAction`?
A. 200 OK
B. 201 Created
C. 204 No Content
D. 202 Accepted

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It returns 201 and adds a `Location` header pointing to the URL where the newly created resource can be retrieved.
</details>

---

## MEDIUM MCQs

### Q6. Why is `[FromBody]` used with POST/PUT?
A. To read data from the URL.
B. To serialize the response.
C. To force the model binder to read data from the HTTP Request Body (Request Payload) and deserialize it (usually from JSON).
D. To validate the data.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Complex data is sent in the body, not the URL. `[FromBody]` targets this stream.
</details>

### Q7. What is the semantic difference between PUT and POST?
A. None.
B. POST is for creating a subordinate resource (server generates ID). PUT is for updating or creating a resource at a known URI (Client provides ID/Full replacement).
C. POST is faster.
D. PUT is deprecated.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
POST: "Create a new member in the collection." PUT: "Update member #5 with this specific data."
</details>

### Q8. In EF Core, what does `context.Entry(entity).State = EntityState.Modified` do?
A. Deletes the entity.
B. Marks the entity as modified so that `SaveChanges()` generates an UPDATE SQL statement.
C. Creates a new entity.
D. Nothing.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is a way to force an update for a disconnected entity.
</details>

### Q9. Ideally, what should a successful DELETE request return?
A. 200 OK or 204 No Content.
B. 404 Not Found.
C. 201 Created.
D. 500 Error.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
204 No Content is very common as there is no data to return after deletion. 200 OK is used if you return status text or the deleted object.
</details>

### Q10. Why use `await` when calling `_context.SaveChangesAsync()`?
A. To slow it down.
B. To prevent the UI from freezing.
C. To allow the web server thread to handle other requests while waiting for the database to finish the operation (Scalability).
D. It is required by syntax.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
It prevents thread starvation in high-load web applications.
</details>

---

## HARD MCQs

### Q11. Is POST idempotent?
A. Yes.
B. No.
C. Only on Tuesdays.
D. Depends on the database.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Idempotent means "effect is the same if executed once or multiple times". Running POST multiple times creates multiple duplicate records. Running PUT/DELETE multiple times results in the same final state.
</details>

### Q12. How does `CreatedAtAction(nameof(GetById), new { id = 5 }, data)` construct the Location header?
A. It guesses.
B. It uses the Routing middleware to look up the route-template associated with the action named `GetById`, substitutes `id=5` into the template, and produces the absolute URL.
C. It hardcodes it.
D. It asks the client.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This ensures the location URL is always correct even if route templates change.
</details>

### Q13. In a PUT request, if the ID in the URL (`/api/items/5`) differs from the ID in the JSON body (`{id: 6, ...}`), what should you do?
A. Update item 5.
B. Update item 6.
C. Return 400 Bad Request.
D. Update both.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Ideally, IDs should match. Validating this consistency is a standard security/integrity check.
</details>

### Q14. What happens if you call a synchronous method (like `Thread.Sleep`) inside an async controller action?
A. It works fine.
B. It blocks the thread pool thread, negating the benefits of async/await and potentially hurting throughput ("Async over Sync" anti-pattern).
C. It throws an error.
D. It runs in background.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Never block an async thread synchronously.
</details>

### Q15. `ActionResult<IEnumerable<T>>`: Why wrap the collection in ActionResult?
A. No reason.
B. It allows you to return EITHER the clean data type `List<T>` (which serializes to 200 OK) OR an `IActionResult` type like `NotFound()` or `BadRequest()` from the same method.
C. It improves speed.
D. It is mandatory.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It provides type safety for Swagger documentation while retaining flexibility for HTTP error responses.
</details>
