# 20_Interface_Injection – MCQs

## EASY MCQs

### Q1. In Interface Injection, the method used to inject the dependency is defined in:
A. The consumer class directly.  
B. A specific Interface that the consumer implements.  
C. The specific Service class.  
D. The Main method.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
An interface (e.g., `ISetService`) defines a method signature like `SetService(IService s)`, and the consumer implements this interface.
</details>

### Q2. Is Interface Injection common in modern .NET development?
A. Yes, it is the standard.  
B. No, Constructor Injection is far more common.  
C. It is the only way.  
D. It replaced Constructor Injection.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Interface injection is relatively rare in modern .NET DI applications compared to Constructor or Property injection.
</details>

### Q3. To receive a dependency via Interface Injection, the consumer class must:
A. Inherit from a base class.  
B. Implement an injection-specific interface.  
C. Have a public property.  
D. Have a static constructor.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The class must implement the `IInjector` style interface to signal that it accepts a dependency via a specific method.
</details>

### Q4. The injection method typically looks like:
A. `void Inject(IDependency d)`  
B. `IDependency Get()`  
C. `void SetDependency()`  
D. `IDependency Prop { get; set; }`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It is a void method accepting the dependency as a parameter, used to set the internal field.
</details>

### Q5. Who calls the injection method (e.g., `SetService`)?
A. The object itself in the constructor.  
B. The injector (container) or the main caller.  
C. The dependency.  
D. The garbage collector.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The external code that creates the object sees that it implements the Interface (e.g., `ISetService`) and calls the injection method to provide the dependency.
</details>

---

## MEDIUM MCQs

### Q6. Difference between Interface Injection and Setter Injection:
A. Setter uses properties; Interface uses a method defined by an interface contract.  
B. No difference.  
C. Interface Injection is faster.  
D. Setter injection is safer.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Setter injection relies on public properties (convention). Interface injection relies on an explicit interface contract (enforcement).
</details>

### Q7. One benefit of Interface Injection is:
A. It is less verbose.  
B. It makes the dependency requirement explicit via the interface type system (if you see `ILoggerAware`, you know it needs a logger).  
C. It works with private methods.  
D. It avoids interfaces.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It explicitly categorizes classes. A container can scan for all classes implementing `IAuthAware` and inject the Auth service into them.
</details>

### Q8. The provided example uses `ISetService`. What is its purpose?
A. To define the business logic.  
B. To define the `SetServiceAndRun` method signature for injection.  
C. To replace `IService`.  
D. To implement the service.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It serves as the contract for injection, ensuring the consumer has a method to accept the `IService`.
</details>

### Q9. Steps for Interface Injection:
1. Define Service Interface (`IService`)
2. Define Injection Interface (`ISetService`)
3. Consumer implements `ISetService`
4. ???
5. Caller invokes method defined in `ISetService`.

What is step 4?
A. Consumer implements the method to assign the passed dependency to a field.  
B. Consumer creates the service internally.  
C. Consumer ignores the parameter.  
D. Consumer declares a property.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The implementation class must wire the passed parameter to its local field.
</details>

### Q10. Compared to Constructor Injection, Interface Injection is considered:
A. "Invasive" (requires implementing extra interfaces).  
B. "Clean".  
C. "Invisible".  
D. "Deprecated".  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It pollutes the class hierarchy. Your business classes now implement framework-specific interfaces (`IInjectable...`) just to get their dependencies.
</details>

---

## HARD MCQs

### Q11. Which DI container feature relies on Interface Injection logic?
A. Auto-wiring constructors.  
B. "Aware" interfaces (e.g., `ServletContextAware` in Java Spring, or similar patterns in older .NET frameworks).  
C. Factory method.  
D. Singleton scope.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
"Aware" interfaces are the classic example. If a bean implements `IFooAware`, the container calls `setFoo(foo)` automatically.
</details>

### Q12. Can you enforce mandatory dependencies with Interface Injection?
A. Yes, perfectly.  
B. No, like Setter injection, the object is created first, then the method is called. There is a temporal gap.  
C. Yes, the compiler prevents creation.  
D. Yes, if the interface has a constructor.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Construction happens before injection. The object exists in an uninitialized state until the injector calls the method.
</details>

### Q13. If `BusinessLogicImplementation` did NOT implement `ISetService`, could we use Interface Injection?
A. No.  
B. Yes, via Reflection.  
C. Yes, via dynamic keyword.  
D. Yes, via casting.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The definition of Interface Injection is literally that the injection mechanism is driven by the interface type. Without it, it's just Method Injection or Setter Injection.
</details>

### Q14. Is Method Injection considered the same as Interface Injection?
A. Yes.  
B. No. Interface injection is a subset where the method is part of an interface contract. Method injection can be any arbitrary public method.  
C. No, Method injection is static.  
D. No, Interface injection is static.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Method injection is passing a dependency to a method that needs it (e.g. `Render(DrawService s)`). Interface injection is specifically about setting the object's state via an interface method.
</details>

### Q15. Why might a framework prefer Interface Injection over Reflection-based Setter Injection?
A. Performance. Calling an interface method is faster than reflecting over properties.  
B. Reflection is faster.  
C. Interface injection is slower.  
D. Properties are private.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Direct method calls (even via interface dispatch) are generally faster than reflection, though modern optimizations minimize this gap. It provides compile-time safety.
</details>
