# 29_SOLID_Principles_Overview – MCQs

## EASY MCQs

### Q1. Who introduced the SOLID principles?
A. Bill Gates  
B. Robert C. Martin (Uncle Bob)  
C. Linus Torvalds  
D. James Gosling  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Robert C. Martin promoted these five principles as the pillars of agile software design.
</details>

### Q2. What does the "S" in SOLID stand for?
A. Simple Class Principle  
B. Single Responsibility Principle  
C. Static Variable Principle  
D. Source Code Principle  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A class should have one, and only one, reason to change.
</details>

### Q3. What does "O" (Open/Closed) mean?
A. Open for modification, closed for extension.  
B. Open source, closed source.  
C. Open for extension, closed for modification.  
D. Database connection is open.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
You should be able to extend the behavior of a system (add features) without changing the existing source code (modifying).
</details>

### Q4. Liskov Substitution Principle (LSP) deals mainly with:
A. Inheritance and Polymorphism.  
B. Database connection.  
C. File I/O.  
D. User Interface.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It ensures that objects of a derived class can replace objects of the base class without breaking the application correctness.
</details>

### Q5. Dependency Inversion Principle says we should depend on:
A. Concrete classes.  
B. Abstractions (Interfaces).  
C. Strings.  
D. Third-party libraries.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Both high-level interactions and low-level details should rely on abstractions to decouple the system.
</details>

---

## MEDIUM MCQs

### Q6. Which principle suggests that "Many specific interfaces are better than one general interface"?
A. SRP  
B. OCP  
C. ISP (Interface Segregation Principle)  
D. DIP  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
ISP states clients should not be forced to implement methods they do not use. Break fat interfaces into smaller ones.
</details>

### Q7. If you have a class `Report` that calculates data, formats it as HTML, saves it to PDF, and emails it... which principle is violated?
A. SRP  
B. LSP  
C. ISP  
D. DIP  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It has too many responsibilities (Calculation, Formatting, Persistence, Notification).
</details>

### Q8. A common way to achieve OCP (Open/Closed) is using:
A. Large switch/if statements.  
B. Inheritance and Polymorphism (Abstract classes/Interfaces).  
C. Comments.  
D. Global variables.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
By defining a contract `IShape`, you can add `Triangle` without changing the `AreaCalculator` class's logic.
</details>

### Q9. The "Circle-Ellipse" or "Square-Rectangle" problem is a classic violation of:
A. SRP  
B. LSP  
C. ISP  
D. DIP  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Assuming a Square "is-a" Rectangle often fails in behavior (setting width = height automatically), meaning the Square cannot validly substitute a Rectangle in all contexts.
</details>

### Q10. Tightly coupling a high-level `OrderService` to a low-level `SqlRepository` violates:
A. SRP  
B. ISP  
C. DIP  
D. OCP  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The high-level module depends on detail. Instead, `OrderService` should depend on `IRepository`, and `SqlRepository` should implement `IRepository`.
</details>

---

## HARD MCQs

### Q11. SOLID principles primarily aim to reduce:
A. Performance overhead.  
B. Compiler errors.  
C. Code Coupling and Fragility.  
D. Development time (initially).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
They make the system robust to change (less fragility) and easier to maintain/test (decoupled).
</details>

### Q12. "Programming to an Interface, not an Implementation" is most closely related to:
A. SRP and ISP.  
B. DIP and LSP.  
C. OCP.  
D. All of them.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is the core mechanism enabling DIP (abstraction) and LSP (substitutability).
</details>

### Q13. If you implement an interface but throw `NotImplementedException` in 3 out of 5 methods because your class doesn't need them, you are violating:
A. ISP.  
B. SRP.  
C. OCP.  
D. DIP.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The interface is too "fat". The client expects the methods to work. You should have split the interface so your class only implements what it supports.
</details>

### Q14. Can code be SOLID but still perform poorly?
A. Yes.  
B. No, SOLID ensures performance.  
C. SOLID code is always fast.  
D. Impossible.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
SOLID focuses on Architecture/Maintainability. It often introduces layers of abstraction (virtual calls, object allocation) which technically add minor overhead. You optimize *inside* the clean architecture.
</details>

### Q15. Is Dependency Injection the same as Dependency Inversion?
A. Yes.  
B. No. Dependency Inversion is the Principle (D of SOLID). Dependency Injection is a Pattern/Technique to apply that principle.  
C. DI is older.  
D. DIP is a tool.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
DIP says "Depend on abstractions". DI answers "How do I get those abstractions into my class at runtime?".
</details>
