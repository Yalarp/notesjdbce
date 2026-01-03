# 08_Hosting_Models – MCQs

## EASY MCQs

### Q1. What is the "Default" hosting model for a new ASP.NET Core application on Windows?
A. OutOfProcess
B. InProcess
C. Service Hosted
D. Cloud Hosted

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Unless configured otherwise, ASP.NET Core apps default to InProcess hosting on Windows to maximize performance by running inside the IIS worker process.
</details>

### Q2. In the "InProcess" hosting model on full IIS, what is the name of the worker process?
A. `dotnet.exe`
B. `w3wp.exe`
C. `nginx.exe`
D. `chrome.exe`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
In InProcess, the app runs directly inside the IIS Worker Process, which is named `w3wp.exe` for full IIS (or `iisexpress.exe` for IIS Express).
</details>

### Q3. In the "OutOfProcess" hosting model, which internal web server is responsible for running the application code?
A. Apache
B. Tomcat
C. Kestrel
D. Node.js

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
In OutOfProcess, the external server (IIS/Nginx) relays requests to the internal Kestrel server, which actually hosts and runs the .NET code.
</details>

### Q4. Which hosting model requires TWO web servers functioning together?
A. InProcess
B. OutOfProcess
C. Console App
D. Windows Service

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
OutOfProcess uses a Reverse Proxy (Server 1) forwarding to Kestrel (Server 2). InProcess uses only one server (IIS/IIS Express).
</details>

### Q5. What is the main advantage of InProcess hosting over OutOfProcess on Windows?
A. It works on Linux.
B. Higher request throughput and performance (no loopback network penalty).
C. It allows using Nginx.
D. It restarts faster.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
InProcess avoids the HTTP network hop between the reverse proxy and Kestrel. The request is processed in the same memory space, leading to significantly better performance.
</details>

---

## MEDIUM MCQs

### Q6. Which element in the `.csproj` file controls the hosting model?
A. `<KestrelConfig>`
B. `<AspNetCoreHostingModel>`
C. `<HostingEnvironment>`
D. `<OutputType>`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You specify `<AspNetCoreHostingModel>InProcess</AspNetCoreHostingModel>` or `OutOfProcess` in the project configuration file.
</details>

### Q7. If you use `dotnet run` (CLI), which hosting model is effectively used?
A. InProcess (IIS)
B. It ignores the IIS settings and runs the app on Kestrel directly (similar to OutOfProcess architecture, but without the reverse proxy during dev).
C. Windows Service
D. Cloud Service

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`dotnet run` launches the application as a standalone process using Kestrel. It does not use IIS or the ASP.NET Core Module. The process name is usually `dotnet` or the project name.
</details>

### Q8. Which hosting model allows you to run ASP.NET Core on Linux with Nginx?
A. InProcess
B. OutOfProcess
C. Windows Authentication
D. IIS Express

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
InProcess is a Windows/IIS-only feature (using `AspNetCoreModuleV2`). On Linux, you must use the OutOfProcess model where Nginx acts as the reverse proxy for Kestrel.
</details>

### Q9. What is "IIS Express"?
A. A production server.
B. A lightweight, self-contained version of IIS designed for development purposes on Windows.
C. A Linux server.
D. A database.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It provides the features of IIS without requiring a full OS-level installation or admin rights, making it ideal for testing InProcess hosting during development.
</details>

### Q10. What happens if you define `commandName: "Project"` in `launchSettings.json`?
A. It forces InProcess hosting.
B. It launches Kestrel directly, ignoring any `AspNetCoreHostingModel` configuration in the csproj.
C. It crashes.
D. It opens Notepad.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
"Project" command means "Run as a console application with Kestrel". Hosting model configurations basically apply when running behind a host like IIS.
</details>

---

## HARD MCQs

### Q11. In InProcess hosting, `WebApplication.CreateBuilder` internally calls which method?
A. `UseKestrel()`
B. `UseIIS()`
C. `UseApache()`
D. `UseNginx()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The builder detects the setting and configures the app to integrate with the IIS pipeline (`UseIIS()`), allowing IIS to manage the lifecycle and native I/O.
</details>

### Q12. Why doesn't OutOfProcess hosting support `UseIIS()`?
A. Because IIS is not used.
B. Because in OutOfProcess, IIS is just a generic proxy (TCP/HTTP forwarder). The app runs in a separate dotnet process on Kestrel, so it calls `UseKestrel()` instead.
C. Because IIS is incompatible with .NET Core.
D. It does support it.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
In OutOfProcess, the app is decoupled. IIS connects via HTTP. The app manages its own server (Kestrel). `UseIISIntegration` might still be used for forwarding headers, but `UseIIS` (InProcess specific) is not.
</details>

### Q13. How would you programmatically check if your app is running InProcess or OutOfProcess?
A. Check `System.Diagnostics.Process.GetCurrentProcess().ProcessName`.
B. You cannot check.
C. Check the file size.
D. Check the CPU temperature.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
If the process name is `w3wp` or `iisexpress`, you are likely InProcess using IIS. If the process name is `dotnet` or `YourProjectName`, you are likely running OutOfProcess (Kestrel self-hosted).
</details>

### Q14. What component is responsible for handling the startup for InProcess hosting in IIS?
A. `AspNetCoreModuleV2` (ANCM)
B. `mod_rewrite`
C. `IsapiModule`
D. `CGI.exe`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The ASP.NET Core Module V2 handles the bootstrapping. In InProcess mode, it loads the .NET runtime into the IIS worker process. In OutOfProcess mode, it launches the external dotnet process.
</details>

### Q15. Why might you theoretically choose OutOfProcess on Windows even if InProcess is faster?
A. To make it slower.
B. For stronger process isolation. (e.g., if the app crashes, it doesn't crash the IIS worker process; or to run multiple apps on different .NET versions that might conflict in the same process).
C. To use less memory.
D. OutOfProcess is always default.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Process isolation is the main valid reason. It ensures that app instability affects only that specific Kestrel process, not the main IIS worker handling other sites (though typically App Pools provide isolation anyway).
</details>
