# 19_Setter_Injection – MCQs

## EASY MCQs

### Q1. What is another name for Setter Injection?
A. Constructor Injection  
B. Property Injection  
C. Interface Injection  
D. Method Injection  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It involves setting dependencies via public properties (Setters), hence Property Injection.
</details>

### Q2. Setter Injection is best used when the dependency is:
A. Mandatory.  
B. Optional.  
C. Static.  
D. Private.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Since the object can be created without calling the setter, this pattern implies the dependency is not strictly required for the object to exist (optional).
</details>

### Q3. Does Setter Injection require a parameterized constructor?
A. Yes.  
B. No, it typically works with the default (parameterless) constructor.  
C. Yes, but only for the interface.  
D. Only in abstract classes.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The object is instantiated normally `new Obj()`, and then `obj.Prop = dep` is called.
</details>

### Q4. Which C# feature is used to implement Setter Injection?
A. Fields.  
B. Properties (get/set).  
C. Events.  
D. Indexers.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Public properties with a `set` accessor allow the caller to inject the dependency.
</details>

### Q5. What is a risk of Setter Injection compared to Constructor Injection?
A. It is too slow.  
B. The object might be used before the dependency is set (NullReferenceException).  
C. It consumes more memory.  
D. It cannot be tested.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
There is a temporal gap between creation `new()` and injection `Prop = ...`. If a method is called in that gap, the dependency is null.
</details>

---

## MEDIUM MCQs

### Q6. In the provided example `TestSetterInjection`, what check is performed before using `Client`?
A. `if (Client != null)`  
B. `try-catch`  
C. `using statement`  
D. No check.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Because the dependency is optional/settable, defensive coding requires checking if it has been injected (is not null) before usage.
</details>

### Q7. Can you change the dependency during the lifetime of the object with Setter Injection?
A. No, it is readonly.  
B. Yes, because the property setter is public.  
C. Only using reflection.  
D. Only once.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Unlike `readonly` fields in Constructor Injection, properties are typically mutable, allowing the strategy/service to be swapped at runtime.
</details>

### Q8. Which scenario favors Setter Injection?
A. A critical database connection.  
B. A massive configuration object needed everywhere.  
C. An optional Logger service (if not present, just don't log).  
D. The class's own ID.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Logging is a classic example. If a logger is provided, use it. If not, the application logic usually proceeds fine without logging.
</details>

### Q9. Syntactically, how do you inject via Main?
A. `new Obj(dep)`  
B. `obj.Dep = dep`  
C. `obj.Inject(dep)`  
D. `Injector.Bind(obj, dep)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Standard property assignment syntax.
</details>

### Q10. Does modern .NET Core DI container support Property Injection by default?
A. Yes, automatically.  
B. No, it primarily supports Constructor Injection (Property injection requires extra configuration or 3rd party containers).  
C. Yes, for static properties.  
D. Only for controllers.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The default `IServiceProvider` in .NET Core focuses on Constructor Injection. Property injection is not done automatically to encourage better design (avoiding hidden dependencies), though 3rd party libraries (Autofac) do it.
</details>

---

## HARD MCQs

### Q11. Resolving Circular Dependencies:
A. Impossible with Setter Injection.  
B. Setter Injection can solve circular dependencies that block Constructor Injection.  
C. Causes compiler error.  
D. Requires Service Locator.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You can create Object A (empty), create Object B (empty), then set `A.B = B` and `B.A = A`. The cycle is closed after creation. Constructor injection deadlocks here.
</details>

### Q12. "Object Valid on Create" property:
A. Applies to Setter Injection.  
B. Does NOT apply to Setter Injection.  
C. Applies to both.  
D. Applies to neither.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
With setter injection, the object exists in a "partially initialized" state until the setters are called. This violates the principle that an object should always be in a valid state.
</details>

### Q13. Encapsulation concern:
A. Setter Injection exposes internal dependencies as public mutable properties, potentially breaking encapsulation.  
B. Setter Injection is more encapsulated than Constructor Injection.  
C. No difference.  
D. Setters are private.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Exposing `public IService Client { get; set; }` means *anyone* can change the service at any time, which might not be desired. Constructor injection keeps the field private/readonly.
</details>

### Q14. If you have a class with 10 optional dependencies (e.g., various formatters), which is better?
A. Constructor with 10 arguments.  
B. Setter Injection for the ones needed.  
C. Service Locator.  
D. Hard coding.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Ideally, break the class up. But if necessary, Setter Injection avoids a massive constructor ("Telescoping Constructor" problem) when most dependencies are defaults/optional.
</details>

### Q15. Is it possible to mix Constructor and Setter injection?
A. No.  
B. Yes, required in constructor, optional in setters.  
C. Yes, but it causes runtime errors.  
D. Only in separate files.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is a valid hybrid approach. Ensure the critical parts are present (Constructor), and allow tweaking of auxiliary parts (Setter).
</details>
