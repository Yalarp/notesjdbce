# Anonymous Functions and IIFE in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Anonymous Functions](#2-anonymous-functions)
3. [Function Expressions](#3-function-expressions)
4. [Passing Functions as Arguments (Callbacks)](#4-passing-functions-as-arguments-callbacks)
5. [IIFE (Immediately Invoked Function Expression)](#5-iife-immediately-invoked-function-expression)
6. [Arrow Functions](#6-arrow-functions)
7. [Arrow Functions in Array Methods](#7-arrow-functions-in-array-methods)
8. [Quick Reference](#8-quick-reference)
9. [Interview Questions](#9-interview-questions)

---

## 1. Introduction

### 1.1 Definition
An **anonymous function** is a function that does not have a name. It is typically assigned to a variable or passed as an argument to another function.

### 1.2 Purpose
- **Callbacks**: Pass functionality to other functions
- **Encapsulation**: Create scope without polluting global namespace
- **One-time use**: Functions that don't need to be reused by name
- **Inline definitions**: Define behavior right where it's needed

### 1.3 Problem Solved
- Reduces global namespace pollution
- Enables functional programming patterns
- Makes code more concise and readable for simple operations

---

## 2. Anonymous Functions

### 2.1 Basic Syntax

```javascript
// Named function
function namedFunction() {
    return "I have a name";
}

// Anonymous function assigned to variable
var anonymousFunction = function() {
    return "I have no name";
};
```

### 2.2 Anonymous Function Example

```javascript
<script>
var go = function() {
    return "This is a String";
}

var testStr = go();      // testStr contains "This is a string"
document.write(testStr);

var testCopy = go;       // testCopy is a pointer to the function
var testing = testCopy(); // testing contains "This is a string"
document.write(testing);
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 1 | `var go = function()` | Assigns anonymous function to variable `go` |
| 2 | `return "This is a String"` | Function returns a string |
| 5 | `var testStr = go()` | Calls function, assigns return value to `testStr` |
| 6 | `document.write(testStr)` | Prints "This is a String" |
| 8 | `var testCopy = go` | Copies the function REFERENCE (no parentheses!) |
| 9 | `var testing = testCopy()` | Calls the function via the copied reference |
| 10 | `document.write(testing)` | Prints "This is a String" |

**Memory Diagram:**
```
┌────────────────────────────────────────────────────────┐
│ go ─────────────┐                                       │
│                 ↓                                       │
│              function() {                               │
│                  return "This is a String";             │
│              }                                          │
│                 ↑                                       │
│ testCopy ───────┘                                       │
│                                                         │
│ testStr = "This is a String"                            │
│ testing = "This is a String"                            │
└────────────────────────────────────────────────────────┘
```

### 2.3 Key Concept: Reference vs Call

| Syntax | Meaning | Result |
|--------|---------|--------|
| `go` | Reference to the function object | The function itself |
| `go()` | Call/execute the function | The return value |

```javascript
document.write(go);    // Prints: function(){ return "This is a String"; }
document.write(go());  // Prints: This is a String
```

---

## 3. Function Expressions

### 3.1 Definition
A function expression is when a function is assigned to a variable. The function can be named or anonymous.

### 3.2 Named vs Anonymous Function Expressions

```javascript
// Anonymous function expression
var greet1 = function() {
    return "Hello";
};

// Named function expression
var greet2 = function sayHello() {
    return "Hello";
};
```

### 3.3 Differences from Function Declarations

| Aspect | Function Declaration | Function Expression |
|--------|---------------------|---------------------|
| Hoisting | ✅ Fully hoisted | ❌ Variable hoisted, not function |
| Named required | ✅ Yes | ❌ No (can be anonymous) |
| Call before declaration | ✅ Works | ❌ Error |

```javascript
// This works (declaration is hoisted)
console.log(declared());  // "I work!"
function declared() { return "I work!"; }

// This fails (expression not hoisted)
console.log(expressed());  // TypeError: expressed is not a function
var expressed = function() { return "I fail!"; };
```

---

## 4. Passing Functions as Arguments (Callbacks)

### 4.1 What is a Callback?
A callback is a function passed as an argument to another function, to be executed later.

### 4.2 Passing Named Functions

```javascript
<script>
let s = function(a) {
    return a * a;
}

let c = function(a) {
    return a * a * a;
}

var go = function(w, d) {
    alert(w(d));
}

go(c, 2);   // Alerts 8 (2*2*2)
go(s, 3);   // Alerts 9 (3*3)
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 1-3 | `let s = function(a)` | `s` is a function that squares |
| 5-7 | `let c = function(a)` | `c` is a function that cubes |
| 9-11 | `var go = function(w, d)` | `go` takes a function `w` and a value `d` |
| 10 | `alert(w(d))` | Calls `w` with argument `d` |
| 13 | `go(c, 2)` | Passes cube function and 2 |
| 14 | `go(s, 3)` | Passes square function and 3 |

**Execution Flow for `go(c, 2)`:**
```
1. go(c, 2) is called
2. w = c (reference to cube function)
3. d = 2
4. w(d) = c(2) = 2 * 2 * 2 = 8
5. alert(8)
```

**Memory Diagram:**
```
s ─────→ function(a) { return a * a; }
c ─────→ function(a) { return a * a * a; }
go ────→ function(w, d) { alert(w(d)); }

go(c, 2):
  w ────→ [same as c] ────→ function(a) { return a * a * a; }
  d = 2
```

### 4.3 Passing Anonymous Functions Directly

```javascript
<script>
var go = function(w) {
    alert(w(5));
}

go(function(a) {
    return a * a * a;
});  // Alerts 125 (5*5*5)
</script>
```

**Key Point**: The anonymous function is passed directly as an argument without being assigned to a variable first.

### 4.4 Callback Pattern Example

```javascript
<script>
function mydata(param1, param2, callback) {
    alert('Started learning at.\n\nIt has: ' + param1 + ', ' + param2);
    callback();  // Execute the callback
}

mydata('vita', 'DAC', function() {
    alert('Finished learning DAC');
});
</script>
```

**Execution Flow:**
```
1. mydata('vita', 'DAC', [callback function]) is called
2. Alert: "Started learning at.\n\nIt has: vita, DAC"
3. callback() is executed
4. Alert: "Finished learning DAC"
```

---

## 5. IIFE (Immediately Invoked Function Expression)

### 5.1 Definition
An IIFE is a function that is defined and executed immediately. It runs as soon as it is defined.

### 5.2 Basic Syntax

```javascript
(function() {
    // Code here runs immediately
})();
```

**Anatomy of an IIFE:**
```
(function() { ... })();
 ↑                   ↑
 |                   |
 Wrap in parentheses  Invoke immediately
 (to make it expression)
```

### 5.3 Basic IIFE Example

```javascript
<script>
(function() {
    alert("This is a String");
})();
</script>
```

**What Happens:**
1. Browser parses the script
2. Encounters the IIFE
3. Immediately executes the function
4. Alert shows "This is a String"

### 5.4 IIFE with Parameters

```javascript
<script>
var r = (function(a) {
    return a * a;
}(5));

document.write(r);  // 25
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 1 | `var r = (function(a)` | Start of IIFE assigned to `r` |
| 2 | `return a * a;` | Function returns square of `a` |
| 3 | `}(5));` | Immediately invoke with argument 5 |
| 5 | `document.write(r)` | Prints 25 |

### 5.5 Comparing IIFE with Regular Function

| Regular Function | IIFE |
|-----------------|------|
| `var go = function(a) { return a*a; }` | `(function(a) { return a*a; }(5))` |
| `go(5)` → 25 | Returns 25 immediately |
| Function persists | Function executes and is gone |
| Callable multiple times | Executes only once |

### 5.6 Why Use IIFE?

1. **Avoid Global Pollution**
```javascript
(function() {
    var privateVar = "I'm private";
    // privateVar is not accessible outside
})();
// privateVar is undefined here
```

2. **Create a Fresh Scope**
```javascript
for (var i = 0; i < 3; i++) {
    (function(j) {
        setTimeout(function() {
            console.log(j);  // 0, 1, 2 (not 3, 3, 3)
        }, 1000);
    })(i);
}
```

3. **Module Pattern**
```javascript
var module = (function() {
    var privateVar = 10;
    
    return {
        getPrivate: function() { return privateVar; },
        setPrivate: function(val) { privateVar = val; }
    };
})();

module.getPrivate();  // 10
```

### 5.7 IIFE in jQuery

```javascript
// jQuery library structure
(function(window, undefined) {
    // jQuery code here
})(window);
```

This pattern:
- Creates a private scope for jQuery
- Prevents conflicts with other libraries
- Ensures `undefined` is truly undefined

---

## 6. Arrow Functions

### 6.1 Definition
Arrow functions are a concise syntax for writing functions, introduced in ES6. They use the `=>` syntax.

### 6.2 Syntax Variations

```javascript
// No parameters
var getName = () => "TSYS";

// Single parameter (parentheses optional)
var reflect = value => value;

// Multiple parameters
var sum = (num1, num2) => num1 + num2;

// Multiple statements (need braces and return)
var getItem = id => {
    let name = "Temp";
    return { id: id, name: name };
};

// Returning object literal (wrap in parentheses)
var getTempItem = id => ({ id: id, name: "Temp" });
```

### 6.3 Comparison: Regular vs Arrow Functions

| Regular Function | Arrow Function |
|-----------------|----------------|
| `var reflect = function(value) { return value; }` | `var reflect = value => value;` |
| `var sum = function(num1, num2) { return num1 + num2; }` | `var sum = (num1, num2) => num1 + num2;` |
| `var getName = function() { return "TSYS"; }` | `var getName = () => "TSYS";` |

### 6.4 Detailed Examples

**Example 1: Single Parameter, Single Expression**
```javascript
var reflect1 = value => value;
document.write(reflect1(67));  // 67
```

**Example 2: Even/Odd Check**
```javascript
let r = n => n % 2 == 0;
let result = r(4);  // true

if (result == true)
    console.log("Number is even");
```

**Example 3: Multiple Statements**
```javascript
let r = n => {
    if (n % 2 == 0)
        return true;
    else
        return false;
};
```

**Example 4: Factorial**
```javascript
let result = (n) => {
    let f = 1;
    for (let i = 2; i <= n; i++)
        f = f * i;
    return f;
}

let ans = result(5);
console.log(ans);  // 120
```

**Example 5: Cube Function**
```javascript
let cube = n => n * n * n;
let ans = cube(2);
console.log(ans);  // 8
```

**Example 6: Rest Parameters with Arrow**
```javascript
var sumFunction = (...arg) => {
    let sum = 0;
    for (let i = 0; i < arg.length; i++)
        sum = sum + arg[i];
    return sum;
};

let result = sumFunction(5, 6, 3, 2, 1);
console.log(result);  // 17
```

### 6.5 Returning Object Literals

**Problem**: Curly braces are interpreted as function body, not object literal.

```javascript
// ❌ Wrong - {} is interpreted as function body
var getItem = id => { id: id, name: "Temp" };  // Syntax error or undefined

// ✅ Correct - wrap in parentheses
var getTempItem = id => ({ id: id, name: "Temp" });
let obj = getTempItem(5);
document.write(obj.id);  // 5
```

---

## 7. Arrow Functions in Array Methods

### 7.1 Array.sort() with Arrow Functions

**Without Arrow Function:**
```javascript
var values = [6, 2, 4, 5, 1, 9];
var result = values.sort(function(a, b) {
    return a - b;
});
document.write(result);  // [1, 2, 4, 5, 6, 9]
```

**With Arrow Function:**
```javascript
var values = [6, 2, 4, 5, 1, 9];
var result = values.sort((a, b) => a - b);
document.write(result);  // [1, 2, 4, 5, 6, 9]
```

**How sort() Works:**
- If callback returns negative: `a` comes before `b`
- If callback returns positive: `b` comes before `a`
- If callback returns 0: order unchanged

```
a = 6, b = 2
a - b = 6 - 2 = 4 (positive)
Therefore: b (2) comes before a (6)
```

### 7.2 Array.map() with Arrow Functions

```javascript
const array1 = [1, 4, 9, 16];

// Pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// Expected output: Array [2, 8, 18, 32]
```

**How map() Works:**
1. Iterates through each element
2. Calls the callback for each element
3. Creates new array with return values

```
Original: [1, 4, 9, 16]
Callback: x => x * 2
         1 * 2 = 2
         4 * 2 = 8
         9 * 2 = 18
         16 * 2 = 32
Result: [2, 8, 18, 32]
```

### 7.3 Other Common Array Methods with Arrow Functions

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

// filter - keep elements that pass test
const evens = numbers.filter(n => n % 2 === 0);  // [2, 4, 6]

// find - get first matching element
const firstEven = numbers.find(n => n % 2 === 0);  // 2

// some - check if any pass test
const hasEven = numbers.some(n => n % 2 === 0);  // true

// every - check if all pass test
const allEven = numbers.every(n => n % 2 === 0);  // false

// reduce - accumulate to single value
const sum = numbers.reduce((acc, n) => acc + n, 0);  // 21

// forEach - execute for each
numbers.forEach(n => console.log(n));  // logs each number
```

---

## 8. Quick Reference

### 8.1 Anonymous Function Patterns

| Pattern | Syntax |
|---------|--------|
| Basic | `var fn = function() { };` |
| With params | `var fn = function(a, b) { };` |
| Arrow (no params) | `var fn = () => expression;` |
| Arrow (one param) | `var fn = x => expression;` |
| Arrow (multiple params) | `var fn = (a, b) => expression;` |
| Arrow (with body) | `var fn = (a, b) => { return result; };` |

### 8.2 IIFE Patterns

```javascript
// Standard IIFE
(function() {
    // code
})();

// IIFE with parameters
(function(arg) {
    // code using arg
})(value);

// IIFE with return
var result = (function() {
    return value;
})();

// Arrow function IIFE
(() => {
    // code
})();
```

### 8.3 Arrow Function Rules

| Rule | Example |
|------|---------|
| Single param: parentheses optional | `x => x * 2` |
| No params: parentheses required | `() => "hello"` |
| Multiple params: parentheses required | `(a, b) => a + b` |
| Single expression: implicit return | `x => x * 2` |
| Multiple statements: explicit return | `x => { return x * 2; }` |
| Return object: wrap in parentheses | `x => ({ id: x })` |

---

## 9. Interview Questions

### Q1: What is an anonymous function?
**Answer**: An anonymous function is a function without a name. It's typically assigned to a variable or passed as an argument. Example: `var fn = function() { return "hello"; };`

### Q2: What is an IIFE and why is it used?
**Answer**: IIFE (Immediately Invoked Function Expression) is a function that runs immediately after definition. It's used to:
- Create a private scope
- Avoid polluting the global namespace
- Initialize data immediately
- Implement the module pattern

Syntax: `(function() { /* code */ })();`

### Q3: What is the difference between `fn` and `fn()`?
**Answer**: 
- `fn` is a reference to the function object itself
- `fn()` calls/executes the function and returns the result

### Q4: What is a callback function?
**Answer**: A callback is a function passed as an argument to another function, to be executed at a later time. It's commonly used for asynchronous operations and event handling.

### Q5: What are the differences between arrow functions and regular functions?
**Answer**:
- Arrow functions have shorter syntax
- Arrow functions don't have their own `this` binding
- Arrow functions don't have `arguments` object
- Arrow functions cannot be used as constructors
- Arrow functions cannot be used as generators

### Q6: How do you return an object literal from an arrow function?
**Answer**: Wrap the object in parentheses to distinguish it from a function body:
```javascript
var getObj = id => ({ id: id, name: "Test" });
```

### Q7: What is the purpose of wrapping a function in parentheses in an IIFE?
**Answer**: The parentheses convert the function declaration into a function expression. Without them, JavaScript would try to parse it as a function declaration, which cannot be immediately invoked and would cause a syntax error.

---

## Navigation

← Previous: [03_Functions_and_Scope.md](./03_Functions_and_Scope.md) | Next: [05_Objects_Basics.md](./05_Objects_Basics.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 01*
