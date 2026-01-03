# 13_Model_Validation – MCQs

## EASY MCQs

### Q1. What attribute ensures a property is not null or empty?
A. `[NotNull]`
B. `[Required]`
C. `[Mandatory]`
D. `[Important]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It checks `param != null` and also empty strings if configured.
</details>

### Q2. Which attribute validates an email format?
A. `[Email]`
B. `[EmailAddress]`
C. `[Mail]`
D. `[Format("Email")]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Uses a basic regex to ensure user@domain structure.
</details>

### Q3. Where are these validation attributes found?
A. `System.IO`
B. `System.ComponentModel.DataAnnotations`
C. `System.Linq`
D. `System.Validation`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Common namespace for metadata and validation attributes.
</details>

### Q4. If `[ApiController]` is used, what happens when validation fails?
A. The code enters the action method.
B. A 400 Bad Request response is automatically returned with error details.
C. The server crashes.
D. It saves null values.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Automatic model state validation filter.
</details>

### Q5. How do you validate string length?
A. `[Length]`
B. `[StringLength(max)]` or `[MaxLength(max)]`.
C. `[Size]`
D. `[Count]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Both exist. MaxLength affects DB schema (EF), StringLength is primarily for validation logic.
</details>

---

## MEDIUM MCQs

### Q6. Which property stores the validation errors in a Controller?
A. `ViewData`
B. `ModelState`
C. `ErrorList`
D. `ValidationParams`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`ModelState.IsValid` checks if any binder/validator added errors.
</details>

### Q7. How do you provide a custom error message?
A. `[Required("My Message")]`
B. `[Required(ErrorMessage = "My Message")]`
C. `[Required(Message = "My Message")]`
D. Impossible.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
All validation attributes support the `ErrorMessage` named property.
</details>

### Q8. What does `[Compare("OtherProperty")]` do?
A. Compares equality (e.g., Password and ConfirmPassword).
B. Sorts the list.
C. Compares usage.
D. Creates a foreign key.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Essential for registration forms.
</details>

### Q9. `[Range(18, 99)]` validates what?
A. String length.
B. Array size.
C. Numeric value must be between min and max (inclusive).
D. The number of properties.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Logic: value >= min && value <= max.
</details>

### Q10. Does `[DataType(DataType.Date)]` validate the date?
A. Yes.
B. No. It is a formatting hint for the UI (e.g. renders a date picker), not a server-side validator.
C. Only in Chrome.
D. Sometimes.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Important distinction. Use proper types (DateTime) or Regex for strict validation.
</details>

---

## HARD MCQs

### Q11. Can you create custom validation attributes?
A. No.
B. Yes, by inheriting from `ValidationAttribute` and overriding `IsValid`.
C. Only in paid versions.
D. Yes, using Javascript.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Allows complex domain-specific rules (e.g. `[MustBeEvenNumber]`).
</details>

### Q12. What is the difference between `[Phone]` and `[RegularExpression]`?
A. None.
B. `[Phone]` uses a loose, permissive standard algorithm. `[RegularExpression]` allows you to define a strict custom pattern.
C. `[Phone]` calls the number.
D. `[Phone]` is deprecated.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Phone formats vary wildly globally, so the built-in attribute is very broad.
</details>

### Q13. `ModelState.IsValid` is false. How do you inspect errors?
A. `ModelState.Values.SelectMany(v => v.Errors)`
B. Use debugger only.
C. Check logs.
D. Ask user.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Errors are grouped by key (property name).
</details>

### Q14. Does Validation run before or after Model Binding?
A. Before.
B. After (or during). The binder attempts to set values. If conversion fails (string -> int), a validation error is added. Then attributes are checked on the bound object.
C. Same time.
D. Never.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You iterate on the bound model.
</details>

### Q15. `[Remote]` attribute is used for what?
A. Controlling the TV.
B. Client-side validation that calls a server-side URL (AJAX) to validate data without submitting the form (e.g., checking if Username is taken).
C. Remote desktop.
D. Cloud validation.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Particularly useful in MVC Views, less common in pure APIs (frontend handles it).
</details>
