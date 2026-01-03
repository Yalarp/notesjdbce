# 06_AddMvc_Methods_Comparison – MCQs

## EASY MCQs

### Q1. Which method should you use for a bare-bones Web API project that does NOT require View rendering?
A. `AddMvc()`
B. `AddControllers()`
C. `AddControllersWithViews()`
D. `AddRazorPages()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`AddControllers()` registers only the services necessary for Web API features (Controllers, Model Binding, Data Annotations) without the overhead of the View engine or Razor Pages.
</details>

### Q2. Which method adds support for Controller, Views, and Razor Pages (essentially everything)?
A. `AddMvc()`
B. `AddMvcCore()`
C. `AddControllers()`
D. `AddRazorPages()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`AddMvc()` is the "kitchen sink" method. It internally calls `AddMvcCore()` and adds all possible features including Views, Razor Pages, Tag Helpers, and Data Annotations.
</details>

### Q3. Which method is most appropriate for a standard MVC Web Application (with Views) but without Razor Pages?
A. `AddControllers()`
B. `AddRazorPages()`
C. `AddControllersWithViews()`
D. `AddMvcCore()`
<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`AddControllersWithViews()` adds the services needed for Controllers and Razor Views, making it ideal for a traditional MVC app. It does not include Razor Pages services unless you specifically add them.
</details>

### Q4. What is the main downside of using `AddMvc()` for every project?
A. It causes a runtime error.
B. It adds unnecessary services and overhead (impacting startup time and memory) if you don't need all features (like Razor Pages in an API project).
C. It is deprecated.
D. It prevents using JSON.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
While convenient, `AddMvc()` registers many services that might never be used. Choosing a more specific method (like `AddControllers()`) keeps the application lighter and startup slightly faster.
</details>

### Q5. What does `AddMvcCore()` typically lack that `AddMvc()` includes by default?
A. Routing
B. JSON Formatters and View Engines
C. Middleware
D. Dependency Injection

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`AddMvcCore()` provides the absolute minimum. It does not even include JSON output formatters by default, meaning `return Json(...)` might fail unless you manually add the formatters.
</details>

---

## MEDIUM MCQs

### Q6. If you use `AddControllers()`, which of the following features will NOT work?
A. `[ApiController]` attributes
B. `return View();` (View Rendering)
C. Model Validation
D. Routing

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`AddControllers()` does not register the Razor View Engine. Attempting to return a ViewResult will throw an exception because the service locator cannot find the view services.
</details>

### Q7. How does `AddRazorPages()` differ from `AddControllersWithViews()`?
A. It is exactly the same.
B. `AddRazorPages()` supports Razor Pages (`.cshtml` files with `@page` directive) and lightweight controller support, but avoids some full MVC features. `AddControllersWithViews()` generally excludes the specific Razor Pages infrastructure.
C. `AddRazorPages()` cannot return JSON.
D. `AddRazorPages()` is only for static files.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Each method targets a specific pattern. Razor Pages uses a Page-based model processing pipeline which is distinct from the MVC Controller-Action pipeline, though they share the underlying Razor engine.
</details>

### Q8. In a Microservice architecture using ASP.NET Core as a REST API, which registration is recommended?
A. `services.AddMvc()`
B. `services.AddMvcCore()` then manually adding Formatters and Validation
C. `services.AddControllers()`
D. `services.AddRazorPages()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`AddControllers()` is the sweet spot for APIs. It includes the necessary formatters, CORS, and validation support needed for an API, without the View engine overhead of `AddMvc()`, and without the extreme manual configuration needed for `AddMvcCore()`.
</details>

### Q9. Which method adds support for **Tag Helpers**?
A. `AddControllers()`
B. `AddMvcCore()`
C. `AddControllersWithViews()` and `AddMvc()`
D. `AddApiExplorer()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Tag Helpers run server-side to render HTML. This functionality is part of the Razor View engine logic, which is included in `AddControllersWithViews()` and `AddMvc()`.
</details>

### Q10. Does `AddMvcCore()` invoke `AddMvc()` internally?
A. Yes
B. No, it is the other way around. `AddMvc()` (and others) calls `AddMvcCore()` internally.
C. They are unrelated.
D. They call each other.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`AddMvcCore()` is the base method that registers the core infrastructure (routing, action selection). The other methods call it and then chain additional service registrations (like `.AddViews()`, `.AddRazorPages()`).
</details>

---

## HARD MCQs

### Q11. If you call `AddMvcCore()` and try to return a `JsonResult`, why does it fail with "No service for type 'JsonResultExecutor'"?
A. Because JSON is disabled in .NET Core.
B. Because `AddMvcCore()` is minimal and does not register the `JsonResultExecutor` or default output formatters. You must chain `.AddJsonOptions()` or `.AddFormatterMappings()`.
C. Because you need to restart the server.
D. Because you are missing a NuGet package.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This illustrates the minimalist nature of `AddMvcCore`. It assumes nothing about the response format. The higher-level methods (`AddControllers`, `AddMvc`) default this configuration for you.
</details>

### Q12. Can you mix Razor Pages and MVC Controllers in the same application?
A. No, you must choose one.
B. Yes, by using `AddMvc()` (or `AddControllersWithViews()` + `AddRazorPages()`) and mapping endpoints for specific routes.
C. Only in .NET Framework, not Core.
D. Yes, but they must use different ports.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
They can coexist perfectly. You often see this in apps where the "Admin" section uses Razor Pages while the public API uses Controllers. `AddMvc()` supports both simultaneously.
</details>

### Q13. Which of the following includes "API Explorer" support (essential for Swagger/OpenAPI)?
A. `AddRazorPages()`
B. `AddViews()`
C. `AddControllers()` and above.
D. `AddMvcCore()` alone.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`AddControllers()` registers the `ApiExplorer` services, which allows tools like Swashbuckle to inspect your API endpoints and generate documentation.
</details>

### Q14. What is the impact of `AddAntiforgery()`?
A. It formats dates.
B. It adds services to generate and validate anti-CSRF tokens. Included automatically in `AddMvc()` and `AddControllersWithViews()`, but NOT in `AddControllers()`.
C. It allows CORS.
D. It is for database security.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
APIs (using `AddControllers()`) typically use token-based auth (JWT) rather than cookie-based auth, so they don't usually need Antiforgery (which protects cookie-based sessions). Thus, it is omitted from `AddControllers()`.
</details>

### Q15. In .NET 6+, where do these method calls typically reside?
A. In `Startup.cs`
B. In `Program.cs`, on the `builder.Services` object.
C. In `appsettings.json`
D. In the Controller constructor.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
With the new Minimal Hosting model in .NET 6+, the `Startup` class is often removed, and service registration happens directly in `Program.cs` via the `WebApplicationBuilder`.
</details>
