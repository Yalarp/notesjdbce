# History and Navigator Objects

## Table of Contents
1. [Introduction](#1-introduction)
2. [Navigator Object](#2-navigator-object)
3. [Navigator Properties](#3-navigator-properties)
4. [History Object](#4-history-object)
5. [History Methods](#5-history-methods)
6. [Practical Examples](#6-practical-examples)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 Browser Object Model (BOM)
The `navigator` and `history` objects are part of the Browser Object Model (BOM), which provides access to browser-specific functionality.

```
window
├── navigator  ← Browser information
├── history    ← Session history
├── location   ← Current URL
├── screen     ← Screen information
└── document   ← DOM
```

---

## 2. Navigator Object

### 2.1 Definition
The `window.navigator` object contains information about the visitor's browser. It can be accessed as `navigator` or `window.navigator`.

### 2.2 Basic Example

```javascript
var browser = navigator.appName;
var b_version = navigator.appVersion;
var apcode = navigator.appCodeName;
var lang = navigator.language;
var b = navigator.cookieEnabled;

document.write("Browser name: " + browser);
document.write("<br />");
document.write("Browser version: " + b_version);
document.write("<br />");
document.write("app_code: " + apcode);
document.write("<br />");
document.write("lang: " + lang);
document.write("cookie enabled: " + b);
```

**Output:**
```
Browser name: Netscape
Browser version: 5.0 (Windows)
app_code: Mozilla
lang: en-US
cookie enabled: true
```

---

## 3. Navigator Properties

### 3.1 Properties Table

| Property | Description | Note |
|----------|-------------|------|
| `appName` | Application name | Returns "Netscape" for Chrome, Firefox, IE, Safari, Opera |
| `appCodeName` | Code name | Returns "Mozilla" for most browsers |
| `appVersion` | Version information | Browser version and platform |
| `language` | Browser language | e.g., "en-US" |
| `cookieEnabled` | Cookies enabled? | true/false |
| `onLine` | Online status | true if online |
| `platform` | Operating system | e.g., "Win32" |
| `userAgent` | Full user agent string | Most detailed info |

### 3.2 Browser Identification Issue

> **Warning:** Don't rely on `appName` or `appCodeName` for browser detection!

| Property | Chrome | Firefox | IE | Safari | Opera |
|----------|--------|---------|----|---------| ------|
| `appName` | Netscape | Netscape | Netscape | Netscape | Netscape |
| `appCodeName` | Mozilla | Mozilla | Mozilla | Mozilla | Mozilla |

### 3.3 Checking Online Status

```javascript
if (navigator.onLine) {
    console.log("You are online!");
} else {
    console.log("You are offline!");
}
```

### 3.4 Getting Platform Information

```javascript
console.log("Platform: " + navigator.platform);
// e.g., "Win32", "MacIntel", "Linux x86_64"
```

### 3.5 User Agent String

```javascript
console.log(navigator.userAgent);
// Example output:
// "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 
//  (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
```

---

## 4. History Object

### 4.1 Definition
The `window.history` object contains the browser's session history (pages visited in the current window/tab).

### 4.2 Properties

| Property | Description |
|----------|-------------|
| `length` | Number of entries in history |

```javascript
console.log(history.length);  // Number of pages in history
```

---

## 5. History Methods

### 5.1 Methods Table

| Method | Description | Equivalent |
|--------|-------------|------------|
| `back()` | Go to previous page | Browser back button |
| `forward()` | Go to next page | Browser forward button |
| `go(n)` | Go to specific page | n can be positive or negative |

### 5.2 history.back()

```html
<input type="button" value="back" onclick="history.back()">
```

Same as clicking the browser's back button.

### 5.3 history.forward()

```html
<input type="button" value="next" onclick="history.forward()">
```

Same as clicking the browser's forward button.

### 5.4 history.go()

```javascript
history.go(-1);  // Same as back()
history.go(1);   // Same as forward()
history.go(-2);  // Go back 2 pages
history.go(0);   // Reload current page
```

---

## 6. Practical Examples

### 6.1 Navigation Between Pages

**main.html:**
```html
<html>
<body>
    <a href="copy.html">Go to next file</a>
    <input type="button" value="next" onclick="history.forward()">
</body>
</html>
```

**copy.html:**
```html
<html>
<head>
<script>
function copy() {
    document.getElementById("b").value = document.getElementById("a").value;
}
</script>
</head>
<body>
    <input type="text" id="a">
    <input type="button" onclick="copy()" value="copy data">
    <input id="b">
    <input type="button" value="back" onclick="history.back()">
</body>
</html>
```

### 6.2 Browser Detection (Feature Detection Preferred)

```javascript
// Bad: User agent sniffing
if (navigator.userAgent.indexOf("Chrome") !== -1) {
    console.log("Chrome browser");
}

// Good: Feature detection
if ('serviceWorker' in navigator) {
    console.log("Service Worker supported!");
}
```

### 6.3 Checking Cookie Support

```javascript
function checkCookies() {
    if (navigator.cookieEnabled) {
        console.log("Cookies are enabled");
        return true;
    } else {
        console.log("Cookies are disabled");
        return false;
    }
}
```

### 6.4 Displaying Browser Info

```javascript
function displayBrowserInfo() {
    let info = `
        Browser: ${navigator.appName}
        Version: ${navigator.appVersion}
        Platform: ${navigator.platform}
        Language: ${navigator.language}
        Online: ${navigator.onLine}
        Cookies: ${navigator.cookieEnabled}
    `;
    console.log(info);
}
```

---

## 7. Quick Reference

### 7.1 Navigator Properties

```javascript
navigator.appName        // Browser name
navigator.appVersion     // Version info
navigator.appCodeName    // Code name (always "Mozilla")
navigator.language       // Browser language
navigator.cookieEnabled  // Cookies enabled (boolean)
navigator.onLine         // Online status (boolean)
navigator.platform       // OS platform
navigator.userAgent      // Full user agent string
```

### 7.2 History Methods

```javascript
history.back();      // Previous page
history.forward();   // Next page
history.go(-1);      // Previous page
history.go(1);       // Next page
history.go(-2);      // 2 pages back
history.go(0);       // Reload
history.length;      // Number of history entries
```

### 7.3 Common Patterns

```html
<!-- Back button -->
<button onclick="history.back()">← Back</button>

<!-- Forward button -->
<button onclick="history.forward()">Forward →</button>

<!-- Reload -->
<button onclick="location.reload()">Refresh</button>
```

---

## 8. Interview Questions

### Q1: What is the Navigator object?
**Answer**: The Navigator object contains information about the browser, such as browser name, version, platform, language, and whether cookies are enabled. It's accessed via `window.navigator` or simply `navigator`.

### Q2: Why shouldn't you rely on navigator.appName for browser detection?
**Answer**: Because most browsers return "Netscape" as appName and "Mozilla" as appCodeName for compatibility reasons. It's better to use feature detection (`'feature' in navigator`) than user agent sniffing.

### Q3: What does history.go(0) do?
**Answer**: It reloads the current page. It's equivalent to `location.reload()`.

### Q4: How do you check if cookies are enabled?
**Answer**: Use `navigator.cookieEnabled` which returns a boolean:
```javascript
if (navigator.cookieEnabled) {
    // Cookies are enabled
}
```

### Q5: What is the difference between history.back() and history.go(-1)?
**Answer**: They are equivalent. Both navigate to the previous page in the browser history. `go(-1)` is more flexible as you can specify how many pages to go back/forward.

### Q6: Can you access all URLs in the history from JavaScript?
**Answer**: No. For security reasons, you can only navigate through history using `back()`, `forward()`, and `go()`. You cannot read the actual URLs due to privacy concerns.

---

## Navigation

← Previous: [19_ES6_Collections_Map_Set.md](./19_ES6_Collections_Map_Set.md) | Next: [21_Regular_Expressions.md](./21_Regular_Expressions.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 05*
