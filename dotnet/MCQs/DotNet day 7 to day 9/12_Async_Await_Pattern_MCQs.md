# 12_Async_Await_Pattern – MCQs

## EASY MCQs

### Q1. Which keyword marks a method as asynchronous?
A. `await`  
B. `async`  
C. `task`  
D. `void`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `async` modifier is placed in the method signature to enable the use of the `await` keyword inside it.
</details>

### Q2. What keyword is used to pause the execution of the method until the awaited task completes?
A. `wait`  
B. `yield`  
C. `stop`  
D. `await`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
`await` suspends the evaluation of the enclosing async method until the asynchronous operation represented by its operand completes.
</details>

### Q3. Which is the valid return type for an async method that returns no value?
A. `void`  
B. `Task`  
C. `Task<void>`  
D. `AsyncResult`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Standard async methods should return `Task` instead of `void` to allow the caller to await completion and handle exceptions. `void` is reserved for event handlers.
</details>

### Q4. An async method returning an integer should have a return type of:
A. `int`  
B. `Task<int>`  
C. `Async<int>`  
D. `Future<int>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If the method logically returns an `int`, the async signature must typically be `Task<int>` (or `ValueTask<int>`).
</details>

### Q5. What is the asynchronous equivalent of `Thread.Sleep(1000)`?
A. `Task.Sleep(1000)`  
B. `await Thread.Sleep(1000)`  
C. `await Task.Delay(1000)`  
D. `Task.Wait(1000)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Task.Delay` creates a task that completes after a time delay, without blocking the underlying thread.
</details>

---

## MEDIUM MCQs

### Q6. Why is `async void` generally considered bad practice (except for event handlers)?
A. It runs synchronously.  
B. You cannot await it, and exceptions thrown inside it cannot be caught by the caller, potentially crashing the process.  
C. It is slower.  
D. It is not supported in .NET Core.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`async void` methods are "fire and forget". The caller has no task object to check status or catch exceptions. Unhandled exceptions crash the application context.
</details>

### Q7. When the `await` keyword is encountered, what generally happens to the current thread?
A. It is blocked waiting for the task.  
B. It is terminated.  
C. It is freed up to return to the caller or thread pool to do other work.  
D. It spins in a busy loop.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Use of `await` does NOT block the thread. It registers a continuation and returns execution control to the caller (or message loop), freeing the thread.
</details>

### Q8. Which method creates a task that completes when ALL provided tasks have completed?
A. `Task.WhenAny`  
B. `Task.WhenAll`  
C. `Task.WaitAll`  
D. `Task.JoinAll`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Task.WhenAll` creates a task that completes when all the tasks in the argument list have completed.
</details>

### Q9. What happens if you call `.Result` or `.Wait()` on a task inside an async method instead of `await`?
A. It works the same way.  
B. It blocks the thread, potentially creating a deadlock (especially in UI or ASP.NET classic contexts).  
C. It speeds up execution.  
D. It throws a compiler error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Blocking on async code ("Sync over Async") is dangerous. If the context is single-threaded (like UI), the continuation waits for the thread that is blocked waiting for the task: Deadlock.
</details>

### Q10. What does `ConfigureAwait(false)` do?
A. Cancels the task.  
B. Configures the await to run synchronously.  
C. Tells the awaiter NOT to capture the current SynchronizationContext, possibly resuming on a different thread.  
D. Forces the continuation to run on the UI thread.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
This is a performance optimization and deadlock prevention technique for library code, preventing the overhead of marshalling back to the original context (like UI context).
</details>

---

## HARD MCQs

### Q11. If an exception occurs in an `async Task` method:
A. The app crashes immediately.  
B. The exception is placed on the returned Task object and re-thrown when the task is awaited.  
C. It is ignored.  
D. It is handled by `AppDomain.UnhandledException`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The task transitions to a Faulted state. Awaiting that task triggers the exception re-throw on the calling side.
</details>

### Q12. Can you have `out` or `ref` parameters in an `async` method?
A. Yes, both are allowed.  
B. Only `ref`.  
C. No, neither is allowed.  
D. Only `out`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Due to the nature of the state machine generated by the compiler, `async` methods cannot support `ref` or `out` parameters.
</details>

### Q13. `Task.WhenAny` is useful for:
A. Running tasks sequentially.  
B. Waiting for the fastest task to complete (e.g., trying multiple servers).  
C. Cancelling all tasks.  
D. Waiting for all tasks.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`WhenAny` returns a task that completes as soon as the *first* of the supplied tasks completes.
</details>

### Q14. What does the compiler generate behind the scenes for an `async` method?
A. A recursive function.  
B. A state machine struct/class that implements the `IAsyncStateMachine` interface.  
C. A new thread.  
D. A simple callback.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The compiler rewrites the method into a state machine that tracks execution progress, local variables, and continuation points across `await` boundaries.
</details>

### Q15. Is `return await Task.Run(...)` functionally different from `return Task.Run(...)` at the end of a method?
A. No difference at all.  
B. `return await` overhead involves un-wrapping and re-wrapping the result, but preserves the stack trace of the current method better in exceptions. Direct return is slightly faster but removes the current frame from the stack trace.  
C. Direct return is illegal.  
D. `return await` runs synchronously.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Directly returning the task (`return Task.Run(...)`) avoids the state machine overhead for that method, but if the task fails, the exception stack trace won't show the current method. `await` ensures the method stays in the logical stack.
</details>
