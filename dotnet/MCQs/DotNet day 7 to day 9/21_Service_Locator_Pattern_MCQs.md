# 21_Service_Locator_Pattern – MCQs

## EASY MCQs

### Q1. What is a Service Locator?
A. A design pattern that provides a central registry for registering and resolving services.  
B. A tool to locate lost files.  
C. A GPS service for applications.  
D. A database connection manager.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The Service Locator pattern acts as a central point where services are stored and requested by clients, rather than clients creating them directly.
</details>

### Q2. How is Service Locator typically implemented?
A. Using a static global class or singleton.  
B. Using a database table.  
C. Using a text file.  
D. Using inheritance.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It is usually a static class with methods like `Register<T>(service)` and `Resolve<T>()` accessible from anywhere in the code.
</details>

### Q3. Why is Service Locator often considered an Anti-Pattern in modern Dependency Injection?
A. It is too slow.  
B. It hides dependencies (You can't see what a class needs by looking closer at its API/constructor).  
C. It is deprecated by Microsoft.  
D. It only works with web apps.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Because the dependency is requested internally (`Locator.Get<IService>()`), the external interface (constructor) looks empty, making the class's requirements opaque and "lying" about what it needs.
</details>

### Q4. Which method is clearer to a developer using your class?
A. `public MyClass()` (internally calls ServiceLocator)  
B. `public MyClass(IService service)` (Constructor Injection)  
C. Both are same.  
D. `public MyClass(int id)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Constructor Injection explicitly advertises the dependencies. Use it! Service Locator hides them which can lead to runtime errors if the service isn't registered.
</details>

### Q5. A major downside of Service Locator regarding Unit Testing is:
A. It makes tests faster.  
B. You must set up (and tear down) the global locator state for every test context, which causes test coupling/pollution.  
C. It requires a real database.  
D. It doesn't support mocking.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Since Service Locator relies on global static state, tests running in parallel might interfere with each other unless carefully managed (Shared State problem).
</details>

---

## MEDIUM MCQs

### Q6. In the provided example, `ServiceLocator.SetService(new ClaimService())` is akin to:
A. Resolving a dependency.  
B. Registering a dependency.  
C. Deleting a dependency.  
D. Ignoring a dependency.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Registration is the act of storing a service instance in the locator so it can be retrieved later.
</details>

### Q7. If `ServiceLocator.GetService()` is called without a prior `SetService()`, what typically happens?
A. It automatically creates a default service.  
B. It returns null or throws an exception (runtime error).  
C. It waits until one is available.  
D. It compiles error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is the "Runtime Error" risk. Unlike Constructor Injection which fails at compile time (or object creation time) if arguments are missing, Service Locator fails deep inside the method logic.
</details>

### Q8. When might Service Locator still be acceptable?
A. In the root of the application (Composition Root) for legacy frameworks that don't support DI.  
B. Everywhere.  
C. Never, delete it immediately.  
D. In high-performance loops.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Sometimes frameworks (like old WinForms or WPF converters) don't allow constructor injection easily. A Service Locator might be a necessary evil acting as a bridge in those specific edge cases.
</details>

### Q9. Service Locator violates which SOLID principle most directly?
A. Single Responsibility Principle.  
B. Dependency Inversion Principle (specifically the Interface Segregation part regarding explicit dependencies).  
C. Interface Segregation Principle.  
D. Liskov Substitution Principle.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
While it technically inverts control, it violates the spirit of explicit dependencies (DIP often used with DI to make dependencies explicit). Most argue it forces a dependency on the Locator itself (Service Locator is a dependency).
</details>

### Q10. The `Microsoft.Extensions.DependencyInjection` `IServiceProvider` is essentially:
A. Defined as a Service Locator interface.  
B. A Factory.  
C. A Proxy.  
D. A Decorator.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`IServiceProvider` has one method `GetService(Type t)`. Used improperly (passed around to classes), it acts exactly like a Service Locator. It should only be used by the framework infrastructure.
</details>

---

## HARD MCQs

### Q11. Compare "Constructor Injection" vs "Service Locator" regarding refactoring.
A. Service Locator is easier to refactor because you don't change signatures.  
B. Constructor Injection is easier to refactor because the compiler guides you to all usage sites when a dependency changes.  
C. They are identical.  
D. Service Locator prevents refactoring.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Although changing a constructor signature breaks code, it's a "good break" because the compiler shows you exactly what needs fixing. Service Locator changes might be silent until runtime.
</details>

### Q12. "Ambient Context" is a pattern similar to Service Locator. What is it?
A. `HttpContext.Current` or `Thread.CurrentPrincipal`.  
B. A local variable.  
C. A database context.  
D. A file context.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Ambient Contexts are static accessors to thread-local or global state, acting very much like specialized Service Locators.
</details>

### Q13. Why does Service Locator make code "brittle"?
A. Because it uses glass.  
B. Because classes have hidden assumptions about the environment (the global state must be set up just right).  
C. Because it uses strong types.  
D. Because it is interpreted.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A class should be self-contained. Depending on a global setup creates fragile coupling to that global state.
</details>

### Q14. In the example, `ServiceLocator` uses a static field `_clientLocator`. Thread safety issue?
A. Yes, if multiple threads try to Set/Get simultaneously without locking.  
B. No, statics are always thread-safe.  
C. No, because it is private.  
D. Yes, but only in Debug mode.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Static state is shared across all threads. Without `lock` or other synchronization, race conditions can occur if the service is swapped during execution.
</details>

### Q15. Is `DependencyResolver` in older MVC 5 a Service Locator?
A. Yes.  
B. No.  
C. It is a DI Container.  
D. It is a Constructor.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`DependencyResolver.Current.GetService<T>()` is the classic definition of the Service Locator pattern integrated into ASP.NET MVC 5.
</details>
