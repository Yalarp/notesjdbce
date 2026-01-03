# 09_Kestrel_Web_Server – MCQs

## EASY MCQs

### Q1. What is Kestrel?
A. A web browser.
B. A database engine.
C. The default, cross-platform web server included with ASP.NET Core.
D. A sophisticated firewall.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Kestrel is the high-performance, open-source internal web server that runs .NET Core applications on Windows, Linux, and macOS.
</details>

### Q2. Which command runs the application using Kestrel?
A. `dotnet build`
B. `dotnet run`
C. `dotnet test`
D. `npm start`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`dotnet run` compiles the project and starts the application using the configured web server, which defaults to Kestrel (via the "Project" profile).
</details>

### Q3. What is the default HTTP port for Kestrel?
A. 80
B. 8080
C. 5000
D. 3000

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
By default, Kestrel binds to `http://localhost:5000` and `https://localhost:5001`.
</details>

### Q4. Can Kestrel run on Linux?
A. No, only Windows.
B. Yes, it is cross-platform.
C. Only on Ubuntu.
D. Only with Mono.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Kestrel is designed to be cross-platform, making it the engine that enables ASP.NET Core to run on non-Windows environments.
</details>

### Q5. What is an "Edge Server"?
A. A server located at the edge of the office.
B. An internet-facing web server that handles incoming TCP connections directly from clients.
C. A backup server.
D. A server running Internet Explorer.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
When Kestrel is exposed directly to the internet (without a reverse proxy like Nginx/IIS in front), it is acting as an Edge Server.
</details>

---

## MEDIUM MCQs

### Q6. Which launch profile in Visual Studio typically uses Kestrel?
A. "IIS Express"
B. The profile named after the Project or "http"/"https".
C. "Docker"
D. "Debug"

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The profile with `commandName: "Project"` (often renamed to "http" or "https" in newer templates) configures VS to launch the app using the Kestrel self-host rather than IIS Express.
</details>

### Q7. How can you change the port Kestrel listens on?
A. You cannot change it.
B. By modifying `launchSettings.json` or passing `--urls` command line argument.
C. Reinstalling .NET.
D. Changing the computer name.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You can set `applicationUrl` in `launchSettings.json` or run `dotnet run --urls "http://localhost:8080"` to override the binding.
</details>

### Q8. Why is using a Reverse Proxy (like Nginx) recommended over using Kestrel as an Edge Server in some production scenarios?
A. Kestrel is slow.
B. Reverse proxies offer advanced features like Request Filtering, URL Rewriting, Load Balancing, and easier SSL certificate management that Kestrel may not handle as robustly.
C. Kestrel cannot handle HTTP requests.
D. Nginx is Windows only.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
While Kestrel is fast, mature proxies like Nginx/IIS/Apache provide layers of defense, static file caching, and elaborate configuration options that are useful at the infrastructure edge.
</details>

### Q9. When running `dotnet run`, what "environment" is default?
A. Production
B. Development
C. Staging
D. Testing

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Unless specified otherwise via environment variables, `dotnet run` typically assumes the `Development` environment.
</details>

### Q10. Does Kestrel support HTTPS?
A. No.
B. Yes, with `UseHttps()` and certificate configuration.
C. Only on port 443.
D. Only on Windows.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Kestrel has full support for HTTPS/TLS, widely used for the default secure endpoint `https://localhost:5001`.
</details>

---

## HARD MCQs

### Q11. Can Kestrel be used in "InProcess" hosting with IIS?
A. Yes.
B. No.
C. Only if you rename it.
D. Only on Linux.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is a tricky definition. In "InProcess", the app is hosted inside `w3wp.exe` using an IIS-specific HTTP server implementation (`IISHttpServer`). Kestrel is NOT used. Kestrel is used in "OutOfProcess" scenarios.
</details>

### Q12. How does Kestrel compare to IIS/Apache in terms of architecture?
A. It is based on Event-Driven, Asynchronous I/O (via libuv or Managed Sockets).
B. It uses one thread per request (Synchronous).
C. It is written in Java.
D. It relies on Windows Registry.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Kestrel is designed for high-performance async I/O. It previously used `libuv` (like Node.js) but now defaults to high-performance managed sockets in newer .NET versions.
</details>

### Q13. `app.Urls.Add("http://*:80")` does what?
A. Configures Kestrel to listen on port 80 on all network interfaces.
B. Adds a URL to the database.
C. Redirects users to port 80.
D. Filters port 80 traffic.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
This code lets you programmatically configure the endpoints Kestrel listens to, overriding configuration files. `*` or `0.0.0.0` binds to all IPs.
</details>

### Q14. What is "Connection Pooling" in the context of Kestrel/HTTP?
A. Reusing database connections.
B. Reusing the underlying TCP connections for multiple HTTP requests (Keep-Alive), reducing TLS handshake and TCP setup overhead.
C. Pooling memory.
D. Grouping users.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Modern web servers keep connections open (Keep-Alive) to serve multiple requests from the same client efficiently. Kestrel manages and pools these connections.
</details>

### Q15. Is Kestrel a fully-featured web server like IIS?
A. Yes, it has exactly the same feature set.
B. No, it is designed to be lightweight and fast, intentionally lacking features like GUI administration, advanced process management (App Pools), and Windows Authentication integration (without middleware).
C. Yes, but slower.
D. No, it is only for static files.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Kestrel focuses on serving requests quickly. It delegates process management to the OS (or Docker/Systemd) and advanced features to a Reverse Proxy.
</details>
