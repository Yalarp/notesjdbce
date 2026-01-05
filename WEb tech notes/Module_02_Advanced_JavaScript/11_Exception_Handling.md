# Exception Handling in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [What are Exceptions?](#2-what-are-exceptions)
3. [try-catch Block](#3-try-catch-block)
4. [Error Object Properties](#4-error-object-properties)
5. [Error Types](#5-error-types)
6. [Handling Multiple Exceptions](#6-handling-multiple-exceptions)
7. [The finally Block](#7-the-finally-block)
8. [Throwing Custom Exceptions](#8-throwing-custom-exceptions)
9. [Best Practices](#9-best-practices)
10. [Quick Reference](#10-quick-reference)
11. [Interview Questions](#11-interview-questions)

---

## 1. Introduction

### 1.1 Definition
**Exception handling** refers to the process of responding to and managing errors that occur during program execution. JavaScript provides the `try-catch-finally` construct to handle exceptions gracefully.

### 1.2 Purpose
- Prevent application crashes
- Gracefully handle errors
- Provide meaningful error messages
- Maintain program flow after errors
- Debug and log errors

### 1.3 Evolution
- **Pre-JavaScript 1.5**: Minimal error handling, developers relied on browser errors
- **JavaScript 1.5+**: Full support for `try-catch-finally` constructs

---

## 2. What are Exceptions?

### 2.1 Definition
Exceptions are errors that can be tracked and controlled. When JavaScript encounters an unsupported operation, it generates an exception with a message explaining the problem.

### 2.2 Example: Without Exception Handling

```javascript
<script language="JavaScript">
colours[2] = "red";  // colours is not defined
</script>
```

**Output:**
```
Uncaught ReferenceError: colours is not defined
    at 00without_trycatch.html:4
```

**What Happens:**
1. JavaScript tries to access `colours[2]`
2. `colours` is not defined in the namespace
3. JavaScript generates a `ReferenceError` exception
4. Script execution STOPS
5. Error message displayed in console

---

## 3. try-catch Block

### 3.1 Basic Syntax

```javascript
try {
    // Code that might throw an error
    execute this block
} 
catch (error) {
    // Code to handle the error
    execute this block if error
}
```

### 3.2 Basic Example

```javascript
<script language="JavaScript">
try {
    colours[2] = "red";
} 
catch (e) {
    alert("Oops! Something bad just happened.");
}
</script>
```

**Output:**
```
Oops! Something bad just happened.
```

**Key Points:**
- Code in `try` block is executed
- If error occurs, control moves to `catch` block
- Error is captured in variable `e`
- Script continues after catch block

### 3.3 Execution Flow

```
┌─────────────────────────────────────────────┐
│                   TRY                        │
│  Execute code that might throw an error     │
└─────────────────┬───────────────────────────┘
                  │
        ┌─────────┴─────────┐
        │                   │
    No Error            Error Occurs
        │                   │
        ▼                   ▼
┌───────────────┐   ┌───────────────────────┐
│  Continue     │   │        CATCH          │
│  after try    │   │  Handle the error     │
└───────────────┘   └───────────┬───────────┘
                                │
                                ▼
                        Continue after catch
```

### 3.4 Error Object Inheritance

```
Error Object Hierarchy:

       Object
          │
        Error
       /  |  \
ReferenceError  TypeError  SyntaxError  ...
```

---

## 4. Error Object Properties

### 4.1 Built-in Properties

| Property | Description |
|----------|-------------|
| `name` | Error type (e.g., "ReferenceError") |
| `message` | Error message |
| `fileName` | File where error occurred (non-standard) |
| `lineNumber` | Line number of error (non-standard) |
| `columnNumber` | Column number (non-standard) |
| `stack` | Stack trace |

### 4.2 Accessing Error Properties

```javascript
<script language="JavaScript">
try {
    colours[2] = "red";
} 
catch (e) {
    alert(e.message + " Oops! Something bad just happened. " + e.name);
}
</script>
```

**Output:**
```
colours is not defined Oops! Something bad just happened. ReferenceError
```

### 4.3 Complete Error Information

```javascript
try {
    colours[2] = "red";
} catch (e) {
    console.log("Error Name:", e.name);
    console.log("Error Message:", e.message);
    console.log("File:", e.fileName);      // Non-standard
    console.log("Line:", e.lineNumber);    // Non-standard
    console.log("Column:", e.columnNumber); // Non-standard
    console.log("Stack:", e.stack);
}
```

---

## 5. Error Types

### 5.1 JavaScript Error Types

JavaScript 1.5 defines six primary error types:

| Error Type | Description | Example |
|------------|-------------|---------|
| **EvalError** | Error in eval() function | Deprecated, rarely used |
| **RangeError** | Numeric value out of range | `new Array(-1)` |
| **ReferenceError** | Invalid reference | `undefinedVar = 5` |
| **SyntaxError** | Syntax error in code | `eval("vara x = 1")` |
| **TypeError** | Type mismatch | `null.f()` |
| **URIError** | Error in URI functions | `decodeURI("%")` |

### 5.2 Error Type Examples

```javascript
// ReferenceError
try {
    alert(someArr[18]);  // someArr not defined
} catch (e) {
    console.log(e.name);  // "ReferenceError"
}

// TypeError
try {
    null.f();  // Cannot call method on null
} catch (e) {
    console.log(e.name);  // "TypeError"
}

// RangeError
try {
    var someArr = new Array(89723742304323248456);  // Too large
} catch (e) {
    console.log(e.name);  // "RangeError"
}

// SyntaxError
try {
    eval("vara count = 99");  // Invalid syntax
} catch (e) {
    console.log(e.name);  // "SyntaxError"
}
```

### 5.3 Checking Error Type

```javascript
try {
    colours[2] = "red";
} catch (e) {
    if (e instanceof ReferenceError) {
        alert("Bad or undefined variable!");
    }
}
```

---

## 6. Handling Multiple Exceptions

### 6.1 Multiple Exception Pattern

```javascript
try {
    // execute this block
} catch (error) {
    if (error instanceof TypeError) {
        // handle TypeError
    }
    else if (error instanceof RangeError) {
        // handle RangeError
    }
    else if (error instanceof SyntaxError) {
        // handle SyntaxError
    }
    else {
        // handle all other errors
    }
}
```

### 6.2 Complete Example

```javascript
<script language="JavaScript">
// Ask for user input
code = prompt("Enter some JavaScript code");

// Run the code and catch errors
try {
    eval(code);
    alert("This statement may not get executed");
} catch (e) {
    if (e instanceof TypeError) {
        alert(e.message + " Variable type problem, check your variable definitions! " + e.name);
    }
    else if (e instanceof RangeError) {
        alert(e.message + " Number out of range! " + e.name);
    }
    else if (e instanceof SyntaxError) {
        alert(e.message + " Syntax error in code! " + e.name);
    }
    else {
        alert(e.message + " An unspecified error occurred! " + e.name);
    }
} finally {
    alert("Thank you for playing. Come back soon!");
}
</script>
```

**Test Cases:**
- **ReferenceError**: `alert(someArr[18])`
- **TypeError**: `null.f()`
- **RangeError**: `var someArr = new Array(89723742304323248456)`
- **SyntaxError**: `vara count = 99`

---

## 7. The finally Block

### 7.1 Syntax

```javascript
try {
    // Code that might throw an error
} 
catch (error) {
    // Error handling code
} 
finally {
    // ALWAYS executes after try block
}
```

### 7.2 Key Points

- The `finally` block executes **regardless** of whether an error occurred
- Executes after `try` and `catch` blocks complete
- Used for cleanup operations (closing files, connections, etc.)
- Executes even if there's a `return` statement in try/catch

### 7.3 Example

```javascript
function divide(a, b) {
    try {
        console.log("Attempting division...");
        if (b === 0) {
            throw new Error("Division by zero!");
        }
        return a / b;
    } catch (e) {
        console.log("Error:", e.message);
        return null;
    } finally {
        console.log("Cleanup: Division attempt complete");
    }
}

divide(10, 2);   // Attempting..., Cleanup: Division...
divide(10, 0);   // Attempting..., Error: Division by zero!, Cleanup: Division...
```

### 7.4 General Catch (Without Error Variable)

```javascript
try {
    // execute this block
} 
catch {
    // catch without error variable (ES2019)
    // execute this block if error
} 
finally {
    // execute this block after the try block
}
```

---

## 8. Throwing Custom Exceptions

### 8.1 The throw Statement

Use `throw` to generate custom exceptions:

```javascript
throw expression;  // expression becomes the error
```

### 8.2 Creating Custom Errors

```javascript
// Create new Error object
Idiot = new Error("Idiot user detected, terminating...");

function checkAge() {
    try {
        if (document.forms[0].age.value > 99) {
            throw Idiot;
        }
    } 
    catch (e) {
        alert(e.name + "  " + e.message);
    }
}
```

**Memory Diagram:**
```
Idiot (Error object):
┌────────────────────────────────────────┐
│ name: "Error"                          │
│ message: "Idiot user detected..."      │
└────────────────────────────────────────┘
```

### 8.3 Complete Form Validation Example

```html
<html>
<head>
<script language="JavaScript">
// Create new Error objects
badNameError = new Error("System user name does not match actual user name");
noNameError = new Error("System user name cannot be blank");

function mainExceptionHandler(e) {
    alert(e.message);
}

function validateForm() {
    checkName();
}

function checkName() {
    try {
        if (document.forms[0].username.value == "") {
            throw noNameError;
        }
        if (document.forms[0].username.value != "john") {
            throw badNameError;
        }
    } 
    catch (e) {
        // Any and all errors will go to this handler
        mainExceptionHandler(e);
    }
}
</script>
</head>
<body>
    <form onSubmit="validateForm()">
        Enter your system username:
        <input type="text" name="username">
        <br>
        <input type="submit" name="submit" value="Go">
    </form>
</body>
</html>
```

### 8.4 Throwing Different Types

```javascript
// Throw string
throw "Error occurred";

// Throw number
throw 404;

// Throw boolean
throw false;

// Throw object (recommended)
throw new Error("Custom error message");

// Throw built-in error types
throw new TypeError("Invalid type");
throw new RangeError("Value out of range");
```

---

## 9. Best Practices

### 9.1 Do's

| Practice | Description |
|----------|-------------|
| ✅ Specific handling | Catch specific error types |
| ✅ Meaningful messages | Provide helpful error messages |
| ✅ Log errors | Log to console for debugging |
| ✅ Clean up | Use finally for cleanup |
| ✅ Re-throw | Re-throw if you can't handle |

### 9.2 Don'ts

| Anti-Pattern | Problem |
|--------------|---------|
| ❌ Empty catch | Silently ignoring errors |
| ❌ Catch all | Catching too broadly |
| ❌ eval() | Security risk, avoid if possible |
| ❌ Generic messages | "Something went wrong" unhelpful |

### 9.3 Proper Error Handling

```javascript
// BAD - Empty catch
try {
    eval("some gibberish");
} catch (e) {
    // ignore it - DON'T DO THIS!
}

// GOOD - Proper handling
try {
    someOperation();
} catch (e) {
    if (e instanceof TypeError) {
        console.error("Type error:", e.message);
        // Handle or recover
    } else {
        // Re-throw errors you can't handle
        throw e;
    }
}
```

---

## 10. Quick Reference

### 10.1 Basic Syntax

```javascript
try {
    // risky code
} catch (e) {
    // handle error
} finally {
    // always runs
}
```

### 10.2 Error Properties

```javascript
e.name       // Error type
e.message    // Error message
e.stack      // Stack trace
```

### 10.3 Throwing Errors

```javascript
throw new Error("message");
throw new TypeError("message");
throw new RangeError("message");
throw new SyntaxError("message");
throw new ReferenceError("message");
throw new URIError("message");
```

### 10.4 Type Checking

```javascript
if (e instanceof TypeError) { }
if (e instanceof RangeError) { }
if (e instanceof SyntaxError) { }
if (e instanceof ReferenceError) { }
```

---

## 11. Interview Questions

### Q1: What is exception handling in JavaScript?
**Answer**: Exception handling is a mechanism to handle runtime errors gracefully using `try-catch-finally` blocks. It prevents application crashes and allows developers to manage errors appropriately.

### Q2: What is the difference between try-catch and if-else for error handling?
**Answer**: `try-catch` handles runtime exceptions (errors that occur during execution), while `if-else` handles expected conditions. `try-catch` can catch unexpected errors; `if-else` only checks predetermined conditions.

### Q3: What does the finally block do?
**Answer**: The `finally` block executes regardless of whether an exception occurred or not. It's used for cleanup operations like closing connections, files, or freeing resources.

### Q4: Name the six error types in JavaScript.
**Answer**:
1. **EvalError** - Error in eval()
2. **RangeError** - Number out of range
3. **ReferenceError** - Invalid reference
4. **SyntaxError** - Syntax error
5. **TypeError** - Type mismatch
6. **URIError** - Error in URI functions

### Q5: How do you throw a custom exception?
**Answer**: Use the `throw` statement with an Error object:
```javascript
throw new Error("Custom message");
// or
const customError = new Error("Custom error");
throw customError;
```

### Q6: Can you have try without catch?
**Answer**: Yes, but you must have a `finally` block. `try` must be followed by either `catch`, `finally`, or both.

### Q7: What happens if an exception is not caught?
**Answer**: The exception propagates up the call stack. If no handler catches it, it becomes an unhandled exception, typically causing the script to stop and an error message to appear in the console.

---

## Navigation

← Previous: [10_Private_and_Protected_Members.md](./10_Private_and_Protected_Members.md) | Next: [12_Generators_and_Iterators.md](./12_Generators_and_Iterators.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 03*
