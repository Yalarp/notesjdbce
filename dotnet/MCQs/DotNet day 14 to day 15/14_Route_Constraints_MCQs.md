# 14_Route_Constraints – MCQs

## EASY MCQs

### Q1. What does `{id:int}` signify in a route template?
A. The parameter `id` must be an Integer. If it is "abc", the route won't match (404).
B. The parameter `id` is internal.
C. The parameter `id` is international.
D. The parameter `id` is interval.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Constraint restricts matching to specific types.
</details>

### Q2. How do you specify that a route parameter is optional?
A. `{id:optional}`
B. `{id?}`
C. `{id=null}`
D. `[Optional] id`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Standard syntax `?`.
</details>

### Q3. How do you provide a default value of 1 for `page`?
A. `{page=1}`
B. `{page:1}`
C. `{page(1)}`
D. `{page==1}`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Syntax `{key=value}`.
</details>

### Q4. Which constraint ensures the value is a boolean?
A. `{active:bool}` (matches true/false).
B. `{active:boolean}`
C. `{active:bit}`
D. `{active:b}`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Maps to System.Boolean.
</details>

### Q5. If a URL is `/api/users/abc` and route is `[HttpGet("{id:int}")]`, what status code is returned?
A. 500 Error.
B. 404 Not Found.
C. 200 OK (id = 0).
D. 400 Bad Request.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The route selector sees no match. It acts as if the endpoint doesn't exist for that URL.
</details>

---

## MEDIUM MCQs

### Q6. How do you chain constraints? (e.g., int AND min value 1)
A. `{id:int:min(1)}`
B. `{id:int && min(1)}`
C. `{id:int, min(1)}`
D. `{id:int | min(1)}`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Colon separated.
</details>

### Q7. Which constraint limits string length?
A. `max(10)`
B. `maxlength(10)`
C. `len(10)`
D. `size(10)`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`max` is for numeric magnitude. `maxlength` is for string character count.
</details>

### Q8. What does `{name:alpha}` match?
A. Any string.
B. Only string containing alphabetic characters (A-Z, a-z). No numbers or symbols.
C. Alphanumeric.
D. Alpha version users.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Useful for names, cities (mostly).
</details>

### Q9. Can you use Regex in constraints?
A. No.
B. Yes, e.g., `{ssn:regex(^\d{{3}}-\d{{2}}-\d{{4}}$)}`.
C. Only in Java.
D. Yes, but it is slow.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Provides maximum flexibility. Note the double curly braces `{{ }}` needed to escape regex braces inside the route string.
</details>

### Q10. If you have two routes `[HttpGet("{id:int}")]` and `[HttpGet("{name}")]`, which one matches `/api/5`?
A. `{id:int}`
B. `{name}`
C. Ambiguous Exception.
D. Both.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The router prioritizes specific constrained matches over generic catch-all strings.
</details>

---

## HARD MCQs

### Q11. What is the `guid` constraint?
A. Matching global unique identifiers (e.g., `87063f2e-9907...`).
B. Matching user IDs.
C. Matching guides.
D. Matching google IDs.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
UUID format xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.
</details>

### Q12. Can you create custom route constraints?
A. No.
B. Yes, by implementing `IRouteConstraint` and registering it in `Program.cs`.
C. Yes, using Javascript.
D. Only Microsoft can.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Useful if you need to validate something against a DB or complex logic during routing (rare, but possible).
</details>

### Q13. `min(18)` works on which types?
A. int, long, float, double, decimal.
B. String size.
C. Dates.
D. Arrays.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Numeric comparison.
</details>

### Q14. `{slug:required}` constraint. Is it redundant?
A. Yes, route parameters are required by default (non-optional).
B. No, it ensures it is not empty string.
C. Yes, it does nothing.
D. It makes it optional.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Enforces that the parameter value is non-empty. Useful when mixed with other logic.
</details>

### Q15. Route Constraint vs Model Validation Attribute. What's the difference?
A. None.
B. Route Constraints run during Routing (selecting which action to call). If failed -> 404. Model Validation runs inside the action (or filter) after selection. If failed -> 400.
C. Constraints are for database.
D. Validation is for URL.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Crucial architectural distinction. Use constraints to distinguish actions (GetById vs GetByName). Use validation to check data integrity.
</details>
