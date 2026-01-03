# 05_String_Conversion_Methods – MCQs

## EASY MCQs

### Q1. Which method is recommended for converting user input to a number to avoid exceptions?

A. `int.Parse()`  
B. `Convert.ToInt32()`  
C. `int.TryParse()`  
D. `(int)` casting  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
`int.TryParse()` is recommended for user input because it does not throw an exception if the conversion fails; instead, it returns `false`.
</details>

### Q2. What exception does `int.Parse()` throw if the string format is invalid (e.g., "abc")?

A. ArgumentNullException  
B. FormatException  
C. OverflowException  
D. InvalidCastException  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`int.Parse()` throws a `FormatException` when the string does not represent a valid number in the specified format.
</details>

### Q3. What is the return type of `Double.TryParse`?

A. `double`  
B. `int`  
C. `bool`  
D. `void`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
`TryParse` methods always return a `bool` indicating success or failure. The converted value is returned via an `out` parameter.
</details>

### Q4. Which conversion method handles `null` by returning 0 (or default value) instead of throwing an exception?

A. `int.Parse(null)`  
B. `Convert.ToInt32(null)`  
C. `int.Parse(null)` inside a try-catch  
D. `(int)null`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The `Convert` class methods (like `Convert.ToInt32`) return the default value (0 for numbers) when passed `null`, whereas `Parse` throws an `ArgumentNullException`.
</details>

---

## MEDIUM MCQs

### Q5. What is the key difference between using `Convert.ToInt32(doubleVal)` and casting `(int)doubleVal`?

A. `Convert` truncates, while Casting rounds.  
B. `Convert` rounds to the nearest integer, while Casting truncates the decimal part.  
C. There is no difference; they behave exactly the same.  
D. Casting throws an exception for decimal values.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`Convert.ToInt32()` rounds the number (to nearest even number for .5), whereas explicit casting `(int)` simply truncates (discards) the fractional part.
</details>

### Q6. Consider the following code:
```csharp
string s = null;
int result;
bool success = int.TryParse(s, out result);
```
What will be the values of `success` and `result`?

A. `success`=false, `result`=0  
B. `success`=false, `result`=null  
C. Throws ArgumentNullException  
D. `success`=true, `result`=0  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
`TryParse` handles `null` gracefully. It returns `false` (failure) and sets the `out` parameter to the default value of the type (0 for int).
</details>

### Q7. How would you convert the hexadecimal string "FF" to an integer?

A. `int.Parse("FF")`  
B. `Convert.ToInt32("FF")`  
C. `Convert.ToInt32("FF", 16)`  
D. `int.ToHex("FF")`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
To convert a number from a different base, use `Convert.ToInt32(value, fromBase)`. Base 16 represents Hexadecimal.
</details>

### Q8. Which `Parse` call corresponds to `Convert.ToSingle()`?

A. `Double.Parse()`  
B. `Float.Parse()`  
C. `float.Parse()`  
D. `Decimal.Parse()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
`System.Single` maps to the C# alias `float`. Therefore, `Convert.ToSingle()` corresponds to `float.Parse()`.
</details>

---

## HARD MCQs

### Q9. Regarding `Convert.ToBoolean()`, which string value converts to `true`?

A. "1"  
B. "True" (case-insensitive)  
C. "yes"  
D. Any non-empty string  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`Convert.ToBoolean()` (and `bool.Parse()`) accepts "True" or "False" (case-insensitive). It does not accept numeric strings like "1" or "0", nor other words like "yes".
</details>

### Q10. What is the specific behavior of `Math.Round` or `Convert.ToInt32` when rounding the value `2.5`?

A. It rounds up to 3.  
B. It rounds down to 2.  
C. It rounds to the nearest even number (2).  
D. It throws an AmbiguousMatchException.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
By default, .NET uses "Banker's Rounding" (Round to Nearest Even). So `2.5` rounds to `2`, and `3.5` rounds to `4`.
</details>

### Q11. Which statement correctly converts a binary string "101" to an integer?

A. `int i = int.Parse("101", 2);`  
B. `int i = Convert.ToInt32("101", 2);`  
C. `int i = (int)"101";`  
D. `int i = Binary.Parse("101");`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The `Convert.ToInt32(string, fromBase)` overload allows specifying base 2 for binary conversion. `int.Parse` does not have an overload that takes a base directly in this manner.
</details>

### Q12. If `int.TryParse(string, out int result)` fails, what happens to the variable passed as the `out` parameter?

A. It retains its previous value.  
B. It becomes null.  
C. It is set to the default value of the type (0).  
D. It becomes undefined.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
When `TryParse` returns `false`, the `out` parameter is automatically assigned the default value for that type (e.g., `0` for `int`, `null` for objects, `false` for bool).
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
