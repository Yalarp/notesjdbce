# Window Methods in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Window Object Overview](#2-window-object-overview)
3. [Dialog Methods](#3-dialog-methods)
4. [Navigation Methods](#4-navigation-methods)
5. [Timing Methods](#5-timing-methods)
6. [Utility Methods](#6-utility-methods)
7. [Scrolling Methods](#7-scrolling-methods)
8. [Window Properties](#8-window-properties)
9. [Quick Reference](#9-quick-reference)
10. [Interview Questions](#10-interview-questions)

---

## 1. Introduction

### 1.1 Definition
The `window` object represents the browser window and is the global object in client-side JavaScript. All global variables and functions become properties/methods of the window object.

### 1.2 Purpose
- Interact with browser window
- Display dialogs to users
- Navigate to different pages
- Schedule code execution
- Control window appearance

### 1.3 Key Point
In browsers, `window` is the global object. You can access its properties and methods with or without the `window.` prefix:

```javascript
window.alert("Hello");  // With prefix
alert("Hello");         // Without prefix (same thing)
```

---

## 2. Window Object Overview

### 2.1 Key Window Methods

| Category | Methods |
|----------|---------|
| **Dialogs** | `alert()`, `prompt()`, `confirm()` |
| **Navigation** | `open()`, `close()`, `location` |
| **Timing** | `setInterval()`, `clearInterval()`, `setTimeout()`, `clearTimeout()` |
| **Utility** | `isNaN()`, `isFinite()`, `eval()`, `parseInt()`, `parseFloat()` |
| **Scrolling** | `scrollBy()`, `scrollTo()`, `scrollIntoView()` |
| **Window Control** | `resizeBy()`, `resizeTo()`, `moveBy()`, `moveTo()` |

### 2.2 Key Window Properties

| Property | Description |
|----------|-------------|
| `document` | The Document object |
| `location` | Current URL information |
| `history` | Browser history |
| `navigator` | Browser information |
| `screen` | Screen dimensions |
| `console` | Developer console |
| `localStorage` | Persistent storage |
| `sessionStorage` | Session storage |

---

## 3. Dialog Methods

### 3.1 alert()

Displays a message box with an OK button.

**Syntax:**
```javascript
alert(message);
window.alert(message);
```

**Example:**
```javascript
<script>
alert("hello <br/> world");  // <br/> NOT interpreted as HTML
alert("hello \n world");     // \n creates new line
</script>
```

**Output:**
```
hello <br/> world    // First alert - literal text

hello                // Second alert - actual new line
 world
```

**Custom Alert Function:**
```javascript
<script>
alert = function(a) {
    document.write(a);  // Now "alert" writes to document
}
alert("hello");  // Writes "hello" to the page
</script>
```

> **Note:** This shows that built-in functions can be overridden (though you shouldn't do this in practice).

### 3.2 prompt()

Displays a dialog asking for input.

**Syntax:**
```javascript
prompt(message, defaultValue);
```

**Example:**
```javascript
<script>
var no1 = window.prompt("enter number", 5);  // Default value: 5
var b = parseInt(no1);                        // Convert to integer
var no2 = prompt();                           // Empty prompt

document.write(no1 + no2);    // String concatenation ("56")
document.write("<br/>");
document.write(no1 * no2);    // Numeric multiplication (30)
document.write("<br/>");
document.write(typeof(no1));  // "string"

pno1 = parseInt(no1);
pno2 = parseInt(no2);
var ans = pno1 + pno2;
document.write(ans);          // Numeric addition (11)
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 1 | `prompt("enter number", 5)` | Shows prompt with "5" as default |
| 2 | `parseInt(no1)` | Converts string to integer |
| 5 | `no1 + no2` | + with strings = concatenation |
| 7 | `no1 * no2` | * converts strings to numbers automatically |
| 9 | `typeof(no1)` | prompt() always returns string |
| 11-13 | `parseInt()` | Explicit conversion for addition |

**Key Points:**
- `prompt()` ALWAYS returns a string (or null if cancelled)
- Use `parseInt()` or `parseFloat()` for number conversion
- Use `+` (unary) for quick conversion: `+no1`

**Test Cases:**

| Input | parseInt() | + (unary) |
|-------|------------|-----------|
| "5" | 5 | 5 |
| "5.5" | 5 (truncates) | 5.5 |
| "5abc" | 5 (parses until non-digit) | NaN |
| "abc" | NaN | NaN |

### 3.3 confirm()

Displays a dialog with OK and Cancel buttons.

**Syntax:**
```javascript
var result = confirm(message);
```

**Example:**
```javascript
<script>
var a = confirm("do you want to continue");
alert(a);  // true (OK clicked) or false (Cancel clicked)

if (a) {
    console.log("User confirmed");
} else {
    console.log("User cancelled");
}
</script>
```

**Return Values:**
- `true` - User clicked OK
- `false` - User clicked Cancel or closed dialog

---

## 4. Navigation Methods

### 4.1 open()

Opens a new browser window or tab.

**Syntax:**
```javascript
window.open(URL, name, specs);
```

**Parameters:**

| Parameter | Description |
|-----------|-------------|
| `URL` | Page to open (optional, defaults to about:blank) |
| `name` | Target: `_blank` (new tab), `_self`, or window name |
| `specs` | Comma-separated list of window features |

**Specs Options:**

| Option | Description |
|--------|-------------|
| `width=pixels` | Window width (min 100) |
| `height=pixels` | Window height (min 100) |
| `left=pixels` | Window left position |
| `top=pixels` | Window top position |
| `menubar=yes|no` | Show menu bar |
| `toolbar=yes|no` | Show toolbar |
| `scrollbars=yes|no` | Show scrollbars |
| `resizable=yes|no` | Allow resizing |
| `fullscreen=yes|no` | Open in fullscreen |

**Examples:**
```javascript
// Open in same window
window.open('p.html');

// Open in new tab
window.open('p.html', '_blank');

// Open with specific dimensions
window.open('p.html', '_blank', 'height=200,width=200');

// Open popup with features
function openPopup() {
    window.open('popup.html', 'myPopup', 
        'width=400,height=300,left=100,top=100,scrollbars=yes');
}
```

### 4.2 close()

Closes the current window (only works for windows opened by script).

```javascript
window.close();
```

### 4.3 location

Gets/sets the current URL. It's both a property and an object.

**Redirecting Users:**
```javascript
<script>
function newLocation() { 
    window.location = "p.html";  // Redirect to p.html
}
</script>

<input type="button" id="btn" value="Change URL">
<script>
document.getElementById("btn").addEventListener("click", newLocation, false);
</script>
```

**location Properties:**

| Property | Description | Example |
|----------|-------------|---------|
| `location.href` | Full URL | `http://site.com:8080/page?q=1#top` |
| `location.protocol` | Protocol | `http:` |
| `location.host` | Host with port | `site.com:8080` |
| `location.hostname` | Host only | `site.com` |
| `location.port` | Port number | `8080` |
| `location.pathname` | Path | `/page` |
| `location.search` | Query string | `?q=1` |
| `location.hash` | Fragment | `#top` |

---

## 5. Timing Methods

### 5.1 setTimeout()

Executes code once after a specified delay.

**Syntax:**
```javascript
var timerId = setTimeout(function, milliseconds);
```

**Example:**
```javascript
<script>
// Execute once after 6 seconds
var t = setTimeout("alert('hi')", 6000);
console.log(t);  // Timer ID

// Using function reference
setTimeout(function() {
    alert("6 seconds passed");
}, 6000);

// Cancel the timeout
clearTimeout(t);
</script>
```

### 5.2 setInterval()

Executes code repeatedly at specified intervals.

**Syntax:**
```javascript
var intervalId = setInterval(function, milliseconds);
```

**Example:**
```javascript
<script>
// Execute every 1 second
var t = setInterval("alert('hi')", 1000);

// Stop after some condition
setTimeout(function() {
    clearInterval(t);  // Stops the interval
}, 5000);
</script>
```

### 5.3 Comparison

| Method | Execution | Use Case |
|--------|-----------|----------|
| `setTimeout()` | Once after delay | Delayed actions |
| `setInterval()` | Repeated at intervals | Animations, polling |
| `clearTimeout()` | Cancels setTimeout | Stop pending action |
| `clearInterval()` | Cancels setInterval | Stop repeating action |

### 5.4 Practical Examples

**Countdown Timer:**
```javascript
let count = 10;
let timerId = setInterval(function() {
    console.log(count);
    count--;
    if (count < 0) {
        clearInterval(timerId);
        console.log("Countdown complete!");
    }
}, 1000);
```

**Auto-Refresh (30 seconds):**
```javascript
setTimeout(function() {
    location.reload();
}, 30000);
```

**Simple Animation:**
```javascript
let position = 0;
let box = document.getElementById("box");
let animation = setInterval(function() {
    position += 5;
    box.style.left = position + "px";
    if (position >= 400) {
        clearInterval(animation);
    }
}, 50);
```

---

## 6. Utility Methods

### 6.1 eval()

Evaluates a string as JavaScript code.

**Syntax:**
```javascript
eval(string);
```

**Examples:**
```javascript
<script>
var a = "5+2-3";
document.write(a);           // "5+2-3" (string)
document.write(eval(a));     // 4 (evaluated)

document.write(eval("5+2-3*6/2"));  // -2
// Calculation: 5+2-9 = -2 (follows BODMAS)

document.write(eval("55+6"));  // 61
</script>
```

**Dynamic Variable Access:**
```javascript
<script>
var no1 = prompt("enter no1", "5");
var no2 = prompt("enter no2", "5");
var no3 = prompt("enter no3", "5");

for(var i = 1; i <= 3; i++) {
    document.write("no" + i + ": ");
    document.write(eval("no" + i));  // Accesses no1, no2, no3
    document.write("<br/>");
}
</script>
```

**Output:**
```
no1: 5
no2: 5
no3: 5
```

> **⚠️ Security Warning:** `eval()` is dangerous! It can execute malicious code. Avoid using it with user input. This is related to **XSS** (Cross-Site Scripting) and **CSRF** attacks.

### 6.2 isNaN()

Checks if a value is Not-a-Number.

```javascript
isNaN(123);      // false (is a number)
isNaN("Hello");  // true (not a number)
isNaN("123");    // false (can be converted to number)
isNaN(NaN);      // true
isNaN(undefined); // true
isNaN(null);     // false (null converts to 0)
```

### 6.3 isFinite()

Checks if a value is a finite number.

```javascript
isFinite(123);        // true
isFinite(Infinity);   // false
isFinite(-Infinity);  // false
isFinite(NaN);        // false
isFinite("123");      // true (converted to number)
```

### 6.4 parseInt() and parseFloat()

```javascript
parseInt("10");       // 10
parseInt("10.5");     // 10 (truncates decimal)
parseInt("10px");     // 10 (parses until non-digit)
parseInt("hello");    // NaN

parseFloat("10.5");   // 10.5
parseFloat("10.5px"); // 10.5
parseFloat("hello");  // NaN

// With radix (base)
parseInt("10", 2);    // 2 (binary 10 = decimal 2)
parseInt("ff", 16);   // 255 (hex ff = decimal 255)
```

---

## 7. Scrolling Methods

### 7.1 scrollBy()

Scrolls the window by relative pixels.

```javascript
window.scrollBy(x, y);

// Scroll down 100 pixels
window.scrollBy(0, 100);

// Scroll right and down
window.scrollBy(50, 50);

// Scroll up (negative)
window.scrollBy(0, -100);
```

### 7.2 scrollTo()

Scrolls to absolute coordinates.

```javascript
window.scrollTo(x, y);

// Scroll to top
window.scrollTo(0, 0);

// Scroll to position 0, 500
window.scrollTo(0, 500);
```

### 7.3 scrollIntoView()

Scrolls an element into the visible area.

```javascript
element.scrollIntoView();       // Element at TOP of viewport
element.scrollIntoView(true);   // Same as above
element.scrollIntoView(false);  // Element at BOTTOM of viewport

// With options
element.scrollIntoView({
    behavior: "smooth",   // "auto" or "smooth"
    block: "start"        // "start", "center", "end", "nearest"
});
```

### 7.4 Forbid Scrolling

```javascript
// Freeze the page
document.body.style.overflow = "hidden";

// Restore scrolling
document.body.style.overflow = "";
```

**Use Case:** Show a modal/popup that requires user attention.

### 7.5 Complete Example

```html
<body style="height: 2000px;">
    <button onclick="window.scrollBy(0, 100)">
        Scroll Down 100px
    </button>
    
    <button onclick="window.scrollTo(0, 0)">
        Scroll to Top
    </button>
    
    <div id="target" style="margin-top: 1500px;">Target Element</div>
    
    <button onclick="document.getElementById('target').scrollIntoView()">
        Scroll to Target
    </button>
    
    <button onclick="document.body.style.overflow = 'hidden'">
        Disable Scroll
    </button>
    
    <button onclick="document.body.style.overflow = ''">
        Enable Scroll
    </button>
</body>
```

---

## 8. Window Properties

### 8.1 Dimension Properties

| Property | Description |
|----------|-------------|
| `window.innerWidth` | Viewport width (including scrollbar) |
| `window.innerHeight` | Viewport height |
| `window.outerWidth` | Browser window width |
| `window.outerHeight` | Browser window height |
| `screen.width` | Screen width |
| `screen.height` | Screen height |

### 8.2 Position Properties

| Property | Description |
|----------|-------------|
| `window.screenX` | Window X position on screen |
| `window.screenY` | Window Y position on screen |
| `window.scrollX` | Horizontal scroll position |
| `window.scrollY` | Vertical scroll position |

### 8.3 Example

```javascript
console.log("Viewport:", window.innerWidth, "x", window.innerHeight);
console.log("Window:", window.outerWidth, "x", window.outerHeight);
console.log("Screen:", screen.width, "x", screen.height);
console.log("Scroll position:", window.scrollX, window.scrollY);
```

---

## 9. Quick Reference

### 9.1 Dialog Methods

```javascript
alert("message");                    // Show message
var result = confirm("question?");   // Returns true/false
var input = prompt("message", "default");  // Returns string
```

### 9.2 Timing Methods

```javascript
// Execute once after delay
var id = setTimeout(function, delay);
clearTimeout(id);

// Execute repeatedly
var id = setInterval(function, interval);
clearInterval(id);
```

### 9.3 Navigation

```javascript
window.location = "url";        // Redirect
window.location.href = "url";   // Same as above
window.location.reload();       // Refresh page
window.open("url", "_blank");   // New window/tab
window.close();                 // Close window
```

### 9.4 Scrolling

```javascript
window.scrollBy(x, y);          // Relative scroll
window.scrollTo(x, y);          // Absolute scroll
element.scrollIntoView();       // Scroll element into view
```

### 9.5 Common Window Properties

```javascript
window.document         // The document
window.location         // URL information
window.history          // Browser history
window.navigator        // Browser info
window.localStorage     // Local storage
window.sessionStorage   // Session storage
```

---

## 10. Interview Questions

### Q1: What is the difference between window and document?
**Answer**: 
- `window` is the global object representing the browser window; it contains properties like `location`, `history`, and methods like `alert()`, `setTimeout()`
- `document` is a property of window representing the HTML document; it's used for DOM manipulation

### Q2: What is the difference between setTimeout and setInterval?
**Answer**:
- `setTimeout` executes a function ONCE after a specified delay
- `setInterval` executes a function REPEATEDLY at specified intervals
- Both return IDs that can be used with `clearTimeout`/`clearInterval` to cancel

### Q3: Why is eval() considered dangerous?
**Answer**: `eval()` executes any string as JavaScript code. If user input is passed to eval(), malicious code could be executed, leading to XSS (Cross-Site Scripting) attacks. It also makes code harder to optimize and debug.

### Q4: What does prompt() return?
**Answer**: `prompt()` always returns a string (the user's input) or `null` if the user clicked Cancel. Even if the user enters a number, it's returned as a string.

### Q5: How do you redirect a user to another page?
**Answer**: Multiple ways:
- `window.location = "url"`
- `window.location.href = "url"`
- `window.location.assign("url")`
- `window.location.replace("url")` (no history entry)

### Q6: What's the difference between scrollBy and scrollTo?
**Answer**:
- `scrollBy(x, y)` scrolls RELATIVE to current position
- `scrollTo(x, y)` scrolls to ABSOLUTE coordinates from document origin

### Q7: How can you prevent a page from scrolling?
**Answer**: Set `document.body.style.overflow = "hidden"`. To restore, set it back to `""`.

---

## Navigation

← Previous: [06_External_JS_and_Events.md](./06_External_JS_and_Events.md) | Next: [08_Closures.md](../Module_02_Advanced_JavaScript/08_Closures.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 02*
