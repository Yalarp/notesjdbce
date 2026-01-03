# 02_Why_DotNet_Core_WebAPI – MCQs

## EASY MCQs

### Q1. What is the main advantage of .NET Core over the traditional .NET Framework?
A. It has more buttons.
B. It is Cross-Platform (runs on Windows, Linux, macOS).
C. It only runs on Windows.
D. It costs more.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This was the primary driver for creating .NET Core—breaking the dependency on Windows/IIS.
</details>

### Q2. Is .NET Core Open Source?
A. No, it is proprietary.
B. Yes, fully open source (MIT License) and community-driven.
C. Only for students.
D. Partially.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Source code is available on GitHub and accepts community contributions.
</details>

### Q3. Which built-in web server provides high performance for ASP.NET Core?
A. Apache
B. Tomcat
C. Kestrel
D. Nginx

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Kestrel is a lightweight, asynchronous, event-driven web server optimized for speed.
</details>

### Q4. How does .NET Core handle dependencies?
A. It includes everything in one DLL.
B. It uses a Modular Design via NuGet packages ("Pay for what you use").
C. It uses text files.
D. It downloads them from Facebook.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Instead of a monolithic framework (System.Web), you only reference the specific libraries you need (e.g., `Microsoft.EntityFrameworkCore`), keeping the app lightweight.
</details>

### Q5. What is the entry point file for a .NET Core 6+ Web API application?
A. `Global.asax`
B. `Startup.cs`
C. `Program.cs`
D. `Web.config`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The Minimal Hosting model consolidates startup and configuration logic into `Program.cs`.
</details>

---

## MEDIUM MCQs

### Q6. Which Dependency Injection lifetime creates a **new instance** for every request?
A. `AddSingleton`
B. `AddTransient`
C. `AddScoped`
D. `AddStatic`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Transient` = New instance every time needed. `Scoped` = New instance per HTTP request (reused within that request).
</details>

### Q7. What is the "Minimal Hosting Model"?
A. Hosting on a small server.
B. A simplified `Program.cs` structure that reduces boilerplate code by using top-level statements and a builder pattern.
C. Using Notepad to code.
D. Hosting without a database.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It removes the need for a separate `Startup` class and `Main` method declaration, making the code cleaner.
</details>

### Q8. Which tool provides interactive API documentation out-of-the-box?
A. Postman
B. Swagger (Swashbuckle)
C. Word
D. Excel

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Swagger generation and UI middleware are included in the default Web API template.
</details>

### Q9. In the context of performance, how does Kestrel compare to IIS (classic)?
A. Kestrel is slower.
B. Kestrel is significantly faster, capable of handling millions of requests per second.
C. They are the same.
D. Kestrel cannot handle requests.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Kestrel avoids much of the legacy overhead of full IIS/System.Web pipeline.
</details>

### Q10. What is a "Container" in the context of .NET Core?
A. A variable.
B. A lightweight, standalone package (like Docker) containing everything needed to run the app.
C. A folder.
D. A database table.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
.NET Core's modularity makes it ideal for containerization (Docker/Kubernetes).
</details>

---

## HARD MCQs

### Q11. Explain the difference between `AddSingleton` and `AddScoped`.
A. `AddSingleton` creates one instance per user session.
B. `AddSingleton` creates one instance for the entire application lifetime. `AddScoped` creates one instance per Client Request (HTTP request).
C. `AddScoped` is global.
D. `AddSingleton` is for databases only.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Singleton is shared by ALL requests (dangerous for non-thread-safe data). Scoped is shared only within a single request pipeline (ideal for DbContext).
</details>

### Q12. Where are environment-specific settings (like DB connection strings for Dev vs Prod) typically stored?
A. Hardcoded in C#.
B. `appsettings.json` and `appsettings.{Environment}.json` (e.g., `appsettings.Development.json`).
C. Use system registry.
D. In the HTML.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The configuration system automatically layers `appsettings.json` <- `appsettings.Environment.json` <- Environment Variables.
</details>

### Q13. Can Kestrel be used directly exposed to the internet?
A. No, never.
B. Yes, but it is traditionally recommended to use it behind a Reverse Proxy (IIS, Nginx, Apache) for security features (SSL termination, load balancing), though Kestrel has hardened significantly in recent versions.
C. Yes, it is the only way.
D. No, it requires IIS.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
While Kestrel is fast, reverse proxies provide robust edge-server capabilities.
</details>

### Q14. What enables `.NET Core` to run on Linux?
A. Emulators.
B. The modular CoreCLR (Common Language Runtime) which has been ported to support Linux system calls and memory management.
C. Wine.
D. Java.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is a native implementation, not an emulation.
</details>

### Q15. Why is `.NET Standard` relevant when discussing `.NET Core`?
A. It is the old name.
B. It is a specification of APIs that all .NET implementations (Core, Framework, Xamarin) must support, allowing code sharing across platforms.
C. It is a validation tool.
D. It is a web server.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If you write a class library targeting .NET Standard, it can be consumed by both a legacy .NET Framework app and a modern .NET Core app.
</details>
