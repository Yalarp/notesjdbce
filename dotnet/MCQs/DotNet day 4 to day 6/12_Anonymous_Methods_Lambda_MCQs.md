# 12_Anonymous_Methods_Lambda – MCQs

## EASY MCQs

### Q1. A lambda expression is essentially a concise way to represent:
A. An interface  
B. An anonymous method  
C. A class  
D. A loop  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Lambda expressions `=>` are a shorthand, more readable syntax for defining anonymous methods (inline delegates).
</details>

### Q2. Which operator is known as the "lambda operator"?
A. `+=`  
B. `=>`  
C. `->`  
D. `::`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `=>` operator is read as "goes to". Left side: inputs. Right side: expression/statement block.
</details>

### Q3. `x => x * x` is an example of:
A. Statement Lambda  
B. Expression Lambda  
C. Unary Operator  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
An expression lambda consists of a single expression whose result is implicitly returned. It does not use braces `{}`.
</details>

### Q4. Which delegate type represents a function that returns `void`?
A. `Func`  
B. `Predicate`  
C. `Action`  
D. `Void`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Action` delegates (e.g., `Action<T>`) point to methods that perform an action but return no value (void).
</details>

### Q5. A statement lambda is characterized by:
A. Being one line long.  
B. Enclosure in curly braces `{ }`.  
C. Having no parameters.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Statement lambdas look like standard method bodies inside curly braces `(x) => { return x + 1; }` and can contain multiple statements.
</details>

---

## MEDIUM MCQs

### Q6. `Func<int, int, string>` takes how many input parameters?
A. One  
B. Two  
C. Three  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
In `Func<T1, T2, TResult>`, the last type parameter (`string`) is the Return Type. All preceding types (`int`, `int`) are Input Parameters. So, it takes 2 inputs.
</details>

### Q7. What is a "Closure" in the context of lambdas?
A. Closing the database connection.  
B. A lambda capturing variables from its outer scope.  
C. Keeping the method private.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
A closure occurs when a lambda/anonymous method accesses a variable declared outside its own body. It extends the lifetime of that variable so the lambda can use it even after the scope exits.
</details>

### Q8. `Predicate<T>` is equivalent to:
A. `Func<T, bool>`  
B. `Action<T>`  
C. `Func<bool, T>`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`Predicate<T>` is a specialized delegate that takes one item of type T and returns a `bool` (typically for filtering/conditions).
</details>

### Q9. Can a lambda expression omit parameter types?
A. Yes, they are inferred.  
B. No, C# is strongly typed.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Type inference allows the compiler to deduce the types based on the delegate it is assigned to. `(x) => x*2` is valid if assigned to `Func<int, int>`.
</details>

### Q10. Variables captured by a lambda are evaluated:
A. When the lambda is created.  
B. When the lambda is executed.  
C. At compile time.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is a critical nuance. Capturing variables captures the *variable itself* (reference), not just the value at creation time. If the variable changes before the lambda executes, the lambda sees the *current* value.
</details>

---

## HARD MCQs

### Q11. `List<Action> actions = new List<Action>(); for(int i=0; i<3; i++) actions.Add(() => Console.Write(i)); foreach(var a in actions) a();` Output?
A. 012  
B. 333  
C. Runtime Error  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Classic closure trap. The loop variable `i` is captured. By the time the actions usually execute, the loop has finished and `i` is 3. Result is 333. (Note: This behavior changed in specific newer C# versions for foreach loops, but `for` loops still exhibit this).
</details>

### Q12. Can a lambda expression be assigned to `var`?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
You cannot say `var f = x => x + 1;` because the compiler doesn't know *which* delegate type you intend (e.g., `Func<int, int>` vs `Expression<Func<int, int>>` vs custom delegate). You must specify the type.
</details>

### Q13. Are lambda expressions objects?
A. No, they are code.  
B. Yes, they are instantiated as delegate instances (objects).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
When assigned to a variable, a lambda expression results in an instance of a delegate class (or an Expression Tree object).
</details>

### Q14. Can an anonymous method omit the parameter list entirely?
A. Yes.  
B. No.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Old `delegate` syntax allows omitting parameters if the method body doesn't use them. `delegate { Console.WriteLine("Hi"); }` is compatible with `Action<int>`. Lambdas do not allow this.
</details>

### Q15. `CreateDelegate( int x ) { return () => x; }`. What happens to `x` when `CreateDelegate` returns?
A. It is destroyed from the stack.  
B. It is moved to the heap (hoisted class).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Because `x` is captured by the returned lambda, the compiler generates a hidden "closure class" on the heap to hold `x`, preventing it from dying when the stack frame pops.
</details>
