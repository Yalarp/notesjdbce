# 11_Task_Parallel_Library – MCQs

## EASY MCQs

### Q1. What is the recommended way to start a new Task in typical scenarios?
A. `new Task(...).Start()`  
B. `Task.Factory.StartNew(...)`  
C. `Task.Run(...)`  
D. `Thread.Start(...)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Task.Run` is the standard, simplified API introduced in .NET 4.5 to offload work to the ThreadPool with safe default options.
</details>

### Q2. Which property of a `Task` indicates its current state (e.g., Running, Faulted)?
A. `State`  
B. `CurrentStatus`  
C. `TaskStatus`  
D. `Status`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
The `Status` property returns a `TaskStatus` enum value representing the lifecycle stage of the task.
</details>

### Q3. How do you block the calling thread until a Task completes?
A. `task.Await()`  
B. `task.Stop()`  
C. `task.Wait()`  
D. `task.Block()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Wait()` is a synchronous blocking call that pauses the current thread until the target task finishes.
</details>

### Q4. If a Task needs to return a value (e.g., an integer), which type should you use?
A. `Task`  
B. `Task[int]`  
C. `Task<int>`  
D. `ReturnTask<int>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The generic `Task<TResult>` class represents an asynchronous operation that produces a value of type TResult.
</details>

### Q5. What happens if you access `task.Result` before the task has completed?
A. It returns null immediately.  
B. It blocks the calling thread until the result is available.  
C. It throws an exception.  
D. It returns the default value of the type.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Accessing `.Result` on a `Task<T>` blocks the thread (similar to calling `.Wait()`) until the task finishes and the result is ready.
</details>

---

## MEDIUM MCQs

### Q6. `Task.Factory.StartNew` is generally reserved for:
A. Simple, short-running tasks.  
B. Advanced scenarios requiring specific `TaskCreationOptions` (e.g., LongRunning).  
C. UI updates.  
D. Database calls.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Task.Run` covers most cases. `StartNew` provides granular control (schedulers, creation options) but is more complex and has pitfalls (like not understanding async delegates natively).
</details>

### Q7. What is the default scheduler used by `Task.Run`?
A. The UI thread scheduler.  
B. The Dedicated Thread Scheduler.  
C. The ThreadPool Scheduler.  
D. The Foreground Scheduler.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Task.Run` queues work on the ThreadPool (`TaskScheduler.Default`), which optimizes thread reuse.
</details>

### Q8. If a Task throws an unhandled exception, what happens when you call `task.Wait()`?
A. Nothing, the exception is lost.  
B. The application crashes instantly.  
C. An `AggregateException` is thrown, wrapping the original exception.  
D. The exception is rethrown exactly as is.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Wait() and Result propagate exceptions wrapped in an `AggregateException` (because a task might have child tasks that also failed).
</details>

### Q9. Which method allows you to wait for an array of tasks to ALL complete?
A. `Task.WaitAny()`  
B. `Task.WaitAll()`  
C. `Task.SleepAll()`  
D. `Task.JoinAll()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Task.WaitAll(params Task[] tasks)` blocks until every task in the provided array has completed.
</details>

### Q10. Why is `Thread.Sleep` generally bad inside a `Task` running on the ThreadPool?
A. It throws an exception.  
B. It blocks a ThreadPool thread, preventing it from doing other work, reducing scalability.  
C. It cancels the task.  
D. It causes a memory leak.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Blocking a pool thread defeats the purpose of the ThreadPool. The thread sits idle instead of being returned to the pool to handle other requests.
</details>

---

## HARD MCQs

### Q11. Difference between `new Task(...)` and `Task.Run(...)`:
A. `new Task` starts immediately; `Task.Run` is cold.  
B. `new Task` creates a "Cold" task that must be manually started; `Task.Run` creates and starts a "Hot" task.  
C. `new Task` is for generic types only.  
D. `Task.Run` is deprecated.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`new Task(...)` is in the `Created` state (Cold) and requires `.Start()` to run. `Task.Run` creates it and schedules it immediately (Hot).
</details>

### Q12. What does `TaskCreationOptions.LongRunning` do?
A. It increases the priority of the thread.  
B. It keeps the task alive forever.  
C. It suggests to the scheduler to oversubscribe or create a dedicated thread, avoiding ThreadPool starvation.  
D. It forces the task to run on the UI thread.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
It tells the scheduler "this will take a while, don't block a quick-turnaround ThreadPool thread." Usually, this spins up a dedicated background thread.
</details>

### Q13. `Task.Yield()` is used to:
A. Stop the task.  
B. Force the method to complete synchronously.  
C. Asynchronously yield execution back to the current context/scheduler (forcing a continuation later).  
D. Return a result.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`await Task.Yield()` forces the method to yield and schedule the continuation, useful for keeping UI responsive or breaking up tight loops.
</details>

### Q14. What occurs if you use `Task.Run` inside an ASP.NET request?
A. It is always faster.  
B. It can reduce throughput ("sync over async" if you Wait()) or simply shift work to another threadpool thread, adding switching overhead without benefit (if blocking).  
C. It allows access to `HttpContext.Current`.  
D. It crashes the server.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
In a web server, threads are already from the pool. Offloading CPU work to *another* pool thread (`Task.Run`) just adds overhead. It's useful only for parallelism, not simple async offloading.
</details>

### Q15. A task in the `RanToCompletion` state:
A. Can still be cancelled.  
B. Has finished successfully without exception or cancellation.  
C. Is currently executing.  
D. Was waiting for children to finish.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is the final success state of a task.
</details>
