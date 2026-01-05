# Modules and Exports in Node.js

## Table of Contents
1. [Introduction](#1-introduction)
2. [CommonJS Modules](#2-commonjs-modules)
3. [Exporting Modules](#3-exporting-modules)
4. [Importing Modules](#4-importing-modules)
5. [Built-in Modules](#5-built-in-modules)
6. [Module Patterns](#6-module-patterns)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 What is a Module?
A **module** is a reusable block of code whose existence does not impact other code. Node.js treats each file as a separate module.

### 1.2 Why Modules?
- Code organization
- Reusability
- Encapsulation
- Dependency management
- Maintainability

### 1.3 Module Types in Node.js

| Type | Description |
|------|-------------|
| Core Modules | Built-in (fs, http, path) |
| Local Modules | Your own modules |
| Third-party Modules | NPM packages |

---

## 2. CommonJS Modules

### 2.1 How Modules Work
Every file in Node.js is wrapped in a function:

```javascript
(function(exports, require, module, __filename, __dirname) {
    // Your module code
});
```

### 2.2 Module Wrapper Parameters

| Parameter | Description |
|-----------|-------------|
| `exports` | Reference to module.exports |
| `require` | Function to import modules |
| `module` | Reference to current module |
| `__filename` | Absolute path to file |
| `__dirname` | Directory path |

### 2.3 Example

```javascript
console.log(__filename);  // C:\Users\app\myModule.js
console.log(__dirname);   // C:\Users\app
```

---

## 3. Exporting Modules

### 3.1 Using module.exports

**Single Export:**
```javascript
// calculator.js
function add(a, b) {
    return a + b;
}

module.exports = add;
```

**Multiple Exports (Object):**
```javascript
// calculator.js
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

module.exports = {
    add: add,
    subtract: subtract
};

// Shorthand (ES6)
module.exports = { add, subtract };
```

### 3.2 Using exports

```javascript
// calculator.js
exports.add = function(a, b) {
    return a + b;
};

exports.subtract = function(a, b) {
    return a - b;
};
```

### 3.3 exports vs module.exports

```javascript
// exports is a reference to module.exports
exports === module.exports  // true (initially)

// This works
exports.add = function() {};

// This DOES NOT work (breaks reference)
exports = function() {};  // Wrong!

// This works
module.exports = function() {};  // Correct!
```

**Rule**: Use `module.exports` when exporting a single item. Use `exports.xxx` when exporting multiple items.

---

## 4. Importing Modules

### 4.1 The require() Function

```javascript
// Import module
const calculator = require('./calculator');

// Use it
console.log(calculator.add(5, 3));  // 8
```

### 4.2 Import Patterns

**Import entire module:**
```javascript
const calc = require('./calculator');
calc.add(5, 3);
```

**Destructuring import:**
```javascript
const { add, subtract } = require('./calculator');
add(5, 3);
```

**Import single export:**
```javascript
const add = require('./calculator');  // If module.exports = add
add(5, 3);
```

### 4.3 Path Resolution

| Syntax | Resolves To |
|--------|-------------|
| `require('./module')` | Local file |
| `require('../module')` | Parent directory |
| `require('module')` | node_modules or core |

### 4.4 Module Resolution Order

1. Core modules (fs, http, path)
2. File modules (starts with ./ or ../)
3. node_modules folder

---

## 5. Built-in Modules

### 5.1 Common Core Modules

| Module | Description |
|--------|-------------|
| `fs` | File system operations |
| `http` | HTTP server |
| `path` | File path utilities |
| `os` | Operating system info |
| `events` | Event handling |
| `url` | URL parsing |
| `crypto` | Cryptographic functions |

### 5.2 Using Core Modules

```javascript
// File System
const fs = require('fs');
fs.readFileSync('file.txt', 'utf8');

// HTTP
const http = require('http');
http.createServer((req, res) => {
    res.end('Hello World');
}).listen(3000);

// Path
const path = require('path');
path.join(__dirname, 'folder', 'file.txt');

// OS
const os = require('os');
console.log(os.platform());
```

---

## 6. Module Patterns

### 6.1 Export Object Pattern

```javascript
// math.js
module.exports = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b,
    multiply: (a, b) => a * b
};

// app.js
const math = require('./math');
math.add(5, 3);
```

### 6.2 Export Function Pattern

```javascript
// logger.js
module.exports = function(message) {
    console.log(`[${new Date().toISOString()}] ${message}`);
};

// app.js
const log = require('./logger');
log('Server started');
```

### 6.3 Export Class Pattern

```javascript
// User.js
class User {
    constructor(name) {
        this.name = name;
    }
    greet() {
        return `Hello, ${this.name}`;
    }
}
module.exports = User;

// app.js
const User = require('./User');
const user = new User('John');
console.log(user.greet());
```

### 6.4 Revealing Module Pattern

```javascript
// counter.js
module.exports = (function() {
    let count = 0;  // Private
    
    return {
        increment: () => ++count,
        decrement: () => --count,
        getCount: () => count
    };
})();

// app.js
const counter = require('./counter');
counter.increment();
console.log(counter.getCount());  // 1
```

---

## 7. Quick Reference

### 7.1 Exporting

```javascript
// Single export
module.exports = myFunction;

// Multiple exports (object)
module.exports = { func1, func2 };

// Named exports
exports.myFunction = function() {};
```

### 7.2 Importing

```javascript
// Import entire module
const mod = require('./module');

// Destructure imports
const { func1, func2 } = require('./module');

// Core module
const fs = require('fs');
```

### 7.3 Module Variables

```javascript
__filename  // Full path to current file
__dirname   // Directory of current file
module      // Current module object
exports     // Shorthand for module.exports
require     // Function to import modules
```

---

## 8. Interview Questions

### Q1: What is a module in Node.js?
**Answer**: A module is a reusable block of code encapsulated in a file. Node.js treats each file as a separate module that can export functionality to be used by other modules.

### Q2: What is the difference between exports and module.exports?
**Answer**: `exports` is a reference to `module.exports`. You can add properties to `exports`, but if you reassign `exports` itself, it breaks the reference. Always use `module.exports` when exporting a single item.

### Q3: What is require()?
**Answer**: `require()` is a function used to import modules in Node.js. It reads the module, executes it, and returns the exported content.

### Q4: What are core modules?
**Answer**: Core modules are built-in modules that come with Node.js installation. Examples include `fs`, `http`, `path`, and `os`. They don't need to be installed via npm.

### Q5: How does Node.js resolve module paths?
**Answer**:
1. Core modules (fs, http) - checked first
2. File modules (./ or ../) - relative paths
3. node_modules folder - third-party packages

### Q6: What are __filename and __dirname?
**Answer**:
- `__filename`: Absolute path of the current module file
- `__dirname`: Absolute path of the directory containing the current module

---

## Navigation

← Previous: [31_NPM_and_Package_Management.md](./31_NPM_and_Package_Management.md) | Next: [33_File_System_Operations.md](./33_File_System_Operations.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 07*
