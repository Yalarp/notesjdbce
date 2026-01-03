# 11_List_Validation – MCQs

## EASY MCQs

### Q1. What is the common issue when validating a required dropdown list bound to a non-nullable integer?
A. It works perfectly.
B. If the user selects the default option (value=""), the validation error says "The value '' is invalid" instead of the custom `[Required]` message.
C. The dropdown disappears.
D. The form submits automatically.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
An empty string cannot be converted to an `int` (value type), resulting in a model binding type conversion error before the Required attribute even runs.
</details>

### Q2. How do you ensure the "Please Select" option in a dropdown has an empty value?
A. `<option value="0">Please Select</option>`
B. `<option value="">Please Select</option>`
C. `<option>Please Select</option>`
D. `<option value="null">Please Select</option>`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Setting `value=""` ensures that when selected, an empty string is sent to the server, which is treated as "no selection" by validation logic.
</details>

### Q3. Which property type is recommended for a required Dropdown list to ensure proper validation?
A. `int`
B. `int?` (Nullable int)
C. `string`
D. `double`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
A nullable type can hold `null`. When `""` is posted, it binds as `null`, allowing the `[Required]` attribute to detect the absence of a value and show the custom error message.
</details>

### Q4. How do you generate a specific error message like "Please select a department"?
A. `[Required(ErrorMessage = "Please select a department")]`
B. `[Error("Please select a department")]`
C. `[Message("Please select a department")]`
D. `[Select("Please select a department")]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
The `ErrorMessage` property of the `[Required]` attribute allows you to override the default text.
</details>

### Q5. What happens if you forget to repopulate the `ViewBag` (or `ViewData`) for the dropdown in the POST method when validation fails?
A. The form validates successfully.
B. The dropdown list is empty or causes a runtime error when the View renders.
C. The previous values are automatically remembered.
D. The page redirects to Index.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`ViewBag` data does not survive the request. If you return `View(model)` without reloading the list data, the `asp-items` helper has no source to bind to.
</details>

---

## MEDIUM MCQs

### Q6. Validating an Enum dropdown often requires the property to be nullable. Why?
A. Enums are reference types.
B. Enums are value types and have a default value (usually 0, e.g., `Gender.Male`). If not nullable, the default value is valid, so the user might unintentionally submit "Male" even if they didn't touch the dropdown.
C. Enums are strict.
D. Enums cannot be validated.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Making the enum nullable (`Gender?`) ensures no default value is assumed; "Please Select" binds to null, triggering the `[Required]` error.
</details>

### Q7. Consider this code: `[Display(Name = "Department")] public int deptId { get; set; }`. What error message is shown by default if binding fails for an empty string?
A. "Department is required."
B. "The value '' is invalid."
C. "Error."
D. None.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is the default system message for a type conversion failure (string to int). It is not user-friendly.
</details>

### Q8. Which helper generates options from an Enum type?
A. `Html.GetEnumSelectList<TEnum>()`
B. `Html.DropDownListForEnum()`
C. `Html.EnumList()`
D. `Html.GetOptions<TEnum>()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
This helper inspected the Enum type and creates a `SelectList` where the text is the enum name and the value is the underlying integer.
</details>

### Q9. In the POST action, `ViewData["DeptId"] = new SelectList(list, "Id", "Name", model.DeptId);` - what is the purpose of the 4th argument (`model.DeptId`)?
A. To sort the list.
B. To filter the list.
C. To select the item that the user previously chose, ensuring their selection is preserved when the form reloads with errors.
D. To validate the ID.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
This sets the `SelectedValue` property of the `SelectList`, causing the corresponding `<option>` to have the `selected` attribute in HTML.
</details>

### Q10. Why is `ModelState.IsValid` essential in the POST method?
A. It checks if the database is online.
B. It confirms that the incoming data satisfies all validation rules (Attributes like Required, Range, etc.) before proceeding to save.
C. It checks if the user is logged in.
D. It formats the data.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Always check this flag. If false, return the view (with data repopulated) to show errors.
</details>

---

## HARD MCQs

### Q11. If you strictly CANNOT change the Model property type to nullable (e.g. legacy DB schema uses `int`), how can you validate the "Please Select" effectively?
A. You cannot.
B. Use a View Model with a nullable property for the API/View layer, then map it to the Domain Model (which has non-nullable int) after validation passes.
C. Use JavaScript only.
D. Hardcode value 0.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Using a ViewModel (`EmployeeCreateViewModel`) separates the presentation logic (which needs validation) from the storage logic. This is the architectural best practice.
</details>

### Q12. What does `asp-validation-summary="All"` display?
A. Only property errors.
B. Both global (Model-level) errors and individual property errors.
C. Only server errors.
D. Only JavaScript errors.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`ModelOnly` shows generic errors. `All` shows every error found in the ModelState structure.
</details>

### Q13. If `DepartmentId` is nullable `int?`, but the database column is `NOT NULL`, when does the conversion happen?
A. Automatically by Entity Framework.
B. You must handle it manually during the mapping (e.g., `emp.DeptId = viewModel.DeptId.Value`). Since validation passed, you know `.Value` is safe to access (not null).
C. It throws an error.
D. It saves as 0.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The `[Required]` attribute guarantees `ModelState.IsValid` is true only if the value is NOT null. So safely accessing `.Value` is permissible inside the `if (ModelState.IsValid)` block.
</details>

### Q14. Can you disable client-side validation for a specific form?
A. No.
B. Yes, by removing the `jquery.validate.unobtrusive` script for that page or specific section.
C. Yes, using `asp-novalidate`.
D. Only globally.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Client-side validation is driven by scripts parsing the `data-val` attributes. Providing the attributes (server-side) without the scripts disables the client-side check.
</details>

### Q15. How does the generic `Range` attribute behave with nullable types?
A. It crashes.
B. Validates only if value is present. If value is null, `Range` creates no error (unless `[Required]` is also present).
C. Treats null as 0.
D. Treats null as infinity.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Most validation attributes (besides `[Required]`) return `Success` if the input is null, allowing them to be optional.
</details>
