# Closures in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [The Problem: Global vs Local Variables](#2-the-problem-global-vs-local-variables)
3. [Nested Functions and Scope](#3-nested-functions-and-scope)
4. [What is a Closure?](#4-what-is-a-closure)
5. [Creating Closures](#5-creating-closures)
6. [Practical Closure Examples](#6-practical-closure-examples)
7. [Common Use Cases](#7-common-use-cases)
8. [Memory Considerations](#8-memory-considerations)
9. [Quick Reference](#9-quick-reference)
10. [Interview Questions](#10-interview-questions)

---

## 1. Introduction

### 1.1 Definition
A **closure** is a function that has access to its outer (enclosing) function's scope, even after the outer function has returned. Closures "remember" the environment in which they were created.

### 1.2 Purpose
- Create private variables
- Maintain state between function calls
- Implement data encapsulation
- Create function factories
- Preserve context in callbacks

### 1.3 Key Concept
Global variables can be made **private (local)** using closures. This provides the benefits of encapsulation while maintaining state.

---

## 2. The Problem: Global vs Local Variables

### 2.1 Problem 1: Global Variables

```javascript
<script>
let counter = 0;  // Global variable

function add() {
    counter += 1;
    return counter;
}

document.write(add());  // 1
document.write(add());  // 2
document.write(add());  // 3
</script>
```

**Memory Diagram:**
```
GLOBAL SCOPE:
┌────────────────────┐
│ counter = 0 → 1 → 2 → 3
│ add = function()   │
└────────────────────┘
```

**Problem:**
- ✅ Counter increments correctly
- ❌ `counter` is GLOBAL - can be modified from anywhere
- ❌ Any code can accidentally overwrite it
- ❌ No data protection

### 2.2 Problem 2: Local Variables

```javascript
<script>
function add() {
    let counter = 0;  // Local variable
    counter += 1;
    return counter;
}

document.write(add());  // 1
document.write(add());  // 1
document.write(add());  // 1
</script>
```

**What Happens:**
```
First call:  counter = 0 → counter = 1 → return 1 → counter destroyed
Second call: counter = 0 → counter = 1 → return 1 → counter destroyed
Third call:  counter = 0 → counter = 1 → return 1 → counter destroyed
```

**Problem:**
- ✅ Counter is LOCAL (protected)
- ❌ Counter is **re-initialized to 0** on every call
- ❌ Cannot maintain state between calls
- ❌ Always returns 1

### 2.3 The Dilemma

| Approach | Maintains State | Protected |
|----------|-----------------|-----------|
| Global variable | ✅ Yes | ❌ No |
| Local variable | ❌ No | ✅ Yes |
| **Closure** | ✅ Yes | ✅ Yes |

**We need a solution that provides BOTH state persistence AND protection.**

---

## 3. Nested Functions and Scope

### 3.1 Nested Function Example

```javascript
<script>
function add() {
    var counter = 0;
    
    function plus() {
        counter += 1;
    }
    
    plus();
    return counter;
}

document.write(add());  // 1
document.write(add());  // 1
</script>
```

**Key Observations:**
- JavaScript supports **nested functions**
- Nested functions have access to the **outer function's scope**
- `plus()` can access `counter` from the parent function `add()`

**Problem:**
- `plus()` is NOT accessible from outside
- `counter = 0` is executed every time `add()` is called
- Still prints 1, 1 instead of 1, 2

**What We Need:**
1. Access to `plus()` from outside
2. Execute `counter = 0` only ONCE

**Solution: Closures!**

---

## 4. What is a Closure?

### 4.1 Definition
A closure is the combination of a function and the lexical environment (scope) within which that function was declared. This environment consists of any variable that was in scope at the time the closure was created.

### 4.2 Key Characteristics

| Characteristic | Description |
|---------------|-------------|
| **Remembers Scope** | Retains access to outer function's variables |
| **Survives Parent** | Works even after outer function has returned |
| **Private Data** | Creates private variables inaccessible from outside |
| **Maintains State** | Variables persist between function calls |

### 4.3 How Closures Work

```javascript
function outerFunction() {
    let outerVariable = "I'm from outer!";
    
    function innerFunction() {
        console.log(outerVariable);  // Can access outerVariable
    }
    
    return innerFunction;  // Return the inner function
}

let closure = outerFunction();  // outerFunction runs and returns innerFunction
closure();  // "I'm from outer!" - Still has access to outerVariable!
```

**Memory Diagram:**
```
After outerFunction() returns:
┌───────────────────────────────────────────┐
│  outerFunction's scope (preserved)        │
│  ┌─────────────────────────────────────┐  │
│  │ outerVariable = "I'm from outer!"   │  │
│  └─────────────────────────────────────┘  │
│             ↑                              │
│  closure ───┘ (innerFunction)              │
└───────────────────────────────────────────┘
```

---

## 5. Creating Closures

### 5.1 The Counter Closure Solution

```javascript
<script>
let plus = function() {
    var counter = 0;
    
    return function() {
        return counter += 1;
    }
}();  // Immediately invoke!

document.write(plus());  // 1
document.write(plus());  // 2
document.write(plus());  // 3
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 1 | `let plus = function() {` | Start of self-invoking function |
| 2 | `var counter = 0;` | Private variable, initialized ONCE |
| 4 | `return function() {` | Returns inner function (the closure) |
| 5 | `return counter += 1;` | Inner function increments and returns |
| 7 | `}();` | Immediately invokes the outer function |
| 9 | `plus()` | Calls the returned inner function |

**Execution Flow:**
```
1. Self-invoking function executes immediately
2. counter = 0 is set (only once!)
3. Inner function is returned and assigned to 'plus'
4. Each call to plus() increments counter

Call 1: counter = 0 → 1, return 1
Call 2: counter = 1 → 2, return 2
Call 3: counter = 2 → 3, return 3
```

**Memory Diagram:**
```
GLOBAL SCOPE:
┌────────────────────────────────────┐
│ plus → [reference to inner function]
└────────────────────────────────────┘
        │
        ↓
CLOSURE SCOPE (preserved):
┌────────────────────────────────────┐
│ counter = 0 → 1 → 2 → 3            │
│ inner function (returned by IIFE) │
└────────────────────────────────────┘
```

### 5.2 Alternative: add Variable Pattern

```javascript
var add = (function() {
    var counter = 0;
    return function() {
        return counter += 1;
    }
})();

add();  // 1
add();  // 2
add();  // 3
```

### 5.3 Closure with Button Click

```html
<!DOCTYPE html>
<html>
<body>
    <p>Counting with a local variable.</p>
    <button type="button" onclick="myFunction()">Count!</button>
    <p id="demo">0</p>
    
    <script>
    var add = (function() {
        var counter = 0;
        return function() {
            return counter += 1;
        }
    })();
    
    function myFunction() {
        document.getElementById("demo").innerHTML = add();
    }
    </script>
</body>
</html>
```

**Execution Flow:**
```
1. Page loads
2. IIFE executes, counter = 0
3. add now references the inner function
4. User clicks button
5. myFunction() calls add()
6. counter increments
7. Display updated

Click 1: counter 0 → 1, displays 1
Click 2: counter 1 → 2, displays 2
Click 3: counter 2 → 3, displays 3
```

---

## 6. Practical Closure Examples

### 6.1 Function Factory

Create multiple independent counters:

```javascript
function createCounter(start = 0) {
    let count = start;
    
    return {
        increment: function() { return ++count; },
        decrement: function() { return --count; },
        getCount: function() { return count; }
    };
}

let counter1 = createCounter(0);
let counter2 = createCounter(100);

console.log(counter1.increment());  // 1
console.log(counter1.increment());  // 2
console.log(counter2.increment());  // 101
console.log(counter1.getCount());   // 2
console.log(counter2.getCount());   // 101
```

**Key Point:** Each counter has its OWN private `count` variable!

### 6.2 Private Variables (Encapsulation)

```javascript
function createPerson(name, age) {
    // Private variables
    let _name = name;
    let _age = age;
    
    return {
        getName: function() { return _name; },
        getAge: function() { return _age; },
        setAge: function(newAge) {
            if (newAge > 0 && newAge < 150) {
                _age = newAge;
            }
        },
        toString: function() {
            return `${_name}, ${_age} years old`;
        }
    };
}

let person = createPerson("John", 30);
console.log(person.getName());   // "John"
console.log(person._name);       // undefined (private!)
person.setAge(31);
console.log(person.getAge());    // 31
```

### 6.3 Module Pattern

```javascript
var myModule = (function() {
    // Private variables
    var privateVar = "I am private";
    
    // Private functions
    function privateFunction() {
        console.log(privateVar);
    }
    
    // Public API
    return {
        publicMethod: function() {
            privateFunction();
        },
        publicVar: "I am public"
    };
})();

myModule.publicMethod();  // "I am private"
console.log(myModule.publicVar);  // "I am public"
console.log(myModule.privateVar); // undefined
```

### 6.4 Event Handler with Preserved Context

```javascript
function setupButtons() {
    for (var i = 1; i <= 3; i++) {
        (function(buttonNum) {
            document.getElementById("btn" + buttonNum).onclick = function() {
                alert("Button " + buttonNum + " clicked!");
            };
        })(i);  // Create closure to capture current i value
    }
}
```

**Without Closure (Bug):**
```javascript
for (var i = 1; i <= 3; i++) {
    document.getElementById("btn" + i).onclick = function() {
        alert("Button " + i + " clicked!");  // Always shows 4!
    };
}
```

---

## 7. Common Use Cases

### 7.1 Memoization (Caching)

```javascript
function memoize(fn) {
    var cache = {};
    
    return function(...args) {
        var key = JSON.stringify(args);
        
        if (cache[key]) {
            console.log("From cache");
            return cache[key];
        }
        
        console.log("Computing...");
        var result = fn.apply(this, args);
        cache[key] = result;
        return result;
    };
}

function slowFactorial(n) {
    if (n <= 1) return 1;
    return n * slowFactorial(n - 1);
}

var fastFactorial = memoize(slowFactorial);
fastFactorial(5);  // Computing... 120
fastFactorial(5);  // From cache 120
```

### 7.2 Debounce Function

```javascript
function debounce(func, delay) {
    var timer;
    
    return function(...args) {
        clearTimeout(timer);
        timer = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}

// Usage: Only execute after user stops typing for 300ms
var debouncedSearch = debounce(function(query) {
    console.log("Searching for:", query);
}, 300);
```

### 7.3 Once Function (Execute Only Once)

```javascript
function once(fn) {
    var called = false;
    var result;
    
    return function(...args) {
        if (!called) {
            called = true;
            result = fn.apply(this, args);
        }
        return result;
    };
}

var initialize = once(function() {
    console.log("Initializing...");
    return "Initialized!";
});

initialize();  // "Initializing..." → "Initialized!"
initialize();  // "Initialized!" (function not executed again)
```

---

## 8. Memory Considerations

### 8.1 Closures and Memory

Closures keep references to outer variables, which means those variables are **not garbage collected** as long as the closure exists.

**Potential Memory Leak:**
```javascript
function createHeavyClosure() {
    var largeData = new Array(1000000).fill("data");
    
    return function() {
        console.log(largeData.length);
    };
}

var closure = createHeavyClosure();  // largeData stays in memory!
```

**Solution: Release When Done**
```javascript
closure = null;  // Allow garbage collection
```

### 8.2 Best Practices

1. **Don't over-use closures** - Only when you need private state
2. **Clean up references** - Set to null when done
3. **Be aware of scope** - Closures capture the entire scope
4. **Avoid accidental closures** - Be intentional about what you capture

---

## 9. Quick Reference

### 9.1 Closure Patterns

```javascript
// Basic Closure
function outer() {
    var x = 10;
    return function inner() {
        return x;
    };
}

// IIFE with Private State
var module = (function() {
    var private = 0;
    return {
        get: function() { return private; },
        set: function(val) { private = val; }
    };
})();

// Factory Function
function createX(initial) {
    var x = initial;
    return function() { return x++; };
}
```

### 9.2 Key Points Summary

| Concept | Description |
|---------|-------------|
| **Definition** | Function + its lexical scope |
| **Purpose** | Private variables, maintain state |
| **Created when** | Inner function accesses outer scope |
| **Scope chain** | Inner → Outer → Global |
| **Memory** | Outer scope preserved as long as closure exists |
| **Use cases** | Modules, factories, callbacks, memoization |

---

## 10. Interview Questions

### Q1: What is a closure in JavaScript?
**Answer**: A closure is a function that retains access to variables from its outer (enclosing) function's scope, even after the outer function has returned. Closures "remember" the environment in which they were created.

### Q2: What are the benefits of using closures?
**Answer**:
- Data privacy/encapsulation (private variables)
- State preservation between function calls
- Function factories
- Callback functions with preserved context
- Module pattern implementation

### Q3: How do closures help create private variables?
**Answer**: Variables declared in the outer function are only accessible through the inner function (closure). Since the outer function's scope is preserved but not directly accessible, these variables become private.

### Q4: What is the difference between closure scope and function scope?
**Answer**: Function scope lasts only during function execution. Closure scope persists even after the outer function returns because the inner function maintains a reference to it.

### Q5: Can closures cause memory leaks?
**Answer**: Yes, because closures keep references to outer scope variables. If a closure exists indefinitely and references large objects, those objects cannot be garbage collected. Solution: Set closure references to null when no longer needed.

### Q6: Write a closure that maintains a private counter.
**Answer**:
```javascript
function createCounter() {
    let count = 0;
    return {
        increment: () => ++count,
        decrement: () => --count,
        get: () => count
    };
}
```

### Q7: Why does this loop print "3" three times, and how do you fix it?
```javascript
for (var i = 0; i < 3; i++) {
    setTimeout(function() { console.log(i); }, 1000);
}
```
**Answer**: `var` is function-scoped, so all callbacks share the same `i`. By the time they execute, `i` is 3.

**Fixes:**
1. Use `let` (block-scoped): `for (let i = 0; ...)`
2. Use IIFE: `(function(j) { setTimeout(..., j); })(i);`
3. Use bind: `setTimeout(console.log.bind(null, i), 1000);`

---

## Navigation

← Previous: [07_Window_Methods.md](../Module_01_JavaScript_Fundamentals/07_Window_Methods.md) | Next: [09_ES6_Objects_and_Classes.md](./09_ES6_Objects_and_Classes.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 03*
