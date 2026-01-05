# Functions and Scope in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Function Basics](#2-function-basics)
3. [Function Parameters and Arguments](#3-function-parameters-and-arguments)
4. [Return Values](#4-return-values)
5. [Default Parameters](#5-default-parameters)
6. [Rest Parameters](#6-rest-parameters)
7. [The arguments Object](#7-the-arguments-object)
8. [Spread Operator](#8-spread-operator)
9. [Scope in JavaScript](#9-scope-in-javascript)
10. [Quick Reference](#10-quick-reference)
11. [Interview Questions](#11-interview-questions)

---

## 1. Introduction

### 1.1 Definition
A function is a reusable block of code designed to perform a particular task. Functions allow you to write code once and use it multiple times.

### 1.2 Purpose
- **Reusability**: Write once, use many times
- **Modularity**: Break complex problems into smaller parts
- **Maintainability**: Easier to update and debug
- **Abstraction**: Hide complex logic behind simple function calls

### 1.3 Problem Solved
Without functions:
- Code duplication everywhere
- Difficult to maintain
- Hard to read and understand
- No way to organize related logic

---

## 2. Function Basics

### 2.1 Function Declaration Syntax

```javascript
function functionName(parameter1, parameter2) {
    // Function body - code to execute
    return value; // Optional return statement
}
```

### 2.2 Key Characteristics in JavaScript

| Characteristic | Description |
|---------------|-------------|
| **Dynamic Return Type** | Functions can return any type; no type declaration needed |
| **No Parameter Types** | Parameters don't have type declarations |
| **Default Return** | Functions return `undefined` if no return statement |
| **First-Class Citizens** | Functions can be assigned to variables, passed as arguments |

### 2.3 Basic Function Example

```javascript
<script>
"use strict";
function go() {  
    document.write("hello");
}

go();              // Function call - prints "hello"
var r = go();      // Calls go(), r receives undefined
console.log(r);    // undefined

document.write(typeof(go));  // "function"
document.write("<hr/>");
document.write(go);          // Prints function definition
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 1 | `"use strict"` | Enables strict mode |
| 2 | `function go()` | Declares function named `go` with no parameters |
| 3 | `document.write("hello")` | Function body - writes "hello" |
| 6 | `go()` | Calls the function, executes the body |
| 7 | `var r = go()` | Calls `go()`, stores return value in `r` |
| 8 | `console.log(r)` | Prints `undefined` (no return statement) |
| 10 | `typeof(go)` | Returns `"function"` |
| 12 | `document.write(go)` | Prints the entire function definition |

**Key Insight:**
- `go()` - Executes the function
- `go` (without parentheses) - References the function object itself

**Execution Flow:**
```
1. Browser parses script
2. Function `go` is registered in memory
3. `go()` is called → "hello" is written
4. `go()` is called again → "hello" is written, undefined returned to r
5. r is printed → undefined
6. typeof(go) → "function"
7. go (reference) → prints function body text
```

---

## 3. Function Parameters and Arguments

### 3.1 Parameters vs Arguments

| Term | Definition | Example |
|------|------------|---------|
| **Parameter** | Variable in function definition | `function call(a, b)` - a, b are parameters |
| **Argument** | Actual value passed when calling | `call(5, 7)` - 5, 7 are arguments |

### 3.2 Function with Parameters

```javascript
<script>
"use strict";
function call(a, b) {
    var p;
    p = a * b;
    return p;
}

var x, y;
x = 5;
y = 7;
var r = call(x, y);
document.write(r);        // 35
document.write(call(3, 3)); // 9
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 2-6 | `function call(a, b)` | Function with two parameters |
| 3 | `var p;` | Local variable declaration |
| 4 | `p = a * b` | Multiplies parameters |
| 5 | `return p;` | Returns the product |
| 8-9 | `x = 5; y = 7;` | Variables in calling scope |
| 11 | `call(x, y)` | Passes x and y as arguments |

**Memory Diagram:**
```
Calling Scope:          Function Scope (1st call):    Function Scope (2nd call):
┌─────────┐            ┌─────────┐                    ┌─────────┐
│ x = 5   │            │ a = 5   │                    │ a = 3   │
│ y = 7   │            │ b = 7   │                    │ b = 3   │
│ r = 35  │            │ p = 35  │                    │ p = 9   │
└─────────┘            └─────────┘                    └─────────┘
```

### 3.3 Passing Fewer Arguments Than Parameters

**JavaScript does NOT throw an error if you pass fewer arguments!**

```javascript
<script>
"use strict";
function call(a, b) {
    var p;
    p = a * b;
    return p;
}

var x = 5;
var r = call(x);        // Only passing one argument!
document.write(r);       // NaN
</script>
```

**What Happens:**
- `a` receives `5`
- `b` receives `undefined` (no argument passed)
- `5 * undefined` = `NaN`

**Memory Diagram:**
```
┌─────────┐
│ a = 5   │
│ b = undefined │
│ p = NaN │
└─────────┘
```

### 3.4 Checking for Undefined Parameters

```javascript
<script>
"use strict";
function call(a, b) {
    var p;
    if (a != undefined && b != undefined)
        p = a * b;
    else if (a != undefined)
        p = a;
    return p;
}

var r = call(5);
document.write(r);  // 5
document.write(call(3, 3));  // 9
</script>
```

**Execution Flow:**
```
call(5):
1. a = 5, b = undefined
2. Check: a != undefined && b != undefined → FALSE
3. Check: a != undefined → TRUE
4. p = a = 5
5. Return 5

call(3, 3):
1. a = 3, b = 3
2. Check: a != undefined && b != undefined → TRUE
3. p = 3 * 3 = 9
4. Return 9
```

---

## 4. Return Values

### 4.1 Explicit Return

```javascript
function add(a, b) {
    return a + b;  // Explicit return
}
var result = add(3, 4);  // result = 7
```

### 4.2 Implicit Return (undefined)

```javascript
function greet(name) {
    document.write("Hello " + name);
    // No return statement
}
var result = greet("John");  // result = undefined
```

### 4.3 Multiple Returns

```javascript
function checkAge(age) {
    if (age >= 18) {
        return "Adult";
    }
    return "Minor";  // Only reached if age < 18
}
```

---

## 5. Default Parameters

### 5.1 ES6 Default Parameter Syntax

```javascript
<script>
"use strict";
function call(a, b = 1) {
    var p;
    p = a * b;
    return p;
}

var r = call(5);         // b defaults to 1
document.write(r);       // 5

document.write(call(3, 3)); // 9 (overrides default)
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 2 | `function call(a, b = 1)` | `b` has default value of 1 |
| 7 | `call(5)` | Only `a` is passed, `b` uses default |
| 9 | `call(3, 3)` | Both passed, default is overridden |

**Memory Diagram:**
```
call(5):                 call(3, 3):
┌─────────┐            ┌─────────┐
│ a = 5   │            │ a = 3   │
│ b = 1   │ (default)  │ b = 3   │ (overridden)
│ p = 5   │            │ p = 9   │
└─────────┘            └─────────┘
```

### 5.2 Rules for Default Parameters

1. **Default parameters must be at the END** of the parameter list
2. Parameters without defaults CANNOT come after those with defaults

```javascript
// ❌ WRONG - Will cause issues
function wrong(a = 1, b) { }

// ✅ CORRECT
function right(a, b = 1) { }
```

### 5.3 Logical OR for Defaults (Older Method)

Before ES6, developers used the logical OR operator:

```javascript
<script>
"use strict";
function call(a, b) {
    var p;
    b = b || 3;  // If b is falsy, use 3
    p = a * b;
    return p;
}

var r = call(5);
document.write(r);  // 15 (5 * 3)
document.write(call(3, 4));  // 12
</script>
```

**How `b = b || 3` Works:**
- If `b` is truthy, use `b`
- If `b` is falsy (undefined, null, 0, "", false, NaN), use `3`

**Falsy Values in JavaScript:**
- `false`
- `0`
- `""` (empty string)
- `null`
- `undefined`
- `NaN`

> **Warning**: This method has a bug! If you intentionally pass `0` or `false`, it will be replaced with the default!

---

## 6. Rest Parameters

### 6.1 Definition
Rest parameters allow a function to accept an indefinite number of arguments as an array.

### 6.2 Syntax

```javascript
function functionName(...restParameter) {
    // restParameter is an array
}
```

### 6.3 Example: Variable Number of Arguments

```javascript
<script>
"use strict";
function multiply(...myarg) {
    console.log(myarg);             // Array [2, 3]
    console.log(typeof myarg);      // "object"
    console.log(myarg.constructor); // function Array()
    
    let sum = 0;
    for (let i = 0; i < myarg.length; i++)
        sum = sum + myarg[i];
    return sum;
}

var arr = multiply(2, 3);
document.write(arr);  // 5

arr = multiply(2, 3, 5, 6, 7);
document.write(arr);  // 23
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 2 | `function multiply(...myarg)` | `myarg` collects ALL arguments into an array |
| 3 | `console.log(myarg)` | Prints the array of arguments |
| 4 | `typeof myarg` | Returns "object" (arrays are objects) |
| 5 | `myarg.constructor` | Returns Array constructor |
| 7-9 | For loop | Iterates through array and sums values |
| 13 | `multiply(2, 3)` | `myarg` = [2, 3] |
| 16 | `multiply(2, 3, 5, 6, 7)` | `myarg` = [2, 3, 5, 6, 7] |

### 6.4 Rest Parameter with Regular Parameters

```javascript
<script>
"use strict";
function multiply(m, ...myarg) {
    console.log(myarg);  // [2, 3] (m gets 1)
    console.log(typeof myarg);  // "object"
    
    let sum = 0;
    for (let i = 0; i < myarg.length; i++)
        sum = sum + myarg[i];
    return sum;
}

var arr = multiply(1, 2, 3);
document.write(arr);  // 5
</script>
```

**How Arguments Are Distributed:**
```
multiply(1, 2, 3):
- m = 1 (first argument goes to regular parameter)
- myarg = [2, 3] (rest go to rest parameter)
```

### 6.5 Rest Parameter Must Be Last

```javascript
// ❌ SyntaxError: Rest parameter must be last formal parameter
function wrong(...myarg, m) { }

// ✅ Correct
function right(m, ...myarg) { }
```

---

## 7. The arguments Object

### 7.1 Definition
The `arguments` object is an array-like object available inside all non-arrow functions that contains the values of the arguments passed to the function.

### 7.2 Example: Using arguments Object

```javascript
<script>
"use strict";
function findMax() {
    var i, max = arguments[0];
    for (i = 1; i < arguments.length; i++) {
        if (arguments[i] > max) {
            max = arguments[i];
        }
    }
    console.log(arguments);           // Arguments object
    console.log(typeof arguments);    // "object"
    return max;
}

var x = findMax(1, 123, 500, 115, 44, 88);
document.write(x);  // 500
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 2 | `function findMax()` | No parameters defined |
| 3 | `var i, max = arguments[0]` | Initialize max with first argument |
| 4-7 | For loop | Iterate through arguments to find max |
| 9 | `console.log(arguments)` | Shows Arguments object with all values |

**arguments Object Structure:**
```
arguments = {
    0: 1,
    1: 123,
    2: 500,
    3: 115,
    4: 44,
    5: 88,
    length: 6,
    callee: [function reference]
}
```

### 7.3 arguments vs Rest Parameters

| Feature | arguments | Rest Parameters |
|---------|-----------|-----------------|
| Type | Array-like object | True Array |
| Array methods | ❌ Not available | ✅ Available |
| Arrow functions | ❌ Not available | ✅ Available |
| Named binding | No | Yes (you name the parameter) |
| Additional properties | Yes (callee, etc.) | No |

**Example: Array Methods**
```javascript
// arguments - need to convert
function withArguments() {
    // arguments.map(x => x * 2);  // ❌ Error!
    var arr = Array.from(arguments);  // Convert first
    return arr.map(x => x * 2);  // ✅ Works
}

// rest parameters - works directly
function withRest(...args) {
    return args.map(x => x * 2);  // ✅ Works directly
}
```

---

## 8. Spread Operator

### 8.1 Definition
The spread operator (`...`) allows an iterable (like an array) to be expanded in places where zero or more arguments or elements are expected.

### 8.2 Spread vs Rest

| Spread | Rest |
|--------|------|
| Expands an array into elements | Collects elements into an array |
| Used in function calls, array literals | Used in function parameters |
| `myFunction(...args)` | `function myFn(...args)` |

### 8.3 Spread in Function Calls

```javascript
<script>
"use strict";
function myFunction(x, y, z) {
    return x + y + z;
}

var args = [0, 1, 2];
var r = myFunction(...args);  // Spreads array into arguments
console.log(r);  // 3
</script>
```

**What Happens:**
```
args = [0, 1, 2]
myFunction(...args) equivalent to myFunction(0, 1, 2)
x = 0, y = 1, z = 2
Result = 0 + 1 + 2 = 3
```

### 8.4 Spread with Other Arguments

```javascript
<script>
"use strict";
function myFunction(v, w, x, y, z) { 
    return v + w + x + y + z;
}

var args = [0, 1];
var result = myFunction(-1, ...args, 2, 3);
console.log(result);  // 5
</script>
```

**Distribution:**
```
v = -1    (regular argument)
w = 0     (from spread)
x = 1     (from spread)
y = 2     (regular argument)
z = 3     (regular argument)
Result = -1 + 0 + 1 + 2 + 3 = 5
```

### 8.5 Spread for Array Copying

```javascript
var arr1 = [1, 2, 3];
var arr2 = [...arr1];  // Creates a new array
arr2.push(4);

console.log(arr1);  // [1, 2, 3] (unchanged)
console.log(arr2);  // [1, 2, 3, 4]
```

---

## 9. Scope in JavaScript

### 9.1 Types of Scope

| Scope Type | Description | Example |
|------------|-------------|---------|
| **Global** | Available everywhere | Variables outside functions |
| **Function** | Available only within function | Variables with `var` inside function |
| **Block** | Available only within `{}` | Variables with `let`/`const` inside `{}` |

### 9.2 Global vs Local Variables

```javascript
<script>
    var x;              // Global variable
    
    function call() {
        a = 5;          // Also global (no var keyword)! BAD!
        var c = 7;      // Local variable
        document.write("welcome");
        x = 9;          // Modifies global x
    }
    
    // document.write(a);  // Error: a not defined yet
    call();
    document.write(a);     // 5 (now defined after function call)
    // document.write(c);  // Error: c is not defined (out of scope)
    document.write(x);     // 9
</script>
```

**Memory Diagram:**
```
GLOBAL MEMORY:          FUNCTION MEMORY (after call):
┌─────────┐            ┌─────────┐
│ x = undefined │      │ c = 7   │ ← Local, destroyed after function
│ a = 5   │ ← Added by function  
│ x = 9   │ ← Modified │
└─────────┘            └─────────┘
```

### 9.3 The Danger of Undeclared Variables

Without `'use strict'`:
```javascript
function person(nm, mks) {
    alert(this);      // Shows Window object
    this.name = nm;   // Adds to window!
    this.marks = mks; // Adds to window!
}

person("raj", 30);    // Called without 'new'
document.write(window.name);  // "raj" - added to window!
```

With `'use strict'`:
```javascript
"use strict"
function person(nm, mks) {
    alert(this);      // undefined
    this.name = nm;   // TypeError: Cannot set property 'name' of undefined
}

person("raj", 30);    // Error!
```

### 9.4 Variable Shadowing

```javascript
var x = 10;  // Global

function test() {
    var x = 20;  // Local, shadows global
    console.log(x);  // 20
}

test();
console.log(x);  // 10 (global unchanged)
```

---

## 10. Quick Reference

### 10.1 Function Syntax Summary

```javascript
// Function Declaration
function name(params) { return value; }

// Function Expression
var name = function(params) { return value; };

// Arrow Function (ES6)
var name = (params) => expression;
var name = (params) => { return value; };

// With Default Parameter
function name(a, b = 1) { }

// With Rest Parameter
function name(...args) { }
```

### 10.2 Parameter Features Comparison

| Feature | Syntax | Purpose |
|---------|--------|---------|
| Regular | `function(a, b)` | Fixed number of parameters |
| Default | `function(a, b = 1)` | Provide fallback values |
| Rest | `function(...args)` | Accept variable arguments |
| Spread | `fn(...array)` | Expand array into arguments |

### 10.3 Scope Rules

| Keyword | Scope | Hoisted | Re-declare |
|---------|-------|---------|------------|
| `var` | Function | Yes (undefined) | Yes |
| `let` | Block | Yes (TDZ) | No |
| `const` | Block | Yes (TDZ) | No |
| No keyword | Global | N/A | Creates global |

---

## 11. Interview Questions

### Q1: What is the difference between function declaration and function expression?
**Answer**:
- **Declaration**: `function name() {}` - Hoisted, can be called before declaration
- **Expression**: `var name = function() {}` - Not hoisted, cannot be called before assignment

### Q2: What happens if you pass fewer arguments than parameters?
**Answer**: The unprovided parameters receive `undefined`. JavaScript does not throw an error for missing arguments.

### Q3: What is the difference between rest parameters and the arguments object?
**Answer**:
- Rest parameters are a true array with all array methods available
- arguments object is array-like but lacks array methods
- Rest parameters work in arrow functions; arguments does not
- Rest parameters can be named; arguments is always called `arguments`

### Q4: What is the spread operator used for?
**Answer**: The spread operator expands an iterable (array/string) into individual elements. It's used for:
- Passing array elements as function arguments
- Copying arrays
- Merging arrays
- Converting iterables to arrays

### Q5: Explain variable scope in JavaScript.
**Answer**: JavaScript has three types of scope:
- **Global scope**: Variables declared outside functions
- **Function scope**: Variables declared with `var` inside functions
- **Block scope**: Variables declared with `let`/`const` inside `{}`

### Q6: What is the default return value of a function?
**Answer**: If a function doesn't have a `return` statement or has an empty `return`, it returns `undefined`.

### Q7: Can you have multiple rest parameters in a function?
**Answer**: No. A function can have only one rest parameter, and it must be the last parameter in the list.

---

## Navigation

← Previous: [02_Data_Types_and_Variables.md](./02_Data_Types_and_Variables.md) | Next: [04_Anonymous_Functions_and_IIFE.md](./04_Anonymous_Functions_and_IIFE.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 01*
