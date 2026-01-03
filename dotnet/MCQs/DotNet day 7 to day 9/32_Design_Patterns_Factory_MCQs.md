# 32_Design_Patterns_Factory – MCQs

## EASY MCQs

### Q1. What is the main purpose of the Factory Pattern?
A. To destroy objects.  
B. To encapsulate object creation logic.  
C. To create database tables.  
D. To implement singletons.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It moves the instantiation logic (`new ConcreteClass()`) into a dedicated class/method so the client doesn't need to know the specific class details.
</details>

### Q2. The Singleton pattern ensures:
A. A class has infinite instances.  
B. A class has exactly one instance and provides a global point of access to it.  
C. A class cannot be instantiated.  
D. A class is static.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Useful for shared resources like Configuration, Logging services, or Connection Pools.
</details>

### Q3. Why is the constructor of a Singleton class private?
A. To prevent other classes from creating instances with `new`.  
B. Because it has no code.  
C. To save memory.  
D. It is mandatory in C#.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
If the constructor were public, anyone could create multiple instances, violating the pattern.
</details>

### Q4. In the Factory example, the return type of `CreateLogger` is:
A. `FileLogger`  
B. `ConsoleLogger`  
C. `ILogger` (Interface)  
D. `Object`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Factories return Abstractions (Interfaces or Abstract Classes), allowing the client to be decoupled from the concrete implementation.
</details>

### Q5. A static class differs from a Singleton because:
A. It isn't different.  
B. A Singleton is an object (can pass as parameter, implement interface), whereas a static class is just a container for methods.  
C. Static classes are faster.  
D. Singletons are slower.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Singleton provides object-oriented features (inheritance, interface implementation) and controlled instantiation (lazy loading), which static classes do not fully support.
</details>

---

## MEDIUM MCQs

### Q6. Which implementation of Singleton is most recommended for modern C# for thread safety and simplicity?
A. Double-Check Locking.  
B. `Lazy<T>`.  
C. Static Constructor.  
D. Eager Initialization.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Lazy<T>` handles thread safety guarantees internally and is very clean to write.
</details>

### Q7. The "Open/Closed Principle" is supported by Factory Pattern because:
A. It isn't.  
B. You can add new product types (e.g., `CloudLogger`) by extending the factory logic, without changing the client code that uses `ILogger`.  
C. It uses text files.  
D. It opens the database.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The client depends on `ILogger`. Adding a new logger only requires changes in the Factory, protecting the rest of the application.
</details>

### Q8. What is "Double-Check Locking"?
A. Locking the door twice.  
B. A pattern to ensure thread safety in Singleton by checking `if null` before AND after acquiring the lock.  
C. Using two locks.  
D. Checking for errors twice.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It optimizes performance. The expensive `lock` is only taken the very first time the instance needs creating. Subsequent calls satisfy the first `null` check and return immediately.
</details>

### Q9. "Simple Factory" vs "Factory Method" vs "Abstract Factory". The example shown (switching on a string) is mostly:
A. Simple Factory.  
B. Factory Method.  
C. Abstract Factory.  
D. Builder.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
A static method that takes a parameter and decides which class to instantiate is typically called a Simple Factory. Factory Method uses inheritance (`Create` is abstract).
</details>

### Q10. Why is Singleton often called an "Anti-Pattern"?
A. It introduces global state, which hides dependencies and makes unit testing (mocking) difficult.  
B. It is too easy to implement.  
C. It is slow.  
D. It consumes too much memory.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Modern design prefers Dependency Injection (where the Container manages the "Singleton" lifetime) rather than hardcoding `MyClass.Instance`.
</details>

---

## HARD MCQs

### Q11. Can `Lazy<T>` create value types?
A. No.  
B. Yes.  
C. Only integers.  
D. Only structs.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Yes, `Lazy<T>` works with any type T, delaying its initialization until `.Value` is accessed.
</details>

### Q12. If a Singleton implements `IDisposable`, when is `Dispose()` called?
A. Automatically when app closes.  
B. It's tricky. Since the instance is held statically for the app lifetime, it acts like a root. Usually, explicit disposal logic or app shutdown hooks are needed.  
C. Garbage Collector handles it immediately.  
D. Never.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Static members are GC roots. They don't get collected until the AppDomain unloads. Managing disposable resources in a Singleton requires care.
</details>

### Q13. Example of Factory Pattern in .NET Framework?
A. `Convert.ToInt32()`  
B. `WebDriver.ChromeDriver()`  
C. `WebRequest.Create("http://...")`  
D. `Console.WriteLine()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`WebRequest.Create` looks at the URI scheme (http, ftp, file) and returns the appropriate subclass (`HttpWebRequest`, `FtpWebRequest`, etc.). This is a classic Factory.
</details>

### Q14. What if the Singleton constructor throws an exception?
A. It is retried.  
B. The access throws `TypeInitializationException` and the class typically becomes unusable for the life of the AppDomain.  
C. It returns null.  
D. Nothing happens.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Static initialization failure is cached. Subsequent attempts to access the Singleton will re-throw the same exception wrapper.
</details>

### Q15. "Dependency Injection (DI) Container" vs "Factory Pattern".
A. A DI Container is essentially a smart, configurable, generic Factory for the entire application.  
B. They are unrelated.  
C. Factory is better.  
D. DI is simpler.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Instead of writing hundreds of manual Factory classes, a DI container (AutoFac, Core DI) instantiates objects and resolves graphs automatically based on registration.
</details>
