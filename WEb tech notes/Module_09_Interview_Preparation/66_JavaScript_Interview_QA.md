# JavaScript & HTML5 Interview Questions

## Table of Contents
1. [HTML5 Questions](#1-html5-questions)
2. [JavaScript Basic Questions](#2-javascript-basic-questions)
3. [JavaScript DOM & BOM](#3-javascript-dom--bom)
4. [JavaScript Objects & Arrays](#4-javascript-objects--arrays)
5. [Advanced JavaScript](#5-advanced-javascript)

---

## 1. HTML5 Questions

### Q1: What is HTML5?
**Answer**: HTML5 is the most recent version of the HTML (Hypertext Markup Language). It is a language for structuring and displaying content for the World Wide Web. It includes new features like `<section>`, `<article>`, `<header>`, `<nav>`, `<video>`, `<audio>`, and `<canvas>` to handle multimedia and graphical content without plugins.

### Q2: What is `<!DOCTYPE>`? Is it necessary?
**Answer**: The `<!DOCTYPE>` is an instruction to the web browser about what version of HTML the page is written in. In HTML5, it is simply `<!DOCTYPE html>`. It must be the very first thing in the document. It allows the browser to render the page in "Standard Mode" rather than "Quirks Mode".

### Q3: List some new features of HTML5.
**Answer**:
-   **Canvas** (`<canvas>`): For 2D drawing using JavaScript.
-   **Media**: `<video>` and `<audio>` elements.
-   **Storage**: `localStorage` and `sessionStorage`.
-   **Semantic Elements**: `<article>`, `<footer>`, `<header>`, `<nav>`, `<section>`.
-   **Forms**: New input types like `date`, `email`, `url`, `number`, `range`.

### Q4: List advantages of HTML5.
**Answer**:
1.  Cleaner markup and improved semantics.
2.  Offline Application Cache.
3.  No need for external plugins (like Flash) for audio/video.
4.  Better error handling.
5.  Device independence.

### Q5: What is Canvas?
**Answer**: The `<canvas>` element allows for dynamic, scriptable rendering of 2D shapes and bitmap images.
```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

### Q6: What is HTML5 Geolocation?
**Answer**: It is an API used to locate a user’s position. `navigator.geolocation.getCurrentPosition(success, error)` is used to retrieve the latitude and longitude.

### Q7: What is `sessionStorage` vs `localStorage`?
**Answer**:
-   **sessionStorage**: Stores data for one session (data is lost when the browser tab is closed).
-   **localStorage**: Stores data with no expiration date (data persists even after closing the browser).

---

## 2. JavaScript Basic Questions

### Q8: What is JavaScript?
**Answer**: JavaScript is a lightweight, interpreted, object-based scripting language. It is widely used for client-side validation and interactivity. It is cross-platform and complementary to Java and HTML.

### Q9: Difference between JavaScript and JScript?
**Answer**: JScript is Microsoft's implementation of JavaScript, used in Internet Explorer. They are essentially the same, but JScript was named differently to avoid trademark issues.

### Q10: Data Types in JavaScript?
**Answer**:
-   **Primitive**: String, Number, Boolean, Undefined, Null, Symbol (ES6), BigInt.
-   **Non-Primitive**: Object (includes Array, Function, RegExp).

### Q11: Difference between `==` and `===`?
**Answer**:
-   `==` (Abstract Equality): Checks value only (performs type coercion). `5 == "5"` is true.
-   `===` (Strict Equality): Checks both value and type. `5 === "5"` is false.

### Q12: What is the output of `10+20+"30"`?
**Answer**: `3030`.
-   `10 + 20` evaluated first (numbers) -> `30`.
-   `30 + "30"` (concatenation) -> `"3030"`.

### Q13: What is the output of `"10"+20+30`?
**Answer**: `102030`.
-   `"10" + 20` (concatenation) -> `"1020"`.
-   `"1020" + 30` (concatenation) -> `"102030"`.

### Q14: What is `NaN`?
**Answer**: `NaN` stands for "Not a Number". It is a property of the global object. The `isNaN()` function checks if a value is not a number.
`10 / "apple" // NaN`

### Q15: Difference between `null` and `undefined`?
**Answer**:
-   `undefined`: Variable declared but not assigned a value.
-   `null`: Assignment value representing "no value" or explicit emptiness.

---

## 3. JavaScript DOM & BOM

### Q16: What is BOM?
**Answer**: BOM (Browser Object Model) allows interaction with the browser. The default object is `window`. It includes `navigator`, `history`, `screen`, `location`.

### Q17: What is DOM?
**Answer**: DOM (Document Object Model) represents the HTML document as a tree structure. It is used to access and modify the content, structure, and style of the document.

### Q18: What is the `history` object?
**Answer**: Used to manipulate browser history.
-   `history.back()`: Load previous page.
-   `history.forward()`: Load next page.
-   `history.go(n)`: Load specific page relative to current.

### Q19: How to detect Client OS?
**Answer**: Using `navigator.appVersion` or `navigator.platform` string.

### Q20: Pop-up boxes in JavaScript?
**Answer**:
1.  `alert("msg")`: Display message with OK.
2.  `confirm("msg")`: Display message with OK/Cancel. Returns true/false.
3.  `prompt("msg")`: Input dialog. Returns text or null.

---

## 4. JavaScript Objects & Arrays

### Q21: How to create functions?
**Answer**:
-   **Named**: `function msg() { ... }`
-   **Anonymous**: `var msg = function() { ... }`

### Q22: What is an Anonymous Function?
**Answer**: A function without a name. Often used as an argument to other functions or assigned to a variable.

### Q23: What is a Closures?
**Answer**: A closure is a function that remembers its outer variables and can access them even when the outer function has finished executing.
```javascript
function outer() {
  var num = 10;
  return function inner() { console.log(num); }
}
```

### Q24: What is the `arguments` object?
**Answer**: An array-like object accessible inside functions that contains the values of the arguments passed to that function.

### Q25: How to create Objects?
**Answer**:
1.  Object Literal: `var emp = {id: 1, name: "John"};`
2.  `new Object()` instance.
3.  Constructor Function / Class.

---

## 5. Advanced JavaScript

### Q26: `this` keyword?
**Answer**: Refers to the object that is executing the current function.
-   Global scope -> Window.
-   Method -> The Object.
-   Event -> The Element.

### Q27: Exception Handling?
**Answer**: Using `try`, `catch`, `finally`, and `throw`.
```javascript
try {
  // code
} catch (err) {
  // handle error
}
```

### Q28: Strict Mode?
**Answer**: Activated by `"use strict";`. It catches common coding bloopers (like undeclared variables), prevents usage of unsafe features, and throws exceptions for errors that were previously silent.

### Q29: Debugging?
**Answer**:
-   `console.log()`
-   `debugger` keyword (stops execution if DevTools is open).

### Q30: Difference between Client-side and Server-side JS?
**Answer**:
-   **Client-side**: Runs in browser (V8, SpiderMonkey), interacts with DOM/BOM (e.g., Validation, UI logic).
-   **Server-side**: Runs on server (Node.js), interacts with File System, Database, Network.

---

## Navigation

← Previous: [65_jQuery_AJAX.md](../Module_08_jQuery/65_jQuery_AJAX.md) | Next: [67_Node_Express_Interview_QA.md](./67_Node_Express_Interview_QA.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Notes_CCEE_InterviewQA_Web*
