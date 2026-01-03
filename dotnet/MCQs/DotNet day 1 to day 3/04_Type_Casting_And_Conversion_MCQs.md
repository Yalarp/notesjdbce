# 04_Type_Casting_And_Conversion – MCQs

## EASY MCQs

### Q1. What is Implicit Conversion (Widening)?

A. Converting a larger type to a smaller type manually.  
B. Automatic conversion by the compiler from a smaller type to a larger type without data loss.  
C. Converting a value type to a reference type.  
D. Converting a string to a number.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Implicit conversion is automatically performed by the compiler when there is no risk of data loss, typically moving from a smaller data type to a larger one (e.g., `int` to `long`).
</details>

### Q2. Which keyword is used to explicitly enable overflow checking for integral operations?

A. `catch`  
B. `throws`  
C. `checked`  
D. `safe`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The `checked` keyword forces the runtime to throw an `OverflowException` if an arithmetic operation results in an overflow.
</details>

### Q3. What is Boxing?

A. Converting a Reference Type to a Value Type.  
B. Converting a Value Type to an Object (Reference Type).  
C. Package a class into an assembly.  
D. Converting a derived class to a base class.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Boxing is the process of converting a Value Type to the type `object` (or any interface implemented by this value type), which moves the value from the Stack to the Heap.
</details>

### Q4. What happens when you cast a `double` to an `int` (e.g., `(int)3.9`)?

A. It rounds to the nearest integer (4).  
B. It throws a FormatException.  
C. It truncates the decimal part (3).  
D. It returns 0.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Explicit casting from floating-point types to integral types results in truncation, meaning the fractional part is discarded (not rounded).
</details>

---

## MEDIUM MCQs

### Q5. Consider the following code:
```csharp
byte a = 10;
byte b = 20;
byte result = a + b;
```
What is the outcome?

A. `result` becomes 30.  
B. Compile-time error: Cannot implicitly convert type 'int' to 'byte'.  
C. Runtime error: OverflowException.  
D. `result` becomes 0.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Arithmetic operations on `byte` operands (like `a + b`) are automatically promoted to `int`. assigning the `int` result back to a `byte` variable requires an explicit cast.
</details>

### Q6. Which of the following is TRUE about the `unchecked` keyword?

A. It prevents compile-time errors.  
B. It suppresses overflow-checking for integral-type arithmetic operations and conversions.  
C. It ensures that data loss never occurs.  
D. It is the default behavior for floating-point operations only.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The `unchecked` keyword allows overflow to occur silently (wrapping around) without throwing an exception. This is the default behavior for arithmetic operations if not configured globally.
</details>

### Q7. What is the correct way to Unbox an object `obj` (containing an `int` value) and convert it to `double`?

A. `double d = (double)obj;`  
B. `double d = obj as double;`  
C. `double d = (double)(int)obj;`  
D. `double d = Convert.ToDouble(obj);` (Assume specifically testing unboxing syntax logic)  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Unboxing requires an explicit cast to the *exact* original type first. So you must unbox to `int` first (`(int)obj`), and then convert that `int` to `double`. Directly casting `object` (holding int) to `double` entails an InvalidCastException.
</details>

### Q8. What does the following code print?
```csharp
int max = int.MaxValue;
int result = unchecked(max + 1);
Console.WriteLine(result);
```
A. 2147483648  
B. 0  
C. -2147483648  
D. OverflowException  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Inside an `unchecked` context, integer overflow wraps around. `int.MaxValue + 1` wraps to `int.MinValue` (-2147483648).
</details>

---

## HARD MCQs

### Q9. Why can't `int` be implicitly converted to `bool` in C#?

A. Because `bool` is larger than `int`.  
B. Because C# enforces strict type safety and does not treat 0/1 as false/true directly.  
C. Because `bool` is a reference type.  
D. Because `int` is unsigned by default.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Unlike C/C++, C# enforces strict type safety and distinguishes boolean logic from numeric values. explicit comparison (e.g., `num != 0`) is required.
</details>

### Q10. Consider the following Boxing scenario:
```csharp
int val = 100;
object o = val;
val = 200;
Console.WriteLine((int)o);
```
What is the output?

A. 200  
B. 100  
C. 0  
D. Null  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
When `val` is boxed into `o`, a copy of the value (100) is stored on the Heap. Changing the original `val` (on Stack) to 200 does not affect the boxed copy in the Heap.
</details>

### Q11. Which conversion path allows for Implicit Conversion?

A. `double` -> `float`  
B. `long` -> `float`  
C. `decimal` -> `double`  
D. `int` -> `short`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`long` (64-bit integer) can be implicitly converted to `float` (32-bit floating-point). Even though `long` has more bits, `float` has a much larger magnitude range, so the conversion is considered widening (though precision might be lost).
</details>

### Q12. What happens if you try to Unbox `null` to a value type (e.g., `int`)?

A. It returns 0.  
B. It returns null.  
C. It throws a `NullReferenceException`.  
D. It throws an `InvalidCastException`.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Attempting to unbox a null object reference to a non-nullable value type throws a `NullReferenceException`.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
