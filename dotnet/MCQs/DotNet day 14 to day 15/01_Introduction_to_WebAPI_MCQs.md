# 01_Introduction_to_WebAPI – MCQs

## EASY MCQs

### Q1. What is the primary purpose of a Web API?
A. To generate HTML pages for browsers.
B. To act as a bridge allowing different applications to exchange data (typically JSON/XML) over HTTP.
C. To style web pages.
D. To manage database schemas.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Web APIs provide a platform-independent interface for data exchange between clients (browsers, mobile apps) and servers.
</details>

### Q2. Which architectural style does ASP.NET Core Web API typically follow?
A. SOAP
B. REST (Representational State Transfer)
C. WCF
D. CORBA

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
REST is the dominant architectural style, emphasizing stateless communication, resource-oriented URLs, and standard HTTP methods.
</details>

### Q3. Which attribute enables API-specific behaviors like automatic 400 responses?
A. `[Controller]`
B. `[ApiController]`
C. `[WebMethod]`
D. `[RestClient]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The `[ApiController]` attribute simplifies API development by automating model validation, binding source inference, and requiring attribute routing.
</details>

### Q4. Which base class should a Web API controller inherit from if it doesn't need View support?
A. `Controller`
B. `ControllerBase`
C. `Object`
D. `ApiBase`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`ControllerBase` provides all the necessary functionality for handling HTTP requests without the overhead of View-related methods (like `View()`, `ViewBag`) found in `Controller`.
</details>

### Q5. Which HTTP method is NOT idempotent?
A. GET
B. PUT
C. DELETE
D. POST

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**
POST is not idempotent because making the same request N times results in N new resources being created.
</details>

---

## MEDIUM MCQs

### Q6. What is the standard data format for modern Web APIs?
A. XML
B. JSON (JavaScript Object Notation)
C. CSV
D. Binary

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
JSON is lightweight, easy to parse, and natively supported by JavaScript, making it the de facto standard for web APIs.
</details>

### Q7. What does the `[Route("api/[controller]")]` attribute do?
A. It hardcodes the route to "api/controller".
B. It defines a route template where `[controller]` is replaced by the controller's class name (minus "Controller").
C. It enables routing for Views.
D. It is mandatory for all C# classes.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If the class is `MemberController`, the route becomes `/api/member`. This is known as Token Replacement in Attribute Routing.
</details>

### Q8. Which HTTP status code indicates a successful creation of a resource (POST)?
A. 200 OK
B. 201 Created
C. 204 No Content
D. 302 Found

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
201 Created is the specific success code for POST requests, typically accompanied by a Location header pointing to the new resource.
</details>

### Q9. What defines a "Stateless" communication in REST?
A. The server stores the user's state in memory.
B. Each request contains all information needed to process it; the server retains no session information request-to-request.
C. The client has no state.
D. The database is read-only.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Scalability is improved because any server in a farm can handle any request without needing to know context from previous requests.
</details>

### Q10. In the controller method `public Members Get(int id)`, how is the `id` populated?
A. From the POST body.
B. From the Route path (URL segment) matching `{id}`.
C. From a cookie.
D. From the database.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Model binding maps the `{id}` token in the `[HttpGet("{id}")]` route template to the action parameter `id`.
</details>

---

## HARD MCQs

### Q11. Why is `[FromBody]` needed for complex types in POST methods (without `[ApiController]`)?
A. It isn't needed.
B. By default, MVC tries to bind from form data. `[FromBody]` instructs the model binder to use configuration Input Formatters (like `System.Text.Json`) to deserialize the request body stream directly.
C. To validate the body.
D. To encrypt the body.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Note that with `[ApiController]`, `[FromBody]` is inferred automatically for complex types, but understanding the mechanism is crucial.
</details>

### Q12. What is the main difference between PUT and PATCH?
A. No difference.
B. PUT replaces the *entire* resource. PATCH applies *partial* updates (only fields sent are modified).
C. PUT creates, PATCH updates.
D. PATCH is safer.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
PUT expects a complete representation of the resource. If you send a partial object to PUT, missing fields might be overwritten with nulls/defaults.
</details>

### Q13. The `ControllerBase` class provides helper methods like `Ok()`, `NotFound()`, `BadRequest()`. What do these methods return?
A. `void`
B. Instances of `IActionResult` (specifically subclasses like `OkObjectResult`, `NotFoundResult`) that represent HTTP responses.
C. Integers.
D. Strings.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
They abstract the creation of the underlying HTTP response message, ensuring correct status codes and headers are set.
</details>

### Q14. In the request flow `Client -> Kestrel -> Middleware -> Routing -> Controller`, what is Kestrel?
A. A database.
B. A cross-platform, high-performance web server implementation for ASP.NET Core that listens for HTTP requests.
C. A browser.
D. A logger.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Kestrel is the default web server that hosts the application process.
</details>

### Q15. Why might a Web API return XML instead of JSON?
A. It's faster.
B. If Content Negotiation is enabled and the client sends `Accept: application/xml` header.
C. JSON is deprecated.
D. XML is the default.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
ASP.NET Core supports Content Negotiation. If configured (`AddXmlSerializerFormatters`), it respects the client's `Accept` header.
</details>
