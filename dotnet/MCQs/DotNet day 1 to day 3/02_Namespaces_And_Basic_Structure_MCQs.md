# 02_Namespaces_And_Basic_Structure – MCQs

## EASY MCQs

### Q1. What is the primary purpose of a Namespace in C#?

A. To increase the execution speed of the program.  
B. To manage memory allocation on the Heap.  
C. To organize code and avoid naming collisions.  
D. To define the entry point of the application.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Namespaces are logical groupings used to organize related types and prevent naming conflicts, similar to folders in a file system.
</details>

### Q2. What is the default access modifier for a top-level class declared directly in a namespace?

A. public  
B. private  
C. protected  
D. internal  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** D

**Explanation:**  
The default access modifier for a top-level class (one declared directly in a namespace) is `internal`, meaning it is accessible only within the same assembly.
</details>

### Q3. What must be the name of the entry point method in a C# program?

A. main  
B. Main  
C. start  
D. Program  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The entry point method in C# must be named `Main` (with a capital 'M'). `main` (lowercase) is not a valid entry point by default.
</details>

### Q4. Which directive is used to include a namespace in a C# program so that its types can be used without fully qualified names?

A. import  
B. include  
C. using  
D. package  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The `using` directive allows you to use types from a namespace without specifying the full namespace path every time.
</details>

---

## MEDIUM MCQs

### Q5. Which of the following is a valid signature for the Main method?

A. `public void Main()`  
B. `static int Main()`  
C. `public static string Main(String[] args)`  
D. `void Main(String[] args)`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`static int Main()` is a valid signature. The Main method must be `static` and can return `void` or `int`. Non-static versions or those returning `string` are invalid.
</details>

### Q6. What happens if you try to apply the `public` access modifier to a namespace declaration?

A. The namespace becomes accessible globally.  
B. It causes a compile-time error.  
C. It has no effect as namespaces are public by default.  
D. It allows the namespace to be inherited.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Namespaces cannot have access modifiers. They are purely organizational constructs and do not have visibility in the traditional sense.
</details>

### Q7. What feature does the `using static` directive (introduced in C# 6.0) provide?

A. It imports all classes from a namespace as static classes.  
B. It allows importing static members of a class so they can be used without the class name.  
C. It makes the entire class static.  
D. It prevents the class from being instantiated.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`using static` allows you to import static members (like methods and properties) of a class directly. For example, `using static System.Console;` allows writing `WriteLine()` instead of `Console.WriteLine()`.
</details>

### Q8. What is the default access modifier for members (fields, methods) of a class?

A. public  
B. internal  
C. private  
D. protected  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The default access modifier for class members (fields, methods) is `private`, meaning they are accessible only within the class itself.
</details>

---

## HARD MCQs

### Q9. Consider the following code snippet regarding access modifiers:
```csharp
namespace MyApp {
    class MyClass { }
    internal class MyOtherClass { }
}
```
Which statement is TRUE?

A. `MyClass` is private and `MyOtherClass` is internal.  
B. Both `MyClass` and `MyOtherClass` are internal.  
C. `MyClass` is public and `MyOtherClass` is internal.  
D. `MyClass` is protected.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
For top-level classes, the default access modifier is `internal`. Therefore, `MyClass` is implicitly internal, making it equivalent to `MyOtherClass` which is explicitly internal.
</details>

### Q10. What is the correct way to declare a nested namespace?

A. `namespace A { namespace B { } }`  
B. `namespace A.B { }`  
C. Both A and B are correct.  
D. Namespaces cannot be nested.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Both syntaxes are valid. You can nest namespaces by placing one inside another block (`namespace A { namespace B {} }`) or by using the dot notation (`namespace A.B {}`).
</details>

### Q11. Which of the following Main method signatures allows returning a status code to the operating system?

A. `static void Main()`  
B. `static int Main()`  
C. `static bool Main()`  
D. `static object Main()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The Main method can return `int`, which is used as an exit status code for the operating system (typically `0` for success). Returning `void` does not return a value to the OS.
</details>

### Q12. In the execution flow, what role does the `Program.exe` file play immediately after complication?

A. It contains native code ready to run on the CPU.  
B. It acts as a script file for the C# interpreter.  
C. It contains MSIL and a Manifest, waiting for the CLR to load it.  
D. It is executed directly by the Windows Kernel without CLR.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The `.exe` produced by the C# compiler contains MSIL (Microsoft Intermediate Language) and Metadata (Manifest). It cannot run directly on the CPU; the CLR must load it and JIT compile it first.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
