# 18_Indexers – MCQs

## EASY MCQs

### Q1. What does an Indexer allow you to do in C#?

A. Index a database.  
B. Access an instance of a class using array-like syntax (`obj[index]`).  
C. Create a static array.  
D. Sort an array.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Indexers allow an object to be indexed just like an array. This is often called a "smart array".
</details>

### Q2. Which keyword is used to define an indexer?

A. `indexer`  
B. `property`  
C. `this`  
D. `item`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
An indexer is defined using the `this` keyword, e.g., `public string this[int index] { ... }`.
</details>

### Q3. Can an indexer have more than one parameter?

A. No, only one (int).  
B. Yes, like a 2D array (`this[int r, int c]`).  
C. Only if passed by reference.  
D. No.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Yes, indexers can take multiple parameters to simulate multi-dimensional access, commonly used in Grid or Matrix classes.
</details>

### Q4. Can indexers be static?

A. Yes.  
B. No.  
C. Only in static classes.  
D. Yes, if read-only.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Indexers are strictly instance members because they operate on a specific object instance (using `this`). They cannot be static.
</details>

---

## MEDIUM MCQs

### Q5. What distinguishes an Indexer from a Property?

A. Syntax: Indexers use `[]`, Properties use `.Name`. Indexers don't have a specific name (they use `this`).  
B. Indexers are faster.  
C. Properties cannot store data.  
D. Indexers are only for integer access.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
Properties are identified by names (`obj.Name`), while indexers are identified by their signature and accessed via bracket notation on the instance (`obj[0]`).
</details>

### Q6. Can you overload indexers?

A. No.  
B. Yes, by having different parameter types or counts.  
C. Yes, by having different return types only.  
D. Only in abstract classes.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Like methods, indexers can be overloaded. You can have `this[int index]` and `this[string name]` in the same class.
</details>

### Q7. What access modifiers can indexer accessors (`get`/`set`) have?

A. Only public.  
B. Same as the indexer itself.  
C. You can restrict the visibility of one accessor (e.g., `public get`, `private set`), just like properties.  
D. None (implicit public).  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Indexers support asymmetric accessor accessibility to restrict read or write access.
</details>

### Q8. If you define an indexer `public string this[string key]`, how do you access it?

A. `obj.["key"]`  
B. `obj["key"]`  
C. `obj.this("key")`  
D. `obj.Key`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The standard syntax is `instance[argument]`.
</details>

---

## HARD MCQs

### Q9. In the `set` accessor of an indexer, what does the implicit parameter `value` contain?

A. The index being accessed.  
B. The value being assigned to the element at the index.  
C. The object itself.  
D. The previous value.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Just like properties, `value` represents the data coming from the right-hand side of the assignment.
</details>

### Q10. Can an interface define an indexer?

A. No.  
B. Yes, `type this[paramType param] { get; set; }`.  
C. Yes, but implementation must be provided.  
D. Only if it is generic.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Interfaces can declare indexers, which implementing classes must provide.
</details>

### Q11. Can you pass an indexer element as a `ref` or `out` parameter (e.g., `Method(ref obj[0])`)?

A. Yes.  
B. No.  
C. Only if the underlying storage is an array.  
D. Yes, for value types.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Like properties, indexers are methods (`get_Item`, `set_Item`) under the hood and do not expose a direct memory address (variable) that `ref` or `out` requires.
</details>

### Q12. What structure uses indexers extensively to provide key-based access?

A. `List<T>`  
B. `Dictionary<TKey, TValue>`  
C. `Queue<T>`  
D. `Stack<T>`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`Dictionary` uses an indexer `val = dict[key]` to quickly retrieve values based on keys. `List` also uses one for position-based access (`list[0]`).
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
