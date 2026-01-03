# 15_Static_Files_wwwroot – MCQs

## EASY MCQs

### Q1. What is the default implementation of the "Web Root" folder in ASP.NET Core?
A. `public`
B. `assets`
C. `wwwroot`
D. `static`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`wwwroot` is the standard directory name used by the framework to identify the root for serving static content.
</details>

### Q2. Which middleware must be added to `Program.cs` to serve CSS, JS, and Image files?
A. `app.UseMvc()`
B. `app.UseStaticFiles()`
C. `app.UseFiles()`
D. `app.UseAssets()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Without `UseStaticFiles()`, request for files (e.g., `/style.css`) will pass through the pipeline and likely result in a 404 because no middleware handled them.
</details>

### Q3. Is the folder name `wwwroot` included in the URL when accessing a file?
A. Yes (e.g., `/wwwroot/images/logo.png`)
B. No (e.g., `/images/logo.png`)
C. Only if configured.
D. Only in Debug mode.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The middleware maps the *contents* of `wwwroot` to the root of the application URL path (`/`). The folder name itself is hidden.
</details>

### Q4. Are files outside of `wwwroot` accessible to the public by default?
A. Yes, all files are accessible.
B. No, only files inside the configured Web Root are serveable. This is a security feature to prevent downloading source code or config files.
C. Yes, if they are .cs files.
D. No, unless the user is Admin.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Security by default. You must explicitly configure additional file providers if you want to serve files from other directories.
</details>

### Q5. In a Razor View, what does the tilde `~` represent (e.g., `~/css/site.css`)?
A. User Home Directory.
B. Application Web Root.
C. The C: Drive.
D. The current controller.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`~` is syntax handled by Razor (and Tag Helpers) to resolve paths relative to the application root, ensuring links work correctly even if the app is hosted in a virtual directory.
</details>

---

## MEDIUM MCQs

### Q6. Where should `app.UseStaticFiles()` be placed in the middleware pipeline?
A. At the very end (after `Run`).
B. Before `UseRouting` and `UseAuthentication` (typically).
C. After `UseEndpoints`.
D. It doesn't matter.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It should be early. Handling a request for `style.css` is simple and shouldn't require Authentication complexity or Routing overhead. If the file exists, it serves it and terminates.
</details>

### Q7. Does `UseStaticFiles` support Authorization by default?
A. Yes, it checks user login.
B. No. It serves files anonymously to anyone who requests them (public assets).
C. Yes, if you use `[Authorize]` attribute.
D. Only for images.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Static Files middleware does not check `HttpContext.User`. If you need to secure files (e.g., private invoices), you should not put them in `wwwroot` or you must serve them via a Controller action that returns `FileResult` with auth checks.
</details>

### Q8. What does `asp-append-version="true"` do in a script tag?
A. It changes the file name.
B. It adds a query string hash (Cache Busting) to the URL (e.g., `script.js?v=xyz...`). If the file content changes, the hash changes, forcing the browser to reload securely instead of using a stale cache.
C. It downloads the latest version of ASP.NET.
D. It minifies the file.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This Tag Helper solves the "browser caching" problem where users don't see CSS/JS updates because their browser uses an old cached version.
</details>

### Q9. If you create an **Empty** ASP.NET Core project, does it include `wwwroot` and `UseStaticFiles`?
A. Yes.
B. No. You have to create the folder manually and add the middleware line yourself.
C. Yes, but hidden.
D. Only in .NET 5.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The "Empty" template is truly minimal. It essentially has just `MapGet("/", ... "Hello World")`. Static file support is an opt-in feature.
</details>

### Q10. Can you change the Web Root folder from `wwwroot` to something else like `public`?
A. No, it is hardcoded.
B. Yes, by configuring `WebHostOptions` (e.g., `builder.WebHost.UseWebRoot("public")`).
C. Yes, by renaming the folder in File Explorer only.
D. Yes, via DNS.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
While `wwwroot` is the default convention, the framework is flexible and allows you to specify any folder as the web root during host construction.
</details>

---

## HARD MCQs

### Q11. How do you serve files from a folder **other than** `wwwroot` (e.g., `MyStaticFiles`)?
A. You cannot.
B. By calling `app.UseStaticFiles()` a second time with `StaticFileOptions`, specifying the `FileProvider` (PhysicalFileProvider) and `RequestPath`.
C. By just copying the folder.
D. By creating a Controller.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This allows you to map physical directories to URL paths. E.g., Map `D:/Photos` to `/gallery`.
</details>

### Q12. What does `UseDirectoryBrowser()` do?
A. Opens a file explorer on the server.
B. Allows users to see a listing of files in a directory (like an FTP view) in their browser.
C. Finds files.
D. Deletes files.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
By default, directory browsing is disabled for security. `UseDirectoryBrowser` enables listing the contents, usually for specific public folders.
</details>

### Q13. `UseFileServer` is a wrapper that combines which middleware?
A. `UseStaticFiles` and `UseRouting`.
B. `UseStaticFiles`, `UseDefaultFiles`, and optionally `UseDirectoryBrowser`.
C. `UseMvc`.
D. `UseAuth`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If you want "standard web server" behavior (serve static files + serve index.html for root URLs), `UseFileServer` adds all necessary components in one call.
</details>

### Q14. If you have `index.html` in `wwwroot`, does `UseStaticFiles()` serve it when browsing to `/`?
A. Yes.
B. No. You need `UseDefaultFiles()` (before StaticFiles) to rewrite `/` to `/index.html`.
C. Only in Production.
D. Yes, always.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`UseStaticFiles` only handles specific file requests (`/index.html`). It does not handle default documents for directory roots. `UseDefaultFiles` rewrites the URL, and *then* `UseStaticFiles` serves the file.
</details>

### Q15. Can `UseStaticFiles` serve files with creating specific Content-Type headers?
A. It guesses automatically.
B. Yes, you can customize the `ContentTypeProvider` in options to map file extensions (like `.myapp`) to specific MIME types.
C. No, limited to standard types.
D. It serves as text/plain always.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If you have a custom file extension that the server doesn't recognize, it won't serve it by default (security). You must explicitly register the MIME type in options.
</details>
