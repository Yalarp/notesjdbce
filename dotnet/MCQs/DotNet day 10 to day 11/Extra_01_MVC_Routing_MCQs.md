# Extra_01_MVC_Routing – MCQs

## EASY MCQs

### Q1. What is the main purpose of "Routing" in ASP.NET Core MVC?
A. To map incoming HTTP request URLs to specific Controller Action methods.
B. To find files on disk.
C. To route packages.
D. To configure the database.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Routing decouples the URL structure from the physical file structure. It parses the URL (e.g., `/Home/Index`) and determines which code (Controller + Action) should execute.
</details>

### Q2. What is the default route pattern configured in most MVC apps?
A. `"{controller=Home}/{action=Index}/{id?}"`
B. `"{action}/{controller}"`
C. `"{id}/{controller}"`
D. `"{guid}"`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
This standard pattern conventionally maps the first segment to the Controller, the second to the Action, and the third to an optional ID parameter.
</details>

### Q3. In the URL `/Student/Edit/5`, what is the value of the `controller` segment?
A. `Student`
B. `StudentController`
C. `Edit`
D. `5`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The URL segment is `Student`. The framework appends the suffix "Controller" to find the class `StudentController`.
</details>

### Q4. What does the question mark `?` signify in the route parameter `{id?}`?
A. It is a query string.
B. It makes the parameter **Optional**.
C. It means integer only.
D. It is a syntax error.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If a parameter is optional ( `{id?}` ), the route matches even if that segment is missing from the URL (e.g., `/Home/Index` matches). Without `?`, the ID would be required.
</details>

### Q5. If the request URL is `http://localhost/`, which Controller and Action are selected by default?
A. `HomeController`, `Index` method.
B. `DefaultController`, `Index` method.
C. None (404).
D. `LoginController`, `Login` method.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The default values in the route pattern `{controller=Home}/{action=Index}` specify that if segments are missing, `Home` and `Index` are used.
</details>

---

## MEDIUM MCQs

### Q6. How does ASP.NET Core find the controller class from the URL segment "Home"?
A. It looks for a class named "Home".
B. It appends "Controller" to the segment name (Result: `HomeController`) and looks for that class.
C. It scans all classes.
D. It checks a text file.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Convention over configuration. The "Controller" suffix is required on class names but omitted in URLs.
</details>

### Q7. Can you have multiple routes in an application?
A. No, only one.
B. Yes, you can register multiple routes using `MapControllerRoute`. They are evaluated in sequence (top to bottom).
C. Yes, but they execute in parallel.
D. Only in .NET 5.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You often add specific routes (like `/blog/{slug}`) before the general default route. The first route that matches the URL wins.
</details>

### Q8. What happens if a URL matches TWO defined routes?
A. An exception is thrown.
B. The **first** route that matches (in registration order) is used.
C. Both actions are executed.
D. The last one is used.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Order matters. Specific routes should be registered before general/default routes.
</details>

### Q9. In the URL `http://localhost/Home/Details?id=5`, how is the ID passed?
A. As a route parameter (segment).
B. As a **Query String**.
C. As a Header.
D. In the Body.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Since it follows the `?` character in the URL, `id=5` is a query string parameter, not a route segment (which would look like `/Home/Details/5`). Both can be bound to action parameters.
</details>

### Q10. Which method is used to configure routes in `Program.cs`?
A. `app.UseRoutes()`
B. `app.MapControllerRoute()`
C. `app.RegisterRoutes()`
D. `app.StartRouting()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`MapControllerRoute` is the standard method in .NET 6+ to define endpoints for MVC controllers.
</details>

---

## HARD MCQs

### Q11. Validating the route `pattern: "api/{controller}/{id?}"` with defaults `new { action = "Index" }`: What action is called for URL `/api/Products`?
A. `Index`
B. `Products`
C. `Api`
D. None (404)

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
URL `/api/Products` matches the pattern.
- Literal `api` matches.
- `{controller}` matches `Products`.
- `{id}` is missing (optional).
- `{action}` is NOT in the pattern, but the `defaults` object specifies `action = "Index"`.
So `ProductsController.Index()` is called.
</details>

### Q12. What are "Route Constraints"?
A. They limit the traffic.
B. They enforce rules on route parameters (e.g., `{id:int}`), allowing a route to match only if the parameter satisfies the constraint (is an integer).
C. They are passwords.
D. They delete routes.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Constraints allow overloading URLs. `/users/5` (matches `{id:int}`) vs `/users/scott` (matches `{name:alpha}`).
</details>

### Q13. Attribute Routing (`[Route("...")]`) vs Conventional Routing (`MapControllerRoute`):
A. Startups must use Attribute Routing.
B. Conventional Routing is defined globally in `Program.cs`. Attribute Routing is defined on the Controller/Action itself.
C. They cannot be mixed.
D. Attribute routing is slower.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Conventional is good for UI/MVC apps with consistent patterns. Attribute routing is preferred for REST APIs where paths might vary significantly.
</details>

### Q14. If you have a route parameter named `{id}` and an action parameter `public IActionResult Edit(int studentId)`, will it bind automatically?
A. Yes.
B. No. The names do not match (`id` vs `studentId`). Model binding requires matching names.
C. Yes, it matches by type.
D. Only if you use `[FromRoute]`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Asp.Net Core binding looks for a parameter named `id` to match the route key `id`.
</details>

### Q15. Where does the route middleware place the parsed values?
A. `HttpContext.Items`
B. `HttpContext.Request.RouteValues` (RouteData).
C. `Session`
D. `Cookies`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The selected controller, action, and any parameters are stored in the `RouteValues` dictionary, which valid model binders access later.
</details>
