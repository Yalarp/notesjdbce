# 11_Events_Complete_Guide – MCQs

## EASY MCQs

### Q1. Events in C# are based on which concept?
A. Interfaces  
B. Delegates  
C. Abstract Classes  
D. Structs  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Events are a wrapper around delegates, providing a structured publisher-subscriber model with restricted access (only add/remove from outside).
</details>

### Q2. Which pattern do events implement?
A. Singleton Pattern  
B. Factory Pattern  
C. Publisher-Subscriber (Observer) Pattern  
D. Repository Pattern  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Events allow a class (Publisher) to notify other classes (Subscribers) when something interesting happens, which is the core of the Observer design pattern.
</details>

### Q3. Which keyword is used to declare an event?
A. `delegate`  
B. `event`  
C. `raise`  
D. `notify`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The syntax is `public event DelegateType EventName;`.
</details>

### Q4. Which operator is used to subscribe to an event?
A. `=`  
B. `+=`  
C. `->`  
D. `=>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You use `+=` to add a handler method to the event's invocation list. Using `=` is generally not allowed outside the declaring class to prevent overwriting other subscribers.
</details>

### Q5. Who can raise (invoke) an event?
A. Any class.  
B. Only the Subscriber.  
C. Only the Publisher (declaring class).  
D. The Main method only.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
This is the key security feature of events vs. raw delegates. Only the class that declares the event has the right to invoke it.
</details>

---

## MEDIUM MCQs

### Q6. What is the standard signature for an event handler in .NET?
A. `void Handler()`  
B. `int Handler(object sender)`  
C. `void Handler(object sender, EventArgs e)`  
D. `bool Handler(EventArgs e)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The standard convention conforms to the `EventHandler` delegate: it returns void and takes two parameters: the source of the event (`sender`) and data regarding the event (`e`).
</details>

### Q7. Why should you check for null before raising an event?
A. To check if the publisher exists.  
B. To check if there are any subscribers.  
C. It is required by the compiler.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If no one has subscribed to the event, the underlying delegate is `null`. Invoking a null delegate throws a `NullReferenceException`.
</details>

### Q8. What happens if you forget to unsubscribe from an event?
A. Nothing, the GC handles it.  
B. It causes a memory leak.  
C. The program crashes immediately.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The publisher holds a reference to the subscriber's handler method. This prevents the subscriber object from being garbage collected as long as the publisher is alive.
</details>

### Q9. Which method is the modern thread-safe way to raise an event?
A. `if (Event != null) Event(this, args);`  
B. `Event?.Invoke(this, args);`  
C. `Event.Raise(this, args);`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The null-conditional operator `?.` is thread-safe because it evaluates the left-hand operand (the event delegate) only once, preventing a race condition where another thread might unsubscribe just after a null check but before invocation.
</details>

### Q10. Can an event be virtual?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, events can be marked virtual in a base class and overridden in a derived class, allowing the derived class to change the implementation of the add/remove accessors.
</details>

---

## HARD MCQs

### Q11. Can you use the `=` operator on an event from outside the class?
A. Yes, to reset it.  
B. No, strictly prohibited.  
C. Yes, if it is null.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
External classes are restricted to `+=` and `-=` operations. The assignment operator `=` (which would wipe out all existing subscribers) is forbidden outside the declaring class.
</details>

### Q12. `event EventHandler MyEvent;` What is the type of `MyEvent`?
A. `EventHandler`  
B. `Method`  
C. `Action`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It is a multicast delegate of type `EventHandler`.
</details>

### Q13. Custom event arguments classes should inherit from:
A. `object`  
B. `System.Exception`  
C. `System.EventArgs`  
D. `System.Delegate`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
To follow .NET conventions, any class carrying event data should derive from `System.EventArgs`.
</details>

### Q14. What is the difference between `EventHandler` and `EventHandler<T>`?
A. `EventHandler` uses `EventArgs`; `EventHandler<T>` uses a custom type `T` derived from `EventArgs`.  
B. `EventHandler` is for static events only.  
C. They are the same.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`EventHandler` is the non-generic version. `EventHandler<TEventArgs>` allows you to specify a strongly-typed format for the event data, removing the need for casting in the handler.
</details>

### Q15. Is it possible to explicitly implement `add` and `remove` accessors for an event?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Yes, similar to property `get`/`set`. You can manually implement `add` and `remove` blocks to control how the underlying delegate storage is managed (e.g., using a collection or locking for thread safety).
</details>
