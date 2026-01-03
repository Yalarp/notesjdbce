# 20_CORS_Configuration – MCQs

## EASY MCQs

### Q1. What does CORS stand for?
A. Cross-Origin Resource Sharing
B. Cross-Object Relation System
C. Computer Origin Routing Service
D. Code Optimization Resource Standard

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
CORS allows a server to indicate any origins (domain, scheme, or port) other than its own from which a browser should permit loading resources.
</details>

### Q2. Which middleware is used to enable CORS in ASP.NET Core?
A. `app.UseRouting()`
B. `app.UseCors()`
C. `app.UseStaticFiles()`
D. `app.UseAuthentication()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`UseCors` adds the CORS middleware to the pipeline.
</details>

### Q3. By default, what does a browser do if a JS script tries to fetch data from a different domain without CORS?
A. It allows the request freely.
B. It blocks the request/response for security reasons (Same-Origin Policy).
C. It redirects the user.
D. It crashes the browser.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The Same-Origin Policy restricts how a document or script loaded from one origin can interact with a resource from another origin.
</details>

### Q4. What constitute an "Origin"?
A. Just the domain name (e.g., google.com).
B. The Scheme (Protocol), Domain, and Port.
C. The IP address only.
D. The URL path.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`https://myapp.com:443` is a different origin from `http://myapp.com:80`. All three parts must match.
</details>

### Q5. Where should `app.UseCors()` generally be placed in the pipeline?
A. Before `app.UseAuthorization()`.
B. After `app.MapControllers()`.
C. At the very end.
D. It doesn't matter.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
It must be applied before endpoints are executed and before authorization happens (since the browser needs the CORS headers to decide if it can even read the response), and definitively for Preflight requests.
</details>

---

## MEDIUM MCQs

### Q6. Which instruction allows ANY website to access your API?
A. `options.AllowAnyOrigin()`
B. `options.WithOrigins("http://google.com")`
C. `options.AllowCredentials()`
D. `options.BlockNone()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`AllowAnyOrigin()` sets the Access-Control-Allow-Origin header to `*`.
</details>

### Q7. What is a "Preflight Request"?
A. A request sent before the API boots up.
B. An `OPTIONS` request sent by the browser to check if the actual request is safe to send.
C. A POST request.
D. A request to check user balance.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
For "complex" requests (e.g., using PUT/DELETE or custom headers like Authorization), the browser first sends an OPTIONS request to verify permission.
</details>

### Q8. If you want to allow a specific frontend (e.g., `https://my-app.com`) to access your API, which method do you use?
A. `WithOrigins("https://my-app.com")`
B. `AllowAnyOrigin()`
C. `WithHeaders("https://my-app.com")`
D. `WithMethods("GET")`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
This restricts access only to the specified domain(s).
</details>

### Q9. Which configuration causes an exception if combined with `AllowAnyOrigin()`?
A. `AllowAnyMethod()`
B. `AllowAnyHeader()`
C. `AllowCredentials()`
D. `SetPreflightMaxAge()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The CORS spec prohibits using a wildcard `*` for origin when credentials (cookies/auth headers) are involved. You must explicitly list the allowed origins.
</details>

### Q10. How can you apply a CORS policy to a specific controller only, instead of globally?
A. You cannot.
B. Use `[EnableCors("PolicyName")]` attribute on the controller/action.
C. Use `if` statements in `Program.cs`.
D. Create a separate project.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Attributes allow granular control over CORS policies per endpoint.
</details>

---

## HARD MCQs

### Q11. What response status code does the server typically return for a successful Preflight (OPTIONS) request?
A. 200 OK or 204 No Content
B. 201 Created
C. 403 Forbidden
D. 302 Redirect

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The browser just needs the headers; it doesn't need content. 204 is very common.
</details>

### Q12. If a browser sends a request with `Authorization: Bearer ...` header, and your CORS policy does not include `.WithHeaders("Authorization")` (or `.AllowAnyHeader()`), what happens?
A. The API works fine.
B. The browser blocks the request (or the server rejects it during preflight).
C. The header is stripped but request continues.
D. The server crashes.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Explicit permission for custom headers must be granted via `Access-Control-Allow-Headers`.
</details>

### Q13. What is the effect of `[DisableCors]` attribute?
A. It turns off the internet.
B. It prevents the controller from being accessed by any origin other than the API's own origin (effectively enforcing Same-Origin).
C. It allows everything.
D. It deletes the CORS middleware.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It overrides global CORS enablement for that specific action/controller, reverting to standard browser behavior (blocking cross-origin).
</details>

### Q14. Why is `RequireCors` not a standard method call? (Wait, trick question context) - Let's rephrase: What is the benefit of Named Policies (e.g., `AddPolicy("MyPolicy")`) over Default Policy?
A. Named policies are faster.
B. Named policies allow you to define different rules for different endpoints (e.g., Open policy for public API, strict for Admin API).
C. Default can only support one origin.
D. There is no benefit.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You can register multiple named policies and apply them selectively using `[EnableCors("PolicyName")]`.
</details>

### Q15. Which header is exposed to the client JavaScript only if explicitly added via `WithExposedHeaders()`?
A. `Content-Type`
B. `Content-Length`
C. Custom headers (e.g., `X-Pagination`)
D. `Cache-Control`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
By default, browsers only expose "Safe" response headers to the JS XHR/Fetch object. To read custom headers, the server must send `Access-Control-Expose-Headers`.
</details>
