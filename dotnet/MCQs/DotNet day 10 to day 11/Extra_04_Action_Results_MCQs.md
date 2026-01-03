# Extra_04_Action_Results – MCQs

## EASY MCQs

### Q1. What is the base class for all return types in an MVC Action Method?
A. `ControllerResult`
B. `ActionResult` (or the interface `IActionResult`)
C. `WebResult`
D. `Response`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`ActionResult` is the abstract base class. Typical usage uses the interface `IActionResult` for flexibility.
</details>

### Q2. Which helper method returns a `ViewResult` (HTML)?
A. `return Html();`
B. `return View();`
C. `return Page();`
D. `return Render();`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The `View()` method searches for the matching .cshtml file and renders it.
</details>

### Q3. Which helper method returns JSON data?
A. `return Data();`
B. `return Json(data);`
C. `return Object();`
D. `return JS();`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Json(obj)` serializes the object to JSON format and sets the Content-Type to application/json.
</details>

### Q4. Which result is used to send the user to a different URL or Action?
A. `ForwardResult`
B. `RedirectResult` (or `RedirectToActionResult`)
C. `MoveResult`
D. `GoToResult`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Redirects send a 301/302 HTTP response to the browser, telling it to navigate elsewhere.
</details>

### Q5. What does `Content("Hello")` return?
A. JSON
B. A View
C. Plain Text (ContentResult) with the string "Hello".
D. A File

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
`ContentResult` writes string literal content directly to the response body, default type is text/plain.
</details>

---

## MEDIUM MCQs

### Q6. Which redirect method is strongly typed to a Controller/Action name?
A. `Redirect("url")`
B. `RedirectToAction("ActionName", "ControllerName")`
C. `RedirectToPage()`
D. `Return()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`RedirectToAction` generates the URL based on routing configuration, which is safer than hardcoding "http://..." strings.
</details>

### Q7. What is the difference between `View()` and `PartialView()`?
A. `PartialView()` does not run `_ViewStart.cshtml` (Layout) code; it renders ONLY the specific .cshtml fragment. `View()` typically renders the full page with Layout.
B. `PartialView` is deprecated.
C. `PartialView` is for PDFs.
D. None.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Partial views are used for reusable components (like a navbar or widget) embedded inside other views or loaded via AJAX. They shouldn't include the full `<html>` skeleton.
</details>

### Q8. To return a 404 error from an action, you use:
A. `return Error(404);`
B. `return NotFound();`
C. `return Null();`
D. `return Missing();`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`NotFound()` is a helper returning `NotFoundResult` (HTTP 404).
</details>

### Q9. Which result is best for downloading a PDF file stored on disk?
A. `FileResult` (specifically `PhysicalFile` or `FileStream`)
B. `pdfResult`
C. `ViewResult`
D. `JsonResult`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`return File(bytes, "application/pdf")` serves binary content with the correct MIME type.
</details>

### Q10. What action result allows you to return specific HTTP Status codes?
A. `StatusResult`
B. `StatusCode(418)`
C. `CodeResult`
D. `HttpResult`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`StatusCode(int)` allows returning arbitrary HTTP codes (like 500, 429, etc.).
</details>

---

## HARD MCQs

### Q11. Why use `IActionResult` return type instead of `ViewResult`?
A. It is slower.
B. It allows polymorphism. The action can return different types (e.g., `View()` on success, `NotFound()` on failure) which both implement `IActionResult`.
C. It is required.
D. It converts to JSON automatically.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Flexibility. If you define return type as `ViewResult`, you cannot return `Json()` or `NotFound()` from the same method without compilation errors.
</details>

### Q12. Post-Redirect-Get (PRG) pattern typically involves:
A. Returning `View()` after POST.
B. Returning `RedirectToAction()` after a successful POST operation.
C. Returning `Json()` after POST.
D. Returning `null`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This prevents the "Confirm Form Resubmission" warning if the user refreshes the page. Redirecting changes the browser state to a safe GET request.
</details>

### Q13. `EmptyResult` generates:
A. A blank HTML page.
B. A 200 OK response with 0 length body.
C. A 204 No Content response.
D. An Exception.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Sometimes you want to do nothing (void). `EmptyResult` writes nothing to the response stream.
</details>

### Q14. Should methods returning `JSON` use `[HttpPost]`?
A. Always.
B. Not necessarily. JSON can be returned via GET (e.g., fetching data). However, for sensitive actions modifying data, POST is preferred.
C. Never.
D. Only for Arrays.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
AJAX GET requests (`$.get`) often consume JSON endpoints.
</details>

### Q15. `Forbid()` vs `Unauthorized()`:
A. They are the same.
B. `Unauthorized()` returns 401 (Not Authenticated - "Who are you?"). `Forbid()` returns 403 (Forbidden - "I know who you are, but you can't come in").
C. `Forbid` is for admins.
D. `Unauthorized` is for files.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Semantic difference in HTTP status codes regarding authentication vs authorization failures.
</details>
