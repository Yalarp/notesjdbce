# jQuery Selectors and DOM Manipulation

## Table of Contents
1. [Introduction](#1-introduction)
2. [jQuery Selectors](#2-jquery-selectors)
3. [DOM Manipulation (Get/Set)](#3-dom-manipulation-getset)
4. [Adding/Removing Elements](#4-addingremoving-elements)
5. [Practical Example](#5-practical-example)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

jQuery simplifies the process of selecting HTML elements and manipulating the DOM (content, attributes, CSS).

---

## 2. jQuery Selectors

### 2.1 Basic Selectors
jQuery selectors allow you to select and manipulate HTML elements as a group or as a single element.

| Selector | Example | Description |
|----------|---------|-------------|
| **ID** | `$("#test")` | Selects element with id="test" |
| **Class** | `$(".test")` | Selects all elements with class="test" |
| **Element** | `$("p")` | Selects all `<p>` elements |
| **All** | `$("*")` | Selects all elements |
| **Multiple** | `$("p, div")` | Selects all `<p>` and `<div>` elements |

### 2.2 Hierarchical Selectors
| Selector | Example | Description |
|----------|---------|-------------|
| **Descendant** | `$("div p")` | Selects `<p>` inside `<div>` (any depth) |
| **Child** | `$("div > p")` | Selects direct child `<p>` of `<div>` |
| **Sibling** | `$("div + p")` | Selects `<p>` immediately after `<div>` |

### 2.3 Attribute Selectors
| Selector | Example | Description |
|----------|---------|-------------|
| **Has Attribute** | `$("[href]")` | Selects all with href attribute |
| **Exact Value** | `$("[target='_blank']")` | target attribute equals '_blank' |
| **Ends With** | `$("[src$='.jpg']")` | src attribute ends with .jpg |

---

## 3. DOM Manipulation (Get/Set)

Three simple, but useful, jQuery methods for DOM manipulation are:
- `text()` - Sets or returns the text content of selected elements.
- `html()` - Sets or returns the content of selected elements (including HTML markup).
- `val()` - Sets or returns the value of form fields.
- `attr()` - Get or set attribute values.

### 3.1 Getting Content

```javascript
var text = $("#p1").text();
var html = $("#p1").html();
var val = $("#input1").val();
var href = $("#link").attr("href");
```

### 3.2 Setting Content

```javascript
$("#p1").text("Hello World!");
$("#p1").html("<b>Hello World!</b>");
$("#input1").val("John Doe");
$("#link").attr("href", "https://google.com");
```

---

## 4. Adding/Removing Elements

### 4.1 Adding Content
| Method | Description |
|--------|-------------|
| `append()` | Inserts content at the **end** of the selected elements |
| `prepend()` | Inserts content at the **beginning** of the selected elements |
| `after()` | Inserts content **after** the selected elements |
| `before()` | Inserts content **before** the selected elements |

### 4.2 Removing Content
| Method | Description |
|--------|-------------|
| `remove()` | Removes the selected element (and its child elements) |
| `empty()` | Removes the child elements from the selected element |

---

## 5. Practical Example

This example demonstrates getting input values and setting content dynamically.

**Original Code (Based on `getset.html`):**

```html
<!DOCTYPE html>
<html>
<head>
<script src="jquery-3.7.1.js"></script>
<script>
$(document).ready(function(){
  $("#btn1").click(function(){
    // Set text
    $("#test1").text("Hello world!");
  });
  
  $("#btn2").click(function(){
    // Set HTML
    $("#test2").html("<b>Hello world!</b>");
  });
  
  $("#btn3").click(function(){
    // Set Value
    $("#test3").val("Dolly Duck");
  });

  $("#btn4").click(function(){
      alert("Text: " + $("#test1").text());
  });
});
</script>
</head>
<body>

<p id="test1">This is a paragraph.</p>
<p id="test2">This is another paragraph.</p>
<p>Input field: <input type="text" id="test3" value="Mickey Mouse"></p>

<button id="btn1">Set Text</button>
<button id="btn2">Set HTML</button>
<button id="btn3">Set Value</button>
<button id="btn4">Get Text</button>

</body>
</html>
```

**Execution Flow:**
1. Page loads with initial text "Mickey Mouse" in input.
2. User clicks "Set Value".
3. `$("#test3").val("Dolly Duck")` executes.
4. Input value changes to "Dolly Duck".
5. User clicks "Set HTML".
6. Paragraph `#test2` content changes to bold **Hello world!**.

---

## 6. Quick Reference

| Operation | Method |
|-----------|--------|
| **Get Text** | `$(sel).text()` |
| **Set Text** | `$(sel).text("New")` |
| **Get HTML** | `$(sel).html()` |
| **Set HTML** | `$(sel).html("<b>New</b>")` |
| **Input Value** | `$(sel).val()` |
| **Attribute** | `$(sel).attr("href")` |

---

## 7. Interview Questions

### Q1: What is the difference between `text()` and `html()`?
**Answer**:
- `text()` works with just the text content. If you set `text("<b>Hi</b>")`, it prints the tags literally on screen.
- `html()` parses the content as HTML. If you set `html("<b>Hi</b>")`, it renders bold text.

### Q2: How do you add a class to an element?
**Answer**: `$(selector).addClass("classname")`. There is also `removeClass()` and `toggleClass()`.

### Q3: How do you select the first paragraph on the page?
**Answer**: `$("p:first")` or `$("p").first()`.

### Q4: What does `$("*")` select?
**Answer**: It selects ALL elements in the DOM.

---

## Navigation

← Previous: [58_jQuery_Introduction.md](./58_jQuery_Introduction.md) | Next: [60_jQuery_Traverse.md](./60_jQuery_Traverse.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 12*
