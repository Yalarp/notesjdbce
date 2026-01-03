# 04_Routing_Fundamentals – MCQs

## EASY MCQs

### Q1. What are the two primary routing types in ASP.NET Core MVC?
A. Local and Global.
B. Conventional Routing and Attribute Routing.
C. Static and Dynamic.
D. HTTP and HTTPS.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Conventional is defined globally (usually in Program.cs/Startup), while Attribute routing uses attributes directly on the controller/action methods.
</details>

### Q2. What is the standard default conventional route pattern?
A. `{controller=Home}/{action=Index}/{id?}`
B. `{id}/{controller}/{action}`
C. `{action}/{controller}`
D. `api/{controller}`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
This pattern maps the first segment to the Controller, second to Action, and third to an optional ID.
</details>

### Q3. In Attribute Routing, what does `[Route("Home/Index")]` do?
A. It creates a folder.
B. It explicit maps the URL path `/Home/Index` to the decorated action method.
C. It redirects the user.
D. It deletes the route.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It overrides conventional routing conventions and creates a specific endpoint for that action.
</details>

### Q4. Which attribute allows an action to handle HTTP POST requests?
A. `[HttpPost]`
B. `[HttpGet]`
C. `[Route]`
D. `[Post]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Verbs attributes (`HttpPost`, `HttpGet`, `HttpPut`, `HttpDelete`) restrict the action to specific HTTP methods.
</details>

### Q5. What does the `?` in `{id?}` indicate?
A. The parameter is secret.
B. The parameter is **Optional**.
C. The parameter is a boolean.
D. The parameter is required.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If the ID is omitted from the URL (e.g., `/Home/Details`), the route still matches.
</details>

---

## MEDIUM MCQs

### Q6. How do you combine a Route on the Controller with a Route on an Action?
```csharp
[Route("api/users")]
public class UsersController : Controller {
    [Route("{id}")]
    public IActionResult Get(int id) { ... }
}
```
What is the resulting URL?
A. `/id`
B. `/api/users`
C. `/api/users/{id}`
D. `/users/api/{id}`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Action routes append to the Controller route prefix.
</details>

### Q7. What is a "Route Constraint" used for?
Example: `{id:int}`
A. To enforce that the parameter must be convertible to an integer for the route to match.
B. To convert the string to int automatically (Parsing only).
C. To restrict access to admins.
D. To limit string length.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
If the URL provides "abc", the constraint `:int` fails, and the route is skipped (likely resulting in 404 if no other route matches).
</details>

### Q8. What does the catch-all parameter `{*path}` do?
A. It deletes files.
B. It matches the remainder of the URL path, often including slashes.
C. It matches only one segment.
D. It matches query strings.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Used for file servers or proxying where you want to capture everything after a certain point (e.g. `/files/images/2023/logo.png`).
</details>

### Q9. What is the benefit of using `[controller]` and `[action]` tokens in route attributes?
A. They look cool.
B. They automatically are replaced by the actual class/method name, making the code resilient to renaming refactors.
C. They are required.
D. They improve performance.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`[Route("[controller]/[action]")]` adapts automatically if you rename `HomeController` to `MainController`.
</details>

### Q10. If an action has a route parameter `int id`, but the URL does not provide it and it is not optional, what happens?
A. The action is called with id=0.
B. 404 Not Found (or route doesn't match).
C. 500 Server Error.
D. The browser crashes.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If a required segment is missing, the route template does not match the request.
</details>

---

## HARD MCQs

### Q11. Difference between `[Route("/Home")]` (starting with slash) and `[Route("Home")]` (no slash) on an action, when the controller also has a `[Route("api")]`:
A. Same result.
B. `/Home` ignores the controller prefix, resulting in `localhost/Home`. `Home` combines, resulting in `localhost/api/Home`.
C. Both ignore the controller prefix.
D. Both combine.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Ideally, a leading slash `/` in an attribute route makes it **Root-Relative**, overriding the controller-level route prefix.
</details>

### Q12. Can you apply multiple `[Route]` attributes to a single action?
A. No.
B. Yes, the action will be accessible via multiple URL patterns (aliases).
C. Only if they are different verbs.
D. Yes, but only one works.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Example: `[Route("checkout")]` and `[Route("cart/checkout")]` can both point to same method.
</details>

### Q13. How does `MapControllerRoute` differ from `MapDefaultControllerRoute`?
A. `MapDefaultControllerRoute` adds the standard `{controller=Home}/{action=Index}/{id?}` pattern automatically. `MapControllerRoute` requires you to specify the pattern manually.
B. They are different libraries.
C. `MapDefault` is only for Admin.
D. No difference.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`MapDefaultControllerRoute()` is a convenience shorthand helper method.
</details>

### Q14. What is the order of precedence if both Attribute Routing and Conventional Routing are used?
A. Conventional wins.
B. Attribute Routing takes precedence for the specific actions it decorates; Conventional routing handles the rest.
C. They conflict and throw an error.
D. Random.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Attribute routes are more specific and are evaluated as part of the endpoint selection. If an action has an attribute route, it is generally not reachable via the conventional table unless explicitly configured.
</details>

### Q15. In generic routing, what is "Endpoint Routing"?
A. A middleware concept in .NET Core where routing decisions (`UseRouting`) are separated from endpoint execution (`UseEndpoints`).
B. A hardware router.
C. A legacy feature.
D. Routing for endpoints only.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
It decouples matching (calculating which endpoint will run) from dispatching (running it). This allows middleware like Authorization to run *after* a route is selected but *before* the action executes (so it knows which [Authorize] attributes apply).
</details>
