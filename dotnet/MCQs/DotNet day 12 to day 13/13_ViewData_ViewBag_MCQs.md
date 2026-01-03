# 13_ViewData_ViewBag – MCQs

## EASY MCQs

### Q1. What is the primary purpose of `ViewData` and `ViewBag`?
A. To save data to the database.
B. To pass data from the Controller to the View.
C. To pass data from View to Controller.
D. To replace Sessions.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
They provide a way to pass small amounts of data (like titles, messages, or dropdown lists) distinct from the main Model.
</details>

### Q2. `ViewData` is of what type?
A. `Dynamic`
B. `Dictionary<string, object>` (ViewDataDictionary)
C. `String`
D. `Array`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It stores data as generic objects accessible via string keys.
</details>

### Q3. `ViewBag` utilizes which C# feature?
A. Generics
B. `dynamic` keyword (introduced in C# 4.0).
C. Async/Await
D. Pointers

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This allows dynamic property access (e.g., `ViewBag.Title`) instead of dictionary syntax.
</details>

### Q4. Which syntax checks for null in `ViewData` correctly?
A. `ViewData.Has("Key")`
B. `if (ViewData["Key"] != null)`
C. `ViewData.IsSet("Key")`
D. `ViewData.Contains("Key")`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Since it returns `null` if the key is missing (or value is null), a simple null check works.
</details>

### Q5. Do `ViewData`/`ViewBag` allow passing data from one Controller Action to ANOTHER Action (redirect)?
A. Yes.
B. No. Their life cycle is limited to the **current request** only.
C. Yes, if keys start with _.
D. Yes, if using HTTPS.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Data is lost upon redirect. For cross-request persistence (Redirect scenarios), use `TempData`.
</details>

---

## MEDIUM MCQs

### Q6. Comparison: `ViewData["Title"] = "ABC"` vs `ViewBag.Title = "ABC"`. Are they related?
A. No, they are separate storage.
B. Yes, `ViewBag` is just a dynamic wrapper around `ViewData`. They modify the same underlying collection.
C. `ViewData` is faster.
D. `ViewBag` overwrites `ViewData` entirely.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You can set `ViewBag.Title` in Controller and read `ViewData["Title"]` in View (and vice versa). They share the state.
</details>

### Q7. Major disadvantage of `ViewBag`?
A. It is too fast.
B. Lack of compile-time type checking and no IntelliSense. If you misspell a property name, you only find out at runtime (it returns null).
C. It cannot store strings.
D. It requires a database.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Unlike strong-typed models, dynamic types are late-bound errors waiting to happen.
</details>

### Q8. When retrieving a complex object from `ViewData`, what must you do?
A. Nothing.
B. Explicit Type Casting. e.g., `var list = (List<string>)ViewData["MyList"];`
C. Use `json.parse`.
D. Use `ToString()`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`ViewData` stores everything as `object`. You must cast it back to use specific methods/properties. `ViewBag` does this automatically (dynamically).
</details>

### Q9. What is better for passing the "Main" data object to a view?
A. `ViewBag`
B. A Strongly-Typed `ViewModel` (passed via `return View(model)`).
C. `ViewData`
D. `Session`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
ViewModels provide type safety, refactoring support, validation, and IntelliSense. Use `ViewBag/ViewData` only for peripheral data (layout titles, sidebar widgets).
</details>

### Q10. Can you pass a Model AND `ViewBag` data to the same View?
A. No.
B. Yes. `return View(myModel);` passes the model, and any properties set on `ViewBag` are also available in the view.
C. Only in .NET 5.
D. Only if the model is dynamic.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
They function in parallel. The Model is accessed via `@Model`, and the bag via `@ViewBag`.
</details>

---

## HARD MCQs

### Q11. Which is slightly faster internally?
A. `ViewBag`
B. `ViewData`
C. They are identical.
D. `TempData`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`ViewBag` adds the overhead of the dynamic DLR (Dynamic Language Runtime) to resolve properties to dictionary keys. `ViewData` is a direct dictionary lookup. Ideally negligible, but `ViewData` is technically faster.
</details>

### Q12. How does `ViewData.Model` relate to `@Model`?
A. They are unrelated.
B. `ViewData.Model` creates a new model.
C. The `@Model` directive in Razor is actually syntactic sugar for accessing `ViewData.Model`.
D. It throws an error.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
The `ViewDataDictionary` has a special property `.Model` where the strongly typed model object is stored.
</details>

### Q13. If you have `@model Employee` in your view, can you still use `ViewData`?
A. No.
B. Yes, `ViewData` is still available for weakly-typed auxiliary data.
C. Only if User is Admin.
D. No, it clears `ViewData`.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is the standard pattern: Strong model for the form, ViewData for the page title or user greeting.
</details>

### Q14. What happens if you try to use `@ViewBag.NonExistentProperty` in a View?
A. Runtime Exception "Property not found".
B. It returns `null` (and renders nothing if just outputting to HTML).
C. Compile Error.
D. It prints "undefined".

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Dynamics return null for missing members. However, if you try to access a method on it like `@ViewBag.BadProp.ToString()`, THEN you get a NullReferenceException.
</details>

### Q15. Is `ViewBag` available in Razor Pages (as opposed to MVC Views)?
A. Yes.
B. No. Razor Pages use `ViewData` only (via the `ViewData` property on the `PageModel`). Note: Some versions alias it, but `ViewData` is the primary citizen in Razor Pages.
C. Yes, but it's called `PageBag`.
D. Only in OnGet.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Razor Pages `PageModel` exposes a `ViewData` property. While you *can* use the dynamic feature, the explicit API design favors `ViewData`.
</details>
