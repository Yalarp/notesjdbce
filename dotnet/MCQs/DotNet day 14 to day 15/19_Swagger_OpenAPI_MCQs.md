# 19_Swagger_OpenAPI – MCQs

## EASY MCQs

### Q1. What is the primary function of Swagger (Swashbuckle) in ASP.NET Core?
A. To compile C# code.
B. To generate interactive API documentation and the OpenAPI specification.
C. To handle database migrations.
D. To authenticate users.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Swashbuckle generates the `swagger.json` (OpenAPI spec) and provides a UI to visualize and test the API endpoints.
</details>

### Q2. Which service method is required to register the Swagger generator?
A. `builder.Services.AddControllers()`
B. `builder.Services.AddSwaggerGen()`
C. `builder.Services.AddCors()`
D. `builder.Services.AddDbContext()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`AddSwaggerGen` adds the services responsible for generating the OpenAPI document.
</details>

### Q3. What file does Swagger generate to describe your API?
A. `web.config`
B. `swagger.json`
C. `api.xml`
D. `index.html`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It creates a JSON file following the OpenAPI Specification (OAS) that describes paths, operations, parameters, and schemas.
</details>

### Q4. By default, at what URL is the Swagger UI available?
A. `/swagger/index.html`
B. `/api/help`
C. `/docs`
D. `/home/swagger`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The standard route for Swashbuckle's UI is `domain.com/swagger`.
</details>

### Q5. Should Swagger UI generally be enabled in a Production environment?
A. Yes, always.
B. No, it should generally be disabled to avoid exposing API structure to potential attackers.
C. Yes, but only for GET requests.
D. It doesn't matter.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
While not a vulnerability itself, it provides a "map" for attackers. It's best practice to disable it in production unless it's a public API.
</details>

---

## MEDIUM MCQs

### Q6. What is the purpose of `AddEndpointsApiExplorer()`?
A. It allows the browser to explore files.
B. It enables API endpoint discovery, commonly required for Swagger to work, especially with Minimal APIs.
C. It replaces Controllers.
D. It generates the UI.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It provides metadata about the endpoints in the application, which the Swagger Generator uses to build the document.
</details>

### Q7. How do you add XML code comments (descriptions) to the Swagger UI?
A. It happens automatically.
B. You must manually type them in the browser.
C. Enable XML documentation in `.csproj` and configure `options.IncludeXmlComments()` in `AddSwaggerGen`.
D. Use a separate tool like Postman.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
First, `GenerateDocumentationFile` must be true in the project file. Then, the path to the generated XML must be passed to Swashbuckle.
</details>

### Q8. Which attribute allows you to specify the HTTP status codes that an action might return, for documentation purposes?
A. `[ProducesResponseType]`
B. `[HttpGet]`
C. `[Route]`
D. `[Authorize]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
e.g., `[ProducesResponseType(StatusCodes.Status200OK)]`. This information populates the "Responses" section in Swagger UI.
</details>

### Q9. If you want to use JWT Authentication within the Swagger UI (the "Authorize" button), what must you configure?
A. Nothing, it works by default.
B. `AddSecurityDefinition` and `AddSecurityRequirement` in `AddSwaggerGen`.
C. Just `app.UseAuthentication()`.
D. Add a Login controller.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You need to define the Security Scheme (e.g., "Bearer") and the Requirement (where to apply it) so Swagger knows to send the Authorization header.
</details>

### Q10. What does `app.UseSwagger()` do compared to `app.UseSwaggerUI()`?
A. They are the same.
B. `UseSwagger` exposes the raw JSON/YAML data; `UseSwaggerUI` serves the HTML/JS page that consumes that JSON.
C. `UseSwagger` is for production; `UseSwaggerUI` is for dev.
D. `UseSwaggerUI` creates the JSON.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`UseSwagger` creates the middleware that serves the document. `UseSwaggerUI` creates the middleware that serves the visual interface.
</details>

---

## HARD MCQs

### Q11. How can you make the Swagger UI load at the root of your application (e.g., `http://localhost:5000/`)?
A. It is not possible.
B. Set `options.RoutePrefix = string.Empty;` inside `UseSwaggerUI`.
C. Move the wwwroot folder.
D. Change the controller route.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
By clearing the `RoutePrefix` (default is "swagger"), the middleware serves the UI at the application root.
</details>

### Q12. In the `OpenApiSecurityScheme` configuration for JWT, what should `Type` be set to?
A. `SecuritySchemeType.OAuth2`
B. `SecuritySchemeType.ApiKey`
C. `SecuritySchemeType.Http`
D. `SecuritySchemeType.OpenIdConnect`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Typically, `ApiKey` is used for generic header-based patterns or `Http` with scheme `bearer`. Swashbuckle often uses `ApiKey` with `In = ParameterLocation.Header` and `Name = "Authorization"` for manual manual JWT handling, or `Http` class for cleaner Bearer support. (Note: Both are valid approaches depending on exact config, but `ApiKey` is the generic "put this string in this header" approach shown in many tutorials).
</details>

### Q13. If you possess a controller with a public method that is NOT an HTTP action, how do you prevent Swagger from crashing or trying to document it?
A. Make the method `private`.
B. Add `[ApiExplorerSettings(IgnoreApi = true)]` to the method.
C. Delete the method.
D. Rename it.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Swagger scans public methods in controllers. If one isn't an action (or has duplicate routes), it can cause errors. Explicitly ignoring it tells the generator to skip it.
</details>

### Q14. What does `options.DocExpansion(DocExpansion.None)` achieve in Swagger UI config?
A. It removes all documentation.
B. It expands all endpoints by default.
C. It collapses all controller endpoints, making the UI cleaner initially.
D. It deletes the JSON file.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Great for large APIs. The UI starts with all sections closed (collapsed), so the user isn't overwhelmed by hundreds of endpoints.
</details>

### Q15. To group endpoints in Swagger UI (e.g., "v1", "v2"), what property in `SwaggerDoc` is primarily key?
A. Description
B. Version and the name of the document (e.g., "v1").
C. Contact info.
D. License.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You define a document (e.g., "v1"). You can then filter which actions belong to which document (often via ApiExplorerSettings or convention), but the `SwaggerDoc("v1", ...)` call initializes that grouping container.
</details>
