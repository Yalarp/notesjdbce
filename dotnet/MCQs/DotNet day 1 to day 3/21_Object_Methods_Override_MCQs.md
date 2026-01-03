# 21_Object_Methods_Override – MCQs

## EASY MCQs

### Q1. Which class is the ultimate base class of all classes in C#?
A. `System.Root`  
B. `System.Object`  
C. `System.Base`  
D. `System.Universal`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
In C#, every class implicitly or explicitly inherits from `System.Object`.
</details>

### Q2. What is the default return value of the `ToString()` method?
A. The object's data in JSON format.  
B. The fully qualified name of the object's type.  
C. An empty string.  
D. The object's memory address.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
By default, `ToString()` returns the fully qualified name of the type (e.g., "Namespace.ClassName"), unless it is overridden.
</details>

### Q3. What is the return type of the `GetHashCode()` method?
A. `long`  
B. `string`  
C. `int`  
D. `byte`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`GetHashCode()` returns an `int` (32-bit integer) which serves as a numeric identifier for the object, primarily for hash-based collections.
</details>

### Q4. By default, what does the `Equals(object obj)` method check for reference types?
A. It checks if all properties are equal.  
B. It checks if the objects are of the same type.  
C. It checks for reference equality (do they point to the same memory?).  
D. It always returns true.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
For reference types, the default implementation of `Equals` uses `ReferenceEquals` to check if the two variables point to the exact same object in memory.
</details>

### Q5. When should you override the `Finalize()` method?
A. For every class.  
B. To close database connections immediately.  
C. Only when implementing custom clean-up for unmanaged resources (rarely).  
D. To reset static variables.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Overriding `Finalize` (via a destructor) is rare and used generally for unmanaged resources. For standard cleanup, `IDisposable` and the `Dispose` pattern are preferred.
</details>

---

## MEDIUM MCQs

### Q6. If you override `Equals()`, what other method must you implicitly override to maintain contract correctness?
A. `ToString()`  
B. `GetHashCode()`  
C. `Clone()`  
D. `Dispose()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If two objects are considered equal (via `Equals`), they MUST return the same hash code. Failing to override `GetHashCode` breaks this contract and causes issues in collections like Dictionary and HashSet.
</details>

### Q7. How do you call the base class implementation of `ToString()` from an overridden version?
A. `super.ToString()`  
B. `this.ToString()`  
C. `base.ToString()`  
D. `parent.ToString()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
In C#, the `base` keyword is used to access members of the immediate parent class.
</details>

### Q8. What happens if you use a class in a `HashSet` that overrides `Equals` but NOT `GetHashCode`?
A. It works perfectly fine.  
B. It throws a compilation error.  
C. It throws a Runtime Exception immediately.  
D. The HashSet may fail to identify duplicate objects correctly.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
The `HashSet` first uses the hash code to locate the bucket. If hash codes differ (which they likely will if `GetHashCode` isn't overridden), `Equals` might never even be called, allowing duplicates of "equal" objects.
</details>

### Q9. What is the benefit of implementing `IEquatable<T>`?
A. It allows the class to be serialized.  
B. It provides a type-safe `Equals` method, avoiding boxing for value types.  
C. It generates `GetHashCode` automatically.  
D. It forces the class to be sealed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`IEquatable<T>` defines `Equals(T other)`, which avoids casting (and boxing for structs) compared to the standard `Equals(object obj)`.
</details>

### Q10. Which helper method is recommended in Modern C# to generate a hash code from multiple fields?
A. `Math.Abs(field1 + field2)`  
B. `field1 ^ field2`  
C. `HashCode.Combine(field1, field2, ...)`  
D. `object.GetHashCode(field1, field2)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`HashCode.Combine()` provides a robust algorithm for combining multiple hash codes into a single integer, handling bit-shifting and distribution better than manual XOR operations.
</details>

---

## HARD MCQs

### Q11. Which of the following statements about `GetHashCode()` collisions is TRUE?
A. Two unequal objects MUST have different hash codes.  
B. Two unequal objects MAY have the same hash code.  
C. Two equal objects MAY have different hash codes.  
D. Hash codes are unique for every object in memory forever.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Hash collisions are allowed (and inevitable since `int` is finite). Unequal objects can share a hash code. However, equal objects MUST share the same hash code.
</details>

### Q12. Why is mutable data dangerous in `GetHashCode()`?
A. It causes the computation to be too slow.  
B. It throws an exception if the fields change.  
C. If the object is keys in a Dictionary, changing the field changes the hash, losing the object in the collection.  
D. Mutable data cannot be hashed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
If a field used in `GetHashCode` changes while the object is in a hash-based collection, the hash code changes. The collection will look for the object in the wrong "bucket" and fail to find it or remove it.
</details>

### Q13. Consider the following modern pattern for `Equals`. What does `obj is Person other` do?
```csharp
public override bool Equals(object obj) {
    return obj is Person other && this.Id == other.Id;
}
```
A. It checks if obj is Person, and if null throws an exception.  
B. It checks if obj is Person, and if so, casts it to `other` and proceeds; returns false if null or wrong type.  
C. It only checks the type but does not ignore nulls.  
D. It performs a reference equality check first.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is pattern matching. It safely checks if `obj` is compatible with `Person` AND not null. If successful, it assigns the result to the variable `other` for immediate use.
</details>

### Q14. What is the difference between `object.ReferenceEquals(a, b)` and `a.Equals(b)`?
A. They are identical.  
B. `ReferenceEquals` always checks identity; `Equals` can be overridden to check value equality.  
C. `ReferenceEquals` calls the overridden `Equals` method.  
D. `Equals` works on static classes only.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`Object.ReferenceEquals` is a static method that strictly checks memory identity (do they point to the same address?). `Equals` is a virtual method that can be customized to equate objects based on their content (values).
</details>

### Q15. If you overload the `==` operator, what is the best practice?
A. Don't touch `Equals()`.  
B. Override `Equals()` and implement `GetHashCode()` to ensure consistency between `==` and `Equals`.  
C. Make `==` private.  
D. Only implement `!=` and let the compiler handle `==`.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It is expected that if `a == b` is true, then `a.Equals(b)` is also true. Therefore, when overloading operators, you should override `Equals` and `GetHashCode` to match the logic.
</details>
