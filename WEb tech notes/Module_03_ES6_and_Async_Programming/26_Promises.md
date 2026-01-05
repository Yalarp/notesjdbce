# Promises in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Promise Basics](#2-promise-basics)
3. [Promise States](#3-promise-states)
4. [Consumers: then, catch, finally](#4-consumers-then-catch-finally)
5. [Promise vs Callbacks](#5-promise-vs-callbacks)
6. [Promise Chaining](#6-promise-chaining)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 The Analogy
Imagine you're a top singer, and fans ask day and night for your upcoming song. To get some relief, you **promise** to send it to them when it's published. You give your fans a subscription list.

- **Producing code** ("singer"): Does something that takes time (e.g., loads data)
- **Consuming code** ("fans"): Wants the result once it's ready
- **Promise** ("subscription list"): Links the producing and consuming code together

### 1.2 Definition
A **Promise** is a special JavaScript object that links the "producing code" and the "consuming code" together. It makes the result available to all subscribed code when it's ready.

---

## 2. Promise Basics

### 2.1 Constructor Syntax

```javascript
let promise = new Promise(function(resolve, reject) {
    // executor (the producing code, "singer")
});
```

### 2.2 The Executor Function
- The function passed to `new Promise` is called the **executor**
- When `new Promise` is created, the executor runs automatically
- It receives two callbacks provided by JavaScript: `resolve` and `reject`

### 2.3 Resolve and Reject

```javascript
let promise = new Promise(function(resolve, reject) {
    // After 1 second signal that the job is done with result "done"
    setTimeout(() => resolve("done"), 1000);
});

// OR for rejection
let promise = new Promise(function(resolve, reject) {
    // After 1 second signal that the job failed with an error
    setTimeout(() => reject(new Error("Whoops!")), 1000);
});
```

### 2.4 Key Rules
- Call **only one**: `resolve` OR `reject`
- All further calls are ignored

```javascript
let promise = new Promise(function(resolve, reject) {
    resolve("done");
    
    reject(new Error("…"));           // ignored
    setTimeout(() => resolve("…"));   // ignored
});
```

---

## 3. Promise States

### 3.1 State Diagram

```
┌─────────────────────────────────────────────────────────┐
│                    new Promise()                         │
│                         ↓                                │
│                    ┌─────────┐                          │
│                    │ pending │                          │
│                    │ state   │                          │
│                    └────┬────┘                          │
│              ┌──────────┴──────────┐                    │
│              ↓                     ↓                    │
│    ┌─────────────────┐   ┌─────────────────┐            │
│    │   "fulfilled"   │   │   "rejected"    │            │
│    │   resolve(value)│   │   reject(error) │            │
│    │   result: value │   │   result: error │            │
│    └─────────────────┘   └─────────────────┘            │
└─────────────────────────────────────────────────────────┘
```

### 3.2 State Properties

| State | Meaning | Result |
|-------|---------|--------|
| `pending` | Initial state | `undefined` |
| `fulfilled` | Operation succeeded | `value` |
| `rejected` | Operation failed | `error` |

**Note:** A promise that is either fulfilled or rejected is called "**settled**".

---

## 4. Consumers: then, catch, finally

### 4.1 then()

The most important, fundamental method:

```javascript
promise.then(
    function(result) { /* handle a successful result */ },
    function(error) { /* handle an error */ }
);
```

**Example - Success:**
```javascript
let promise = new Promise(function(resolve, reject) {
    setTimeout(() => resolve("done!"), 1000);
});

// resolve runs the first function in .then
promise.then(
    result => alert(result),  // shows "done!" after 1 second
    error => alert(error)     // doesn't run
);
```

**Example - Rejection:**
```javascript
let promise = new Promise(function(resolve, reject) {
    setTimeout(() => reject(new Error("Whoops!")), 1000);
});

// reject runs the second function in .then
promise.then(
    result => alert(result),  // doesn't run
    error => alert(error)     // shows "Error: Whoops!" after 1 second
);
```

**Only success handler:**
```javascript
let promise = new Promise(resolve => {
    setTimeout(() => resolve("done!"), 1000);
});

promise.then(alert);  // shows "done!" after 1 second
```

### 4.2 catch()

If we're interested only in errors:

```javascript
let promise = new Promise((resolve, reject) => {
    setTimeout(() => reject(new Error("Whoops!")), 1000);
});

// .catch(f) is the same as promise.then(null, f)
promise.catch((data) => alert(data));  // shows "Error: Whoops!" after 1 second
```

### 4.3 finally()

Always runs when the promise is settled (success or failure):

```javascript
new Promise((resolve, reject) => {
    /* do something that takes time, and then call resolve/reject */
})
    .finally(() => stop loading indicator)  // runs regardless of outcome
    .then(result => show result, err => show error)
```

**Key Points about finally:**
- Has **no arguments** (doesn't know if success/failure)
- **Passes through** results and errors to the next handler

```javascript
new Promise((resolve, reject) => {
    setTimeout(() => resolve("result"), 2000);
})
    .finally(() => alert("Promise ready"))
    .then(result => alert(result));  // <-- .then handles the result
```

---

## 5. Promise vs Callbacks

### 5.1 Callback Example

```javascript
setTimeout(
    function() {
        myFunction("I love JS !!!");
    }, 3000
);

function myFunction(value) {
    document.getElementById("demo").innerHTML = value;
}
```

### 5.2 Promise Example

```javascript
let myPromise = new Promise(function(myResolve, myReject) {
    setTimeout(function() {
        myResolve("I love JS !!");
    }, 3000);
});

myPromise.then((value) => {
    document.getElementById("demo").innerHTML = value;
});
```

### 5.3 Comparison

| Promises | Callbacks |
|----------|-----------|
| Natural order: First run, .then handle result | Must have callback ready beforehand |
| Call `.then` as many times as we want | Can have only one callback |
| Better error handling with `.catch` | Error handling can be messy |
| Avoid "callback hell" | Deeply nested callbacks |

---

## 6. Promise Chaining

### 6.1 Multiple Handlers

```javascript
new Promise((resolve, reject) => {
    throw new Error("error");
})
    .finally(() => alert("Promise ready"))
    .then(r => alert(r), err => alert(err))
    .then(r => alert(r))
    .catch(err => alert(err));
```

### 6.2 Real-World Example with XMLHttpRequest

**Callback Version:**
```javascript
function getFile(myCallback) {
    let req = new XMLHttpRequest();
    req.open('GET', "mycar.html");
    
    req.onload = function() {
        if (req.status == 200) {
            myCallback(this.responseText);
        } else {
            myCallback("Error: " + req.status);
        }
    };
    req.send();
}

getFile(myDisplayer);
```

**Promise Version:**
```javascript
let myPromise = new Promise(function(myResolve, myReject) {
    let req = new XMLHttpRequest();
    req.open('GET', "mycar.html");
    
    req.onload = function() {
        if (req.status == 200) {
            myResolve(req.response);
        } else {
            myReject("File not Found");
        }
    };
    req.send();
});

myPromise.then(
    function(value) { myDisplayer(value); },
    function(error) { myDisplayer(error); }
);
```

---

## 7. Quick Reference

### 7.1 Creating Promises

```javascript
// Basic
let promise = new Promise((resolve, reject) => {
    // async operation
    if (success) resolve(data);
    else reject(error);
});

// Immediate resolve
let resolved = Promise.resolve(value);

// Immediate reject
let rejected = Promise.reject(error);
```

### 7.2 Consuming Promises

```javascript
promise
    .then(result => { /* handle success */ })
    .catch(error => { /* handle error */ })
    .finally(() => { /* cleanup */ });
```

### 7.3 Promise States

```
pending   → fulfilled (resolve called)
pending   → rejected (reject called)
```

---

## 8. Interview Questions

### Q1: What is a Promise?
**Answer**: A Promise is an object representing the eventual completion or failure of an asynchronous operation. It allows you to attach callbacks for success and error handling instead of passing callbacks into a function.

### Q2: What are the three states of a Promise?
**Answer**:
- **Pending**: Initial state, neither fulfilled nor rejected
- **Fulfilled**: Operation completed successfully
- **Rejected**: Operation failed

### Q3: What is the difference between .then() and .catch()?
**Answer**:
- `.then(onFulfilled, onRejected)`: Handles both success and error
- `.catch(onRejected)`: Only handles errors, equivalent to `.then(null, onRejected)`

### Q4: What does .finally() do?
**Answer**: `.finally()` runs when the promise is settled (success or failure). It doesn't receive any arguments and passes through results/errors to the next handler.

### Q5: What happens if you call both resolve() and reject()?
**Answer**: Only the first call is honored. Subsequent calls to resolve or reject are ignored.

### Q6: Why are Promises better than callbacks?
**Answer**:
- Avoid callback hell (pyramid of doom)
- Better error handling with chained `.catch()`
- More readable, sequential code
- Can attach multiple handlers with multiple `.then()`

---

## Navigation

← Previous: [25_Object_Destructuring.md](./25_Object_Destructuring.md) | Next: [27_Async_Await.md](./27_Async_Await.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 06*
