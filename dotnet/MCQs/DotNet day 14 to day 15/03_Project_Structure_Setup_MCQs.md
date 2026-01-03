# 03_Project_Structure_Setup – MCQs

## EASY MCQs

### Q1. Which file serves as the main entry point for a .NET Core Web API application?
A. `Global.asax`
B. `Startup.cs`
C. `Program.cs`
D. `App.config`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`Program.cs` contains the logic to create the builder, register services, and configure the request pipeline.
</details>

### Q2. Which folder typically contains the classes defining the data structure?
A. `Controllers`
B. `Models`
C. `Services`
D. `Views`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The `Models` folder holds POCO (Plain Old CLR Objects) classes like `Member`, `Book`, etc.
</details>

### Q3. What is the purpose of `appsettings.json`?
A. To store source code.
B. To store Application Configuration settings (connection strings, logging levels, API keys).
C. To store database records.
D. To configure Visual Studio layout.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is the standard place for runtime configuration, capable of storing structured/hierarchical data.
</details>

### Q4. Which file is used to configure launch profiles (e.g., IIS Express vs Kestrel) and is NOT deployed to production?
A. `appsettings.json`
B. `launchSettings.json`
C. `Program.cs`
D. `web.config`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Found in the `Properties` folder, it controls how the dev environment starts the app (ports, environment variables).
</details>

### Q5. In `Program.cs`, which object is used to register services (DI)?
A. `app`
B. `builder.Services`
C. `config`
D. `router`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`builder.Services` (an `IServiceCollection`) is where you add `AddControllers()`, `AddScoped<...>()`, etc.
</details>

---

## MEDIUM MCQs

### Q6. What does `builder.Build()` do?
A. Compiles the C# code.
B. Finalizes the DI container configuration and creates the `WebApplication` instance (`app`), ready for middleware configuration.
C. Starts the server.
D. Deletes the database.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Before `Build()`, you register services. After `Build()`, you configure the pipeline (`app.Use...`).
</details>

### Q7. Why is the ORDER of middleware registration in `Program.cs` important?
A. It isn't important.
B. Middleware executes in the order defined. For example, `UseAuthorization` must come *after* `UseAuthentication` to work correctly.
C. It sorts alphabetically.
D. It depends on file size.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The pipeline is linear. A request passes through middleware 1 -> 2 -> 3. If Authentication (2) hasn't run, Authorization (3) can't check permissions.
</details>

### Q8. What does `app.UseSwagger()` do?
A. Generates the UI webpage.
B. Exposes the generated OpenAPI JSON specification (usually at `/swagger/v1/swagger.json`).
C. Validates the code.
D. Secures the API.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`UseSwagger` creates the raw JSON document describing the API. `UseSwaggerUI` creates the nice webpage that consumes that JSON.
</details>

### Q9. Which method call enables Attribute Routing and Controller discovery?
A. `app.Run()`
B. `app.MapControllers()`
C. `builder.Services.AddRouting()`
D. `app.UseStaticFiles()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`MapControllers()` inspects the registered controllers and creates endpoints based on their `[Route]` attributes.
</details>

### Q10. What is the correct way to handle environments (Dev vs Prod)?
A. Comment out code manually.
B. Use `if (app.Environment.IsDevelopment()) { ... }` block in `Program.cs`.
C. Use two different project files.
D. Delete files.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This allows you to conditionally enable features like Swagger or Developer Exception Pages only in safe environments.
</details>

---

## HARD MCQs

### Q11. Can you edit `builder.Services` AFTER calling `builder.Build()`?
A. Yes, anytime.
B. No. The DI container is immutable once built. Any attempt to modify it throws an exception.
C. Only if using Reflection.
D. Only in Debug mode.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The boundary between "Registration Phase" and "Pipeline Phase" is strict.
</details>

### Q12. How do you access `IConfiguration` inside a Service class?
A. Read the JSON file manually.
B. Constructor Injection: `public MyService(IConfiguration config) { ... }`.
C. Use `Global.Configuration`.
D. Use `StaticConfig.Get()`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Configuration is a first-class citizen in the DI container and can be injected anywhere.
</details>

### Q13. What is the role of `.csproj` file?
A. Nothing.
B. It defines the project SDK, Target Framework (e.g., `net8.0`), and strict list of NuGet package dependencies.
C. It stores passwords.
D. It is the compiler.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is the MSBuild project definitions file.
</details>

### Q14. What does `app.UseHttpsRedirection()` do?
A. Encrypts data.
B. Issues a 307 Temporary Redirect response to any HTTP request, forcing the client to retry over HTTPS.
C. Blocks HTTP.
D. Generates certificates.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Enforces security by ensuring communication happens over an encrypted channel.
</details>

### Q15. If `launchSettings.json` has `"applicationUrl": "http://localhost:5000"`, but `appsettings.json` has `"Kestrel": { "Endpoints": ... }`, which one wins?
A. `launchSettings.json` wins when running from Visual Studio/CLI (`dotnet run`). `appsettings.json` wins in production/deployed scenarios (where launchSettings doesn't exist).
B. Always `appsettings.json`.
C. Always `launchSettings.json`.
D. Random.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`launchSettings.json` is purely a development-time tool for the launcher. Kestrel configuration is the production standard.
</details>
