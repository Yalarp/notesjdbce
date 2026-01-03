# 10_Threading_Fundamentals – MCQs

## EASY MCQs

### Q1. Which namespace contains the basic `Thread` class in C#?
A. `System.Threading.Tasks`  
B. `System.Threading`  
C. `System.Diagnostics`  
D. `System.Process`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `Thread` class resides in the `System.Threading` namespace.
</details>

### Q2. What is the modern, recommended alternative to using the `Thread` class directly for most concurrent work?
A. `BackgroundWorker`  
B. `Task` (Task Parallel Library)  
C. `Timer`  
D. `Process`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The Task Parallel Library (TPL) and the `Task` class provide a higher-level abstraction, better resource management (Thread Pool), and easier composition (async/await) than raw threads.
</details>

### Q3. Which method blocks the calling thread until the target thread terminates?
A. `Thread.Stop()`  
B. `Thread.Sleep()`  
C. `Thread.Join()`  
D. `Thread.Wait()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Join()` causes the current thread to pause execution and wait for the thread on which `Join` was called to complete its execution.
</details>

### Q4. What does `Thread.Sleep(1000)` do?
A. Stops the thread forever.  
B. Pauses the current thread for 1000 milliseconds (1 second).  
C. Pauses the current thread for 1000 seconds.  
D. Pauses all threads in the application.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Thread.Sleep` suspends the current thread for the specified amount of time in milliseconds.
</details>

### Q5. A `Task` in C# generally runs on:
A. The UI thread.  
B. A newly created OS thread every time.  
C. A thread from the Thread Pool.  
D. The garbage collector thread.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Tasks are scheduled by the TaskScheduler, which by default uses the Thread Pool (`System.Threading.ThreadPool`) to reuse worker threads efficiently.
</details>

---

## MEDIUM MCQs

### Q6. Difference between `Thread` and `Task` regarding return values:
A. Both return values easily.  
B. `Thread` has no built-in return value mechanism; `Task<T>` is designed to return a result.  
C. `Thread` returns `int`; `Task` returns `void`.  
D. Neither can return values.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Thread` constructors typically take `ThreadStart` (void). To get a result, you need shared variables/state. `Task<ResultType>` has a `Result` property specifically for returning data.
</details>

### Q7. How do you handle exceptions in a raw `Thread`?
A. Using a try-catch block inside the thread's method.  
B. Using a global try-catch in Main.  
C. They are automatically swallowed.  
D. By checking `Thread.Error`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Exceptions thrown in a separate thread must be caught within that thread. If unhandled, they can crash the application. They do not automatically bubble up to the waiting thread (unlike `Task`).
</details>

### Q8. What is the benefit of the Thread Pool?
A. It ensures threads never stop.  
B. It reduces the overhead of creating and destroying threads by reusing them.  
C. It allows infinite threads.  
D. It guarantees FIFO execution.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Creating a thread is expensive (stack allocation, OS calls). The Thread Pool maintains a set of ready-to-use threads, improving performance for short-lived tasks.
</details>

### Q9. `Task.Run(() => DoWork())` is roughly equivalent to:
A. `new Thread(DoWork).Start()`  
B. `Task.Factory.StartNew(DoWork)` (configured for default scheduler)  
C. Calling `DoWork()` synchronously.  
D. Both A and B.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Task.Run` is a shortcut for `Task.Factory.StartNew` with safe default options (DenyChildAttach, etc.) intended to run work on the ThreadPool.
</details>

### Q10. What happens if you call `task.Wait()` and the task throws an exception?
A. Nothing happens.  
B. The exception is swallowed.  
C. An `AggregateException` is thrown on the calling thread.  
D. The application crashes immediately without catch blocks.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Task` captures exceptions thrown during execution. When you `Wait` or access `Result`, these exceptions are re-thrown wrapped in an `AggregateException`.
</details>

---

## HARD MCQs

### Q11. Foreground vs Background threads:
A. Background threads keep the app alive; foreground threads do not.  
B. Foreground threads keep the process alive; background threads effectively terminate when all foreground threads end.  
C. Tasks are always foreground threads.  
D. There is no difference.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The CLR keeps the process running as long as there is at least one foreground thread. If only background threads remain, the process terminates abruptly.
</details>

### Q12. Can a default `Task` be set to correspond to a Long Running operation?
A. No.  
B. Yes, using `TaskCreationOptions.LongRunning`.  
C. Yes, by using `Thread.Sleep`.  
D. Yes, by initializing it with `Thread`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `LongRunning` hint suggests to the scheduler that it might be better to create a dedicated thread rather than consuming a ThreadPool thread (which is optimized for short tasks).
</details>

### Q13. `CancellationToken` is primarily used with:
A. `Thread.Abort()`  
B. `Task` and async operations to support cooperative cancellation.  
C. `Process.Kill()`  
D. `Application.Exit()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `CancellationToken` source/token pattern is the standard, safe way to signal cancellation in TPL and async methods, as opposed to the dangerous `Thread.Abort`.
</details>

### Q14. What is the value of `IsBackground` for a thread created via `new Thread(...)` by default?
A. `true`  
B. `false` (it is a foreground thread)  
C. null  
D. It depends on the parent thread.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Manually created threads (`new Thread`) are Foreground threads by default. ThreadPool threads (used by Tasks) are Background threads.
</details>

### Q15. Why is `Thread.Abort()` discouraged or obsolete in modern .NET?
A. It is too slow.  
B. It can leave shared state in a corrupt manner because it raises an exception at an arbitrary point.  
C. It doesn't work on Windows.  
D. It requires admin privileges.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Thread.Abort` injects a `ThreadAbortException` into the target thread at an unpredictable location, potentially interrupting `finally` blocks or critical sections, leading to app instability.
</details>
