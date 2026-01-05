# Data Types and Variables in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Variables: var, let, and const](#2-variables-var-let-and-const)
3. [Data Types](#3-data-types)
4. [Type Checking with typeof](#4-type-checking-with-typeof)
5. [Undefined and Null](#5-undefined-and-null)
6. [Type Coercion and Conversion](#6-type-coercion-and-conversion)
7. [Variable Hoisting](#7-variable-hoisting)
8. [let vs var: Scope Differences](#8-let-vs-var-scope-differences)
9. [const: Constant Declarations](#9-const-constant-declarations)
10. [Quick Reference](#10-quick-reference)
11. [Interview Questions](#11-interview-questions)

---

## 1. Introduction

### 1.1 Definition
Variables are named containers that store data values. In JavaScript, variables are **dynamically typed**, meaning the type is determined at runtime based on the value assigned.

### 1.2 Purpose
- Store data for later use
- Reference and manipulate values
- Create readable, maintainable code

### 1.3 Problem Solved
Variables allow us to:
- Store user input
- Keep track of program state
- Avoid repeating literal values
- Create reusable calculations

---

## 2. Variables: var, let, and const

### 2.1 Overview of Declaration Keywords

| Keyword | Introduced | Scope | Hoisting | Re-declaration | Re-assignment |
|---------|------------|-------|----------|----------------|---------------|
| `var` | ES1 | Function/Global | Yes (undefined) | ✅ Yes | ✅ Yes |
| `let` | ES6 | Block | Yes (TDZ) | ❌ No | ✅ Yes |
| `const` | ES6 | Block | Yes (TDZ) | ❌ No | ❌ No |

### 2.2 Declaring Variables

**Syntax:**
```javascript
var variableName;           // Declaration (undefined)
var variableName = value;   // Declaration + Initialization

let variableName;           // Declaration (undefined)
let variableName = value;   // Declaration + Initialization

const CONSTANT_NAME = value; // Must initialize immediately
```

### 2.3 Example: Variable Declaration

```javascript
<script>
    var a;
    document.write(a + "<br/>");  // undefined
    
    let b;
    document.write(b + "<br/>");  // undefined
    
    const x = 2;
    document.write(x + "<br/>");  // 2
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 1 | `var a;` | Declares variable `a` without initialization |
| 2 | `document.write(a + "<br/>")` | Prints `undefined` because `a` has no value |
| 4 | `let b;` | Declares variable `b` without initialization |
| 5 | `document.write(b + "<br/>")` | Prints `undefined` because `b` has no value |
| 7 | `const x = 2;` | Declares constant `x` with value 2 (must initialize) |
| 8 | `document.write(x + "<br/>")` | Prints `2` |

**Key Points:**
- **Unassigned var/let**: Prints `undefined`
- **const without initialization**: Causes `SyntaxError: missing initialization`
- **Undeclared variable**: Causes `ReferenceError: variable is not defined`

### 2.4 Undeclared vs Uninitialized Variables

```javascript
// Declared but not initialized = undefined
var a;
document.write(a);  // undefined

// Undeclared but used = ReferenceError (with 'use strict')
document.write(z);  // ReferenceError: z is not defined

// Undeclared but assigned (without 'use strict') = Creates global
a = 5;              // Creates window.a = 5 (BAD PRACTICE!)
document.write(a);  // 5
```

> **Warning**: In JavaScript, you can assign to undeclared variables without error (in non-strict mode). This is DANGEROUS because typos create new variables instead of causing errors!

**Example of the Danger:**
```javascript
Fname = "VITA";
// Later, you meant to use Fname but typed:
document.write(Fnme);  // Fnme is undefined, not an error!
```

---

## 3. Data Types

### 3.1 Primitive Data Types

JavaScript has **7 primitive data types**:

| Type | Description | Example |
|------|-------------|---------|
| **Number** | All numeric values (integer and float) | `5`, `5.5`, `NaN`, `Infinity` |
| **String** | Text enclosed in quotes | `"hello"`, `'world'` |
| **Boolean** | Logical true or false | `true`, `false` |
| **Undefined** | Variable declared but not assigned | `undefined` |
| **Null** | Intentional absence of value | `null` |
| **Symbol** | Unique identifier (ES6) | `Symbol('id')` |
| **BigInt** | Large integers (ES2020) | `9007199254740991n` |

### 3.2 Non-Primitive Data Type

| Type | Description | Example |
|------|-------------|---------|
| **Object** | Collection of key-value pairs | `{name: "John", age: 30}` |

### 3.3 Example: Data Types in Action

```javascript
<script>
    var a = 5;
    document.write(typeof(a));     // number
    
    var aa = 5.5;
    document.write(typeof(aa));    // number
    
    var b = "hello";
    document.write(typeof(b));     // string
    
    var c = 'h';
    document.write(typeof(c));     // string
    
    var p = true;
    document.write(typeof(p));     // boolean
    
    var y;
    document.write(y);             // undefined
    
    var x = 2;
    document.write(y + 2);         // NaN
    
    var str = "hi";
    document.write(x + 2);         // 4
    document.write(str + 2);       // hi2
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 1 | `var a = 5` | Assigns integer 5 to `a` |
| 2 | `typeof(a)` | Returns `"number"` (integers are numbers) |
| 4 | `var aa = 5.5` | Assigns float 5.5 to `aa` |
| 5 | `typeof(aa)` | Returns `"number"` (floats are also numbers) |
| 7 | `var b = "hello"` | Assigns string "hello" to `b` |
| 8 | `typeof(b)` | Returns `"string"` |
| 10 | `var c = 'h'` | Assigns single character to `c` |
| 11 | `typeof(c)` | Returns `"string"` (no char type in JS!) |
| 13 | `var p = true` | Assigns boolean to `p` |
| 14 | `typeof(p)` | Returns `"boolean"` |
| 16 | `var y;` | Declares `y` without value |
| 17 | `document.write(y)` | Prints `undefined` |
| 20 | `document.write(y + 2)` | Prints `NaN` (undefined + number = NaN) |
| 23 | `document.write(x + 2)` | Prints `4` (2 + 2 = 4, number addition) |
| 24 | `document.write(str + 2)` | Prints `"hi2"` (string + number = concatenation) |

**Key Observations:**
- JavaScript has **NO separate char type** - single characters are strings
- JavaScript has **ONE number type** - handles both integers and floats
- **undefined + number = NaN** (Not a Number)
- **string + number = string concatenation** (+ is overloaded!)

---

## 4. Type Checking with typeof

### 4.1 The typeof Operator

The `typeof` operator returns a string indicating the type of the operand.

**Syntax:**
```javascript
typeof operand
typeof(operand)  // Parentheses are optional
```

### 4.2 typeof Results

| Value | typeof Result |
|-------|---------------|
| `5` | `"number"` |
| `5.5` | `"number"` |
| `"hello"` | `"string"` |
| `true` | `"boolean"` |
| `undefined` | `"undefined"` |
| `null` | `"object"` ⚠️ (This is a known bug!) |
| `{}` | `"object"` |
| `[]` | `"object"` |
| `function(){}` | `"function"` |
| `NaN` | `"number"` ⚠️ |

### 4.3 Special Cases

```javascript
let no = null;
console.log(typeof no);  // "object" (historical bug in JavaScript!)

console.log(typeof NaN);  // "number" (NaN is still type "number")
```

> **Important**: `typeof null` returning `"object"` is a **known bug** in JavaScript that cannot be fixed for backward compatibility reasons.

---

## 5. Undefined and Null

### 5.1 Undefined

**Definition**: A variable that has been declared but not assigned a value.

```javascript
var x;
console.log(x);        // undefined
console.log(typeof x); // "undefined"
```

**When you get undefined:**
- Variable declared but not initialized
- Function parameter not passed
- Function with no return statement
- Accessing non-existent object property

### 5.2 Null

**Definition**: An intentional assignment indicating "no value" or "empty".

```javascript
let no = null;
console.log(no);        // null
console.log(typeof no); // "object" (this is a bug!)
```

### 5.3 Undefined vs Null

| Aspect | undefined | null |
|--------|-----------|------|
| **Meaning** | Value not assigned | Intentionally empty |
| **typeof** | `"undefined"` | `"object"` |
| **Assignment** | Automatic | Manual |
| **In math** | Becomes `NaN` | Becomes `0` |

```javascript
console.log(undefined + 5);  // NaN
console.log(null + 5);       // 5 (null converts to 0)
```

---

## 6. Type Coercion and Conversion

### 6.1 Automatic Type Coercion

JavaScript automatically converts types when operators are used with different types.

**Critical Example: The + Operator**

```javascript
var x = 5 + 7;       // 12, typeof x is number
var x = 5 + "7";     // "57", typeof x is string
var x = "5" + 7;     // "57", typeof x is string
var x = 5 - 7;       // -2, typeof x is number
var x = 5 - "7";     // -2, typeof x is number
var x = "5" - 7;     // -2, typeof x is number
var x = 5 - "y";     // NaN, typeof x is number
var x = "5" * "7";   // 35, typeof x is number
```

**Line-by-Line Explanation:**

| Expression | Result | Type | Explanation |
|------------|--------|------|-------------|
| `5 + 7` | `12` | number | Both numbers, addition |
| `5 + "7"` | `"57"` | string | String present, + becomes concatenation |
| `"5" + 7` | `"57"` | string | String first, + becomes concatenation |
| `5 - 7` | `-2` | number | Both numbers, subtraction |
| `5 - "7"` | `-2` | number | String "7" converted to number 7 |
| `"5" - 7` | `-2` | number | String "5" converted to number 5 |
| `5 - "y"` | `NaN` | number | "y" cannot be converted to number |
| `"5" * "7"` | `35` | number | * always does math, converts both |

**Critical Rule:**
> **If the FIRST operand is a string and the operator is +, then + acts as CONCATENATION, not addition!**

### 6.2 The + Operator is Overloaded

```javascript
var a = 5;
var b = 9;

document.write(a + b);              // 14 (addition)
document.write(a + b + " ans ");    // "14 ans" (add first, then concat)
document.write("ans=" + a + b);     // "ans=59" (concat all!)
document.write("ans=" + (a + b));   // "ans=14" (parentheses force addition first)
```

**Execution Flow:**

1. `a + b` → `5 + 9` → `14`
2. `a + b + " ans "` → `14 + " ans "` → `"14 ans"`
3. `"ans=" + a + b` → `"ans=" + 5` → `"ans=5" + 9` → `"ans=59"`
4. `"ans=" + (a + b)` → `"ans=" + 14` → `"ans=14"`

### 6.3 Explicit Type Conversion

| Function | Converts To | Example |
|----------|-------------|---------|
| `parseInt()` | Integer | `parseInt("5.7")` → `5` |
| `parseFloat()` | Float | `parseFloat("5.7")` → `5.7` |
| `Number()` | Number | `Number("5.7")` → `5.7` |
| `String()` | String | `String(5)` → `"5"` |
| `+ (unary)` | Number | `+"5"` → `5` |
| `.toString()` | String | `(5).toString()` → `"5"` |
| `.valueOf()` | Primitive | `objNum.valueOf()` → number |

---

## 7. Variable Hoisting

### 7.1 What is Hoisting?

Hoisting is JavaScript's behavior of moving declarations to the top of their scope during compilation.

### 7.2 How var is Hoisted

```javascript
console.log(x);  // undefined (not ReferenceError!)
var x = 5;
console.log(x);  // 5
```

**What JavaScript sees:**
```javascript
var x;            // Declaration hoisted
console.log(x);   // undefined
x = 5;            // Assignment stays
console.log(x);   // 5
```

### 7.3 How let and const are Hoisted

`let` and `const` are hoisted but NOT initialized. They exist in a **Temporal Dead Zone (TDZ)** until their declaration is executed.

```javascript
console.log(y);  // ReferenceError: Cannot access 'y' before initialization
let y = 5;
```

---

## 8. let vs var: Scope Differences

### 8.1 var: Function Scope

```javascript
for (var i = 1; i <= 3; i++) {
    document.write(i);  // 1, 2, 3
}
document.write(i);      // 4 (i is accessible outside loop!)
```

**Explanation:**
- `var` has **function scope** (or global if not in a function)
- The variable `i` is "hoisted" to the top of the enclosing function
- After the loop, `i` exists and equals 4

### 8.2 let: Block Scope

```javascript
for (let i = 1; i <= 3; i++) {
    document.write(i);  // 1, 2, 3
}
document.write(i);      // ReferenceError: i is not defined
```

**Explanation:**
- `let` has **block scope** (enclosed by `{}`)
- Variable `i` is destroyed when the block ends
- Accessing `i` outside the block causes an error

### 8.3 Re-declaration

```javascript
var a = 55;
var a = 99;  // No error with var
console.log(a);  // 99

let b = 55;
let b = 99;  // SyntaxError: redeclaration of let b
```

> **Best Practice**: **Always prefer `let` over `var`** because it prevents accidental redeclaration and has more predictable block scope.

---

## 9. const: Constant Declarations

### 9.1 Basic Rules

```javascript
// Valid constant
const MAX_ITEMS = 30;

// Syntax error: missing initialization
const NAME;  // SyntaxError!

// Syntax error: cannot reassign
const NAME = "VITA";
NAME = "CDAC";  // TypeError: Assignment to constant variable
```

### 9.2 const with Objects and Arrays

**Important**: `const` prevents **reassignment**, NOT **mutation**!

```javascript
const MY_OBJECT = {'key': 'value'};

// ❌ Reassigning the object throws error
MY_OBJECT = {'OTHER_KEY': 'value'};  // TypeError!

// ✅ Modifying properties is allowed
MY_OBJECT.key = 'otherValue';  // Works!
MY_OBJECT.newKey = 'newValue'; // Works!
```

```javascript
const MY_ARRAY = [];

// ✅ Adding elements is allowed
MY_ARRAY.push('A');  // ['A']
MY_ARRAY.push('B');  // ['A', 'B']

// ❌ Reassigning the array throws error
MY_ARRAY = ['C'];  // TypeError!
```

**Diagram: const Behavior**
```
const obj ----> { key: 'value' }
                      ↓
                Changes allowed to properties
                      ↓
                { key: 'otherValue', newKey: 'newValue' }

const obj ---X--> { OTHER_KEY: 'value' }
                  ↑
                  Reassignment NOT allowed
```

### 9.3 Making Objects Immutable

Use `Object.freeze()` to prevent modifications:

```javascript
const MY_OBJECT = {'key': 'value'};
Object.freeze(MY_OBJECT);

MY_OBJECT.key = 'newValue';  // Silently fails (or throws in strict mode)
console.log(MY_OBJECT.key);  // 'value' (unchanged)
```

### 9.4 const Scope

Like `let`, `const` has **block scope**:

```javascript
if (true) {
    const MAX_ITEMS = 5;
    console.log(MAX_ITEMS);  // 5
}
console.log(MAX_ITEMS);  // ReferenceError: MAX_ITEMS is not defined
```

---

## 10. Quick Reference

### 10.1 Variable Declaration Comparison

| Feature | var | let | const |
|---------|-----|-----|-------|
| Scope | Function | Block | Block |
| Hoisting | Yes (undefined) | Yes (TDZ) | Yes (TDZ) |
| Re-declaration | ✅ Allowed | ❌ Error | ❌ Error |
| Re-assignment | ✅ Allowed | ✅ Allowed | ❌ Error |
| Initialization | Optional | Optional | Required |

### 10.2 Data Types Summary

| Type | Example | typeof |
|------|---------|--------|
| Number | `42`, `3.14` | `"number"` |
| String | `"hello"` | `"string"` |
| Boolean | `true` | `"boolean"` |
| Undefined | `undefined` | `"undefined"` |
| Null | `null` | `"object"` |
| Object | `{a: 1}` | `"object"` |
| Array | `[1, 2]` | `"object"` |
| Function | `function(){}` | `"function"` |

### 10.3 Type Coercion Rules

| Expression | Result | Rule |
|------------|--------|------|
| string + any | string | Concatenation |
| number - string | number | String converted to number |
| number * string | number | String converted to number |
| undefined + number | NaN | Undefined becomes NaN |
| null + number | number | Null becomes 0 |

---

## 11. Interview Questions

### Q1: What is the difference between var, let, and const?
**Answer**: 
- `var` has function scope, is hoisted with value `undefined`, and allows re-declaration
- `let` has block scope, is hoisted but in TDZ, and does NOT allow re-declaration
- `const` is like `let` but also prevents reassignment (must be initialized)

### Q2: What is hoisting in JavaScript?
**Answer**: Hoisting is JavaScript's behavior of moving variable and function declarations to the top of their containing scope during the compilation phase. With `var`, variables are initialized to `undefined`. With `let` and `const`, they remain in a Temporal Dead Zone until declaration.

### Q3: What is the Temporal Dead Zone (TDZ)?
**Answer**: The TDZ is the period between entering a scope where a `let` or `const` variable is declared and the actual declaration statement. Accessing the variable during TDZ throws a `ReferenceError`.

### Q4: Why does typeof null return "object"?
**Answer**: This is a historical bug in JavaScript from its first implementation. It was never fixed because doing so would break existing code. Null is actually a primitive value, not an object.

### Q5: What happens when you add a string and number in JavaScript?
**Answer**: The `+` operator is overloaded. When one operand is a string, `+` performs string concatenation instead of addition. For example, `"5" + 3` results in `"53"`.

### Q6: Can you modify properties of a const object?
**Answer**: Yes! `const` only prevents reassignment of the variable itself, not modification of the object's properties. To make an object truly immutable, use `Object.freeze()`.

### Q7: What is NaN and how do you check for it?
**Answer**: NaN stands for "Not a Number" and is the result of invalid math operations. Paradoxically, `typeof NaN` returns `"number"`. To check for NaN, use `isNaN()` or `Number.isNaN()` (latter is more accurate).

---

## Navigation

← Previous: [01_JavaScript_Introduction_and_Setup.md](./01_JavaScript_Introduction_and_Setup.md) | Next: [03_Functions_and_Scope.md](./03_Functions_and_Scope.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 01*
