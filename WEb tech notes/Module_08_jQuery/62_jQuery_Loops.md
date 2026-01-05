# jQuery Loops

## Table of Contents
1. [Introduction](#1-introduction)
2. [The `.each()` Method](#2-the-each-method)
3. [Looping through Elements](#3-looping-through-elements)
4. [Looping through Arrays/Objects](#4-looping-through-arraysobjects)
5. [Practical Example](#5-practical-example)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

jQuery provides utility methods to iterate over jQuery objects (collections of DOM elements) as well as raw JavaScript arrays and objects. The most important one is `.each()`.

---

## 2. The `.each()` Method

The `.each()` method specifies a function to run for each matched element in the jQuery object.

**Syntax:**
```javascript
$(selector).each(function(index, element) {
  // code to run for each element
});
```
- `index`: The index position of the element.
- `element` (or `this`): The current DOM element.

---

## 3. Looping through Elements

You can iterate through all selected elements to update them individually based on their content or index.

```javascript
$("li").each(function(index) {
  console.log(index + ": " + $(this).text());
});
```

---

## 4. Looping through Arrays/Objects

jQuery also has a generic iterator `$.each()` which works on plain JS arrays and objects (similar to `forEach`).

**Syntax:**
```javascript
$.each(collection, function(indexOrKey, value) { ... });
```

**Example:**
```javascript
var arr = ["a", "b", "c"];
$.each(arr, function(index, value) {
    console.log(index + ": " + value);
});
```

---

## 5. Practical Example

This example iterates through all paragraph (`<p>`) tags and temporarily changes their content on mouse hover. This demonstrates using `.each()` to attach specific logic to multiple elements.

**Original Code (Based on Day 12 `test.html`):**

```javascript
$(document).ready(function() {

    // Iterate over every <p> element
    $("p").each(function () {
        // Capture original text for THIS specific paragraph
        let originalText = $(this).html();  

        // Attach Mouse Enter Event
        $(this).mouseenter(function () {
            $(this).html("<b>Hovering over! Content changed.</b>");
        });

        // Attach Mouse Leave Event
        $(this).mouseleave(function () {
            // Restore the specifically stored original text
            $(this).html(originalText);
        });
    });

});
```

**Execution Flow:**
1. `$("p").each(...)` finds all paragraphs.
2. For *Paragraph 1*:
   - Stores "para 1" in `originalText` (closure variable).
   - Attaches handlers.
3. For *Paragraph 2*:
   - Stores "div para 1" in its own `originalText`.
   - Attaches handlers.
4. When user hovers over Paragraph 2:
   - Text changes to bold message.
   - Using loop ensures closure scope works correctly for each element (remembering its own original text).
5. When user leaves:
   - Specific original text ("div para 1") is restored.

---

## 6. Quick Reference

| Method | Use Case |
|--------|----------|
| `$(selector).each(cb)` | Iterate over DOM Elements |
| `$.each(array, cb)` | Iterate over Data (Array/Object) |
| `this` | Refers to DOM Element (use `$(this)` to wrap) |
| `return false` | Breaks the loop (like `break`) |
| `return true` | Continues to next iteration (like `continue`) |

---

## 7. Interview Questions

### Q1: What is the difference between `$(selector).each()` and `$.each()`?
**Answer**:
- `$(selector).each()` is used to iterate over a **jQuery selection** of DOM elements.
- `$.each()` is a **utility function** used to iterate over any Javascript array or object.

### Q2: How do you break out of a jQuery `.each()` loop?
**Answer**: Return `false` from the callback function.

### Q3: What does `this` refer to inside the `.each()` callback?
**Answer**: `this` refers to the **DOM Element** currently being processed. If you want to use jQuery methods on it, you must wrap it: `$(this)`.

---

## Navigation

← Previous: [61_jQuery_Events.md](./61_jQuery_Events.md) | Next: [63_jQuery_Effects.md](./63_jQuery_Effects.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 12/13*
