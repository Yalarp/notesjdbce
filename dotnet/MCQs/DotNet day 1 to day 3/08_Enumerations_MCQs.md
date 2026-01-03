# 08_Enumerations – MCQs

## EASY MCQs

### Q1. What is the default underlying type for an `enum` in C#?

A. `long`  
B. `int`  
C. `string`  
D. `bool`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
By default, the underlying type of each element in an enum is `int`.
</details>

### Q2. Which attribute is used to allow an enum to represent a combination of values (bitwise flags)?

A. `[Serializable]`  
B. `[Flags]`  
C. `[Combine]`  
D. `[Bitwise]`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The `[Flags]` attribute indicates that an enumeration can be treated as a bit field; that is, a set of flags that can be combined using bitwise OR.
</details>

### Q3. How do you convert a string "Monday" to an enum value `Days.Monday`?

A. `Enum.ToString()`  
B. `Enum.Parse()`  
C. `(Days)"Monday"`  
D. `Convert.ToEnum()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`Enum.Parse()` (or `Enum.TryParse()`) is used to convert the string representation of the name or numeric value to an equivalent enum object.
</details>

### Q4. If an enum is defined as `enum Color { Red, Green, Blue }`, what is the integer value of `Blue`?

A. 0  
B. 1  
C. 2  
D. 3  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Enum values start at 0 by default. Red=0, Green=1, Blue=2.
</details>

---

## MEDIUM MCQs

### Q5. Can you specify a custom underlying type for an enum?

A. No, it is always `int`.  
B. Yes, but only `long`.  
C. Yes, any integral type (byte, sbyte, short, ushort, int, uint, long, ulong).  
D. Yes, any type including `string` and `double`.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
You can explicitly specify the underlying type of an enum to be any integral type (except `char`). For example: `enum Small : byte { ... }`.
</details>

### Q6. Refer to the code:
```csharp
enum Status { None = 10, Running, Stopped }
```
What is the value of `Status.Stopped`?

A. 0  
B. 2  
C. 12  
D. 11  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
If a value is not specified, it is incremented by 1 from the previous member. None=10, Running=11, Stopped=12.
</details>

### Q7. What method is used to retrieve an array of the values of the constants in a specified enumeration?

A. `Enum.GetNames()`  
B. `Enum.GetValues()`  
C. `Enum.GetList()`  
D. `Enum.ToArray()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`Enum.GetValues(typeof(MyEnum))` returns an array containing the values of the constants in the enumeration.
</details>

### Q8. Which of the following is NOT a good practice when defining Enums?

A. Using singular names for regular enums.  
B. Using plural names for Flags enums.  
C. Defining a 'None' or default value (0).  
D. Using enums for values that change frequently in the database.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** D

**Explanation:**  
Enums should be used for sets of constants that rarely change (like days of the week). If values change frequently (like product categories), a database table is better than recompiling code.
</details>

---

## HARD MCQs

### Q9. When using the `[Flags]` attribute, why is it recommended to assign values in powers of 2 (1, 2, 4, 8...)?

A. To make the numbers look nicer.  
B. To allow unique combinations using bitwise OR operations.  
C. To save memory.  
D. It is a requirement of the CLR; otherwise it won't compile.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Powers of 2 correspond to individual bits (binary 0001, 0010, 0100). This allows multiple flags to be combined without overlapping, ensuring that `Flag A | Flag B` creates a unique value representing both.
</details>

### Q10. What happens if you cast an integer to an Enum type that does not have that value defined?

A. It throws an `ArgumentOutOfRangeException`.  
B. It throws an `InvalidCastException`.  
C. It succeeds, and the variable holds the integer value as the Enum type, even though it has no name.  
D. It defaults to the first value (0).  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Casting an integer to an enum is unchecked. The enum variable will simply hold the numeric value, even if it doesn't correspond to any named constant in the enum definition.
</details>

### Q11. Which method would you use to check if a specific flag is set in a Flags Enum variable?

A. `enumVar.Contains(Flag)`  
B. `enumVar.HasFlag(Flag)`  
C. `enumVar.IsSet(Flag)`  
D. `Enum.Check(enumVar, Flag)`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
The `HasFlag()` method (available on the Enum class) provides a clean way to determine if a specific bit field is set in the current instance.
</details>

### Q12. Describe the result of the following bitwise operation: `Permissions p = Permissions.Read | Permissions.Write; p &= ~Permissions.Write;`

A. It adds Write permission.  
B. It removes Write permission.  
C. It toggles Read permission.  
D. It sets p to null.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`~Permissions.Write` creates a bitmask of all bits EXCEPT Write. `p &= ...` performs a bitwise AND, effectively clearing the Write bit while keeping other bits (`Read`) intact.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
