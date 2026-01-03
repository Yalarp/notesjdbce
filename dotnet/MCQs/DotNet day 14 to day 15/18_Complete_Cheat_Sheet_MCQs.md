# 18_Complete_Cheat_Sheet – MCQs

## EASY MCQs

### Q1. Which command creates a new ASP.NET Core Web API project?
A. `dotnet new console`
B. `dotnet new webapi`
C. `dotnet build`
D. `dotnet run`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`dotnet new webapi` initializes a new Web API project with the default template.
</details>

### Q2. Which HTTP method corresponds to the "Create" operation in CRUD?
A. GET
B. PUT
C. POST
D. DELETE

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
POST is standard for creating new resources.
</details>

### Q3. What is the return code for a successful GET request?
A. 201 Created
B. 204 No Content
C. 200 OK
D. 404 Not Found

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
200 OK is the standard response for a successful retrieval.
</details>

### Q4. Which attribute is used to bind a parameter from the URL path?
A. `[FromBody]`
B. `[FromQuery]`
C. `[FromRoute]`
D. `[FromHeader]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`[FromRoute]` binds data from the route template (e.g., `/api/items/{id}`).
</details>

### Q5. What is the standard file for storing application secrets and configuration?
A. `Program.cs`
B. `appsettings.json`
C. `web.config`
D. `packages.config`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`appsettings.json` is the modern standard for configuration in ASP.NET Core.
</details>

---

## MEDIUM MCQs

### Q6. Which DI lifetime is most appropriate for a `DbContext` in a Web API?
A. Singleton
B. Transient
C. Scoped
D. Static

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`Scoped` creates one instance per HTTP request, which aligns with the Unit-of-Work pattern of EF Core and prevents threading issues.
</details>

### Q7. What is the purpose of `Include()` in EF Core?
A. To include a new file.
B. To perform Eager Loading of related data.
C. To filter data.
D. To sort data.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Include()` tells EF Core to load related entities (e.g., fetching Categories with Products) in the same query (JOIN).
</details>

### Q8. In the controller method `CreatedAtAction(nameof(GetById), new { id = item.Id }, item)`, what does this return?
A. 200 OK
B. 201 Created with a Location header.
C. 204 No Content
D. 500 Error

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It returns a 201 status and adds a `Location` header pointing to the URL where the newly created resource can be retrieved.
</details>

### Q9. Which Data Annotation attribute is used to validate an email format?
A. `[DataType(DataType.EmailAddress)]`
B. `[EmailAddress]`
C. `[RegularExpression("email")]`
D. `[Required]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`[EmailAddress]` performs the actual validation logic. `[DataType]` is mostly for UI hinting.
</details>

### Q10. Why is `async/await` recommended for I/O bound operations in Web APIs?
A. It makes the database query faster.
B. It frees up the request thread to handle other requests while waiting for the I/O to complete, improving scalability.
C. It ensures data is encrypted.
D. It is required by C#.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It prevents thread starvation under high load by not blocking threads during non-CPU intensive waits.
</details>

---

## HARD MCQs

### Q11. Identify the issue in this code:
```csharp
public IActionResult Get()
{
    var data = _service.GetAsync().Result; 
    return Ok(data);
}
```
A. It returns void.
B. It compiles but may cause a Deadlock (Sync-over-Async).
C. It is missing the `[HttpGet]` attribute.
D. `Result` is deprecated.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Blocking on an async task (`.Result` or `.Wait()`) in a synchronized context (like ASP.NET Classic, though less severe in Core, still bad practice) can lead to deadlocks and thread pool exhaustion. Always use `await`.
</details>

### Q12. When configuring JWT Authentication, what does `ValidateLifetime = true` ensure?
A. The token has not expired.
B. The token was issued by a trusted server.
C. The token is for this API.
D. The token is signed correctly.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
It checks the `exp` (expiration) and `nbf` (not before) claims to ensure the token is currently valid in time.
</details>

### Q13. In EF Core, if you have a `Category` and `Item` (One-to-Many), and you want to prevent object cycles during JSON serialization, what attribute should be added to the navigation property?
A. `[ForeignKey]`
B. `[JsonIgnore]`
C. `[Required]`
D. `[NotMapped]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`[JsonIgnore]` prevents the serializer from following the circular reference (Child -> Parent -> Child...) which would otherwise throw an exception.
</details>

### Q14. What is the difference between `AddSingleton` and `AddTransient`?
A. Singleton creates one instance per request; Transient creates one globally.
B. Singleton creates one instance for the app lifetime; Transient creates a new instance every time it is injected.
C. Singleton is for databases; Transient is for caching.
D. There is no difference.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Singleton = Shared globally. Transient = Lightweight, stateless, created fresh on every injection.
</details>

### Q15. Which CORS method configures the policy to allow credentials (cookies/auth headers)?
A. `AllowAnyOrigin()`
B. `AllowCredentials()`
C. `AllowAnyHeader()`
D. `WithMethods("POST")`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`AllowCredentials()` enables the client to send credentials. **Crucial:** It cannot be used with `AllowAnyOrigin()`; explicit origins must be specified.
</details>
