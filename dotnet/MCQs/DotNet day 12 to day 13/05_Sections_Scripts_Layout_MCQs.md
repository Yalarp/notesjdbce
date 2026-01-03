# 05_Sections_Scripts_Layout – MCQs

## EASY MCQs

### Q1. What is the primary purpose of a `_Layout.cshtml` file?
A. To process database queries.
B. To define the common UI structure (header, footer, navigation) used by multiple views (Master Page).
C. To run scripts.
D. To define the database schema.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It enforces a consistent look and feel across the application and eliminates duplicating HTML like `<html>`, `<head>`, and navbar code in every view.
</details>

### Q2. Which method call helps render the content of the child view inside the layout?
A. `@RenderPage()`
B. `@RenderBody()`
C. `@RenderView()`
D. `@RenderChild()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`@RenderBody()` is the placeholder in the Layout where the specific View's content is injected.
</details>

### Q3. What is a "Section" in a Layout?
A. A database table.
B. A specific named area in the layout (e.g., "Scripts" or "Sidebar") where a view can inject optional or required content.
C. A div tag.
D. A security zone.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Defined via `@RenderSection("Name")` in Layout and `@section Name { ... }` in View.
</details>

### Q4. Which file automatically specifies the default Layout for all views in a folder?
A. `_ViewImports.cshtml`
B. `_ViewStart.cshtml`
C. `Program.cs`
D. `Index.cshtml`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`_ViewStart.cshtml` is executed before the view. It typically contains `Layout = "_Layout";`.
</details>

### Q5. Typically, where are JavaScript script tags referencing libraries (like jQuery) placed in the Layout?
A. Inside the `<title>` tag.
B. At the very top of `<body>`.
C. Near the closing `</body>` tag (for performance).
D. Outside the `<html>` tag.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Placing scripts at the bottom allows the HTML content to render/display before the potentially heavy scripts take time to load/parse.
</details>

---

## MEDIUM MCQs

### Q6. How do you define a section named "Scripts" in the Layout that is **Optional**?
A. `@RenderSection("Scripts", required: false)`
B. `@RenderSection("Scripts", true)`
C. `@RenderSection("Scripts")`
D. `@OptionalSection("Scripts")`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The second parameter `required` determines if an exception is thrown when the child view doesn't define the section.
</details>

### Q7. If a Layout has `@RenderSection("Header", required: true)` and the View does not have `@section Header { ... }`, what happens?
A. It works fine, section is empty.
B. Runtime Error (Exception).
C. The page reloads.
D. It uses a default header.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`InvalidOperationException`: The section "Header" has been defined as required but has not been implemented.
</details>

### Q8. How do you check if a section is defined before trying to render it?
A. `if (SectionExists("Name"))`
B. `if (IsSectionDefined("Name"))`
C. `if (HasSection("Name"))`
D. `try-catch`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`IsSectionDefined` returns a boolean, allowing conditional rendering logic (e.g., render a default sidebar if the view doesn't provide one).
</details>

### Q9. Can a View use a different layout than the one specified in `_ViewStart.cshtml`?
A. No.
B. Yes, by explicitly setting `Layout = "OtherLayout";` or `Layout = null;` at the top of the View file.
C. Only if Admin.
D. Only via C# code.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
View-level settings override hierarchy/ViewStart settings.
</details>

### Q10. What is the scope of `@section` content?
A. It replaces the entire page.
B. It is moved from the child view and rendered in the corresponding `@RenderSection` location in the parent Layout.
C. It is executed in the browser.
D. It is stored in Session.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It allows "Holing specific content" to be teleported to specific slots in the outer HTML shell.
</details>

---

## HARD MCQs

### Q11. Can you nest layouts (Layout using another Layout)?
A. No.
B. Yes. A view can use `LayoutA`, and `LayoutA` can set `Layout = "LayoutB"`.
C. Only 1 level deep.
D. Deprecated.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is useful for complex sites (e.g., a "TwoColumnLayout" that inherits from a base "MasterLayout"). The child's content bubbles up through multiple `@RenderBody()` calls.
</details>

### Q12. Why shouldn't you put huge logic blocks inside `@section`?
A. It creates a compile error.
B. Sections are primarily for content injection (scripts, styles, sidebars). Heavy logic is hard to debug and violates MVP separation.
C. Sections have a size limit.
D. Sections don't support C#.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
While possible, it's a code smell. View logic should be minimal.
</details>

### Q13. `Layout = null` is often used for:
A. Home Page.
B. Partial Views (returned as full Views), AJAX responses returning HTML fragments, or popups/modals that don't need the site chrome.
C. Error Pages.
D. Login Page.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It tells the engine not to wrap the content in any template.
</details>

### Q14. Can `_ViewStart` be overridden by a file of the same name in a subdirectory?
A. No.
B. Yes, `_ViewStart` is hierarchical. The one closest to the view executes. (Actually, ALL _ViewStart files from root down to the folder are executed in order).
C. Yes, it replaces the root one.
D. No, only one ViewStart allowed.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
They execute hierarchically. Root `_ViewStart` runs, then Subfolder `_ViewStart` runs. The last one setting the Layout wins.
</details>

### Q15. How do you pass data from a Layout to the View?
A. You cannot.
B. Via `ViewBag` / `ViewData`. (e.g. Layout sets `ViewBag.Title`, View reads it -- actually usually View sets it and Layout reads it, but it shares the same dictionary).
C. Via arguments.
D. Via static variables.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
They share the same ViewContext state.
</details>
