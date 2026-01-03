# 07_ASPNETCore_Project_Structure – MCQs

## EASY MCQs

### Q1. What is the entry point of an ASP.NET Core application?
A. `Global.asax`
B. `Startup.cs`
C. `Program.cs` and its `Main` method.
D. `HomeController.cs`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Just like a Console Application, an ASP.NET Core app starts execution in the `static void Main` method inside `Program.cs`.
</details>

### Q2. Which file is primarily used for organizing application configuration settings (like connection strings)?
A. `web.config`
B. `launchSettings.json`
C. `appsettings.json`
D. `Program.cs`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`appsettings.json` is the modern replacement for `web.config` appSettings. It stores configuration data in a structured JSON format. `launchSettings.json` is only for local dev launch profiles.
</details>

### Q3. Where are static files (CSS, Images, JavaScript) stored by default?
A. `StaticFiles` folder
B. `wwwroot` folder
C. `Content` folder
D. `Assets` folder

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The `wwwroot` folder is the "web root". Only files in this directory are accessible publicly by default (once `app.UseStaticFiles()` is enabled).
</details>

### Q4. Which class is responsible for building the web application and configuring services?
A. `ServiceCollection`
B. `WebApplicationBuilder`
C. `ProcessBuilder`
D. `HostManager`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`WebApplication.CreateBuilder(args)` returns a `WebApplicationBuilder`, which exposes the `Services` collection for DI and the `Configuration` properties.
</details>

### Q5. In the new .NET Minimal Hosting model, what happens to the `Startup` class?
A. It is mandatory.
B. It is merged into `Program.cs`.
C. It is renamed to `Config.cs`.
D. It is used only for legacy apps.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
In .NET 6+, the standard templates typically omit `Startup.cs` and place all service registration and pipeline configuration directly in the top-level statements of `Program.cs`.
</details>

---

## MEDIUM MCQs

### Q6. What is the purpose of `builder.Build()`?
A. To compile the code.
B. To create the `WebApplication` instance, finalizing the service registration phase and allowing pipeline configuration to begin.
C. To run the server.
D. To restore NuGet packages.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Build()` marks the transition from "Configuration Phase" (registering services) to the "Pipeline Phase" (setting up middleware). You cannot register services after `Build()` is called.
</details>

### Q7. Consider `app.MapControllerRoute(...)`. What phase of the application lifecycle does this belong to?
A. Service Registration
B. Middleware/Endpoint Configuration
C. Compilation
D. Database Migration

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is part of defining how the application handles requests (Routing). It sets up the endpoints that the app will respond to.
</details>

### Q8. What is the standard naming convention for Controller classes?
A. They must end with "Service".
B. They must end with "Controller" (e.g., `HomeController`).
C. They can be named anything.
D. They must start with "C_".

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
While configurable, the default convention is that classes ending in "Controller" (and inheriting from `Controller` or decorated with `[Controller]`) are discovered as controllers by the framework.
</details>

### Q9. What is the purpose of `_ViewImports.cshtml`?
A. To import CSS files.
B. To define namespaces and Tag Helpers that should be available to ALL views automatically (so you don't have to add `@using` in every file).
C. To import JavaScript.
D. To define the layout.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Common directives like `@using MyProject.Models` and `@addTagHelper` are placed here to keep individual View files clean.
</details>

### Q10. What does `_ViewStart.cshtml` typically contain?
A. The HTML `<html>` tag.
B. Code that runs before every view, usually setting the Layout property.
C. Database connection logic.
D. Error handling logic.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It defaults the Layout for all views (e.g., `Layout = "_Layout";`), ensuring a consistent look and feel without repeating code in every View.
</details>

---

## HARD MCQs

### Q11. Which property of `WebApplicationBuilder` allows access to the current hosting environment (Dev/Prod)?
A. `builder.Hosting`
B. `builder.Environment`
C. `builder.Configuration`
D. `builder.WebRoot`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`builder.Environment` (type `IWebHostEnvironment`) provides properties like `IsDevelopment()`, `WebRootPath`, and `ApplicationName`.
</details>

### Q12. Why is the order of middleware in `Program.cs` critical?
A. It isn't critical.
B. Because middleware form a pipeline. Each component invokes the next. If, for example, `UseAuthorization` is placed before `UseRouting`, it cannot know which endpoint is being accessed to authorize it.
C. It is purely aesthetic.
D. The compiler sorts them automatically.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The pipeline order determines request processing. `StaticFiles` usually comes early (to serve files without hitting MVC). `Authentication` must come before `Authorization`. `Routing` must come before `Endpoints`.
</details>

### Q13. What is the difference between `Properties` folder and `wwwroot` folder?
A. `Properties` contains build/launch settings (internal); `wwwroot` contains public static assets (external).
B. They are the same.
C. `Properties` is for CSS.
D. `wwwroot` is for C# code.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`Properties` holds `launchSettings.json` (IDE config). `wwwroot` is the actual root of the web server for serving static content.
</details>

### Q14. In `Program.cs`, the line `var app = builder.Build();` logically separates what two major activities?
A. Compilation and Runtime.
B. Dependency Injection (Service Registration) and Request Pipeline Configuration (Middleware).
C. Model and View.
D. Header and Footer.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Before `Build()`, you work with `builder.Services` (DI). After `Build()`, you work with `app` (Middleware). You cannot add services after the app is built.
</details>

### Q15. How does the default route pattern `"{controller=Home}/{action=Index}/{id?}"` interpret the URL `/Product/Edit`?
A. Controller = Home, Action = Index, Id = Product.
B. Controller = Product, Action = Edit, Id = null.
C. Controller = Product, Action = Index, Id = Edit.
D. It returns a 404.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Segments match the order. Segment 1 (`Product`) maps to `{controller}`. Segment 2 (`Edit`) maps to `{action}`. Segment 3 (`{id?}`) is missing in the URL, so it's null (optional).
</details>
