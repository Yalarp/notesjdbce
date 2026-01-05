# Async/Await in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Async Functions](#2-async-functions)
3. [Await Keyword](#3-await-keyword)
4. [Error Handling](#4-error-handling)
5. [Practical Examples](#5-practical-examples)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 What is Async/Await?
**Async/Await** is syntactic sugar built on top of Promises. It makes asynchronous code look and behave more like synchronous code, making it easier to read and write.

### 1.2 Why Async/Await?
- More readable than Promise chains
- Easier error handling with try/catch
- Cleaner code structure
- Easier debugging

---

## 2. Async Functions

### 2.1 The async Keyword

The word `async` before a function means one simple thing: the function always returns a Promise.

```javascript
async function f() {
    return 1;
}
```

This is equivalent to:

```javascript
async function f() {
    return Promise.resolve(1);
}
```

### 2.2 Using the Return Value

```javascript
async function f() {
    return 1;
}

f().then(result => alert(result));  // 1
```

### 2.3 Async Wraps Non-Promises

Other values are wrapped in a resolved promise automatically:

```javascript
async function f() {
    return "Hello";
}

// Both work the same:
f().then(result => alert(result));  // "Hello"
```

---

## 3. Await Keyword

### 3.1 Basic Syntax

```javascript
// Works only inside async functions
let value = await promise;
```

**The keyword `await` makes JavaScript wait until that promise settles and returns its result.**

### 3.2 Example

```javascript
async function f() {
    let promise = new Promise((resolve, reject) => {
        setTimeout(() => resolve("done!"), 1000);
    });
    
    let result = await promise;  // wait until the promise resolves (*)
    
    alert(result);  // "done!"
}

f();
```

### 3.3 Key Points
- `await` literally **suspends** function execution until the promise settles
- Then resumes with the promise result
- No CPU resources are wasted - JavaScript can do other things
- More elegant than `.then()` chains

### 3.4 Cannot Use in Regular Functions

```javascript
function f() {
    let promise = Promise.resolve(1);
    let result = await promise;  // Syntax error!
}
```

**`await` only works inside an `async` function.**

---

## 4. Error Handling

### 4.1 Using try/catch

```javascript
async function f() {
    try {
        let response = await fetch('http://no-such-url');
    } catch(err) {
        alert(err);  // TypeError: failed to fetch
    }
}

f();
```

### 4.2 Catching Multiple Awaits

```javascript
async function f() {
    try {
        let response = await fetch('/no-user-here');
        let user = await response.json();
    } catch(err) {
        // catches errors in both fetch and response.json
        alert(err);
    }
}
```

### 4.3 Alternative: Using .catch()

```javascript
async function f() {
    let response = await fetch('http://no-such-url')
        .catch(err => alert(err));
}
```

---

## 5. Practical Examples

### 5.1 Simple Async/Await

```html
<h2>JavaScript async / await</h2>
<p id="demo"></p>

<script>
function myDisplayer(some) {
    document.getElementById("demo").innerHTML = some;
}

async function myFunction() {
    return "Hello";
}

myFunction().then(
    function(value) { myDisplayer(value); },
    function(error) { myDisplayer(error); }
);
</script>
```

### 5.2 Fetching File with XMLHttpRequest

```html
<h2>JavaScript async / await</h2>
<p id="demo"></p>

<script>
async function getFile() {
    let myPromise = new Promise(function(myResolve, myReject) {
        let req = new XMLHttpRequest();
        req.open('GET', "mycar.html");
        
        req.onload = function() {
            if (req.status == 200) {
                myResolve(req.response);
            } else {
                myResolve("File not Found");
            }
        };
        req.send();
    });
    
    document.getElementById("demo").innerHTML = await myPromise;
}

getFile();
</script>
```

### 5.3 Sequential vs Parallel Execution

**Sequential (slower):**
```javascript
async function sequential() {
    let result1 = await fetch('/api/user');
    let result2 = await fetch('/api/posts');
    // Second fetch waits for first to complete
}
```

**Parallel (faster):**
```javascript
async function parallel() {
    let promise1 = fetch('/api/user');
    let promise2 = fetch('/api/posts');
    
    let result1 = await promise1;
    let result2 = await promise2;
    // Both fetches run simultaneously
}
```

---

## 6. Quick Reference

### 6.1 Async Function Declaration

```javascript
// Function declaration
async function myFunc() {
    return "Hello";
}

// Arrow function
const myFunc = async () => {
    return "Hello";
};

// Method
const obj = {
    async myMethod() {
        return "Hello";
    }
};
```

### 6.2 Await Usage

```javascript
async function example() {
    // Wait for promise
    let result = await somePromise;
    
    // Wait for function that returns promise
    let data = await getData();
    
    // Chain operations
    let json = await (await fetch(url)).json();
}
```

### 6.3 Error Handling Patterns

```javascript
// try/catch
async function example() {
    try {
        let result = await riskyOperation();
    } catch (err) {
        console.error(err);
    }
}

// .catch() on async function
example().catch(err => console.error(err));
```

### 6.4 Common Patterns

```javascript
// Multiple awaits
async function getData() {
    let user = await getUser();
    let posts = await getPosts(user.id);
    return posts;
}

// Parallel execution
async function getAll() {
    let [user, posts] = await Promise.all([
        getUser(),
        getPosts()
    ]);
    return { user, posts };
}
```

---

## 7. Interview Questions

### Q1: What does the async keyword do?
**Answer**: The `async` keyword before a function makes the function return a Promise. Non-promise values are automatically wrapped in a resolved Promise.

### Q2: What does await do?
**Answer**: `await` pauses the execution of an async function until a Promise settles, then returns the Promise's result. It only works inside async functions.

### Q3: Can you use await outside an async function?
**Answer**: No. Using `await` outside an async function causes a SyntaxError. (Note: Top-level await is allowed in ES modules.)

### Q4: How do you handle errors with async/await?
**Answer**: Use try/catch blocks:
```javascript
async function f() {
    try {
        let response = await fetch(url);
    } catch (err) {
        console.error(err);
    }
}
```

### Q5: What is the advantage of async/await over Promises?
**Answer**:
- Cleaner, more readable code
- Easier error handling with try/catch
- Easier debugging (appears synchronous)
- Avoids Promise chain complexity

### Q6: How do you run multiple async operations in parallel?
**Answer**: Use `Promise.all()`:
```javascript
async function parallel() {
    let [result1, result2] = await Promise.all([
        asyncOperation1(),
        asyncOperation2()
    ]);
}
```

---

## Navigation

← Previous: [26_Promises.md](./26_Promises.md) | Next: [28_Fetch_API.md](./28_Fetch_API.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 06*
