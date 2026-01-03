# 11_Async_Await_WebAPI – MCQs

## EASY MCQs

### Q1. What is the primary benefit of using `async`/`await` in ASP.NET Core Web API?
A. It makes the database faster.
B. It improves Scalability by freeing up thread pool threads while waiting for I/O operations (like DB queries) to complete.
C. It encrypts the request.
D. It guarantees 100% uptime.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Async doesn't make a single request faster (it adds slight overhead), but it allows the server to handle many more concurrent requests.
</details>

### Q2. Which return type should be used for an asynchronous controller action?
A. `Task<IActionResult>`
B. `void`
C. `IActionResult`
D. `String`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`Task<T>` represents the ongoing operation that the framework yields back to the thread pool.
</details>

### Q3. What keyword pauses the execution of method until the awaited task completes?
A. `stop`
B. `await`
C. `yield`
D. `wait`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
It yields the thread but logically blocks the method's progression until the Task finishes.
</details>

### Q4. Which EF Core method corresponds to the async version of `ToList()`?
A. `ToListImmediately()`
B. `ToListAsync()`
C. `GetAll()`
D. `FetchAsync()`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Standard naming convention for async methods in .NET.
</details>

### Q5. Why should you avoid `async void` in Web APIs?
A. It crashes the process if an exception occurs because the exception cannot be caught by the caller.
B. It is too fast.
C. It is deprecated.
D. It works fine.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
`async void` is "fire-and-forget" intended only for UI Event Handlers (Click events). In APIs, it breaks the error handling pipeline.
</details>

---

## MEDIUM MCQs

### Q6. What happens if you use `.Result` or `.Wait()` on a Task inside a Controller?
A. It works perfectly.
B. It blocks the thread (Sync-over-Async), negating scalability benefits and potentially causing Deadlocks.
C. It makes it async.
D. It cancels the task.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Blocking a thread pool thread defeats the purpose of async.
</details>

### Q7. Does `await` create a new thread?
A. Yes, always.
B. No. It registers a callback and releases the current thread to the pool. When the I/O completes, a thread (conceptually) picks up where it left off.
C. Only on Tuesdays.
D. Only for SQL.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
There is no thread dedication during the "await" period.
</details>

### Q8. What does `Task.WhenAll` do?
A. Waits for all tasks in a collection to complete (running them concurrently).
B. Runs tasks sequentially.
C. Cancels all tasks.
D. Deletes tasks.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Useful for running multiple independent DB queries in parallel.
</details>

### Q9. If an interface defines `Task<int> GetData()`, can the implementation just return `Task.FromResult(0)`?
A. No.
B. Yes, this is useful for synchronous implementations (like hardcoded mock data) satisfying an async interface.
C. Only if void.
D. It throws error.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Allows synchronous code to communicate with async interfaces efficiently.
</details>

### Q10. What is "Thread Pool Starvation"?
A. When the CPU has no electricity.
B. When all available threads are blocked waiting for I/O, preventing the server from accepting new requests. `async/await` helps prevent this.
C. When threads are hungry.
D. When memory is low.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Sync I/O holds threads hostage. Async releases them.
</details>

---

## HARD MCQs

### Q11. Is it true that "Async methods make database queries run faster"?
A. Yes, significantly.
B. No. The database query takes the same amount of time. Async actually adds a tiny overhead for state machine management. The benefit is throughput (handling more users), not individual request latency.
C. Yes, because it uses magic.
D. Only for Oracle.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Crucial distinction: Latency vs Scalability.
</details>

### Q12. `ValueTask<T>` is sometimes used instead of `Task<T>`. Why?
A. It is cooler.
B. It is a value type (struct), reducing memory allocation overhead when the result is often available synchronously (e.g., cached in memory).
C. It supports nulls.
D. It is for older .NET versions.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Optimization primitive.
</details>

### Q13. If you call an async method without `await` (e.g., `_repo.AddAsync(item);`), what happens?
A. The compiler forces you to await.
B. The method starts executing ("fire and forget"), but the Request might finish and dispose the DbContext *before* the operation completes, causing an exception.
C. It runs synchronously.
D. It pauses.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Race condition. The context lives only as long as the request.
</details>

### Q14. What does `ConfigureAwait(false)` do?
A. Configures the UI.
B. Tells the runtime it does not need to return to the original SynchronizationContext (common in UI apps, less needed in Core APIs but good for libraries).
C. Makes it faster.
D. Disables async.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Prevents deadlocks in legacy ASP.NET or UI apps. In ASP.NET Core, it's largely redundant because there is no SynchronizationContext, but harmless.
</details>

### Q15. "Async all the way down". What does this mean?
A. Writing async code at the bottom of the file.
B. If you use async at the repository level, you must use it at Service, Controller, and every layer up the stack. Mixing sync/async calls leads to deadlocks.
C. It is a song.
D. Using async only in database.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
You cannot cleanly wrap async code in a sync shell without risking blocking issues.
</details>
