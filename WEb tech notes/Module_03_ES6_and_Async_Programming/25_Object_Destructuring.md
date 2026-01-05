# Object Destructuring in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Object Destructuring](#2-object-destructuring)
3. [Array Destructuring](#3-array-destructuring)
4. [Default Values](#4-default-values)
5. [Renaming Variables](#5-renaming-variables)
6. [Nested Destructuring](#6-nested-destructuring)
7. [Function Parameters](#7-function-parameters)
8. [Quick Reference](#8-quick-reference)
9. [Interview Questions](#9-interview-questions)

---

## 1. Introduction

### 1.1 What is Destructuring?
**Destructuring** is an ES6 feature that allows you to extract values from objects and arrays into distinct variables. It breaks a data structure into smaller parts.

### 1.2 Why Destructuring?

**Without Destructuring (ES5):**
```javascript
let options = { repeat: true, save: false };

// Extract data manually
let repeat = options.repeat;
let save = options.save;
```

**With Destructuring (ES6):**
```javascript
let options = { repeat: true, save: false };

// Extract data with destructuring
let { repeat, save } = options;
```

---

## 2. Object Destructuring

### 2.1 Basic Syntax

```javascript
let node = { type: "Identifier", name: "foo" };

let { type, name } = node;

console.log(type);  // "Identifier"
console.log(name);  // "foo"
```

### 2.2 Memory Diagram

```
node object:
┌─────────────────────────┐
│ type: "Identifier"      │
│ name: "foo"            │
└─────────────────────────┘
          ↓
   destructuring
          ↓
┌──────────┐  ┌──────────┐
│ type     │  │ name     │
│"Identifier"  │"foo"    │
└──────────┘  └──────────┘
```

### 2.3 Important: Initializer Required

```javascript
// ERROR! Must have initializer
var { type, name };      // Syntax error!
let { type, name };      // Syntax error!
const { type, name };    // Syntax error!

// CORRECT
let { type, name } = node;
```

### 2.4 Destructuring Assignment

```javascript
let node = { type: "Identifier", name: "foo" };
let type = "Literal";
let name = 5;

// Reassign using destructuring
// NOTE: Parentheses required!
({ type, name } = node);

console.log(type);  // "Identifier"
console.log(name);  // "foo"
```

**Why parentheses?** Opening brace `{` would be interpreted as a block statement. Parentheses force it to be an expression.

---

## 3. Array Destructuring

### 3.1 Basic Syntax

```javascript
let colors = ["red", "green", "blue"];

let [first, second, third] = colors;

console.log(first);   // "red"
console.log(second);  // "green"
console.log(third);   // "blue"
```

### 3.2 Skip Elements

```javascript
let colors = ["red", "green", "blue"];

let [, , third] = colors;

console.log(third);  // "blue"
```

### 3.3 Swap Variables

```javascript
let a = 1;
let b = 2;

// Swap without temp variable!
[a, b] = [b, a];

console.log(a);  // 2
console.log(b);  // 1
```

### 3.4 Rest Pattern

```javascript
let colors = ["red", "green", "blue", "yellow"];

let [first, ...rest] = colors;

console.log(first);  // "red"
console.log(rest);   // ["green", "blue", "yellow"]
```

---

## 4. Default Values

### 4.1 Missing Properties

```javascript
let node = { type: "Identifier", name: "foo" };

let { type, name, value } = node;

console.log(type);   // "Identifier"
console.log(name);   // "foo"
console.log(value);  // undefined (doesn't exist)
```

### 4.2 Setting Defaults

```javascript
let node = { type: "Identifier", name: "foo" };

let { type, name, value = true } = node;

console.log(type);   // "Identifier"
console.log(name);   // "foo"
console.log(value);  // true (default value)
```

### 4.3 Array Defaults

```javascript
let colors = ["red"];

let [first, second = "green"] = colors;

console.log(first);   // "red"
console.log(second);  // "green" (default)
```

---

## 5. Renaming Variables

### 5.1 Different Variable Names

```javascript
let node = { type: "Identifier", name: "foo" };

let { type: localType, name: localName } = node;

console.log(localType);   // "Identifier"
console.log(localName);   // "foo"
console.log(type);        // Error! type is not defined
```

**Syntax:** `{ sourceProperty: targetVariable }`

### 5.2 Renaming with Defaults

```javascript
let node = { type: "Identifier" };

let { type: localType, name: localName = "bar" } = node;

console.log(localType);   // "Identifier"
console.log(localName);   // "bar" (default)
```

---

## 6. Nested Destructuring

### 6.1 Nested Objects

```javascript
let node = {
    type: "Identifier",
    name: "foo",
    loc: {
        start: {
            line: 1,
            column: 1
        },
        end: {
            line: 1,
            column: 4
        }
    }
};

let { loc: { start } } = node;

console.log(start.line);    // 1
console.log(start.column);  // 1
```

### 6.2 Deep Nested with Renaming

```javascript
let { loc: { start: localStart } } = node;

console.log(localStart.line);    // 1
console.log(localStart.column);  // 1
```

### 6.3 Extract Specific Value

```javascript
let { loc: { start: { line } } } = node;

console.log(line);  // 1
```

### 6.4 Nested Arrays

```javascript
let colors = ["red", ["green", "lightgreen"], "blue"];

let [firstColor, [secondColor]] = colors;

console.log(firstColor);   // "red"
console.log(secondColor);  // "green"
```

---

## 7. Function Parameters

### 7.1 Destructuring in Parameters

```javascript
let node = { type: "Identifier", name: "foo" };

function outputInfo({ type, name }) {
    console.log(type);  // "Identifier"
    console.log(name);  // "foo"
}

outputInfo(node);
```

### 7.2 With Defaults

```javascript
function setCookie(name, value, { secure = false, expires = 3600 } = {}) {
    console.log(name, value, secure, expires);
}

setCookie("user", "John");
// "user", "John", false, 3600

setCookie("user", "John", { secure: true });
// "user", "John", true, 3600
```

### 7.3 Destructuring Assignment Return

```javascript
let node = { type: "Identifier", name: "foo" };
let type = "Literal";
let name = 5;

function outputInfo(value) {
    console.log(value === node);  // true
}

// Destructuring expression returns right-hand side
outputInfo({ type, name } = node);

console.log(type);  // "Identifier"
console.log(name);  // "foo"
```

---

## 8. Quick Reference

### 8.1 Object Destructuring

```javascript
// Basic
let { a, b } = obj;

// With defaults
let { a = 1, b = 2 } = obj;

// Rename
let { a: x, b: y } = obj;

// Rename with defaults
let { a: x = 1, b: y = 2 } = obj;

// Nested
let { prop: { nested } } = obj;
```

### 8.2 Array Destructuring

```javascript
// Basic
let [a, b] = arr;

// Skip elements
let [, , c] = arr;

// With defaults
let [a = 1, b = 2] = arr;

// Rest pattern
let [first, ...rest] = arr;

// Swap
[a, b] = [b, a];
```

### 8.3 Common Patterns

```javascript
// Import specific methods
const { readFile, writeFile } = require('fs');

// React hooks (conceptual)
const [state, setState] = useState(initialValue);

// API response
const { data, error, loading } = response;

// Config options
function configure({ host = 'localhost', port = 8080 } = {}) {
    // ...
}
```

---

## 9. Interview Questions

### Q1: What is destructuring?
**Answer**: Destructuring is an ES6 feature that unpacks values from arrays or properties from objects into distinct variables, making code more concise and readable.

### Q2: Why do we need parentheses for object destructuring assignment?
**Answer**: Without parentheses, the opening brace `{` would be interpreted as a block statement. Parentheses force JavaScript to evaluate it as an expression.
```javascript
({ a, b } = obj);  // Correct
{ a, b } = obj;    // Error - block statement
```

### Q3: How do you provide default values in destructuring?
**Answer**: Use the `=` operator after the variable name:
```javascript
let { name = "default" } = obj;
let [first = 1, second = 2] = arr;
```

### Q4: How do you rename a variable during destructuring?
**Answer**: Use colon syntax `sourceProperty: newName`:
```javascript
let { oldName: newName } = obj;
```

### Q5: How do you swap two variables using destructuring?
**Answer**:
```javascript
let a = 1, b = 2;
[a, b] = [b, a];
// Now a = 2, b = 1
```

### Q6: What happens if you destructure a property that doesn't exist?
**Answer**: The variable is assigned `undefined`. Use default values to handle this:
```javascript
let { missing } = {};         // undefined
let { missing = 10 } = {};    // 10
```

---

## Navigation

← Previous: [24_LocalStorage_and_SessionStorage.md](./24_LocalStorage_and_SessionStorage.md) | Next: [26_Promises.md](./26_Promises.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 06*
