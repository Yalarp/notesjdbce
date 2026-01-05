# Event Object and All Events

## Table of Contents
1. [Introduction](#1-introduction)
2. [Event Object](#2-event-object)
3. [Mouse Events](#3-mouse-events)
4. [Keyboard Events](#4-keyboard-events)
5. [Form Events](#5-form-events)
6. [Focus Events](#6-focus-events)
7. [Event Properties](#7-event-properties)
8. [Target vs CurrentTarget](#8-target-vs-currenttarget)
9. [Quick Reference](#9-quick-reference)
10. [Interview Questions](#10-interview-questions)

---

## 1. Introduction

### 1.1 What is the Event Object?
The Event object represents an event that takes place in the DOM. It contains information about the event that occurred and provides methods to control event propagation.

### 1.2 Event Categories

| Category | Examples |
|----------|----------|
| Mouse | click, dblclick, mousedown, mouseup, mousemove, mouseenter, mouseleave |
| Keyboard | keydown, keypress, keyup |
| Form | submit, change, input, focus, blur |
| Window | load, resize, scroll, unload |
| Touch | touchstart, touchmove, touchend |

---

## 2. Event Object

### 2.1 Accessing the Event Object

```html
<script type="text/javascript">
function whichType() {
    alert(event.type);       // "keydown"
    console.log(event);      // Full event object
}
</script>

<body onkeydown="whichType()">
<p>Press any key. An alert box will show which type of event occurred.</p>
</body>
```

### 2.2 Event Object Properties

| Property | Description |
|----------|-------------|
| `type` | Type of event (e.g., "click", "keydown") |
| `target` | Element that triggered the event |
| `currentTarget` | Element that has the event listener |
| `timeStamp` | Time the event was created |
| `bubbles` | Whether the event bubbles up |
| `cancelable` | Whether the event can be cancelled |

---

## 3. Mouse Events

### 3.1 Mouse Event Types

| Event | Description |
|-------|-------------|
| `onclick` | Element is clicked |
| `ondblclick` | Element is double-clicked |
| `onmousedown` | Mouse button is pressed |
| `onmouseup` | Mouse button is released |
| `onmousemove` | Mouse is moved |
| `onmouseenter` | Mouse enters element (no bubbling) |
| `onmouseleave` | Mouse leaves element (no bubbling) |
| `onmouseover` | Mouse enters element (bubbles) |
| `onmouseout` | Mouse leaves element (bubbles) |

### 3.2 Mouse Coordinates

```html
<script type="text/javascript">
function coordinates() {
    // Screen coordinates (relative to monitor)
    x = event.screenX;
    y = event.screenY;
    alert("Screen: X=" + x + " Y=" + y);
    
    // Client coordinates (relative to browser viewport)
    x = event.clientX;
    y = event.clientY;
    alert("Client: X=" + x + ", Y=" + y);
}
</script>

<body onmousedown="coordinates()">
<p>Click somewhere. Alert will show coordinates.</p>
</body>
```

**Coordinate Diagram:**
```
┌─────────────────────────────────────┐
│ Screen (Monitor)                    │
│  screenX, screenY = 10, 10          │
│  ┌───────────────────────────────┐  │
│  │ Browser Window                 │  │
│  │  clientX, clientY = 0, 0       │  │
│  │  ┌───────────────────────────┐│  │
│  │  │ Web Page                  ││  │
│  │  │  pageX, pageY             ││  │
│  │  └───────────────────────────┘│  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

### 3.3 mouseleave vs mouseout

```html
<div onmouseleave="myLeaveFunction()">
    <p>onmouseleave: <span id="demo2">Mouse over and leave me!</span></p>
</div>

<div onmouseout="myOutFunction()">
    <p>onmouseout: <span id="demo3">Mouse over and leave me!</span></p>
</div>

<script>
var x = 0;
var y = 0;

function myLeaveFunction() {
    document.getElementById("demo2").innerHTML = x += 1;
}

function myOutFunction() {
    document.getElementById("demo3").innerHTML = y += 1;
}
</script>
```

**Key Difference:**
- `mouseleave` - Only fires when leaving the div itself
- `mouseout` - Fires when leaving div AND when leaving child elements (bubbles)

---

## 4. Keyboard Events

### 4.1 Keyboard Event Types

| Event | When Fired | Character Keys | Non-Character Keys |
|-------|------------|----------------|-------------------|
| `keydown` | Key pressed (first) | ✓ | ✓ |
| `keypress` | Key pressed (character only) | ✓ | ✗ |
| `keyup` | Key released | ✓ | ✓ |

**Event Order:** keydown → keypress → keyup

### 4.2 Preventing Input

```html
<form>
    <!-- Prevent numbers -->
    <input type="text" onkeypress="return noNumbers(event)" />
    
    <!-- Prevent all input -->
    <input type="text" onkeydown="return false" />
</form>

<script type="text/javascript">
function noNumbers(e) {
    var keynum = e.keyCode;
    var keychar = String.fromCharCode(keynum);
    alert(keychar);
    
    var numcheck = /\d/;
    return !numcheck.test(keychar);  // Return false if digit
}
</script>
```

### 4.3 Key Properties

| Property | Description |
|----------|-------------|
| `keyCode` | Numeric code of the key |
| `key` | String representation of key pressed |
| `code` | Physical key on keyboard |
| `shiftKey` | Whether Shift was pressed |
| `ctrlKey` | Whether Ctrl was pressed |
| `altKey` | Whether Alt was pressed |

---

## 5. Form Events

### 5.1 Common Form Events

| Event | Description |
|-------|-------------|
| `onsubmit` | Form is submitted |
| `onchange` | Value changed (after blur) |
| `oninput` | Value being changed (real-time) |
| `onreset` | Form is reset |

### 5.2 onChange Event

```html
<script type="text/javascript">
function favBrowser() {
    var mylist = document.getElementById("myList");
    alert(mylist.selectedIndex);
    document.getElementById("favorite").value = 
        mylist.options[mylist.selectedIndex].text;
}
</script>

<form>
    Select your favorite browser:
    <select id="myList" onchange="favBrowser()">
        <option>select</option>
        <option>Internet Explorer</option>
        <option>Netscape</option>
        <option>Opera</option>
    </select>
    <p>Your favorite browser is: <input type="text" id="favorite" size="20"></p>
</form>
```

### 5.3 onInput Event

```html
<input type="text" id="input">
oninput: <span id="result"></span>

<script>
document.getElementById("input").oninput = function() {
    document.getElementById("result").innerHTML = 
        document.getElementById("input").value;
};
</script>
```

**Key Points:**
- Triggers on EVERY modification (including paste, speech recognition)
- More immediate than `onchange`
- Cannot be prevented with `event.preventDefault()`

### 5.4 onError Event

```html
<!-- Triggers when image fails to load -->
<img src="imae.gif" onerror="alert('The image could not be loaded.')">
```

---

## 6. Focus Events

### 6.1 Focus Event Types

| Event | Description |
|-------|-------------|
| `onfocus` | Element receives focus |
| `onblur` | Element loses focus |
| `onfocusin` | Element receives focus (bubbles) |
| `onfocusout` | Element loses focus (bubbles) |

### 6.2 Example

```html
<script type="text/javascript">
function setStyle() {
    document.getElementById("lname").style.background = "yellow";
}

function change() {
    document.getElementById("fname").style.color = "blue";
}
</script>

<body>
    First name: <input type="text" onblur="change()" id="fname">
    <br />
    Last name: <input type="text" onfocus="setStyle()" id="lname">
</body>
```

**Use Cases:**
- `onfocus`: Highlight active field, show tooltips
- `onblur`: Validate input, remove highlights

---

## 7. Event Properties

### 7.1 Common Event Properties

| Property | Description |
|----------|-------------|
| `type` | Event type ("click", "keydown", etc.) |
| `target` | Element that triggered event |
| `currentTarget` | Element with event listener |
| `bubbles` | Does event bubble? |
| `cancelable` | Can event be cancelled? |
| `defaultPrevented` | Was preventDefault() called? |

### 7.2 Mouse Event Properties

| Property | Description |
|----------|-------------|
| `clientX`, `clientY` | Position relative to viewport |
| `screenX`, `screenY` | Position relative to screen |
| `pageX`, `pageY` | Position relative to document |
| `button` | Which mouse button (0, 1, 2) |

### 7.3 Keyboard Event Properties

| Property | Description |
|----------|-------------|
| `keyCode` | Numeric key code |
| `key` | Key value |
| `code` | Physical key |
| `shiftKey`, `ctrlKey`, `altKey` | Modifier keys |

---

## 8. Target vs CurrentTarget

### 8.1 target

Returns the element that **triggered** the event:

```html
<body onclick="myFunction(event)">
<p>Click on any elements to find out which element triggered the event.</p>
<h1>This is a heading</h1>
<button>This is a button</button>
<p id="demo"></p>

<script>
function myFunction(event) {
    var x = event.target;
    document.getElementById("demo").innerHTML = 
        "Triggered by a " + x.nodeName + " element";
}
</script>
</body>
```

### 8.2 currentTarget

Returns the element whose **event listener** triggered the event:

```html
<body onclick="myFunction(event)">
<p>Click on a paragraph. Alert will show the element with the listener.</p>

<script>
function myFunction(event) {
    alert(event.currentTarget.nodeName);  // Always "BODY"
}
</script>
</body>
```

### 8.3 Comparison

| Click Location | target | currentTarget |
|----------------|--------|---------------|
| `<p>` | P | BODY |
| `<h1>` | H1 | BODY |
| `<button>` | BUTTON | BODY |
| `<body>` | BODY | BODY |

---

## 9. Quick Reference

### 9.1 Mouse Events

```javascript
element.onclick = function(e) { };
element.ondblclick = function(e) { };
element.onmousedown = function(e) { };
element.onmouseup = function(e) { };
element.onmousemove = function(e) { };
element.onmouseenter = function(e) { };
element.onmouseleave = function(e) { };
```

### 9.2 Keyboard Events

```javascript
element.onkeydown = function(e) { };
element.onkeypress = function(e) { };
element.onkeyup = function(e) { };

// Access key info
e.keyCode   // Number
e.key       // String
e.code      // Physical key
```

### 9.3 Form Events

```javascript
form.onsubmit = function(e) { };
input.onchange = function(e) { };
input.oninput = function(e) { };
input.onfocus = function(e) { };
input.onblur = function(e) { };
```

### 9.4 Preventing Default

```javascript
element.onclick = function(e) {
    e.preventDefault();  // Prevent default action
    e.stopPropagation(); // Stop bubbling
    return false;        // Both (in some cases)
};
```

---

## 10. Interview Questions

### Q1: What is the difference between target and currentTarget?
**Answer**:
- `target`: The element that triggered the event (clicked, typed, etc.)
- `currentTarget`: The element with the event listener attached
- They're the same when the listener is on the triggering element

### Q2: What is the difference between keydown, keypress, and keyup?
**Answer**:
- `keydown`: Fires when key is pressed (first), works for all keys
- `keypress`: Fires after keydown (deprecated), only for character keys
- `keyup`: Fires when key is released

### Q3: How do you prevent form submission?
**Answer**: Return false or use `e.preventDefault()`:
```javascript
form.onsubmit = function(e) {
    e.preventDefault();
    return false;
};
```

### Q4: What's the difference between mouseleave and mouseout?
**Answer**:
- `mouseleave`: Only fires when leaving the element itself
- `mouseout`: Also fires when entering child elements (bubbles)

### Q5: What is event bubbling?
**Answer**: Event bubbling is when an event triggers on a child element, then bubbles up to trigger on parent elements. Use `stopPropagation()` to prevent it.

---

## Navigation

← Previous: [21_Regular_Expressions.md](./21_Regular_Expressions.md) | Next: [23_JSON_Handling.md](./23_JSON_Handling.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 05*
