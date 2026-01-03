# 17_Developer_Exception_Page – MCQs

## EASY MCQs

### Q1. What is the primary purpose of `UseDeveloperExceptionPage()`?
A. To handle 404 errors.
B. To display a detailed, interactive error page with stack traces and request info when an application crashes during development.
C. To log errors to a database.
D. To email the developer.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It provides a rich debugging experience, showing the exact line of code that failed, variable states, and headers.
</details>

### Q2. In which environment should you typically use `UseDeveloperExceptionPage()`?
A. Production.
B. Staging.
C. Development ONLY.
D. All environments.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
It exposes sensitive internal details (stack traces, source paths, cookies). Using it in Production is a severe security vulnerability.
</details>

### Q3. Where in the middleware pipeline should `UseDeveloperExceptionPage` come?
A. At the end.
B. As early as possible (start of the pipeline).
C. In the middle.
D. After Routing.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It works by wrapping the *subsequent* middleware in a try-catch block. To catch errors from *any* part of the app (Routing, Auth, MVC), it must stay before them.
</details>

### Q4. What information is shown in the "Routing" tab of the developer exception page?
A. The physical file path.
B. The Endpoint that was matched (e.g., Controller/Action) and route values.
C. Network latency.
D. Wi-Fi password.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It helps debug why a request hit (or didn't hit) a specific controller action by showing the selected endpoint.
</details>

### Q5. Which middleware is recommended for handling errors in **Production**?
A. `UseDeveloperExceptionPage()`
B. `UseExceptionHandler("/Error")`
C. `UseStaticFiles()`
D. `UseMvc()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`UseExceptionHandler` catches exceptions and re-executes the request to a generic error handling path (like `/Home/Error`), allowing you to show a user-friendly custom error page without exposing secrets.
</details>

---

## MEDIUM MCQs

### Q6. How do you conditionally enable the Developer Exception Page?
A. `if (true)`
B. `if (app.Environment.IsDevelopment())`
C. `if (context.Request.IsLocal)`
D. Checks file existence.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This standard check ensures the middleware is only registered when the app runs in the "Development" environment (e.g., set via `launchSettings.json` or Env Vars).
</details>

### Q7. What is the `SourceCodeLineCount` option used for?
A. To limit the lines of code in the project.
B. To configure how many lines of source context (before and after the error line) are displayed in the stack trace view.
C. To count lines of code.
D. To optimize performance.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
By default, it shows around 6 lines. You can increase this to see more of the function context surrounding the exception.
</details>

### Q8. The Developer Exception Page displays which of the following?
A. Stack Trace, Query Strings, Cookies, Headers.
B. Database passwords only.
C. User passwords.
D. Memory dump.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
It aggregates all relevant HTTP context data to help diagnose the state of the request when it failed.
</details>

### Q9. If an exception occurs in a middleware placed **before** `UseDeveloperExceptionPage`, will it be caught by the page?
A. Yes.
B. No. Middleware can only catch exceptions thrown by components *after* it in the pipeline (downstream).
C. Yes, but only in .NET 6.
D. Sometimes.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Execution flows top-to-bottom. If error happens at step 1, step 2 (Exception Page) hasn't started yet. This is why exception handling must be at the very top (Step 1).
</details>

### Q10. Does `UseDeveloperExceptionPage` handle HTTP 404 (Not Found) errors?
A. Yes, it shows a 404 page.
B. No. It only handles **Unhandled Exceptions** (500 errors). 404 is a valid response (no error thrown), just no endpoint matched.
C. Yes, always.
D. Only for images.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
To handle 404s nicely, you typically use `UseStatusCodePages()` or `UseStatusCodePagesWithReExecute()`. Exception Page is strictly for crashes/exceptions.
</details>

---

## HARD MCQs

### Q11. Can `UseDeveloperExceptionPage` show the source code snippet even if the `.pdb` (symbol) files are missing?
A. Yes.
B. No. It relies on the `.pdb` files to map the compiled IL code back to the original C# source file line numbers.
C. Yes, using decompilation.
D. Only if Source Link is enabled.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The PDB files contain the debugging symbols. Without them, the exception stack trace will only show method names and IL offsets, not file paths or line numbers, so the code preview won't work.
</details>

### Q12. How does the Production `UseExceptionHandler` middleware work differently from `UseDeveloperExceptionPage`?
A. It just logs the error.
B. It acts as a "Catch-All" block that, upon catching an exception, resets the current response and re-executes the pipeline with a new path (e.g., `/Error`), allowing a Controller to render a friendly view.
C. It shows the stack trace in plain text.
D. It stops the server.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It's a re-execution mechanism. The browser URL usually doesn't change, but the server internally runs a new request to the error handler path to generate the response HTML.
</details>

### Q13. In the "Cookies" tab, what happens if a cookie is marked `HttpOnly`?
A. It is hidden.
B. It is displayed. The server can read HttpOnly cookies; only the client-side JS cannot.
C. It is encrypted.
D. It is deleted.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The Exception Page runs on the server, which has full access to the request headers, including HttpOnly cookies sent by the browser.
</details>

### Q14. Is it possible to plug in a custom exception handler even in Development?
A. No.
B. Yes. You can choose to use `UseExceptionHandler` in Dev, or even chain them (though redundant). You are not forced to use the default page.
C. No, VS locks it.
D. Only via registry.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
While `UseDeveloperExceptionPage` is the default for templates, you can implement your own custom middleware or use `UseExceptionHandler` if you want to test the production error flow locally.
</details>

### Q15. Does the Developer Exception Page return a JSON response for API clients (e.g., Postman)?
A. No, always HTML.
B. Yes, by default it checks the `Accept` header. If the client asks for JSON, it returns a detailed JSON problem details response instead of the HTML page.
C. Yes, but only XML.
D. No, it returns 404.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Modern versions of the middleware support content negotiation. For APIs, receiving a huge HTML page is useless, so it provides the error details in JSON format if requested.
</details>
