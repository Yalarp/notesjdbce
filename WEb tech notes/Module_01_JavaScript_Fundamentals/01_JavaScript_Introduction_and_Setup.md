# JavaScript Introduction and Setup

## Table of Contents
1. [Introduction](#1-introduction)
2. [What is JavaScript?](#2-what-is-javascript)
3. [JavaScript in Browser](#3-javascript-in-browser)
4. [Writing Your First JavaScript Code](#4-writing-your-first-javascript-code)
5. [The document and window Objects](#5-the-document-and-window-objects)
6. [Order of Execution](#6-order-of-execution)
7. [External JavaScript Files](#7-external-javascript-files)
8. [Using 'use strict'](#8-using-use-strict)
9. [Quick Reference](#9-quick-reference)
10. [Interview Questions](#10-interview-questions)

---

## 1. Introduction

### 1.1 Definition
JavaScript (JS) is a lightweight, interpreted, object-oriented programming language with first-class functions. It is the programming language of the web, primarily used to create interactive and dynamic content on websites.

### 1.2 Purpose
JavaScript exists to add interactivity, dynamic behavior, and logic to web pages. Without JavaScript, web pages would be static HTML documents.

### 1.3 Problem It Solves
- **Static Web Pages**: HTML alone cannot respond to user actions
- **Client-Side Processing**: Reduces server load by handling logic in the browser
- **User Experience**: Creates responsive, interactive interfaces
- **Real-Time Updates**: Enables dynamic content updates without page reloads

### 1.4 Prerequisites
- Basic understanding of HTML
- Understanding of how web browsers work
- A text editor (VS Code recommended)
- A web browser (Chrome, Firefox, Edge)

---

## 2. What is JavaScript?

### 2.1 Core Characteristics

JavaScript is an **Object-Oriented Programming (OOP)** language with the following characteristics:

| Characteristic | Description |
|---------------|-------------|
| **Interpreted** | Code is executed line by line by the JavaScript engine |
| **Dynamically Typed** | Variable types are determined at runtime, not compile time |
| **Loosely Typed** | Variables can hold any type of data and change types |
| **First-Class Functions** | Functions can be stored in variables, passed as arguments, and returned from other functions |
| **Event-Driven** | Responds to user actions and system events |
| **Cross-Platform** | Runs in any browser on any operating system |

### 2.2 JavaScript Engine

Every browser has a built-in **JavaScript Engine** that:
1. **Parses** your JavaScript code
2. **Compiles** it into native machine code
3. **Executes** the code

> **Note**: In browsers, you can **disable JavaScript**. This is why web applications should have graceful fallbacks.

### 2.3 JavaScript vs Java

| JavaScript | Java |
|-----------|------|
| Interpreted language | Compiled language |
| Dynamically typed | Statically typed |
| Prototype-based OOP | Class-based OOP |
| Runs in browser | Runs on JVM |
| Loosely typed | Strongly typed |

---

## 3. JavaScript in Browser

### 3.1 The Script Tag

JavaScript code must be placed within `<script></script>` tags. HTML does not understand JavaScript code directly.

**Syntax:**
```html
<script>
    // JavaScript code goes here
</script>
```

### 3.2 Placement of Script Tags

JavaScript can be placed in:
1. **Head Section** (`<head>`)
2. **Body Section** (`<body>`)
3. **External File** (linked via `src` attribute)

**Example: Script in Head and Body**

```html
<!DOCTYPE html>
<html lang="us-eng">
<head>
    <title>my 1st example</title>
    <meta content="text/html; charset=UTF-8" http-equiv="content-type">
    <style>
        .cl{color:red;}
    </style>
    <script>
        document.write("hello in head");
    </script>
</head>
<body>
    <h1>head----main page</h1>
    <script>
        document.write("<b class= 'cl'>main section</b>");
        document.write("<hr/>");
        console.log(document);
        console.log(window);
    </script>
    <p>again in html part</p>
    <p>Unicode Transformation Format</p>
</body>
</html>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 1 | `<!DOCTYPE html>` | Declares this as an HTML5 document |
| 2 | `<html lang="us-eng">` | Root element with language set to US English |
| 3 | `<head>` | Contains meta information about the document |
| 4 | `<title>my 1st example</title>` | Sets the browser tab title |
| 5 | `<meta content="text/html; charset=UTF-8">` | Character encoding for Unicode support |
| 6-8 | `<style>.cl{color:red;}</style>` | Internal CSS defining a class `.cl` with red color |
| 9-11 | First `<script>` block | JavaScript executed when browser parses head section |
| 10 | `document.write("hello in head")` | Writes text directly to the HTML document |
| 14 | `<h1>head----main page</h1>` | A heading in the body |
| 15-20 | Second `<script>` block | JavaScript executed when browser reaches this point in body |
| 16 | `document.write("<b class='cl'>main section</b>")` | Writes HTML with inline styling |
| 17 | `document.write("<hr/>")` | Writes a horizontal rule |
| 18 | `console.log(document)` | Outputs the document object to browser console |
| 19 | `console.log(window)` | Outputs the window object to browser console |

**Execution Flow:**
```
1. Browser loads HTML file
2. Parses <!DOCTYPE> and <html>
3. Parses <head>:
   - Reads <title>
   - Reads <meta>
   - Reads <style>
   - Executes first <script> → writes "hello in head"
4. Parses <body>:
   - Renders <h1>
   - Executes second <script> → writes bold text and hr
   - Renders remaining HTML
5. Page fully loaded
```

**Output:**
```
hello in head
head----main page
main section
_________________ (horizontal line)
again in html part
Unicode Transformation Format
```

---

## 4. Writing Your First JavaScript Code

### 4.1 The document.write() Method

The `document.write()` method writes content directly to the HTML document.

**Syntax:**
```javascript
document.write("content");
document.write("<html_tag>content</html_tag>");
```

### 4.2 The console.log() Method

The `console.log()` method outputs content to the browser's developer console.

**Syntax:**
```javascript
console.log("message");
console.log(variable);
console.log(object);
```

### 4.3 Understanding the Code Structure

```javascript
document.write("hello in head");
```

**Breakdown:**
- `document` - Reference to the Document object (represents the web page)
- `.` - Member access operator
- `write` - A method of the Document class
- `("hello in head")` - String argument passed to the method

> **Key Insight**: In the statement `console.log(document)`, you see that `document` is a member (property) of the `Window` class. The `window` object is the global object in browsers.

---

## 5. The document and window Objects

### 5.1 The Window Object

The `window` object is the **global object** in browser JavaScript. It represents:
- The browser window
- Global variables and functions
- Browser APIs

**Key Properties and Methods:**
```javascript
window.document      // The document object
window.alert()       // Display alert box
window.prompt()      // Display input dialog
window.confirm()     // Display confirmation dialog
window.location      // Current URL
window.console       // Console object
```

### 5.2 The Document Object

The `document` object represents the web page loaded in the browser. It is an instance of the **Document** class.

**Relationship:**
```
Window (global object)
└── document (Document object)
    └── write() method
    └── getElementById() method
    └── ... more methods
```

**Example:**
```javascript
console.log(document);  // Displays Document object with all its properties
console.log(window);    // Displays Window object with all its properties
```

### 5.3 Understanding the Hierarchy

```
Window Object (Global)
├── document (Document Object)
├── console (Console Object)
├── location (Location Object)
├── history (History Object)
├── navigator (Navigator Object)
└── ... more properties
```

---

## 6. Order of Execution

### 6.1 Top-to-Bottom Execution

JavaScript code is executed **top to bottom** as the browser parses the HTML document.

**Example:**
```html
<script>
    document.write("First");
</script>
<p>Middle</p>
<script>
    document.write("Last");
</script>
```

**Output:**
```
First
Middle
Last
```

### 6.2 Blocking Behavior

By default, `<script>` tags are **blocking** - the browser stops parsing HTML until the script is executed.

**Diagram: Script Execution Flow**
```
HTML Parsing → Script Found → STOP Parsing → Execute Script → Resume Parsing → Continue...
```

---

## 7. External JavaScript Files

### 7.1 Why Use External Files?

| Advantage | Description |
|-----------|-------------|
| **Separation of Concerns** | Keep HTML and JavaScript separate |
| **Reusability** | Same JS file can be used across multiple HTML pages |
| **Caching** | Browsers cache external files, improving performance |
| **Maintainability** | Easier to manage and update code |
| **Team Collaboration** | Different team members can work on different files |

### 7.2 Creating an External JavaScript File

**Step 1: Create a .js file (e.g., `ext.js`)**
```javascript
// ext.js
function call() {
    document.write("hello welcome to javascript");
}
```

**Step 2: Link it in HTML**
```html
<html>
<head>
    <title>VITA</title>
    <script src="js/ext.js"></script>
</head>
<body>
    <script>
        call();
    </script>
</body>
</html>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 1 | `<html>` | Root HTML element |
| 2 | `<head>` | Head section begins |
| 3 | `<title>VITA</title>` | Page title |
| 4 | `<script src="js/ext.js"></script>` | Links external JS file from `js` folder |
| 6 | `<body>` | Body section begins |
| 7-9 | `<script>call();</script>` | Calls the function defined in external file |

**Execution Flow:**
```
1. Browser starts parsing HTML
2. Reaches <script src="js/ext.js">
3. Fetches and executes ext.js
4. Function `call()` is now defined in memory
5. Reaches <script>call();</script> in body
6. Executes call() function
7. "hello welcome to javascript" is written to document
```

### 7.3 External JS with Variables

**External file (ext1.js):**
```javascript
var v = 9;

function call() {
    for(let i = 1; i < 7; i++) {
        document.write("<h" + i + ">Hello</h" + i + ">");
        document.write("<font size=" + i + ">Hello</font>");
    }
}
```

**HTML file:**
```html
<html>
<head>
    <title>VITA</title>
    <script type="text/javascript" src="ext1.js"></script>
</head>
<body>
    <input type="button" onclick="call()"/>
    <script>
        document.write(v);
        call();
    </script>
</body>
</html>
```

**Line-by-Line Explanation (ext1.js):**

| Line | Code | Explanation |
|------|------|-------------|
| 1 | `var v = 9;` | Declares global variable `v` with value 9 |
| 3 | `function call() {` | Function declaration begins |
| 4 | `for(let i = 1; i < 7; i++)` | Loop from 1 to 6 (for h1 to h6 tags) |
| 5 | `document.write("<h" + i + ">Hello</h" + i + ">")` | Dynamically creates h1-h6 tags |
| 6 | `document.write("<font size=" + i + ">Hello</font>")` | Creates font tags with increasing sizes |

**Output:**
```
9
<h1>Hello</h1><font size=1>Hello</font>
<h2>Hello</h2><font size=2>Hello</font>
... (continues for h3-h6)
```

> **Note**: When using events like `onclick`, if `document.write()` is called AFTER the page loads, it **replaces the entire page content**.

---

## 8. Using 'use strict'

### 8.1 What is 'use strict'?

`'use strict'` is a directive that enables **strict mode** in JavaScript. It enforces stricter parsing and error handling.

### 8.2 Why Use Strict Mode?

| Without 'use strict' | With 'use strict' |
|---------------------|-------------------|
| Undeclared variables are allowed | Undeclared variables throw error |
| Silent errors are ignored | Silent errors throw exceptions |
| `this` in functions is `window` | `this` in functions is `undefined` |
| Can use reserved keywords | Reserved keywords throw error |

### 8.3 Example: Without 'use strict'

```javascript
<script>
    a = 5;  // This works! Creates global variable on window
    document.write(a + "<br/>");
</script>
```

**Problem:**
- If you misspell a variable name (e.g., `Fnme` instead of `Fname`), JavaScript creates a NEW variable instead of throwing an error!
- This leads to hard-to-find bugs.

### 8.4 Example: With 'use strict'

```javascript
<script>
    'use strict'
    a = 5;  // ReferenceError: assignment to undeclared variable a
    document.write(a + "<br/>");
</script>
```

**Error Message:**
```
ReferenceError: assignment to undeclared variable a
```

### 8.5 Correct Way with 'use strict'

```javascript
<script>
    'use strict'
    var a = 5;  // Correct: variable is declared
    document.write(a + "<br/>");
</script>
```

> **Best Practice**: ALWAYS use `'use strict'` at the beginning of your JavaScript code for safer and more predictable programming.

### 8.6 Placement of 'use strict'

- **At the top of a script**: Applies to the entire script
- **At the top of a function**: Applies only to that function

```javascript
// Applies to entire script
'use strict';

function myFunction() {
    // strict mode applies here
}
```

```javascript
function strictFunction() {
    'use strict';
    // strict mode applies only inside this function
}

function normalFunction() {
    // normal mode here
}
```

---

## 9. Quick Reference

### 9.1 Key Concepts Summary

| Concept | Description |
|---------|-------------|
| `<script>` tag | Container for JavaScript code |
| `document.write()` | Writes content to HTML document |
| `console.log()` | Outputs to browser console |
| `window` object | Global browser object |
| `document` object | Represents the web page |
| `'use strict'` | Enables strict mode |
| External JS | Use `<script src="file.js">` |

### 9.2 Common Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `ReferenceError: x is not defined` | Using undeclared variable | Declare with `var`, `let`, or `const` |
| Script not executing | Wrong file path in `src` | Check path, use relative or absolute paths correctly |
| `undefined` output | Variable declared but not initialized | Initialize the variable |

### 9.3 Best Practices

1. ✅ Always use `'use strict'`
2. ✅ Declare variables before use
3. ✅ Use external JS files for larger projects
4. ✅ Place scripts at end of `<body>` for performance
5. ✅ Use meaningful variable and function names
6. ❌ Don't rely on global variables
7. ❌ Don't use `document.write()` after page load (use DOM manipulation)

---

## 10. Interview Questions

### Q1: What is JavaScript?
**Answer**: JavaScript is a lightweight, interpreted, object-oriented programming language with first-class functions. It is primarily used to create interactive and dynamic content on websites. It is dynamically typed and runs in the browser's JavaScript engine.

### Q2: What is the difference between `document.write()` and `console.log()`?
**Answer**: 
- `document.write()` writes content directly to the HTML document, visible to users
- `console.log()` outputs to the browser's developer console, intended for debugging

### Q3: What is the Window object?
**Answer**: The `window` object is the global object in browser JavaScript. It represents the browser window and provides access to browser APIs, the document object, and global functions like `alert()`, `prompt()`, and `confirm()`.

### Q4: What is 'use strict' and why should we use it?
**Answer**: `'use strict'` is a directive that enables strict mode in JavaScript. It enforces stricter parsing and error handling, preventing common mistakes like using undeclared variables. It helps write cleaner, more reliable code.

### Q5: Where can you place JavaScript code in an HTML document?
**Answer**: JavaScript can be placed:
1. Inside `<script>` tags in the `<head>` section
2. Inside `<script>` tags in the `<body>` section
3. In external `.js` files linked with `<script src="file.js">`

### Q6: What happens if `document.write()` is called after the page is fully loaded?
**Answer**: If `document.write()` is called after the page is fully loaded (e.g., in response to a button click), it will **completely replace** the existing page content with the new content.

---

## Navigation

← Previous: None (This is the first note) | Next: [02_Data_Types_and_Variables.md](./02_Data_Types_and_Variables.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 01*
