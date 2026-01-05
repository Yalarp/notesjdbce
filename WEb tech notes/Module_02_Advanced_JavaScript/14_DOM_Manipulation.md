# DOM Manipulation in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Selecting Elements](#2-selecting-elements)
3. [classList Property](#3-classlist-property)
4. [getAttribute and setAttribute](#4-getattribute-and-setattribute)
5. [Modifying Styles](#5-modifying-styles)
6. [innerHTML and textContent](#6-innerhtml-and-textcontent)
7. [Creating and Removing Elements](#7-creating-and-removing-elements)
8. [Traversing the DOM](#8-traversing-the-dom)
9. [Quick Reference](#9-quick-reference)
10. [Interview Questions](#10-interview-questions)

---

## 1. Introduction

### 1.1 Definition
The **Document Object Model (DOM)** is a programming interface for web documents. It represents the page as nodes and objects, allowing programs to change the document structure, style, and content.

### 1.2 Purpose
- Access and modify HTML elements
- Change styles dynamically
- Add/remove elements from the page
- Respond to user interactions
- Create interactive web applications

### 1.3 DOM Tree Structure

```
document
    └── html
        ├── head
        │   ├── title
        │   └── script
        └── body
            ├── div
            │   ├── p
            │   └── span
            └── img
```

---

## 2. Selecting Elements

### 2.1 Selection Methods

| Method | Returns | Selector Type |
|--------|---------|---------------|
| `getElementById()` | Single element | ID |
| `getElementsByClassName()` | HTMLCollection | Class |
| `getElementsByTagName()` | HTMLCollection | Tag name |
| `querySelector()` | First matching element | CSS selector |
| `querySelectorAll()` | NodeList | CSS selector |

### 2.2 getElementById()

```javascript
// HTML: <p id="pp">Hello</p>
let element = document.getElementById("pp");
element.innerHTML = "New Content";
```

### 2.3 getElementsByClassName()

```javascript
<ul class="example">
    <li class="child">Coffee</li>
    <li class="child">Tea</li>
</ul>
<ul class="example">
    <li class="child">Bun</li>
    <li class="child">Ice-cream</li>
</ul>

<script>
function myFunction() {
    var list = document.getElementsByClassName("example");
    alert(list.length);  // 2
    
    // Access nested elements
    list[0].getElementsByClassName("child")[0].innerHTML = "Milk";
}
</script>
```

**Memory Diagram:**
```
list (HTMLCollection):
┌─────────────────┐
│ index 0: <ul>   │──→ example (Coffee, Tea)
│ index 1: <ul>   │──→ example (Bun, Ice-cream)
│ length: 2       │
└─────────────────┘
```

### 2.4 querySelector() and querySelectorAll()

```html
<div id="myDIV">
    <p>This is a p element in div.</p>
    <p>This is also a p element in div.</p>
</div>

<script>
function myFunction() {
    // Select ALL matching elements
    var x = document.getElementById("myDIV").querySelectorAll("p");
    x[0].style.backgroundColor = "red";
    x[1].style.backgroundColor = "red";
}

function my() {
    // Select ONLY first matching element
    var x = document.getElementById("myDIV").querySelector("p");
    x.style.color = "blue";
}
</script>
```

### 2.5 Advanced CSS Selectors

```javascript
// By ID
document.querySelector('#foobar');

// By class
var el = document.querySelector(".myclass");

// Complex selector
var el = document.querySelector("div.user-panel.main input[name='login']");

// Child selectors
"h1 span"      // Descendant (any level)
"h1 > span"    // Direct child only
"h1 + span"    // Adjacent sibling
"h1 ~ span"    // General sibling
```

---

## 3. classList Property

### 3.1 What is classList?

The `classList` property returns a live DOMTokenList of the class attributes of an element.

### 3.2 Basic Usage

```html
<div id="myDIV" class="mystyle anotherClass myClass">
    I am a DIV element with multiple classes
</div>

<script>
function myFunction() {
    var x = document.getElementById("myDIV").classList;
    alert(x.length);    // 3
    alert(x[0]);        // "mystyle"
    document.getElementById("demo").innerHTML = x;
}
</script>
```

### 3.3 classList Methods

| Method | Description |
|--------|-------------|
| `add("class")` | Add one or more classes |
| `remove("class")` | Remove one or more classes |
| `toggle("class")` | Add if absent, remove if present |
| `contains("class")` | Returns true/false |
| `replace("old", "new")` | Replace a class with another |

### 3.4 add()

```javascript
<script>
function myFunction() {
    let divobj = document.getElementById("myDIV");
    let y = divobj.classList;
    alert(y.length);       // 2
    alert(y[0]);           // "mystyle"
    
    y.add("anotherClass"); // Add new class
    
    document.getElementById("demo").innerHTML = y[2]; // "anotherClass"
}
</script>
```

**Before:** `<div class="mystyle myClass">`
**After:** `<div class="mystyle myClass anotherClass">`

### 3.5 remove()

```javascript
function myFunction() {
    document.getElementById("myDIV").classList.remove("anotherClass");
}
```

### 3.6 replace()

```javascript
document.getElementById("myDIV").classList.replace("anotherClass", "myClass");
```

### 3.7 contains()

```javascript
function myFunction() {
    var x = document.getElementById("myDIV").classList.contains("anotherClass");
    document.getElementById("demo").innerHTML = x;  // true or false
}
```

### 3.8 toggle()

```javascript
function myFunction() {
    var x = document.getElementById("myDIV").classList.toggle("anotherClass");
    document.getElementById("demo").innerHTML = x;  // true if added, false if removed
}
```

**How toggle() works internally:**
```javascript
function myFunctionToggle() {
    var x = document.getElementById("myDIV").classList.contains("anotherClass");
    if (x == true) {
        document.getElementById("myDIV").classList.remove("anotherClass");
        return false;
    } else {
        document.getElementById("myDIV").classList.add("anotherClass");
        return true;
    }
}
```

---

## 4. getAttribute and setAttribute

### 4.1 Getting and Setting Attributes

```html
<p align="center" id="pp">Hello</p>
<input type="button" onclick="go()" value="Change"/>
<div id="dd"></div>

<script>
function go() {
    // Set attribute
    document.getElementById("pp").setAttribute("align", "left");
    
    // Get attribute
    document.getElementById("dd").innerHTML = 
        document.getElementById("pp").getAttribute("align");  // "left"
}
</script>
```

### 4.2 Common Attribute Operations

```javascript
// Get attribute
element.getAttribute("id");
element.getAttribute("class");
element.getAttribute("src");

// Set attribute
element.setAttribute("id", "newId");
element.setAttribute("class", "newClass");
element.setAttribute("disabled", "true");

// Remove attribute
element.removeAttribute("disabled");

// Check if attribute exists
element.hasAttribute("disabled");  // boolean
```

---

## 5. Modifying Styles

### 5.1 Direct Style Manipulation

```html
<script>
function callme() {
    document.getElementById("pr").style.color = "red";
    document.getElementById("pr").style.background = "yellow";
}

function change() {
    document.getElementById("pr").style.color = "black";
    document.getElementById("pr").style.background = "pink";
}
</script>

<p onmouseover="callme()" id="pr" onmouseout="change()">
    Welcome to world of style and DOM
</p>
```

### 5.2 Using className

```html
<style>
.cl { background-color: yellow; font-size: 250; color: red; }
.cc { color: blue; }
</style>

<script>
function callme() {
    let ob = document.getElementById("pr");
    ob.className = "cl";  // Replace entire class attribute
}
</script>

<p onmouseover="callme()" id="pr" class="cc">
    Welcome to world of style and DOM
</p>
```

### 5.3 Common Style Properties

```javascript
element.style.color = "red";
element.style.backgroundColor = "yellow";
element.style.fontSize = "20px";
element.style.display = "none";
element.style.display = "block";
element.style.visibility = "hidden";
element.style.marginTop = "10px";
element.style.padding = "5px";
element.style.border = "1px solid black";
```

**Note:** CSS properties with hyphens use camelCase in JavaScript:
- `background-color` → `backgroundColor`
- `font-size` → `fontSize`
- `margin-top` → `marginTop`

---

## 6. innerHTML and textContent

### 6.1 innerHTML

Sets or gets the HTML markup contained within an element:

```javascript
// Get
let content = document.getElementById("demo").innerHTML;

// Set (parses HTML)
document.getElementById("demo").innerHTML = "<strong>Bold Text</strong>";
```

### 6.2 textContent

Sets or gets the text content only (no HTML):

```javascript
// Get
let text = document.getElementById("demo").textContent;

// Set (treats as plain text)
document.getElementById("demo").textContent = "<strong>Bold Text</strong>";
// Displays: <strong>Bold Text</strong> (as literal text)
```

### 6.3 Comparison

| Property | Parses HTML | Security |
|----------|-------------|----------|
| `innerHTML` | Yes | XSS risk if using user input |
| `textContent` | No | Safe - escapes HTML |
| `innerText` | No | Slower, respects CSS visibility |

---

## 7. Creating and Removing Elements

### 7.1 Creating Elements

```javascript
// Create element
let newDiv = document.createElement("div");

// Add attributes
newDiv.id = "myNewDiv";
newDiv.className = "container";

// Add content
newDiv.innerHTML = "Hello World";
// or
newDiv.textContent = "Hello World";

// Append to DOM
document.body.appendChild(newDiv);
// or
document.getElementById("parent").appendChild(newDiv);
```

### 7.2 Insert Methods

```javascript
// Insert at end of parent
parent.appendChild(newElement);

// Insert before a reference element
parent.insertBefore(newElement, referenceElement);

// Modern methods (ES6+)
element.before(newElement);   // Insert before element
element.after(newElement);    // Insert after element
element.prepend(newElement);  // Insert as first child
element.append(newElement);   // Insert as last child
```

### 7.3 Removing Elements

```javascript
// Modern way
element.remove();

// Old way (through parent)
parent.removeChild(element);

// Remove all children
element.innerHTML = "";
```

---

## 8. Traversing the DOM

### 8.1 Parent, Children, Siblings

```javascript
// Parent
element.parentNode;
element.parentElement;

// Children
element.childNodes;      // NodeList (includes text nodes)
element.children;        // HTMLCollection (elements only)
element.firstChild;      // First child node
element.firstElementChild; // First element child
element.lastChild;
element.lastElementChild;

// Siblings
element.nextSibling;     // Next node
element.nextElementSibling; // Next element
element.previousSibling;
element.previousElementSibling;
```

### 8.2 Example: Image Array

```html
<script>
function callme() {
    // All images are stored as an array
    alert(document.images.length);
    
    // Access by name
    document.mg.src = "b.bmp";
    
    // Access by index
    document.images[0].src = "b.bmp";
    
    // Access by ID
    document.getElementById("im").src = "b.bmp";
}
</script>

<img name="mg" id="im" src="a.bmp" onmouseover="callme()">
```

---

## 9. Quick Reference

### 9.1 Selection Methods

```javascript
document.getElementById("id");
document.getElementsByClassName("class");
document.getElementsByTagName("tag");
document.querySelector("css-selector");
document.querySelectorAll("css-selector");
```

### 9.2 classList Methods

```javascript
element.classList.add("class");
element.classList.remove("class");
element.classList.toggle("class");
element.classList.contains("class");
element.classList.replace("old", "new");
```

### 9.3 Attribute Methods

```javascript
element.getAttribute("attr");
element.setAttribute("attr", "value");
element.removeAttribute("attr");
element.hasAttribute("attr");
```

### 9.4 Content Properties

```javascript
element.innerHTML = "HTML content";
element.textContent = "Text only";
element.innerText = "Visible text";
element.value = "Form input value";
```

### 9.5 Style Access

```javascript
element.style.property = "value";
element.className = "class-name";
element.classList.add("class");
```

---

## 10. Interview Questions

### Q1: What is the DOM?
**Answer**: The Document Object Model (DOM) is a programming interface that represents an HTML/XML document as a tree structure. Each node in the tree represents part of the document, allowing JavaScript to access and modify content, structure, and styling.

### Q2: What is the difference between getElementById() and querySelector()?
**Answer**: 
- `getElementById()` only selects by ID and returns a single element
- `querySelector()` uses CSS selectors and can select by ID, class, tag, attribute, etc.
- `querySelector()` is more versatile but slightly slower

### Q3: What is the difference between innerHTML and textContent?
**Answer**:
- `innerHTML` parses and renders HTML markup
- `textContent` treats content as plain text (escapes HTML)
- `innerHTML` has XSS risks if using untrusted input

### Q4: What does classList.toggle() do?
**Answer**: `toggle()` adds the class if it doesn't exist, or removes it if it does. It returns `true` if the class was added, `false` if removed.

### Q5: How do you add an element to the DOM?
**Answer**:
```javascript
let el = document.createElement("div");
el.textContent = "Content";
document.body.appendChild(el);
```

### Q6: What's the difference between childNodes and children?
**Answer**:
- `childNodes` returns all child nodes including text nodes and comments
- `children` returns only element children (HTMLCollection)

### Q7: How do you change CSS styles dynamically?
**Answer**: Multiple ways:
- `element.style.propertyName = "value"`
- `element.className = "newClass"`
- `element.classList.add("class")`
- `element.setAttribute("style", "...")`

---

## Navigation

← Previous: [13_Generators_and_Iterators.md](./13_Generators_and_Iterators.md) | Next: [15_Arrays_and_Array_Methods.md](./15_Arrays_and_Array_Methods.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 03-04*
