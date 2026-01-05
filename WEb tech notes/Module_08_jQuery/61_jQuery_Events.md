# jQuery Events

## Table of Contents
1. [Introduction](#1-introduction)
2. [Mouse Events](#2-mouse-events)
3. [Keyboard Events](#3-keyboard-events)
4. [Form Events](#4-form-events)
5. [Document/Window Events](#5-documentwindow-events)
6. [Practical Example](#6-practical-example)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 What are Events?
In jQuery, most DOM events have an equivalent jQuery method. To trigger the event, you execute the method. To handle the event, you pass a function (handler) to the method.

### 1.2 Syntax
```javascript
$("selector").event(function(){
  // Action to be performed
});
```

---

## 2. Mouse Events

| Method | Description |
|--------|-------------|
| `click()` | Triggers when element is clicked |
| `dblclick()` | Triggers when element is double-clicked |
| `mouseenter()` | Triggers when mouse pointer enters element |
| `mouseleave()` | Triggers when mouse pointer leaves element |
| `hover()` | Combination of mouseenter and mouseleave |
| `mousedown()` | Mouse button is pressed down |
| `mouseup()` | Mouse button is released |

---

## 3. Keyboard Events

| Method | Description |
|--------|-------------|
| `keypress()` | Key is pressed down |
| `keydown()` | Key is pressed down (any key) |
| `keyup()` | Key is released |

---

## 4. Form Events

| Method | Description |
|--------|-------------|
| `submit()` | Form is submitted |
| `change()` | Value of input changes |
| `focus()` | Element gets focus |
| `blur()` | Element loses focus |

---

## 5. Document/Window Events

| Method | Description |
|--------|-------------|
| `load()` | Element/Window is fully loaded |
| `resize()` | Browser window is resized |
| `scroll()` | User scrolls in the specified element |
| `unload()` | User leaves the page |

---

## 6. Practical Example

This example demonstrates how to handle mouse enter/leave events to change an element's style dynamically.

**Original Code (Based on `04_mouse_enter_event.html`):**

```html
<!DOCTYPE html>
<html>
<head>
<script src="jquery-1.9.1.js"></script>
<script>
$(document).ready(function(){
  $("#p1").mouseenter(function(){
    // Change background to red when mouse enters
    $(this).css("background-color", "red");
    // Show an alert (optional, usually bad UX but good for demo)
    // alert("You entered p1!");
  });

  $("#p1").mouseleave(function(){
    // Restore background when mouse leaves
    $(this).css("background-color", "#cccccc");
  });
});
</script>
</head>
<body>

<p id="p1">Enter this paragraph.</p>

</body>
</html>
```

**Execution Flow:**
1. Document loads.
2. jQuery attaches a `mouseenter` handler to `#p1`.
3. jQuery attaches a `mouseleave` handler to `#p1`.
4. **User Action**: Moves mouse over "Enter this paragraph."
5. `mouseenter` fires -> Background turns RED.
6. **User Action**: Moves mouse away.
7. `mouseleave` fires -> Background turns GRAY (`#cccccc`).

### 6.1 The `.on()` Method
The `.on()` method attaches one or more event handlers for the selected elements. It is preferred for dynamically added elements.

```javascript
$("p").on("click", function(){
    $(this).hide();
});

// Handling multiple events
$("p").on({
    mouseenter: function(){
        $(this).css("background-color", "lightgray");
    },
    mouseleave: function(){
        $(this).css("background-color", "lightblue");
    },
    click: function(){
        $(this).css("background-color", "yellow");
    }
});
```

---

## 7. Quick Reference

| Category | Methods |
|----------|---------|
| **Mouse** | `click`, `dblclick`, `mouseenter`, `mouseleave`, `hover` |
| **Keyboard** | `keypress`, `keydown`, `keyup` |
| **Form** | `submit`, `change`, `focus`, `blur` |
| **Window** | `resize`, `scroll`, `load` |
| **Generic** | `.on()`, `.off()` |

---

## 8. Interview Questions

### Q1: What is the difference between `click()` and `on('click')`?
**Answer**: Functionally they are similar, but `.on()` reduces memory usage if binding to many elements (when using delegation) and **works for dynamically added elements** if bound to a parent container.

### Q2: What does `$(this)` represent inside an event handler?
**Answer**: It represents the DOM element that triggered the event.

### Q3: How do you prevent the default action of an event?
**Answer**: By using `event.preventDefault()` inside the event handler function. (e.g., to stop a form submission or a link navigation).

### Q4: How do you stop event bubbling?
**Answer**: By using `event.stopPropagation()`.

---

## Navigation

← Previous: [60_jQuery_Traverse.md](./60_jQuery_Traverse.md) | Next: [62_jQuery_Loops.md](./62_jQuery_Loops.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 13*
