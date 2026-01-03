# 02_ViewModel_Pattern – MCQs

## EASY MCQs

### Q1. What is the primary purpose of a ViewModel in ASP.NET Core MVC?
A. To access the database.
B. To hold data specifically designed for a view, often combining data from multiple models.
C. To replace the Controller.
D. To style the page.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
A ViewModel is a Data Transfer Object (DTO) tailored for the View. It acts as a container for all the disparate pieces of data (e.g., Employee object + Page Title + Dropdown lists) required to render a specific page.
</details>

### Q2. In the directive `@model HomeDetailsViewModel`, what does the lowercase `model` keyword do?
A. It creates a new object.
B. It declares the **Type** of the model that the view expects.
C. It accesses the properties of the model.
D. It imports a namespace.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`@model` (lowercase) defines the class type (e.g., `IEnumerable<Student>`), making the view strongly typed. `@Model` (uppercase) is then used to access the instance data.
</details>

### Q3. Which of the following is a disadvantage of using `ViewBag` instead of a ViewModel?
A. It is too fast.
B. It requires extra class files.
C. It lacks compile-time type checking and IntelliSense (it is dynamic).
D. It cannot store strings.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Because `ViewBag` is dynamic, typos (e.g., `ViewBag.Titl`) are not caught until runtime, and you don't get code completion help in Visual Studio.
</details>

### Q4. Where is the recommended location to store ViewModel classes in your project?
A. In the `Controllers` folder.
B. In the `Views` folder.
C. In a dedicated `ViewModels` folder at the root.
D. In the `wwwroot` folder.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**
Keeping them in a separate `ViewModels` folder keeps the project organized and separates them from domain Entity Models.
</details>

### Q5. Can a ViewModel contain multiple different entity objects (e.g., an Employee AND a Department)?
A. No, only one.
B. Yes, that is one of its main use cases.
C. Only if they inherit from the same base class.
D. Only in .NET Framework 4.8.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
A ViewModel allows you to compose complex data structures. For example, a `DashboardViewModel` might contain `User`, `List<Tasks>`, `List<Messages>`, etc.
</details>

---

## MEDIUM MCQs

### Q6. Consider the code:
```csharp
public IActionResult Details() {
    var vm = new DetailsViewModel { PageTitle = "Info", Emp = _repo.Get(1) };
    return View(vm);
}
```
In the View, how do you access the PageTitle?
A. `@ViewBag.PageTitle`
B. `@Model.PageTitle`
C. `@details.PageTitle`
D. `@vm.PageTitle`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The object passed to `View(vm)` becomes the Model property of the WebViewPage. It is accessed via `@Model` (capital M).
</details>

### Q7. What is a key benefit of using a ViewModel for "Create/Edit" forms?
A. It automatically saves data.
B. It allows you to add Validation Attributes (like `[Required]`) that are specific to the UI (e.g., "Confirm Password") without cluttering the domain entity.
C. It is faster than an entity.
D. It bypasses the controller.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Domain models should represent business state. ViewModels represent UI state. Validation logic like "Password must match Confirm Password" belongs in the ViewModel, not the database entity.
</details>

### Q8. If you rename a property in a ViewModel, what happens to the Views that use it (assuming strongly-typed views)?
A. Nothing.
B. You get a compile-time error in the View, alerting you to update usages.
C. The view renders blank data.
D. The application crashes at runtime only.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is the "Refactoring Support" benefit. Since the view knows the type, the compiler checks that the properties exist.
</details>

### Q9. Which pattern follows the Separation of Concerns principle regarding ViewModels?
A. Putting business logic inside the ViewModel getter methods.
B. Using the ViewModel only for data transport, leaving creation logic in the Controller/Service and display logic in the View.
C. Accessing the database directly from the ViewModel.
D. Constructing the ViewModel inside the View.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
ViewModels should be "dumb" containers of data. They should not know about repositories or business rules.
</details>

### Q10. How typically do you map a Domain Model (Entity) to a ViewModel?
A. By casting `(ViewModel)entity`.
B. By manually copying properties (e.g., `vm.Name = entity.Name`) or using a library like AutoMapper.
C. It happens automatically.
D. You cannot map them.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Since they are different classes, you must write code to transfer the data, either line-by-line or using an object mapper tool.
</details>

---

## HARD MCQs

### Q11. Can a ViewModel allow data entry for **nested** lists (e.g., a Teacher with multiple Students)?
A. No.
B. Yes, by using `IList<Student>` properties and correct indexing in the HTML form (e.g., `name="Students[0].Name"`).
C. Yes, but only with AJAX.
D. No, HTML forms don't support lists.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The Model Binder is capable of binding complex nested collections if the HTML field names follow the indexer pattern.
</details>

### Q12. Why might you use a `SelectList` property in a ViewModel?
A. To display a grid.
B. To populate a `<select>` dropdown (e.g., for Department selection) in a form.
C. To list errors.
D. To select a file.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
A standard pattern for dropdowns: The ViewModel contains the selected ID (`int DeptId`) and the list of options (`IEnumerable<SelectListItem> Departments`).
</details>

### Q13. In a "Post-Redirect-Get" scenario with validation errors, why is `return View(viewModel)` necessary in the POST method?
A. To reset the form.
B. To re-render the form with the user's previously entered data (preserved in the ViewModel) and display validation error messages.
C. To save the data.
D. It is not necessary.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
If `ModelState.IsValid` is false, you don't redirect. You return the view, passing the *same* view model back so the user doesn't lose their input. You usually need to repopulate dropdown lists before returning.
</details>

### Q14. Can you inject services directly into a specific View via a ViewModel?
A. Yes.
B. No, the ViewModel is just data. However, the *View* can inject services using `@inject`, or the Controller can populate data into the ViewModel using services.
C. Yes, the ViewModel has a `Services` property.
D. Only in Tag Helpers.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
This is a nuanced point. The ViewModel itself is a POCO. It doesn't do DI. The *View* can do DI (`@inject`), but the ViewModel is just the carrier of state.
</details>

### Q15. Using `[JsonIgnore]` on a ViewModel property is relevant when?
A. Never, ViewModels are for HTML.
B. When the same ViewModel is also returned from an API endpoint (e.g., via AJAX call to a controller action returning `Json(model)`).
C. When using `View()`.
D. When saving to DB.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Sometimes Controller actions are dual-purpose or consumed by client-side JS. You might want to hide certain internal properties during JSON serialization.
</details>
