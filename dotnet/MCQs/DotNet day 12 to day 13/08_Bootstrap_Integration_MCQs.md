# 08_Bootstrap_Integration – MCQs

## EASY MCQs

### Q1. What is **LibMan** (Library Manager) used for in Visual Studio?
A. Managing NuGet packages (DLLs).
B. Managing client-side libraries (CSS, JS) like Bootstrap and jQuery.
C. Managing database libraries.
D. Managing book libraries.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is a lightweight tool for downloading client-side static files from providers like CDNJS or Unpkg without needing NodeJS/NPM.
</details>

### Q2. What is the standard file name for the LibMan configuration?
A. `package.json`
B. `libman.json`
C. `bower.json`
D. `config.xml`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It stores the list of libraries, versions, and destination folders.
</details>

### Q3. Which Bootstrap class creates a responsive, fixed-width centered container?
A. `.box`
B. `.container`
C. `.wrapper`
D. `.content`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`.container` (responsive fixed width) and `.container-fluid` (full width) are the foundational layout elements.
</details>

### Q4. To make an image responsive so it scales with the parent element, which class is used (Bootstrap 4/5)?
A. `.img-responsive`
B. `.img-fluid`
C. `.img-scale`
D. `.responsive`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`img-fluid` applies `max-width: 100%; height: auto;`.
</details>

### Q5. What is the grid system in Bootstrap based on?
A. 10 columns.
B. 12 columns.
C. 16 columns.
D. 4 columns.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The page width is divided into 12 conceptual columns. `col-6` takes half the width.
</details>

---

## MEDIUM MCQs

### Q6. Which combination of classes creates a standard navigation bar?
A. `navbar navbar-expand-sm bg-light navbar-light`
B. `menu main-menu`
C. `nav-bar top`
D. `header navigation`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Top-level `.navbar` establishes the component. `.navbar-expand-sm` handles collapsing behavior. Color schemes are set via `bg-*` and `navbar-*`.
</details>

### Q7. What does the `mt-3` class do?
A. Margin Top 3 pixels.
B. Margin Text 3.
C. Margin Top 3 units (typically 1rem in Bootstrap default).
D. Move Top 3.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Spacing utility: `{property}{side}-{size}`. m=margin, t=top, 3=spacer level 3.
</details>

### Q8. Why is `bootstrap.bundle.js` preferred over `bootstrap.js`?
A. It is smaller.
B. It includes **Popper.js**, which is required for dropdowns, tooltips, and popovers to work.
C. It includes jQuery.
D. It includes CSS.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Without the bundle (or manually including Popper), components relying on positioning (dropdowns) will fail.
</details>

### Q9. Which class hides an element on small screens and shows it on medium and larger?
A. `d-none d-md-block`
B. `hide-sm show-md`
C. `visible-md`
D. `hidden-xs`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`d-none` (display: none everywhere) -> overridden by `d-md-block` (display: block starting at medium breakpoint).
</details>

### Q10. What is the "Hamburger Menu"?
A. A food item.
B. The toggle button (three horizontal lines) that appears on mobile screens to expand the collapsed navigation menu.
C. A footer style.
D. A color scheme.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Implemented via `.navbar-toggler`.
</details>

---

## HARD MCQs

### Q11. In LibMan, what is the default "provider"?
A. `filesystem`
B. `cdnjs` (Content Delivery Network JS).
C. `unpkg`
D. `jsdelivr`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
LibMan fetches files from CDNs. cdnjs is the default.
</details>

### Q12. Difference between `container` and `container-fluid`:
A. `container` is full width; `container-fluid` is fixed.
B. `container-fluid` spans 100% of the viewport width at all times. `container` changes its max-width at each responsive breakpoint (jumping in steps).
C. They are key-value pairs.
D. No difference.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Use fluid for full-width layouts, container for centered boxed layouts.
</details>

### Q13. Which command installs `libman` CLI globally?
A. `npm install libman`
B. `dotnet tool install -g Microsoft.Web.LibraryManager.Cli`
C. `install-package libman`
D. `apt-get install libman`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It is a .NET Core Global Tool.
</details>

### Q14. What does the `sr-only` (or `.visually-hidden` in Bootstrap 5) class do?
A. Hides the element from all users.
B. Hides the element visually but keeps it available for **Screen Readers** (Accessibility).
C. Shows it only to seniors.
D. Highlights it.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Crucial for accessibility, allowing context for screen readers without cluttering visual design.
</details>

### Q15. How do you center content in a column vertically using Flexbox utilities in Bootstrap?
A. `align-items-center` (on the row/parent).
B. `center-y`
C. `vertical-align`
D. `middle`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Bootstrap grid rows are flex containers. `align-items-center` centers items on the cross axis (vertical).
</details>
