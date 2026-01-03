# 13_Memory_Management_GC – MCQs

## EASY MCQs

### Q1. Managed memory in .NET is handled by:
A. The Programmer  
B. The Operating System  
C. The Garbage Collector (GC)  
D. The CPU  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The CLR's Garbage Collector automatically allocates and releases memory for managed objects, preventing common errors like memory leaks and dangling pointers.
</details>

### Q2. Local value type variables are stored on the:
A. Heap  
B. Stack  
C. Hard Drive  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Local variables (scalars, structs) exist within the scope of the method execution and are typically stored on the thread stack (for fast allocation/deallocation).
</details>

### Q3. Reference type objects (class instances) are stored on the:
A. Stack  
B. Heap  
C. Registry  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The object data itself lives on the Managed Heap. The *reference* (pointer) to that object is what lives on the Stack (if it's a local variable).
</details>

### Q4. Which generation contains short-lived objects?
A. Generation 0  
B. Generation 1  
C. Generation 2  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Gen 0 is for newly created objects. Usually, they are short-lived. The GC collects Gen 0 most frequently.
</details>

### Q5. What method is used to manually release unmanaged resources?
A. `Deconstruct`  
B. `Finalize`  
C. `Dispose`  
D. `Clear`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The `Dispose()` method (from `IDisposable` interface) is the standard, deterministic way for a developer to explicitly release resources immediately when finished.
</details>

---

## MEDIUM MCQs

### Q6. Which method is automatically called by the GC before reclaiming an object's memory?
A. `Dispose`  
B. `Close`  
C. `Finalize` (Destructor)  
D. `Delete`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The Finalize method (defined via `~ClassName()`) is called by the GC as a last resort to clean up unmanaged resources if the developer forgot to call Dispose.
</details>

### Q7. The `using` statement in C# is syntax sugar for:
A. A while loop  
B. A try-catch block  
C. A try-finally block calling Dispose  
D. A destructor call  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`using (var x = new X()) { ... }` ensures that `x.Dispose()` is called inside a `finally` block, guaranteeing cleanup even if exceptions occur.
</details>

### Q8. Objects that survive a Generation 0 collection move to:
A. Generation 0  
B. Generation 1  
C. Generation 2  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The GC promotes survivors to the next generation. Gen 0 survivors -> Gen 1. Gen 1 survivors -> Gen 2.
</details>

### Q9. When should you call `GC.Collect()` manually?
A. Always, to keep memory low.  
B. In loops.  
C. Almost never, unless you have specific knowledge of large memory release.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
The GC is self-tuning. Forcing collections is usually detrimental to performance (pausing the app). It is reserved for rare cases like finishing a huge batch process where you know significant memory just became garbage.
</details>

### Q10. What happens if you define a destructor in C#?
A. The object is collected faster.  
B. The object requires at least two GC cycles to be collected.  
C. It acts exactly like `Dispose`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Having a finalizer puts the object on the "Finalization Queue". When it becomes garbage, GC doesn't remove it immediately; it moves it to the "F-Reachable Queue" to run the finalizer (Revival). It is collected in a subsequent sweep.
</details>

---

## HARD MCQs

### Q11. Large Object Heap (LOH) stores objects larger than:
A. 85,000 bytes  
B. 1 MB  
C. 4 KB  
D. 1024 bytes  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Objects >= 85,000 bytes are allocated on the LOH. The LOH is rarely compacted (to avoid moving massive chunks of memory), which can lead to fragmentation.
</details>

### Q12. `GC.SuppressFinalize(this)` is used to:
A. Stop the GC from collecting the object.  
B. Tell GC that `Dispose` has already done the cleanup work.  
C. Delete the object immediately.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Inside `Dispose()`, you call this to tell the GC: "I have already cleaned up manually. Please do NOT put this object on the finalizer queue." This improves performance by avoiding the double-GC-cycle penalty.
</details>

### Q13. `WeakReference` allows an object to be:
A. Collected by GC even if the reference exists.  
B. Never collected.  
C. Moved to stack.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
A WeakReference points to an object but does not prevent the GC from reclaiming it. It allows "caching" objects that can be reconstructed if they disappear.
</details>

### Q14. Are static fields collected by GC?
A. Yes, in Gen 0.  
B. No, they live for the application domain's lifetime.  
C. Yes, if set to null.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Static fields are "GC Roots". They are always considered reachable (unless the AppDomain unloads). This is a common source of memory leaks if static collections grow indefinitely.
</details>

### Q15. Is Garbage Collection deterministic?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You generally do not know exactly when the GC will run. It runs when it decides memory pressure warrants it. `Dispose` is the mechanism for deterministic cleanup.
</details>
