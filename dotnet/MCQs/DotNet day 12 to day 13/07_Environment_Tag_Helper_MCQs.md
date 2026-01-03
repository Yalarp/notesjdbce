# 07_Environment_Tag_Helper – MCQs

## EASY MCQs

### Q1. What is the main purpose of the `<environment>` Tag Helper?
A. To set environment variables.
B. To conditionally render content (usually scripts or CSS links) based on the current hosting environment (e.g., Development vs. Production).
C. To save the planet.
D. To configure the database.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It allows you to serve unminified debug versions of libraries in "Development" and minified CDN versions in "Production".
</details>

### Q2. Which attribute includes content only for specific environments?
A. `names`
B. `include`
C. `only`
D. `target`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Usage: `<environment include="Development">`. Note: `names` was used in earlier versions but `include` is standard now.
</details>

### Q3. Which environment variable does ASP.NET Core check by default?
A. `NODE_ENV`
B. `ASPNETCORE_ENVIRONMENT`
C. `DOTNET_ENV`
D. `SERVER_MODE`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This system environment variable determines if the app runs in `Development`, `Staging`, or `Production`.
</details>

### Q4. Typically, what kind of files are served in the "Development" environment?
A. Minified, bundled files.
B. Unminified, separate files (for easier debugging).
C. Encrypted files.
D. No files.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Debugging is easier with full source code and whitespace.
</details>

### Q5. Where is the `ASPNETCORE_ENVIRONMENT` variable often set for local development?
A. `launchSettings.json`
B. `appsettings.json`
C. `Program.cs`
D. `web.config`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`launchSettings.json` controls the environment configuration when launching from Visual Studio or CLI.
</details>

---

## MEDIUM MCQs

### Q6. What does `<environment exclude="Development">` do?
A. It deletes the Development environment.
B. It renders the content in ALL environments EXCEPT "Development".
C. It renders only in Development.
D. It throws an error in Development.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Useful for "Production" & "Staging" settings where you want to apply the same rule for everything non-dev.
</details>

### Q7. Why is a "CDN Fallback" important when using the Environment Tag Helper?
A. To make it faster.
B. If the user is offline.
C. To ensure the website still functions correctly if the external CDN (Content Delivery Network) is down or blocked.
D. To save money.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Tag Helpers like `asp-fallback-src` detect if the CDN resource loaded; if not, they inject a reference to a local copy of the file.
</details>

### Q8. In the script tag helper, what does `asp-fallback-test` do?
A. It downloads the file.
B. It runs a JavaScript expression (e.g., `window.jQuery`) to check if the library loaded successfully from the CDN.
C. It tests the internet speed.
D. It validates the file size.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If the test returns false (falsy), the browser falls back to the local source.
</details>

### Q9. What is "Subresource Integrity" (SRI) used for in `<link>` or `<script>` tags?
A. Speed.
B. Security. The `integrity` attribute contains a cryptographic hash to ensure the file from the CDN has not been tampered with.
C. Compression.
D. Versioning.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Prevents attacks where a compromised CDN serves malicious code.
</details>

### Q10. Can you list multiple environments in the `include` attribute?
A. No.
B. Yes, comma-separated (e.g., `include="Staging,Production"`).
C. Yes, space-separated.
D. Only with Regex.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Allows targeting a subset of environments.
</details>

---

## HARD MCQs

### Q11. If `ASPNETCORE_ENVIRONMENT` is not set, what is the default value assumed by the host?
A. Development
B. Production
C. Staging
D. Null

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
For safety, ASP.NET Core defaults to "Production" to avoid exposing sensitive developer exception pages.
</details>

### Q12. How does `asp-fallback-test-class` work for CSS files?
A. It checks a JS variable.
B. It adds a test element to the DOM, applies the specified class, and checks if a specific CSS property (via `asp-fallback-test-property`) matches the expected value (`asp-fallback-test-value`).
C. It checks the file name.
D. It pings the server.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Unlike JS, you can't easily check a "variable". You verify that a known style from the library (e.g., `visibility: hidden`) is actually applied to a dummy element.
</details>

### Q13. Can you nesting Environment Tag Helpers?
A. Yes.
B. No.
C. Yes, but inner ones are ignored.
D. Only in Views.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Standard Razor nesting rules apply, though logical utility is limited.
</details>

### Q14. Is the content inside an `<environment>` tag sent to the client if the environment doesn't match?
A. Yes, but hidden with CSS.
B. No, it is removed server-side. The HTML is never generated.
C. Yes, but commented out.
D. Yes, always.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is a server-side feature. The output HTML only contains the content for the matching environment.
</details>

### Q15. Does `asp-fallback-src` work on standard HTML `<script>` tags without the Environment Tag Helper?
A. No.
B. Yes, provided the Script Tag Helper is enabled (`@addTagHelper`). The Environment Tag Helper is a *wrapper*, but the fallback logic belongs to the Script/Link Tag Helpers themselves.
C. Only in .NET 7.
D. Only inside Environment tags.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The attributes `asp-fallback-*` belong to the ScriptTagHelper and LinkTagHelper. They function anywhere those tag helpers are active.
</details>
