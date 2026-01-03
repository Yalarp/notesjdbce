# 04_Controllers_Routing – MCQs

## EASY MCQs

### Q1. A Web API Controller typically inherits from which class?
A. `Controller`
B. `ControllerBase`
C. `ApiController`
D. `BaseController`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`ControllerBase` is optimized for APIs. `Controller` adds View support (MVC), which is unnecessary overhead for pure APIs.
</details>

### Q2. In the route template `[Route("api/[controller]")]`, what does `[controller]` represent?
A. A literal string "controller".
B. A token that gets replaced by the controller's class name (minus the "Controller" suffix).
C. The method name.
D. The user name.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
For `MemberController`, it generates `/api/member`.
</details>

### Q3. Which attribute maps a method to an HTTP GET request?
A. `[HttpPost]`
B. `[HttpGet]`
C. `[Get]`
D. `[Fetch]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Standard verb mapping attribute.
</details>

### Q4. How do you define a route parameter in an attribute?
A. `[HttpGet("id")]`
B. `[HttpGet("{id}")]`
C. `[HttpGet("<id>")]`
D. `[HttpGet("(id)")]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Curly braces `{}` denote a route parameter that will be extracted from the URL path.
</details>

### Q5. What does the `[ApiController]` attribute NOT do?
A. Enforces Attribute Routing.
B. Enables Automatic HTTP 400 responses for validation errors.
C. Automatically infers binding sources (e.g. `[FromBody]`).
D. Generates Views automatically.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**
It is strictly for API behaviors, not View generation.
</details>

---

## MEDIUM MCQs

### Q6. Which route constraint matches only integers?
A. `{id:int}`
B. `{id:integer}`
C. `{id:num}`
D. `{id:d}`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The `int` constraint ensures the action is only selected if the segment is parseable as an Int32.
</details>

### Q7. How do you define an Optional parameter in a route?
A. `{id:optional}`
B. `{id?}`
C. `{id=null}`
D. `[Optional] id`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The question mark makes the parameter optional in the URL matching logic.
</details>

### Q8. What does `[FromRoute]` do?
A. Forces the parameter to be bound from the request body.
B. Forces the parameter to be bound from the Route Data (URL path).
C. Binds from Query String.
D. Binds from Headers.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Useful when you want to be explicit, e.g. `Get([FromRoute] int id)`.
</details>

### Q9. Can a controller have multiple Route attributes?
A. No.
B. Yes, e.g., `[Route("api/[controller]")]` and `[Route("special")]`. The controller actions will be accessible via both prefixes.
C. Only if on different servers.
D. Only in debug mode.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Routing is flexible and additive.
</details>

### Q10. What happens if you have two actions matching the SAME route (Ambiguous Match)?
A. The server crashes with an AmbiguousMatchException.
B. It picks the first one.
C. It picks the last one.
D. It returns a random one.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Routing must be deterministic. If two endpoints have identical templates and constraints, the framework cannot decide.
</details>

---

## HARD MCQs

### Q11. Consider `[HttpGet("search/{term}")]`. Does this match `/api/member/search/` (empty term)?
A. Yes, `term` is null.
B. No, unless the parameter is marked optional `search/{term?}`. Route parameters are required by default.
C. Yes, `term` is empty string.
D. Yes, works automatically.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Required parameters must create a URL segment. The trailing slash implies a missing segment, causing a 404 (or 405) mismatch.
</details>

### Q12. How do you combine constraints? e.g. Integer and Minimum value 1.
A. `{id:int:min(1)}`
B. `{id:int && min(1)}`
C. `{id:int, min(1)}`
D. `{id:int | min(1)}`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Constraints are chained with colons.
</details>

### Q13. If you use `[Route("action")]` on a method, does it combine with the controller's `[Route("api/[controller]")]`?
A. Yes, resulting in `/api/[controller]/action`.
B. No, if the action route starts with `/` (absolute path). Otherwise, yes, it appends.
C. No, it overrides it completely.
D. Yes, but only if you add `~`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
By default, attribute routes on actions are appended to the controller's route prefix. To override, use a leading slash `/` or `~/`.
</details>

### Q14. What binding source is inferred for a complex type parameter `public ActionResult Post(Product p)` in an `[ApiController]`?
A. `[FromQuery]`
B. `[FromForm]`
C. `[FromBody]`
D. `[FromRoute]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The `[ApiController]` convention assumes complex object types come from the Request Body (JSON) by default.
</details>

### Q15. `[HttpGet("{id:int}")]` vs `[HttpGet("{name:alpha}")]`. If URL is `/api/member/123`, which runs?
A. Both.
B. The first one defined.
C. `{id:int}` because "123" satisfies the `int` constraint, but fails `alpha`.
D. Ambiguous Application Exception.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Constraints act as filters/selectors. The routing engine filters out `{name:alpha}` because "123" is not alphabetic, leaving only one valid match.
</details>
