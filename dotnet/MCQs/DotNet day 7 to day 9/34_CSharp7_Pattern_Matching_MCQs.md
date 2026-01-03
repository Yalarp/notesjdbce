# 34_CSharp7_Pattern_Matching – MCQs

## EASY MCQs

### Q1. What keyword is primarily used for pattern matching in C#?
A. `match`  
B. `is`  
C. `check`  
D. `pattern`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`obj is Type variable` is the foundational pattern matching syntax.
</details>

### Q2. In C# 7, `if (obj is string s)` allows you to:
A. Check if `obj` is a string AND assign it to variable `s` if true.  
B. Check if `obj` converts to string.  
C. Find the string length.  
D. Create a string.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
This combines the type check and the cast into one atomic, safe operation.
</details>

### Q3. What is a "Switch Expression" (C# 8)?
A. A switch statement that returns a value (expression context).  
B. A regular switch.  
C. A boolean expression.  
D. A loop.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Uses `value switch { pattern => result, _ => default }` syntax, more concise than traditional `case: return;`.
</details>

### Q4. The `_` (underscore) in pattern matching represents:
A. Null.  
B. The "Discard" or "Default" pattern (matches everything).  
C. Error.  
D. Private variable.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Acts like the `default:` case in switches or a "catch-all" wildcard.
</details>

### Q5. Can you test for `null` using pattern matching?
A. No.  
B. Yes, `if (obj is null)`.  
C. Only with `==`.  
D. Only in C# 1.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The "Constant Pattern" allows checking against `null`, `42`, or other constants.
</details>

---

## MEDIUM MCQs

### Q6. Property Patterns (C# 8) allow checking internal state. Example:
A. `if (obj.Prop == 5)`  
B. `if (obj is { Prop: 5 })`  
C. `if (obj -> Prop: 5)`  
D. `if (obj has Prop 5)`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It inspects the object `obj` to see if it is not null AND its property `Prop` equals `5`.
</details>

### Q7. The `when` keyword in a switch case allows:
A. Adding extra boolean conditions (guards) to a pattern.  
B. Defining time.  
C. Running async code.  
D. Looping.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`case int i when i > 100:` allows fine-grained filtering beyond just type matching.
</details>

### Q8. Positional Patterns work with which method on a type?
A. `Dispose`  
B. `Deconstruct`  
C. `ToString`  
D. `Equals`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`switch (point) { case (0, 0): ... }` works because `point` can be deconstructed into two values (x, y).
</details>

### Q9. Relational Patterns (C# 9) allow:
A. `x is > 5 and < 10`  
B. `x > 5`  
C. `x.Compare(5)`  
D. `Expression<Func<>>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
You can use comparison operators directly in the `is` or switch pattern syntax.
</details>

### Q10. What does `if (obj is not null)` do?
A. Error.  
B. Checks if obj is not null (Negated Pattern).  
C. Same as `!=`.  
D. Both B and C (functionally).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** D
**Explanation:**  
The `not` pattern (C# 9) flips the logic. It's a readable alternative to `!(obj is null)`.
</details>

---

## HARD MCQs

### Q11. Switch Expressions must be:
A. Void.  
B. Exhaustive (handle all possible input values).  
C. Asynchronous.  
D. Inside a class.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
If a switch expression receives an input that doesn't match any case (and no discard `_` is present), it throws a `SwitchExpressionException` at runtime. The compiler warns if it detects missing cases.
</details>

### Q12. "Var Pattern": `if (expr is var x)`
A. Always false.  
B. Always true (matches anything non-null and null) and assigns to x.  
C. Matches only dynamic types.  
D. Error.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It's a way to create a temporary variable for an intermediate result inside an expression. `is var` matches everything.
</details>

### Q13. Logical Patterns allow:
A. `and`, `or`, `not` keywords in patterns.  
B. `&&`, `||`.  
C. `&`, `|`.  
D. SQL syntax.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
C# 9 added these textual logical operators specifically for patterns. `if (c is >= 'a' and <= 'z')`.
</details>

### Q14. Can you nest Property Patterns?
A. No.  
B. Yes. `obj is { Address: { City: "NY" } }`  
C. Only 1 level deep.  
D. Only for structs.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Patterns are recursive. You can drill down deep into the object graph concisely.
</details>

### Q15. Why use Pattern Matching over Polymorphism (virtual methods)?
A. It is always better.  
B. It is useful when you cannot modify the types (e.g., external library classes) or when behavior depends on cross-cutting concerns not native to the type hierarchy.  
C. Polymorphism is dead.  
D. It is faster.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Polymorphism is usually preferred for internal "Is-A" behaviors. Pattern matching is excellent for external inspection logic or switching over data shapes.
</details>
