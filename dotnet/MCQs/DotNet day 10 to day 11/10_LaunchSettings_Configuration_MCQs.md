# 10_LaunchSettings_Configuration – MCQs

## EASY MCQs

### Q1. Where is the `launchSettings.json` file located?
A. Root folder
B. `bin` folder
C. `Properties` folder
D. `wwwroot` folder

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
It is found inside the `Properties` subdirectory of the project.
</details>

### Q2. Is `launchSettings.json` used in Production environments?
A. Yes, it configures the production server.
B. No, it is only used on the local development machine by VS/CLI.
C. Yes, but only on Linux.
D. Yes, for database keys.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This file is strictly for development launch configuration. Publish tools usually ignore it, and production servers (IIS/Kestrel) do not read it. Production config should go in `appsettings.json` or environment variables.
</details>

### Q3. Which property controls whether the browser opens automatically when you start the app?
A. `launchBrowser`
B. `openUrl`
C. `startBrowser`
D. `autoStart`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Setting `"launchBrowser": true` in a profile tells Visual Studio (or `dotnet watch`) to spawn the default web browser pointing to the application URL upon startup.
</details>

### Q4. What does the `commandName` property define?
A. The name of the project.
B. Which server/host mechanism to use (e.g., `IISExpress`, `Project`, `IIS`).
C. The console command to run.
D. The URL.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It determines the launcher. `Project` runs the executable (Kestrel). `IISExpress` runs `iisexpress.exe`. `IIS` attaches to local IIS.
</details>

### Q5. How do you select which Profile to use in Visual Studio?
A. You cannot select it.
B. Using the Dropdown menu next to the "Start Debugging" (Green Play) button.
C. By editing the Registry.
D. By deleting the file.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
VS parses the `profiles` config and populates the Run dropdown, allowing you to easily switch between IIS Express and Kestrel (http/https) profiles.
</details>

---

## MEDIUM MCQs

### Q6. Which environment variable is commonly set inside `launchSettings.json`?
A. `ASPNETCORE_ENVIRONMENT`
B. `PATH`
C. `WINDOWS_HOME`
D. `JAVA_HOME`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
It typically sets `ASPNETCORE_ENVIRONMENT` to `Development`. This forces the app into Dev mode (showing detailed errors) when run locally, distinct from Production.
</details>

### Q7. If `commandName` is set to `"Project"`, which web server is used?
A. Apache
B. IIS
C. Kestrel
D. None

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`Project` means "Run the project as a standalone dotnet process". The standard standalone server for .NET is Kestrel.
</details>

### Q8. What happens if you define a custom environment variable in `launchSettings.json`?
A. It is permanently added to the Windows System variables.
B. It is available to the application process only while running via that specific launch profile.
C. It is ignored.
D. It crashes the app.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
These variables are process-scoped. They are injected into the process environment block at startup but do not affect the global OS.
</details>

### Q9. Why are there two URLs separated by a semicolon in: `"applicationUrl": "https://localhost:5001;http://localhost:5000"`?
A. One for backup.
B. It configures the server to listen on both endpoints (HTTPS and HTTP).
C. It is a syntax error.
D. One is for input, one is for output.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Kestrel can listen on multiple endpoints. This string tells it to bind to port 5001 for SSL and 5000 for clear text.
</details>

### Q10. What is the `iisSettings` section used for?
A. To configure Kestrel.
B. To configure IIS Express global configurations (like Windows Authentication settings and SSL ports).
C. To configure SQL Server.
D. To configure Docker.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This section sits outside the `profiles`. It defines valid authentication modes and ports specifically for when the `IISExpress` profile is used.
</details>

---

## HARD MCQs

### Q11. If you run `dotnet run` without arguments, which profile is picked?
A. The first one in the file.
B. The one with `commandName: "IISExpress"`.
C. The first profile where `commandName` is `"Project"`.
D. It errors out.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`dotnet run` CLI cannot use IIS Express. It looks for a profile compatible with the CLI (i.e., Project/Kestrel) to determine URLs and Environment variables.
</details>

### Q12. Can you use `launchSettings.json` to configure the app to listen on a specific public IP (e.g., `http://0.0.0.0:5000`)?
A. Yes, by modifying `applicationUrl`.
B. No, it only supports localhost.
C. Yes, but only in Production.
D. No.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`applicationUrl` controls binding. Using `0.0.0.0` or specific IPs here works, though typically developers use `localhost` for local dev.
</details>

### Q13. Does `launchSettings.json` override `appsettings.json`?
A. No, they are unrelated.
B. Yes, Environment Variables set in `launchSettings.json` override values loaded from `appsettings.json` (because Env Vars generally have higher precedence than JSON config).
C. Always.
D. Never.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The configuration builder explicitly prioritizes Environment Variables over `appsettings.json`. Since `launchSettings` sets Env Vars, they effectively win for keys that exist in both.
</details>

### Q14. What does `dotnetRunMessages: true` do?
A. It sends emails.
B. It provides feedback in the console when the app starts (e.g., "Now listening on...").
C. It hides errors.
D. It enables chat.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is a flag for the CLI to output the standard startup messages. If false, the startup might be silent until your own logs appear.
</details>

### Q15. Is `launchSettings.json` committed to Source Control (Git)?
A. Never.
B. Typically Yes, so that all developers on the team share the same port configurations and environment setup.
C. No, because it contains passwords.
D. Only the folders are committed.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Unlike `appsettings.Development.json` (which might be user-specific) or `user secrets`, `launchSettings.json` is usually shared to ensure team consistency ("Run button works for everyone"). However, avoid putting real secrets in it.
</details>
