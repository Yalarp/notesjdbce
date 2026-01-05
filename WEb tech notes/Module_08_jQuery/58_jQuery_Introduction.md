# jQuery Introduction

## Table of Contents
1. [Introduction to jQuery](#1-introduction-to-jquery)
2. [Why use jQuery?](#2-why-use-jquery)
3. [Setup and Installation](#3-setup-and-installation)
4. [jQuery Syntax](#4-jquery-syntax)
5. [Document Ready Event](#5-document-ready-event)
6. [Practical Example](#6-practical-example)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction to jQuery

### 1.1 What is jQuery?
**jQuery** is a fast, small, and feature-rich JavaScript library. It makes things like HTML document traversal and manipulation, event handling, animation, and Ajax much simpler with an easy-to-use API that works across a multitude of browsers.

### 1.2 Motto
> "Write Less, Do More"

---

## 2. Why use jQuery?

1.  **Simplicity**: Simplifies DOM selection and manipulation.
2.  **Cross-Browser Compatibility**: Handles browser inconsistencies (IE, Chrome, Firefox, etc.) automatically.
3.  **Chaining**: Allows multiple actions on the same element in a single line of code.
4.  **AJAX**: drastically simplifies AJAX calls.
5.  **Plugins**: Huge ecosystem of plugins for UI components.

---

## 3. Setup and Installation

### 3.1 CDN Method (Recommended)
Include jQuery from a CDN (Content Delivery Network).

```html
<head>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
</head>
```

### 3.2 Local Method
Download the `jquery.js` file and include it.

```html
<script src="jquery-3.7.1.min.js"></script>
```

---

## 4. jQuery Syntax

The syntax is tailored for **selecting** HTML elements and performing some **action** on them.

```javascript
$(selector).action()
```

- `$`: Access to jQuery.
- `(selector)`: To "query" (find) HTML elements.
- `.action()`: A jQuery action to be performed on the elements.

**Examples:**
- `$(this).hide()`: Hides the current element.
- `$("p").hide()`: Hides all `<p>` elements.
- `$(".test").hide()`: Hides all elements with `class="test"`.
- `$("#test").hide()`: Hides the element with `id="test"`.

---

## 5. Document Ready Event

We should ensure that the document is fully loaded before we start running jQuery code.

### 5.1 Standard Value

```javascript
$(document).ready(function(){
  // jQuery methods go here...
});
```

### 5.2 Shorthand

```javascript
$(function(){
   // jQuery methods go here...
});
```

**Why?**
If you try to select an element (e.g., a button) and attach a click event to it *before* the button is rendered in the HTML, the selection will fail. The `ready` event prevents this.

---

## 6. Practical Example

### 6.1 Hello World App

```html
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    $("p").hide();
  });
});
</script>
</head>
<body>

<h2>This is a heading</h2>

<p>This is a paragraph.</p>
<p>This is another paragraph.</p>

<button>Click me to hide paragraphs</button>

</body>
</html>
```

**Execution Flow:**
1. Browser loads HTML.
2. jQuery library loads.
3. `$(document).ready()` waits for DOM content to load.
4. Once loaded, it finds all `<button>` elements.
5. Attaches a `click` event listener.
6. When User clicks the button:
   - Finds all `<p>` elements.
   - Applies `display: none` (hide).

---

## 7. Quick Reference

| Action | Code |
|--------|------|
| **Start Code** | `$(function(){ ... });` |
| **Select ID** | `$("#myId")` |
| **Select Class** | `$(".myClass")` |
| **Select Tag** | `$("div")` |
| **Hide** | `.hide()` |
| **Show** | `.show()` |

---

## 8. Interview Questions

### Q1: What is jQuery?
**Answer**: jQuery is a fast, small, and feature-rich JavaScript library that simplifies DOM manipulation, event handling, animations, and AJAX for web development.

### Q2: Why is `$(document).ready()` used?
**Answer**: It ensures that the jQuery code runs only after the HTML document (text, tags, DOM structure) is fully loaded. This prevents errors where code tries to access elements that haven't been rendered yet.

### Q3: What is the difference between `window.onload` and `$(document).ready()`?
**Answer**: `window.onload` waits for the entire page to load (including images, iframes, styles). `$(document).ready()` triggers as soon as the DOM is ready (typically much faster).

### Q4: Does jQuery replace JavaScript?
**Answer**: No. jQuery IS JavaScript. It is just a library written in JavaScript to make common tasks easier. You can mix raw JS and jQuery.

---

## Navigation

← Previous: [57_React_Bootstrap.md](../Module_07_Advanced_React/57_React_Bootstrap.md) | Next: [59_jQuery_Selectors_and_DOM.md](./59_jQuery_Selectors_and_DOM.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 12*
