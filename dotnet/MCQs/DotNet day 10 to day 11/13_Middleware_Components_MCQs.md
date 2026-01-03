# 13_Middleware_Components – MCQs

## EASY MCQs

### Q1. What is the main characteristic of the `Run()` method?
A. It calls the next middleware.
B. It is a Terminal Middleware; it does not receive a `next` delegate and ends the pipeline.
C. It routes requests.
D. It maps URLs.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Run()` is designed to be the final step. It handles the request and sends the response, intentionally stopping further processing.
</details>

### Q2. What is the `Map()` method used for?
A. To map data to models.
B. To create a branch in the pipeline based on the Request Path (URL).
C. To loop over items.
D. To map database columns.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Map("/admin", app => { ... })` creates a separate middleware pipeline that only runs when the request URL starts with `/admin`.
</details>

### Q3. Which method allows you to execute code both before AND after the next middleware?
A. `Run()`
B. `Use()`
C. `Map()`
D. `Branch()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Use()` receives a `next` delegate. You write "Before" code, call `await next()`, and then write "After" code.
</details>

### Q4. If you register two `app.Run()` calls in sequence, what happens?
A. Both run.
B. Only the first one runs.
C. Only the second one runs.
D. An error occurs.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Since the first `Run()` does not call `next()`, the pipeline terminates there. The code for the second `Run()` is unreachable.
</details>

### Q5. What is "Short-Circuiting"?
A. When an electrical failure occurs.
B. When a middleware decides NOT to call `next()`, creating a deliberate early exit from the pipeline (e.g., sending a 401 Unauthorized response).
C. When loops are forbidden.
D. When middleware is missing.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Short-circuiting is a control flow mechanism. If a condition isn't met (like invalid input or missing auth), the middleware returns immediately, preventing downstream logic from wasting resources.
</details>

---

## MEDIUM MCQs

### Q6. How does `MapWhen()` differ from `Map()`?
A. It is faster.
B. `Map()` branches based on Path prefix only. `MapWhen()` branches based on a general predicate (Condition) over the `HttpContext`.
C. `MapWhen` is deprecated.
D. `MapWhen` is for dates.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Map` works on URL prefixes. `MapWhen(context => context.Request.Query.ContainsKey("branch"), ...)` allows branching logic on headers, query strings, or any other request property.
</details>

### Q7. In an `app.Use()` middleware, if you forget to call `await next()`, what happens?
A. The compiler gives an error.
B. It effectively becomes a terminal middleware; subsequent components don't run.
C. The system automatically calls it for you.
D. The request hangs.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Calling `next()` is manual. Forgetting it causes an implicit short-circuit, which is a common source of bugs (e.g., CSS files failing to load because static file middleware was skipped).
</details>

### Q8. Parameters for the lambda in `app.Use( ... )` are typically:
A. `(HttpContext context)`
B. `(HttpContext context, Func<Task> next)`
C. `(IApplicationBuilder app)`
D. `(HttpRequest request)`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Standard signature: `(context, next)`. Context gives access to the request, and next is the function to invoke to proceed.
</details>

### Q9. Can `Map()`-ped branches rejoin the main pipeline?
A. Yes, automatically.
B. No. Once a request enters a Map branch, it stays in that branch until it finishes. It does not "fall out" back to the main pipeline after the branch logic completes.
C. Yes, if you call return.
D. Only on Tuesdays.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
A branch is its own independent pipeline. If the branch doesn't handle the request (and send a response), the request ends there (often resulting in 404), it doesn't return to the main trunk.
</details>

### Q10. What is the output of the following pipeline for a standard request?
```csharp
app.Use(async (ctx, next) => {
   Console.Write("A");
   await next();
   Console.Write("B");
});
app.Run(async ctx => {
   Console.Write("C");
});
```
A. ABC
B. ACB
C. CBA
D. CAB

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
"A" prints (Before). `next()` invokes Run. "C" prints (Terminal). Run returns. `next()` returns. "B" prints (After).
</details>

---

## HARD MCQs

### Q11. Which method signature does `Run` expect?
A. `RequestDelegate` (which is `Func<HttpContext, Task>`)
B. `Func<HttpContext, Func<Task>, Task>`
C. `Action<IApplicationBuilder>`
D. `void`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`Run` takes a handler that only accepts `context`. Since it doesn't take `next`, it's syntactically enforced (mostly) as terminal.
</details>

### Q12. You have logic to check for a special header "X-Beta". If present, you want to use a completely different pipeline configuration. Which method is best?
A. `Map("/beta", ...)`
B. `Use()`
C. `MapWhen(ctx => ctx.Request.Headers.ContainsKey("X-Beta"), appBeta => { ... })`
D. `Run()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`MapWhen` is designed exactly for conditional branching based on arbitrary request properties like headers.
</details>

### Q13. Conceptually, `app.Run(handler)` is equivalent to `app.Use(...)` where:
A. `next()` is called twice.
B. `next()` is never called.
C. `next()` throws an exception.
D. `next()` returns null.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You could technically write a terminal middleware using `Use` by simply ignoring the `next` parameter, but `Run` makes this intent explicit and cleaner.
</details>

### Q14. In a `Map` branch, can you use `Run`, `Use`, and other middleware?
A. No, only `Run`.
B. Yes, the lambda provides a new `IApplicationBuilder` instance specific to that branch, allowing you to configure a full sub-pipeline (Auth, StaticFiles, etc.) just for that path.
C. No, it inherits the parent pipeline.
D. Only `Use`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This power allows specific areas of the app (like `/api`) to have very different middleware chains (e.g., no cookies, different auth) than the main UI (`/`).
</details>

### Q15. Why might you use `return;` inside an `app.Use` block?
A. To end the function execution, which combined with NOT calling `next()`, effectively short-circuits the pipeline (sends response immediately).
B. To restart the pipeline.
C. To call the previous middleware.
D. It is illegal syntax.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
If you write to the response (e.g., `context.Response.WriteAsync("Error")`) and then `return;`, the request processing stops there and goes back up the stack.
</details>
