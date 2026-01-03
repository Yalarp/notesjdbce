# 30_Single_Responsibility_Principle – MCQs

## EASY MCQs

### Q1. The core definition of SRP is:
A. A class should be short.  
B. A class should have only one reason to change.  
C. A class should have only one method.  
D. A class should be private.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Robert C. Martin defines responsibility as "a reason to change".
</details>

### Q2. In the example, the bad `Invoice` class was handling:
A. Invoice logic, Logging, Emailing, and Logging.  
B. Only Invoice logic.  
C. Database only.  
D. Nothing.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It mixed business rules (invoice) with infrastructure concerns (logging, email), violating SRP.
</details>

### Q3. How do we fix an SRP violation?
A. Delete dependencies.  
B. Move unrelated responsibilities into their own separate classes (Decomposition).  
C. Write more comments.  
D. Make methods private.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Factor out the Logging logic to a `Logger` class, Email logic to `EmailSender`, etc.
</details>

### Q4. Which of these is a valid "Responsibility"?
A. Being a class.  
B. Calculating tax.  
C. Having variables.  
D. Running.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Business rules (like Tax Calculation) represent a distinct axis of change.
</details>

### Q5. A "God Class" or "Kitchen Sink Class" is:
A. A class that does everything (Violates SRP).  
B. A good design pattern.  
C. A static class.  
D. A database.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Used as an anti-pattern term for classes that have grown to control too many unrelated parts of the system.
</details>

---

## MEDIUM MCQs

### Q6. Why does SRP make testing easier?
A. Tests run faster.  
B. You can test the `Invoice` logic without needing to actually send emails or write to disk.  
C. You don't need tests.  
D. The compiler tests it.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
By separating concerns, you can mock the dependencies (`MockEmailSender`) and focus the test solely on the Invoice calculation logic in isolation.
</details>

### Q7. If Developer A works on Logging and Developer B works on Invoicing, and SRP is followed:
A. They will have merge conflicts in `Invoice.cs`.  
B. They will likely work in different files (`Logger.cs` vs `Invoice.cs`) avoiding conflicts.  
C. They cannot work in parallel.  
D. One must wait for the other.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
SRP supports team scalability by decoupling files and responsibilities.
</details>

### Q8. "Cohesion" in SRP terms means:
A. Code that sticks together.  
B. The degree to which elements inside a class belong together. High cohesion is good (SRP).  
C. Low cohesion is good.  
D. Using glue.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A class with High Cohesion has methods and fields that all relate to a single purpose. A violation of SRP usually leads to Low Cohesion.
</details>

### Q9. Is mixing "Presentation Logic" (Console.WriteLine) and "Business Logic" (Calculate) in one class an SRP violation?
A. No.  
B. Yes.  
C. Only in Web Apps.  
D. Only in Databases.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Yes. "How data is displayed" is a different reason to change than "How data is calculated".
</details>

### Q10. Does SRP apply only to Classes?
A. Yes.  
B. No, it applies to Methods and Modules/Packages as well.  
C. Only to Interfaces.  
D. Only to Files.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A method should do one thing. A module should have a coherent set of functionality. The principle scales up and down.
</details>

---

## HARD MCQs

### Q11. Can applying SRP lead to "Class Explosion" (too many small classes)?
A. Yes, and this is considered bad by everyone.  
B. Yes, but having many small, focused classes is generally preferred over few giant, unmaintainable ones.  
C. No, it reduces class count.  
D. It depends on the language.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Critics argue it fragments code (jumping between files). Proponents argue that managing complexity via composition of small parts is the only way to build large robust systems.
</details>

### Q12. "Active Record" pattern (Object saves itself: `obj.Save()`) vs SRP.
A. Active Record strictly follows SRP.  
B. Active Record technically violates SRP because the class handles both Data (Domain) and Persistence (Database).  
C. Active Record is not OOP.  
D. SRP was designed for Active Record.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
While convenient for simple apps, Active Record mixes concerns. The Repository pattern (separate class for saving) separates Domain from Persistence, aligning with SRP.
</details>

### Q13. Refactoring a class to follow SRP often naturally leads to using which other principle?
A. DIP (Dependency Inversion Principle).  
B. None.  
C. Static coupling.  
D. Hard coding.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Once you extract `Logger`, the original class needs to use it. Instead of `new Logger()`, you typically inject `ILogger` (DIP/DI) to maintain decoupling.
</details>

### Q14. Is it ever acceptable to violate SRP?
A. Never.  
B. In very simple scripts or prototypes where the cost of abstraction outweighs the benefit (YAGNI / KISS).  
C. Only on Tuesdays.  
D. If the boss says so.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Engineering is about trade-offs. For a distinct throw-away script, creating 5 classes might be over-engineering. But for production enterprise systems, SRP is crucial.
</details>

### Q15. "Separation of Concerns" (SoC) is:
A. Different from SRP.  
B. The broader architectural concept that SRP implements at the class level.  
C. A UI term.  
D. A database term.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
SoC is the general idea of dividing a computer program into distinct sections. SRP is a specific application of SoC to OOP class design.
</details>
