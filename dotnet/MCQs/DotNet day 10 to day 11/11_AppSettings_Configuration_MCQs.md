# 11_AppSettings_Configuration – MCQs

## EASY MCQs

### Q1. Which file is the primary location for application settings (like Connection Strings) in ASP.NET Core?
A. `web.config`
B. `launchSettings.json`
C. `appsettings.json`
D. `Startup.cs`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
ASP.NET Core replaced `web.config` (XML) with `appsettings.json` (JSON) as the standard place to store application configuration.
</details>

### Q2. How do you access the configuration object in `Program.cs`?
A. `builder.Services`
B. `builder.Configuration`
C. `app.Environment`
D. `System.Configuration`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The `WebApplicationBuilder` exposes the `Configuration` property, which represents the merged configuration from all sources (files, env vars, etc.).
</details>

### Q3. Which method is commonly used to retrieve a connection string?
A. `Configuration.Get("ConnectionStrings")`
B. `Configuration.GetConnectionString("Name")`
C. `Configuration["Database"]`
D. `Configuration.Value`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`GetConnectionString("Name")` is a shorthand helper method that looks up the value in the `ConnectionStrings` section of the JSON.
</details>

### Q4. Which configuration source generally has the Highest Priority (overrides others)?
A. `appsettings.json`
B. Command Line Arguments
C. Environment Variables
D. User Secrets

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Configuration is built in layers. Command Line arguments are typically added last, meaning they override all previous layers (JSON files, Env vars).
</details>

### Q5. What character is used to traverse nested JSON sections in configuration keys?
A. Dot (.)
B. Colon (:)
C. Slash (/)
D. Hyphen (-)

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
To access nested keys, use the colon separator. For example: `Configuration["Logging:LogLevel:Default"]`.
</details>

---

## MEDIUM MCQs

### Q6. In which environment, `appsettings.Development.json` values override `appsettings.json` values?
A. Any environment.
B. Only when `ASPNETCORE_ENVIRONMENT` is set to `Development`.
C. Only in Visual Studio.
D. Only on Linux.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The framework automatically loads `appsettings.{EnvironmentName}.json` after `appsettings.json`. If the environment is Development, the Development-specific file is loaded and overrides the base file.
</details>

### Q7. What is the purpose of the "User Secrets" configuration source?
A. To encrypt data in production.
B. To store sensitive data (like passwords/API keys) during local development so they are NOT committed to source control (git).
C. To manage user login sessions.
D. To configure IIS.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
User Secrets are stored in a separate location on the developer's machine (outside the project folder) to prevent accidental committing of secrets to public repositories.
</details>

### Q8. How do you bind a configuration section to a C# class (Strongly Typed Configuration)?
A. `builder.Services.Configure<MySettings>(Configuration.GetSection("MySettings"));`
B. `var settings = new MySettings();`
C. `Configuration.Bind("MySettings")`
D. You cannot do this.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The Options pattern allows you to map a configuration section to a class and register it in the DI container. You can then inject `IOptions<MySettings>` into services.
</details>

### Q9. If `appsettings.json` contains `"Key": "Val1"` and `appsettings.Production.json` contains `"Key": "Val2"`, what is the value of `Configuration["Key"]` in Production?
A. "Val1"
B. "Val2"
C. "Val1Val2"
D. Null

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The environment-specific file is loaded *after* the base file, so its values overwrite/merge with the base values.
</details>

### Q10. Does `launchSettings.json` configuration merge into `builder.Configuration`?
A. Yes, fully.
B. No, `launchSettings.json` is for the launcher (VS/CLI) only. It sets Environment Variables, which *are* picked up by configuration, but the file itself is not read by `ConfigurationBuilder` directly.
C. Yes, but only in Production.
D. Only on Windows.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`launchSettings.json` is for the tool launching the app. It may set `ASPNETCORE_ENVIRONMENT`, which indirectly affects which appsettings file is loaded, but its content isn't merged like appsettings.json.
</details>

---

## HARD MCQs

### Q11. Which interface is used to inject Strongly Typed configuration settings into a Controller?
A. `IConfiguration`
B. `IOptions<T>` (or `IOptionsSnapshot<T>`, `IOptionsMonitor<T>`)
C. `ISettings`
D. `IConfig`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Once configured using `services.Configure<T>`, you inject `IOptions<T>` to access the `.Value` property containing your settings object.
</details>

### Q12. `Configuration.GetValue<int>("PageSize", 10)` does what?
A. Sets the PageSize to 10.
B. Tries to retrieve "PageSize" and convert it to int. If missing, returns the default value of 10.
C. Returns 10 always.
D. Errors if PageSize is not found.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This generic helper allows retrieving values with type conversion and specifying a fallback default if the key is missing.
</details>

### Q13. How would you override nested key `Logging:LogLevel:Default` using an Environment Variable?
A. `SET Logging_LogLevel_Default=Error`
B. `SET Logging__LogLevel__Default=Error` (Double underscore)
C. `SET Logging.LogLevel.Default=Error`
D. `SET Logging:LogLevel:Default=Error`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Operating systems (like Linux) often do not support colons in environment variable names. ASP.NET Core supports using double underscores (`__`) as a hierarchy separator for Env Vars.
</details>

### Q14. What happens if you define a key in `appsettings.json` but pass it as a Command Line argument during `dotnet run`?
A. The appsettings.json value is used.
B. The command line value is used.
C. An exception is thrown (Dubplicate Key).
D. Both are used.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Command Line arguments are the highest priority source added by the default builder. They overwrite any matching keys found in previous sources.
</details>

### Q15. Where is `appsettings.json` physically located in the published application?
A. It is embedded in the DLL.
B. It is in the root of the publish folder alongside the executable.
C. It is deleted.
D. It is in the user profile.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is a Content file, copied to the output directory. This allows system administrators to edit the JSON file on the production server to change settings without recompiling.
</details>
