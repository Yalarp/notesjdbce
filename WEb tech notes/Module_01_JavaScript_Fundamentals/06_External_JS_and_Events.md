# External JavaScript and Events

## Table of Contents
1. [Introduction](#1-introduction)
2. [Adding External JavaScript Files](#2-adding-external-javascript-files)
3. [Introduction to Events](#3-introduction-to-events)
4. [Event Handling Methods](#4-event-handling-methods)
5. [Common Events](#5-common-events)
6. [Event Handling Best Practices](#6-event-handling-best-practices)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 Definition
**External JavaScript** refers to JavaScript code stored in separate `.js` files and linked to HTML documents. **Events** are actions or occurrences that happen in the browser, which JavaScript can respond to.

### 1.2 Purpose
- Separation of concerns (HTML structure, CSS styling, JS behavior)
- Code reusability across multiple pages
- Better caching and performance
- Easier maintenance and collaboration
- Responding to user interactions

---

## 2. Adding External JavaScript Files

### 2.1 Basic Syntax

**Step 1: Create a JavaScript file (ext.js)**
```javascript
// ext.js
function call() {
    document.write("hello welcome to javascript");
}
```

**Step 2: Link in HTML**
```html
<html>
<head>
    <title>VITA</title>
    <script type="text/javascript" src="ext.js"></script>
</head>
<body>
    <input type="button" onclick="call()"/>
    <script>
        call();
    </script>
</body>
</html>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 4 | `<script src="ext.js">` | Links external JS file |
| 4 | `type="text/javascript"` | Optional in HTML5 (default) |
| 7 | `onclick="call()"` | Calls function on button click |
| 8-10 | Inline script | Calls function immediately on page load |

### 2.2 Script with Variables in External File

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

**Line-by-Line Explanation:**

| Line | External File | Explanation |
|------|---------------|-------------|
| 1 | `var v = 9` | Global variable accessible from HTML |
| 3 | `function call()` | Function declaration |
| 4 | `for(let i = 1; i < 7; i++)` | Loop from 1 to 6 |
| 5 | `"<h" + i + ">"` | Creates h1, h2, h3, h4, h5, h6 dynamically |
| 6 | `"<font size=" + i + ">"` | Creates font tags with sizes 1-6 |

**Execution Flow:**
```
1. Browser loads HTML
2. Parses <head>, finds <script src="ext1.js">
3. Downloads and executes ext1.js
   - var v = 9 is declared globally
   - function call() is registered
4. Continues parsing <body>
5. Finds <input type="button">
6. Finds inline <script>
   - document.write(v) → prints 9
   - call() → generates headings
```

### 2.3 Script Placement Options

| Location | Behavior |
|----------|----------|
| `<head>` | Blocks rendering until loaded; functions available early |
| End of `<body>` | DOM ready when script runs; better performance |
| `async` attribute | Downloads in parallel, executes when ready |
| `defer` attribute | Downloads in parallel, executes after DOM ready |

```html
<!-- Blocking (traditional) -->
<script src="script.js"></script>

<!-- Async (order not guaranteed) -->
<script async src="script.js"></script>

<!-- Defer (order guaranteed, DOM ready) -->
<script defer src="script.js"></script>
```

---

## 3. Introduction to Events

### 3.1 What is an Event?
An event is something that happens in the browser:
- User actions (clicks, keystrokes, mouse movements)
- Browser actions (page load, resize, scroll)
- Form actions (submit, input change, focus)

### 3.2 Event-Driven Programming
JavaScript allows you to execute code when events are detected. This is the foundation of interactive web applications.

```
User Action → Event Triggered → Event Handler Executed → DOM Updated
```

---

## 4. Event Handling Methods

### 4.1 Method 1: Inline Event Handlers (HTML Attribute)

```html
<!DOCTYPE html>
<html>
<head>
    <script>
        function go() {
            alert("you clicked the button");
        }
    </script>
</head>
<body>
    <input type="button" value="Click Me" onclick="go()"/>
</body>
</html>
```

**Pros:**
- Simple and quick

**Cons:**
- Mixes HTML and JavaScript
- Hard to maintain
- Can only have one handler per event

### 4.2 Method 2: DOM Property Assignment

```html
<!DOCTYPE html>
<html>
<head>
    <script>
        function go() {
            alert("you clicked the button");
        }
    </script>
</head>
<body>
    <input type="button" value="Click Me" id="btn"/>
    <script>
        document.getElementById("btn").onclick = go;
    </script>
</body>
</html>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 10 | `id="btn"` | Gives the button an ID for reference |
| 12 | `document.getElementById("btn")` | Gets the button element |
| 12 | `.onclick = go` | Assigns function reference (no parentheses!) |

**Note:** We write `go` NOT `go()`. Using `go()` would execute immediately and assign the return value.

### 4.3 Method 3: addEventListener() (Recommended)

```html
<!DOCTYPE html>
<html>
<head></head>
<body>
    <input type="button" id="btn" value="Change URL">
    <script>
        function newLocation() {
            window.location = "p.html";
        }
        
        document.getElementById("btn").addEventListener("click", newLocation, false);
    </script>
</body>
</html>
```

**Syntax:**
```javascript
element.addEventListener(event, function, useCapture);
```

| Parameter | Description |
|-----------|-------------|
| `event` | Event type as string ("click", "mouseover", etc.) |
| `function` | Function to execute when event occurs |
| `useCapture` | `false` = bubbling phase (default), `true` = capturing phase |

**Advantages of addEventListener:**
- Multiple handlers for same event
- More control over event propagation
- Cleaner separation of concerns
- Works with dynamically added elements (with event delegation)

### 4.4 Comparison of Methods

| Feature | Inline | DOM Property | addEventListener |
|---------|--------|--------------|-----------------|
| Multiple handlers | ❌ No | ❌ No | ✅ Yes |
| Remove handler | ❌ No | ✅ Set to null | ✅ removeEventListener |
| Capture phase | ❌ No | ❌ No | ✅ Yes |
| Separation of concerns | ❌ No | ✅ Yes | ✅ Yes |

---

## 5. Common Events

### 5.1 Mouse Events

| Event | Description |
|-------|-------------|
| `click` | Mouse button clicked on element |
| `dblclick` | Mouse button double-clicked |
| `mousedown` | Mouse button pressed |
| `mouseup` | Mouse button released |
| `mouseover` | Mouse pointer enters element |
| `mouseout` | Mouse pointer leaves element |
| `mousemove` | Mouse pointer moves over element |
| `mouseenter` | Mouse enters (doesn't bubble) |
| `mouseleave` | Mouse leaves (doesn't bubble) |

### 5.2 Keyboard Events

| Event | Description |
|-------|-------------|
| `keydown` | Key pressed down |
| `keyup` | Key released |
| `keypress` | Key pressed (deprecated, use keydown) |

### 5.3 Form Events

| Event | Description |
|-------|-------------|
| `submit` | Form submitted |
| `reset` | Form reset |
| `focus` | Element receives focus |
| `blur` | Element loses focus |
| `change` | Input value changed |
| `input` | Input value being changed |

### 5.4 Window/Document Events

| Event | Description |
|-------|-------------|
| `load` | Page fully loaded |
| `DOMContentLoaded` | DOM ready (before images) |
| `unload` | User leaving page |
| `resize` | Window resized |
| `scroll` | Document scrolled |

### 5.5 Event Examples

**Click Event:**
```html
<button id="myBtn">Click Me</button>
<script>
    document.getElementById("myBtn").addEventListener("click", function() {
        alert("Button was clicked!");
    });
</script>
```

**Mouseover/Mouseout:**
```html
<div id="box" style="width:100px; height:100px; background:blue;">
    Hover me
</div>
<script>
    var box = document.getElementById("box");
    
    box.addEventListener("mouseover", function() {
        this.style.background = "red";
    });
    
    box.addEventListener("mouseout", function() {
        this.style.background = "blue";
    });
</script>
```

**Form Change Event:**
```html
<select id="mySelect">
    <option>Option 1</option>
    <option>Option 2</option>
</select>
<script>
    document.getElementById("mySelect").addEventListener("change", function() {
        alert("Selected: " + this.value);
    });
</script>
```

**Page Load Event:**
```javascript
window.addEventListener("load", function() {
    console.log("Page fully loaded");
});

document.addEventListener("DOMContentLoaded", function() {
    console.log("DOM ready");
});
```

---

## 6. Event Handling Best Practices

### 6.1 Always Put Script at End or Use DOMContentLoaded

**Problem:**
```html
<head>
    <script>
        // This FAILS! Element doesn't exist yet!
        document.getElementById("btn").onclick = function() {};
    </script>
</head>
<body>
    <button id="btn">Click</button>
</body>
```

**Solution 1: Put script at end**
```html
<body>
    <button id="btn">Click</button>
    <script>
        document.getElementById("btn").onclick = function() {};
    </script>
</body>
```

**Solution 2: Use DOMContentLoaded**
```html
<head>
    <script>
        document.addEventListener("DOMContentLoaded", function() {
            document.getElementById("btn").onclick = function() {};
        });
    </script>
</head>
<body>
    <button id="btn">Click</button>
</body>
```

**Solution 3: Use defer attribute**
```html
<head>
    <script defer src="script.js"></script>
</head>
```

### 6.2 Use Function References, Not Calls

```javascript
// ❌ WRONG - Executes immediately
button.onclick = myFunction();  // Assigns return value, not function

// ✅ CORRECT - Assigns reference
button.onclick = myFunction;    // Function executes on click
```

### 6.3 Avoid Inline Event Handlers

```html
<!-- ❌ Not recommended -->
<button onclick="doSomething()">Click</button>

<!-- ✅ Recommended -->
<button id="btn">Click</button>
<script>
    document.getElementById("btn").addEventListener("click", doSomething);
</script>
```

---

## 7. Quick Reference

### 7.1 External Script Linking

```html
<!-- Basic linking -->
<script src="path/to/script.js"></script>

<!-- With defer (recommended for most cases) -->
<script defer src="script.js"></script>

<!-- With async (for independent scripts) -->
<script async src="analytics.js"></script>
```

### 7.2 Event Binding Methods

```javascript
// Method 1: Inline (avoid)
<element onclick="handler()">

// Method 2: DOM property
element.onclick = handler;

// Method 3: addEventListener (recommended)
element.addEventListener("click", handler);

// Method 4: Remove event listener
element.removeEventListener("click", handler);
```

### 7.3 Common Event Patterns

```javascript
// Anonymous function
element.addEventListener("click", function() {
    // handle event
});

// Arrow function
element.addEventListener("click", () => {
    // handle event
});

// Named function
function handleClick() { /* ... */ }
element.addEventListener("click", handleClick);

// With event object
element.addEventListener("click", function(event) {
    event.preventDefault();  // Prevent default action
    event.target;           // Element that triggered event
    event.type;             // Event type ("click")
});
```

---

## 8. Interview Questions

### Q1: What are the benefits of using external JavaScript files?
**Answer**:
- Separation of concerns (HTML, CSS, JS separate)
- Code reusability across multiple pages
- Browser can cache the file for better performance
- Easier maintenance and collaboration
- Cleaner, more readable HTML

### Q2: What's the difference between placing script in head vs body?
**Answer**:
- **Head**: Script blocks HTML parsing; functions available before body loads
- **End of body**: DOM ready when script runs; better initial page load performance
- **With defer/async**: Can be in head without blocking

### Q3: What are the three ways to handle events in JavaScript?
**Answer**:
1. Inline event handlers: `<button onclick="fn()">`
2. DOM property: `element.onclick = fn`
3. addEventListener: `element.addEventListener("click", fn)`

### Q4: What's the difference between onclick and addEventListener?
**Answer**:
- `onclick` only allows one handler per event
- `addEventListener` allows multiple handlers
- `addEventListener` provides control over capturing/bubbling phase
- `addEventListener` handlers can be removed with `removeEventListener`

### Q5: Why should we use function references instead of function calls when assigning event handlers?
**Answer**: Using parentheses `()` executes the function immediately and assigns its return value. We want the function to execute when the event occurs, so we pass the reference without parentheses.

### Q6: What is the DOMContentLoaded event?
**Answer**: `DOMContentLoaded` fires when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading. It's the earliest point where you can safely manipulate the DOM.

---

## Navigation

← Previous: [05_Objects_Basics.md](./05_Objects_Basics.md) | Next: [07_Window_Methods.md](./07_Window_Methods.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 02*
