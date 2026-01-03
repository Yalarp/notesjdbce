# 16_Default_Pages_FileServer – MCQs

## EASY MCQs

### Q1. What is the primary function of `UseDefaultFiles()` middleware?
A. To serve the index.html file to the client.
B. To delete files.
C. To rewrites the URL (e.g., from `/` to `/index.html`) if a default file is found, but it does NOT serve the file itself.
D. To list all files in the directory.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`UseDefaultFiles` is purely a URL rewriter. It checks for the existence of `index.html` (etc.) and updates `HttpContext.Request.Path`, allowing the subsequent `UseStaticFiles` middleware to actually serve the file.
</details>

### Q2. Which middleware actually SERVES the content of `index.html` after `UseDefaultFiles()` has rewritten the URL?
A. `UseDefaultFiles()`
B. `UseStaticFiles()`
C. `UseRouting()`
D. `UseEndpoints()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Since `UseDefaultFiles` only changes the path, you must have `UseStaticFiles` afterward to handle the request for the now-rewritten path.
</details>

### Q3. What is the correct order of middleware registration for default files to work?
A. `UseStaticFiles()` then `UseDefaultFiles()`
B. `UseDefaultFiles()` then `UseStaticFiles()`
C. Order does not matter.
D. `UseRouting()` must be first.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Rewrite must happen BEFORE serving. If `UseStaticFiles` runs first, it sees a request for `/` (folder), which it doesn't handle, so it calls next. Then `UseDefaultFiles` rewrites it to `/index.html`, but `StaticFiles` has already passed!
</details>

### Q4. Which of the following is NOT a standard default file name searched by ASP.NET Core?
A. `index.html`
B. `default.htm`
C. `home.php`
D. `index.htm`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The default list includes `default.htm`, `default.html`, `index.htm`, and `index.html`. `.php` files are not supported by the static file middleware defaults.
</details>

### Q5. What does `UseFileServer()` do?
A. It starts an FTP server.
B. It acts as a wrapper that adds `UseDefaultFiles`, `UseStaticFiles`, and optionally `UseDirectoryBrowser` in one go.
C. It allows file uploads.
D. It serves files from various disks.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`UseFileServer` is a convenience method that sets up the common trio of static file hosting features with a single line of code.
</details>

---

## MEDIUM MCQs

### Q6. If you want `UseDefaultFiles()` to recognize `MyHome.html` as a default document, how do you configure it?
A. Rename the file to index.html.
B. Pass `DefaultFilesOptions` to the middleware, clearing the default list and adding "MyHome.html".
C. It is not possible.
D. Configure it in `web.config`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You customize the behavior by modifying the `DefaultFileNames` collection on the options object passed to `app.UseDefaultFiles(options)`.
</details>

### Q7. Does `UseDefaultFiles()` search subdirectories?
A. No, only the root.
B. Yes, if the request path points to a subdirectory (e.g., `/products/`), it looks for a default file inside that subdirectory (`/products/index.html`).
C. Yes, but only one level deep.
D. No, it redirects to root.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It works for any directory request. If you browse to `/subfolder/`, it checks for `index.html` inside `wwwroot/subfolder/`.
</details>

### Q8. What happens if you call `UseFileServer(new FileServerOptions { EnableDirectoryBrowsing = true })`?
A. It enables users to see a list of files and folders in their browser if no default file is found.
B. It downloads all files.
C. It deletes the directory.
D. It hides the directory.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
This serves a HTML listing of the directory contents, similar to IIS Directory Browsing or Apache Indexes. Usually disabled in production for security.
</details>

### Q9. If both `index.html` and `default.html` exist in the same folder, which one is served by default?
A. `index.html`
B. `default.html`
C. A random one.
D. Both.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The default order is: `default.htm`, `default.html`, `index.htm`, `index.html`. `default.html` (Priority 2) is checked before `index.html` (Priority 4). Note: This priority can vary by version but typically `default.*` comes before `index.*`.
</details>

### Q10. `UseDefaultFiles` rewrites the URL. Does the client (browser) see the URL change?
A. Yes, it sends a 301 Redirect.
B. No, the rewrite happens internally on the server. The browser address bar remains at `/`.
C. Yes, it sends a 302 Found.
D. Only in Chrome.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is a server-side rewrite, not a client-side redirect. The user stays on `/`, but the server responds with the content of `/index.html`.
</details>

---

## HARD MCQs

### Q11. Can `UseFileServer` be used to serve files from a location outside `wwwroot`?
A. No.
B. Yes, by configuring the `FileProvider` (PhysicalFileProvider) in `FileServerOptions`.
C. Only if you use a symbolic link.
D. Only on Windows.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Just like explicit StaticFiles configuration, FileServer supports mapping physical directories to request paths via options.
</details>

### Q12. Why is `EnableDirectoryBrowsing` disabled by default in `UseFileServer`?
A. It causes errors.
B. Security / Information Disclosure. Revealing file structure allows attackers to discover sensitive files, backup files, or understand the app architecture.
C. It uses too much CPU.
D. Browsers don't support it.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Security best practice is to expose only what is necessary. Listing files allows enumeration attacks.
</details>

### Q13. If you have `UseStaticFiles` but NOT `UseDefaultFiles`, what happens when you visit `/`?
A. It serves `index.html`.
B. It returns 404 (Not Found) or passes to the next middleware (likely 404 if no routes match). `UseStaticFiles` ignores directory requests.
C. It lists the directory.
D. It crashes.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`UseStaticFiles` only handles requests that directly match a file. It does not know that `/` should map to `index.html`. You need `UseDefaultFiles` for that logic.
</details>

### Q14. Can you use `UseDefaultFiles` with Razor Pages or MVC Views?
A. Yes, it converts Views to HTML.
B. Generally no/irrelevant. Default Files is for static assets. Razor Pages has its own routing (served at root `/` via `Index.cshtml`) which usually takes precedence if Endpoint Routing is configured.
C. Yes, it is required for MVC.
D. Only for API controllers.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If you have `MapRazorPages()`, a request to `/` will likely be handled by `Pages/Index.cshtml`. `UseDefaultFiles` is typically used for SPA hosting or static sites, not standard MVC apps.
</details>

### Q15. Is it possible to clear all default files and have NO default file?
A. Yes, `options.DefaultFileNames.Clear()`.
B. No, at least one is required.
C. Yes, but it crashes.
D. Only in Main().

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
If you clear the list and add nothing, the middleware effectively does nothing. Requests to `/` will pass through unchanged.
</details>
