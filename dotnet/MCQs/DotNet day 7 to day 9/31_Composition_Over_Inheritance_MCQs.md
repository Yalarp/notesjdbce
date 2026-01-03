# 31_Composition_Over_Inheritance – MCQs

## EASY MCQs

### Q1. "Inheritance" represents which type of relationship?
A. HAS-A  
B. IS-A  
C. USES-A  
D. WAS-A  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Inheritance creates a strict hierarchical relationship where the child "is a" specialized version of the parent (e.g., Dog is an Animal).
</details>

### Q2. "Composition" represents which type of relationship?
A. HAS-A  
B. IS-A  
C. IS-LIKE-A  
D. EXTENDS  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Composition involves building complex objects from simpler ones, where the complex object "has" the simpler object as a part (e.g., Car has an Engine).
</details>

### Q3. Which allows more flexibility at runtime?
A. Inheritance  
B. Composition  
C. Both are equal.  
D. Static classes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
With composition, you can swap out behavior components (e.g., inject a different Logger) at runtime. Inheritance hierarchies are fixed at compile time.
</details>

### Q4. "Favor Composition over Inheritance" means:
A. Never use Inheritance.  
B. Use Inheritance for everything.  
C. Prefer building objects from small, focused components rather than creating deep class hierarchies.  
D. Use only Interfaces.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
It suggests that composition often leads to more maintainable and less coupled designs, avoiding the pitfalls of rigid hierarchies.
</details>

### Q5. In C#, how many classes can you inherit from?
A. One  
B. Multiple  
C. Infinite  
D. Zero  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
C# supports Single Inheritance ONLY. This is a major limitation that Composition helps overcome (you can have multiple composed fields).
</details>

---

## MEDIUM MCQs

### Q6. The "Penguin problem" (LSP violation) typically occurs when:
A. You use interfaces.  
B. You force a subclass (Penguin) to inherit behavior (Fly) that it physically cannot perform, just to fit into a hierarchy.  
C. You use composition.  
D. You use abstract classes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Inheritance forces the child to carry all the luggage of the parent. If the parent has `Fly()` but the child shouldn't, inheritance is the wrong tool.
</details>

### Q7. How does Composition support testing?
A. It makes classes larger.  
B. Dependencies (components) can be injected as interfaces, allowing Mocks/Stubs to be used during testing.  
C. It prevents testing.  
D. It requires a database.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
An object built via composition interacts with its parts via interfaces. You can easily pass a `FakeLogger` instead of `RealLogger` to test logic in isolation.
</details>

### Q8. Identify the Composition pattern:
A. `class Car : Vehicle { }`  
B. `class Car { private Engine _engine = new Engine(); }`  
C. `interface ICar { }`  
D. `abstract class Car { }`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `Car` class holds an instance of `Engine` as a field property. It "has an" engine.
</details>

### Q9. When is Inheritance actually the correct choice?
A. When you want code reuse only.  
B. When there is a genuine, structural "Is-A" relationship and polymorphism is required (e.g., `Button` is a `Control`).  
C. When you have two unrelated classes.  
D. When you are lazy.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Inheritance is powerful for true type hierarchies where the Child can be substituted for the Parent in all contexts (LSP).
</details>

### Q10. What is a "Fragile Base Class" problem?
A. Base classes break easily.  
B. Changes to a base class can unexpectedly break subclass behavior, causing ripple effects throughout the hierarchy.  
C. Base classes cannot have methods.  
D. Subclasses are fragile.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Because subclasses are tightly coupled to the implementation details of the base class, modifying the base (even internally) can cause regressions in children. Composition avoids this coupling.
</details>

---

## HARD MCQs

### Q11. "Delegation" is key to Composition. What does it mean?
A. The outer object passes the work to the inner component object to handle.  
B. Calling the base class method.  
C. Creating a delegate type.  
D. Lazy loading.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Instead of inheriting the logic, the `Car.Start()` method calls `_engine.Start()`. The `Car` delegates the responsibility of starting to the `Engine` component.
</details>

### Q12. Entity Component System (ECS) in game development is an extreme example of:
A. Deep Inheritance.  
B. Pure Composition.  
C. Static classes.  
D. Functional programming.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
In ECS, an entity (like "Player") is just an empty container ID. Behavior is added solely by attaching "Components" (Position, Health, Render, Physics). No inheritance is used.
</details>

### Q13. Mixins (in languages that support them) are an attempt to:
A. Stop inheritance.  
B. Get the benefits of Composition with the convenience of Inheritance (code reuse without strict hierarchy).  
C. Mix data types.  
D. Use static methods.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
C# can simulate Mixins via Default Interface Methods (C# 8+) or Extension Methods, allowing "horizontal" code reuse across unrelated classes.
</details>

### Q14. Inheritance breaks Encapsulation because:
A. It doesn't.  
B. Use of `protected` members exposes internal implementation details of the parent to the child (White-box reuse).  
C. Use of `private` members.  
D. It is public.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Composition is "Black-box reuse" (you only see the public interface of the component). Inheritance often relies on internal knowledge of how the Base works.
</details>

### Q15. Is "Code Reuse" a sufficient reason to use Inheritance?
A. Yes, that is its primary purpose.  
B. No. Code reuse can be achieved via Composition/Delegation without the baggage of a hierarchical relationship. Inheritance is for Polymorphism/Substitutability.  
C. Yes, always.  
D. No, copy-paste is better.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Misusing inheritance just to save typing a few lines of code ("I'll inherit UseDatabase helper even though this class isn't a Database") leads to poor design.
</details>
