# 14_Exception_Handling – MCQs

## EASY MCQs

### Q1. Which keyword initiates the execution of a block of code that handles errors?
A. `throw`  
B. `try`  
C. `catch`  
D. `finally`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `try` block contains the guarded code that might throw an exception.
</details>

### Q2. Which block always runs, regardless of whether an exception occured or not?
A. `try`  
B. `catch`  
C. `finally`  
D. `throw`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`finally` is designed for cleanup code (closing files, connections) and runs after the try/catch logic concludes, even if an unhandled exception crashes the app afterwards.
</details>

### Q3. All exceptions in C# inherit from:
A. `System.Error`  
B. `System.Exception`  
C. `System.Object` only  
D. `System.Trace`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Correct. `System.Exception` is the base class for all exceptions in .NET.
</details>

### Q4. Which keyword is used to manually raise an exception?
A. `raise`  
B. `throw`  
C. `catch`  
D. `try`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You use `throw new Exception(...)` to explicitly generate an exception.
</details>

### Q5. Can you have multiple `catch` blocks for a single `try` block?
A. Yes  
B. No  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, enabling you to handle specific exception types (like FileNotFound) differently from general ones (Exception).
</details>

---

## MEDIUM MCQs

### Q6. Referencing an object that is `null` throws:
A. `IndexOutOfRangeException`  
B. `ArgumentNullException`  
C. `NullReferenceException`  
D. `InvalidOperationException`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Attempting to access a member (method/property) on a null reference causes the runtime to throw `NullReferenceException`.
</details>

### Q7. What happens if you put `catch (Exception ex)` before `catch (DivideByZeroException ex)`?
A. It works fine.  
B. Compiler Error.  
C. The second catch is never reached.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The compiler detects that the second block is unreachable because the first block (`Exception`) covers *everything*. It issues an error forcing you to order them from specific to general.
</details>

### Q8. What does `throw;` (without an exception object) do inside a catch block?
A. Throws a new empty exception.  
B. Rethrows the currently caught exception preserving the stack trace.  
C. Rethrows the exception but resets the stack trace.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`throw;` effectively says "I'm done inspecting this exception, let it bubble up." It preserves the original stack trace info, which is vital for debugging.
</details>

### Q9. `ApplicationException` was originally intended for?
A. System errors.  
B. User-defined application errors.  
C. Windows Forms errors.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Historically, Microsoft recommended deriving custom exceptions from `ApplicationException`, but this advice was later retracted. Modern Best Practice is to derive from `Exception`.
</details>

### Q10. Can you include a `finally` block without a `catch` block?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`try { ... } finally { ... }` is a valid construct. It ensures cleanup happens, although any exception thrown will propagate up immediately unhandled.
</details>

---

## HARD MCQs

### Q11. Difference between `throw ex` and `throw`:
A. None.  
B. `throw ex` resets the stack trace to the current method; `throw` preserves original.  
C. `throw ex` is faster.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Using `throw ex` treats the current line as the source of the error, losing the information about where it actually originated deeper in the call stack. Always use `throw` unless you intentionally want to mask the original source.
</details>

### Q12. Catching non-CLS interpretations (e.g. C++ exceptions that aren't System.Exception) requires:
A. `catch (RuntimeWrappedException e)`  
B. `catch` block with no parameters.  
C. Impossible in C#.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A generic `catch { }` block can catch exceptions from languages like C++ that allow throwing non-objects (like `throw 5;`), which are wrapped by the CLR. Note: In modern .NET, these are usually wrapped in `RuntimeWrappedException` which inherits from `Exception`, so `catch(Exception)` often catches them too.
</details>

### Q13. Exception Filters (C# 6) allow:
A. `catch (Exception e) when (e.Message.Contains("404"))`  
B. `catch (Exception e) if (e.Message == "404")`  
C. Excluding exceptions from logs.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The `when` keyword allows filtering a catch block. If the condition is false, the catch block is skipped (and the stack is NOT unwound yet), which is better for debugging than catching and rethrowing.
</details>

### Q14. Is executing code in a `finally` block guaranteed?
A. absolute 100% guarantee.  
B. Guaranteed unless process is killed (e.g. StackOverflow, Environment.FailFast, power loss).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
While robust, `finally` cannot run if the CLR crashes hard (e.g., `StackOverflowException`, `ExecutionEngineException`) or if the process is terminated abruptly by the OS.
</details>

### Q15. Creating a custom exception:
A. Is not allowed.  
B. Should expose a public default constructor.  
C. Should implement `ISerializable` (recommendation).  
D. Both B and C.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
Standard pattern for custom exceptions includes 3 common constructors (default, message, message+inner) and, for full guideline compliance, serialization support (though less critical in .NET Core/modern app dev).
</details>
