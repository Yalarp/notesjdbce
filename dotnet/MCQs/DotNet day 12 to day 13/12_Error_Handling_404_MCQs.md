# 12_Error_Handling_404 – MCQs

## EASY MCQs

### Q1. What is the standard HTTP status code for "Not Found"?
A. 200
B. 301
C. 404
D. 500

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
404 Indicates that the server can't find the requested resource.
</details>

### Q2. Which middleware is used to show a detailed error page with stack traces?
A. `UseExceptionHandler`
B. `UseDeveloperExceptionPage`
C. `UseStatusCodePages`
D. `UseHsts`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This middleware captures synchronous and asynchronous exceptions from the pipeline and generates HTML error responses with full debug details.
</details>

### Q3. Should `UseDeveloperExceptionPage()` be enabled in Production?
A. Yes, always.
B. No, never. It exposes sensitive security information (source code, connection details) to attackers.
C. Only on Sundays.
D. Yes, if users ask.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is strictly for local development debugging. Production should use user-friendly generic error pages.
</details>

### Q4. Which method returns a 404 result from a Controller?
A. `return Error();`
B. `return NotFound();`
C. `return Null();`
D. `return Void();`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`NotFound()` is a helper method provided by the `ControllerBase` class that returns a `NotFoundResult` (404 status).
</details>

### Q5. What does `UseExceptionHandler("/Home/Error")` do?
A. It prevents errors.
B. It catches unhandled exceptions in the pipeline and redirects the request to the specified path (`/Home/Error`) to display a polite error message.
C. It logs errors to a file.
D. It emails the developer.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is the standard middleware for handling 500 Server Errors in production.
</details>

---

## MEDIUM MCQs

### Q6. Which middleware handles non-exception errors like 404 (URL not matched)?
A. `UseDeveloperExceptionPage`
B. `UseStatusCodePages` (or its variants)
C. `UseRouting`
D. `UseStaticFiles`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Exception handlers only catch Exceptions. If a request simply matches no route, no exception is thrown; the response just ends with 404. `UseStatusCodePages` intercepts this empty 404 response.
</details>

### Q7. Difference between `UseStatusCodePagesWithRedirects` and `UseStatusCodePagesWithReExecute`?
A. No difference.
B. `WithRedirects` sends a 302 to the client (URL changes). `WithReExecute` re-runs the pipeline internally (URL stays the same).
C. `WithRedirects` is for 500 errors only.
D. `WithReExecute` works only in Chrome.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`WithReExecute` is generally preferred for SEO, as the browser (and search engine) sees the original URL returning the error content directly.
</details>

### Q8. What does the placeholder `{0}` represent in `app.UseStatusCodePagesWithReExecute("/Error/{0}")`?
A. The User ID.
B. The Time.
C. The Status Code (e.g., 404, 500).
D. The Exception Message.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
It allows a single Action Method to handle multiple error codes dynamically.
</details>

### Q9. When querying a database for a specific ID (e.g., Details/5), if the item is null, what should you do?
A. Return a blank view.
B. Throw an exception.
C. Set `Response.StatusCode = 404` and return a "NotFound" view (or call `return NotFound()`).
D. Redirect to Home.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Semantically, the resource does not exist. Returning a 404 status is the correct adherence to HTTP protocol and helps search engines know the page is gone.
</details>

### Q10. Why is `Response.StatusCode = 404` important even if you show a custom error view?
A. It isn't important.
B. Browsers and Search Engines care about the status code. If you return a "Not Found" HTML page but with a `200 OK` status, Google will index it as a valid page ("Soft 404"), which hurts SEO.
C. It makes the text red.
D. It prevents caching.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Always ensure the HTTP header matches the semantic result.
</details>

---

## HARD MCQs

### Q11. In `UseStatusCodePagesWithReExecute`, how can you retrieve the original URL that caused the error?
A. `Request.Path`
B. You cannot.
C. `IStatusCodeReExecuteFeature` via `HttpContext.Features`.
D. `Request.Headers["Referer"]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Since the pipeline re-executes, `Request.Path` is updated to the error page path (e.g., `/Error/404`). The *original* path is stored in the `IStatusCodeReExecuteFeature`.
</details>

### Q12. If you use both `UseExceptionHandler` and `UseDeveloperExceptionPage`, which one takes effect?
A. The last one registered.
B. The first one registered.
C. Both.
D. It depends on the `Environment`. Typically, `if(Dev) UseDeveloper... else UseException...` is used so they are mutually exclusive.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**
You rarely register both simultaneously. You branch based on environment.
</details>

### Q13. Does `UseStatusCodePages` handle exceptions thrown by Controllers?
A. Yes.
B. No. It only handles responses that *finish* with an error status code (like 404) without a body. Exceptions cause the pipeline to abort earlier (handled by ExceptionHandler).
C. Sometimes.
D. Only Authorization exceptions.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
They serve different purposes: ExceptionHandler for crashes (500), StatusCodePages for missing routes/resources (400-599).
</details>

### Q14. What happens if you enable `UseHsts()` (HTTP Strict Transport Security) in Development?
A. Nothing.
B. It could permanently force your browser to only access the site via HTTPS, which might cause "Privacy Error" issues with self-signed development certificates.
C. The site becomes faster.
D. It disables JavaScript.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
HSTS headers are cached by browsers. It's usually best to enable it only in Production code blocks.
</details>

### Q15. Can you return a view from the `UseExceptionHandler` path?
A. No, only JSON.
B. Yes, `UseExceptionHandler("/Home/Error")` re-executes the request starting at that path, so it invokes the `Error` action on `HomeController`, which serves a View.
C. No, it must be a static file.
D. Only if using Razor Pages.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This allows your "500 Server Error" page to share the same Layout and look-and-feel as the rest of your site.
</details>
