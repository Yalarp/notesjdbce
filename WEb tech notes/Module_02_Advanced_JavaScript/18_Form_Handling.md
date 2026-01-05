# Form Handling in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Accessing Form Elements](#2-accessing-form-elements)
3. [Text Input Handling](#3-text-input-handling)
4. [Radio Button Handling](#4-radio-button-handling)
5. [Checkbox Handling](#5-checkbox-handling)
6. [Dropdown (Select) Handling](#6-dropdown-select-handling)
7. [Form Validation](#7-form-validation)
8. [Form Submission](#8-form-submission)
9. [Dynamic Form Creation](#9-dynamic-form-creation)
10. [Quick Reference](#10-quick-reference)
11. [Interview Questions](#11-interview-questions)

---

## 1. Introduction

### 1.1 DOM Form Hierarchy

```
document
    └── forms[]
        └── form
            └── elements[]
                ├── text
                ├── password
                ├── radio
                ├── checkbox
                ├── select
                │   └── option
                ├── textarea
                ├── button
                ├── submit
                └── reset
```

### 1.2 Understanding Form Arrays

All forms and their elements are stored as arrays:

```javascript
document.forms[0]              // First form on page
document.forms[0].elements[0]  // First element in first form
document.forms.length          // Number of forms on page
```

---

## 2. Accessing Form Elements

### 2.1 Multiple Access Methods

```javascript
// By form name and element name
document.formName.elementName

// By forms array and elements array
document.forms[0].elements[0]

// By getElementById
document.getElementById("elementId")

// Full path
window.document.formName.elementName
```

### 2.2 Example: Accessing by Name

```html
<script>
function call() {
    var a = document.frm.t1;  // Get textbox by name
    var b = document.frm.t2;
    b.value = a.value;        // Copy value
}
</script>

<form name="frm" action="a.html" onsubmit="return true">
    name <input name="t1"/>
    <input type="button" value="copy" onclick="call()"/>
    copied name <input name="t2"/>
    <input type="submit"/>
</form>
```

### 2.3 Iterating Through Form Elements

```html
<script>
function call() {
    var v = document.forms[0].elements.length;
    alert(document.forms.length);  // Number of forms
    alert(v);                       // Number of elements
    
    for (let i = 0; i < v; i++) {
        document.getElementById("n").innerHTML += 
            document.forms[0].elements[i].value;
    }
}
</script>
```

### 2.4 Passing Form to Function: this.form

```html
<script>
function call(a) {
    v = a.length;
    alert(a);        // Form object
    alert(v);        // Number of elements
    
    let data = "";
    pobj = document.getElementById("pp");
    
    for (i = 0; i < v; i++) {
        data = data + a.elements[i].value;
    }
    pobj.innerHTML = data;
}
</script>

<form>
    <input type="radio" name="rd" value="good">good
    <input type="radio" name="rd" value="better">better
    <input type="radio" name="rd" value="best">best
    <input type="button" value="click" onclick="call(this.form)">
</form>
```

---

## 3. Text Input Handling

### 3.1 Reading and Writing Values

```javascript
// Get the textbox object
var tobj = document.frm.t1;

// Read value
var data = tobj.value;

// Write value
tobj.value = "New Value";

// Get length
var len = data.length;
```

### 3.2 Setting Focus

```javascript
function setcur() {
    var tobj = document.frm.nm;
    tobj.focus();  // Set cursor to this field
}
```

### 3.3 Auto-focus on Page Load

```html
<body onLoad="setcur()">
```

---

## 4. Radio Button Handling

### 4.1 Reading Selected Radio Button

```html
<script>
function readradio() {
    var l = document.frm.rd.length;  // Number of radio buttons
    let pobj = document.getElementById("pp");
    
    if (document.frm.rd[0].checked) {
        pobj.innerHTML = document.frm.rd[0].value;
    } else {
        pobj.innerHTML = document.frm.rd[1].value;
    }
}
</script>

<form name="frm">
    <input type="radio" name="rd" value="yes"/>yes
    <input type="radio" name="rd" value="no" checked/>no
    <input type="button" value="read" onclick="readradio()">
</form>
```

### 4.2 Setting Radio Button Programmatically

```javascript
function cc() {
    document.frm.rd[0].checked = true;
}
```

### 4.3 Key Properties

| Property | Description |
|----------|-------------|
| `checked` | Returns true if selected, false otherwise |
| `value` | The value attribute of the radio button |
| `name` | The name attribute (shared among group) |

### 4.4 Using Radio Buttons for Calculations

```html
<script>
function dotask(operation) {
    let n1 = document.getElementById("n1");
    let n2 = document.getElementById("n2");
    let n3 = document.getElementById("n3");
    
    // + before string converts string to number
    if (operation == "+") {
        n3.value = +n1.value + +n2.value;
    } else if (operation == "*") {
        n3.value = n1.value * n2.value;
    }
}
</script>

<form>
    <input type="text" id="n1"/>
    <input type="text" id="n2"/>
    <input type="radio" name="r1" value="+" onchange="dotask(this.value)"/>+
    <input type="radio" name="r1" value="*" onchange="dotask(this.value)"/>*
    <input type="number" id="n3" disabled/>
</form>
```

---

## 5. Checkbox Handling

### 5.1 Reading Checkbox Values

```html
<script>
function readchk() {
    var sldata = "";
    
    if (document.frm.a.checked)
        sldata += document.frm.a.value;
    
    if (document.frm.b.checked)
        sldata += document.frm.b.value;
    
    if (document.frm.c.checked)
        sldata += document.frm.c.value;
    
    document.getElementById("dd").innerHTML = sldata;
}
</script>

<form name="frm">
    <input type="checkbox" name="a" value="dance"/>dance
    <input type="checkbox" name="b" value="music"/>music
    <input type="checkbox" name="c" value="sports"/>sports
    <div id="dd"></div>
    <input type="button" value="read" onclick="readchk()">
</form>
```

### 5.2 Calculating Total from Checkboxes

```html
<script>
function dosum() {
    var sldata = 0;
    
    if (document.frm.a.checked)
        sldata += +document.frm.a.value;  // + converts to number
    
    if (document.frm.b.checked)
        sldata += +document.frm.b.value;
    
    if (document.frm.c.checked)
        sldata += +document.frm.c.value;
    
    document.getElementById("dd").innerHTML = sldata;
}
</script>

<form name="frm">
    <input type="checkbox" name="a" value="250"/>C 250/-
    <input type="checkbox" name="b" value="750"/>C# 750/-
    <input type="checkbox" name="c" value="550"/>JavaScript 550/-
    <div id="dd"></div>
    <input type="button" value="read" onclick="dosum()">
</form>
```

---

## 6. Dropdown (Select) Handling

### 6.1 Reading Selected Value

```html
<script>
function readradio() {
    var l = document.frm.sl.length;  // Number of options
    
    for (i = 0; i < l; i++) {
        if (document.frm.sl[i].selected) {
            document.frm.t.value = document.frm.sl[i].value;
        }
    }
    
    // Alternative: using selectedIndex
    let pobj = document.getElementById("pp");
    pobj.innerHTML = document.frm.sl.selectedIndex;
    
    let index = document.frm.sl.selectedIndex;
    pobj.innerHTML += document.frm.sl[index].text;
}
</script>

<form name="frm">
    <select name="sl" onchange="readradio()">
        <option value="0">dance</option>
        <option value="1">music</option>
        <option value="2">sports</option>
    </select>
    <input disabled name="t"/>
    <input type="button" value="read" onclick="readradio()">
</form>
```

### 6.2 Key Properties

| Property | Description |
|----------|-------------|
| `selected` | Boolean - if option is selected |
| `selectedIndex` | Index of selected option |
| `value` | Value attribute of option |
| `text` | Display text of option |
| `length` | Number of options |

---

## 7. Form Validation

### 7.1 Basic Validation with onsubmit

```html
<style>.err{color:red}</style>

<script>
function check() {
    var tobj = document.frm.nm;  // textbox
    data = tobj.value;           // value of textbox
    var len = data.length;
    let sobj = document.getElementById("ter");
    
    // Required field check
    if (len == 0) {
        sobj.innerHTML = "Password can not be blank";
        document.frm.nm.focus();
        return false;
    }
    else if (len < 8 || len > 16) {
        sobj.innerHTML = "Minimum 8, maximum 15 characters required";
        return false;
    }
    else {
        sobj.innerHTML = "";
    }
}
</script>

<form name="frm" action="blur.html" onsubmit="return check()">
    <label>Password</label>
    <input type="text" name="nm">
    <span id="ter" class="err"></span>
    <input type="submit" value="submit">
</form>
```

**Key Points:**
- `onsubmit` returns `true` by default
- Return `false` to prevent form submission
- Use `focus()` to set cursor on error field

### 7.2 isNaN() for Number Validation

```javascript
a = isNaN("56 ket");      // true - not a number
b = isNaN(5);             // false - is a number
c = isNaN("5");           // false - "5" converts to 5
b = isNaN(5 + 5);         // false - 10 is a number
```

### 7.3 Validation with onchange

```html
<script>
function validate(a, sid) {
    let s1 = document.getElementById(sid);
    
    if (a.value.length == 0 || a.value == "") {
        s1.innerHTML = "Text field can not be blank";
    }
    if (isNaN(a.value)) {
        s1.innerHTML = "Only number value allowed";
    }
}
</script>

<form>
    <input type="text" id="n1" onchange="validate(this,'err1')"/>
    <span id="err1"></span>
    <input type="text" id="n2" onchange="validate(this,'err2')"/>
    <span id="err2"></span>
</form>
```

---

## 8. Form Submission

### 8.1 Submit via Submit Button

```html
<form name="frm" action="page.html" onsubmit="return validate()">
    <!-- form elements -->
    <input type="submit" value="Submit">
</form>
```

### 8.2 Programmatic Submission

```javascript
function check() {
    var bool = true;
    var data = document.frm.nm.value;
    var len = data.length;
    let sobj = document.getElementById("ter");
    
    if (len == 0) {
        sobj.innerHTML = "Password can not be blank";
        document.frm.nm.focus();
        bool = false;
        return bool;
    }
    else if (len < 8 || len > 16) {
        sobj.innerHTML = "Minimum 8 character required";
        bool = false;
        return bool;
    }
    else {
        sobj.innerHTML = "";
    }
    
    if (bool == true) {
        document.frm.submit();  // Programmatically submit form
    }
}
```

### 8.3 Making Regular Button Work Like Submit

```html
<form name="frm" action="blur.html">
    <label>Password</label>
    <input type="text" name="nm">
    <span id="ter" class="err"></span>
    <!-- Button instead of submit -->
    <input type="button" value="dum" onclick="check()">
</form>
```

---

## 9. Dynamic Form Creation

### 9.1 Creating Form Elements Programmatically

```javascript
function call() {
    // Create form
    var f = document.createElement('form');
    f.name = 'frm';
    
    // Create text input
    var t = document.createElement('input');
    t.type = 'text';
    t.maxlength = 5;
    t.name = "t1";
    
    // Create radio buttons
    r1 = document.createElement('input');
    l1 = document.createElement('label');
    r2 = document.createElement('input');
    l2 = document.createElement('label');
    r1.type = "radio";
    r2.type = "radio";
    r1.name = "nm";
    r2.name = "nm";
    
    // Create labels
    newText1 = document.createTextNode("yes");
    newText2 = document.createTextNode("No");
    l1.appendChild(newText1);
    l2.appendChild(newText2);
    
    // Create select dropdown
    var s = document.createElement('select');
    var o = document.createElement('option');
    var o1 = document.createElement('option');
    o.innerHTML = "India";
    o1.innerHTML = "USA";
    s.appendChild(o);
    s.appendChild(o1);
    
    // Assemble form
    f.appendChild(t);
    f.appendChild(r1);
    f.appendChild(l1);
    f.appendChild(r2);
    f.appendChild(l2);
    f.appendChild(s);
    
    // Add to document
    document.getElementById('dd').appendChild(f);
}
```

---

## 10. Quick Reference

### 10.1 Accessing Elements

```javascript
document.formName.elementName
document.forms[0].elements[0]
document.getElementById("id")
```

### 10.2 Common Properties

| Element | Property | Description |
|---------|----------|-------------|
| Text | `value` | Input text |
| Radio | `checked` | Boolean |
| Radio | `value` | Option value |
| Checkbox | `checked` | Boolean |
| Select | `selectedIndex` | Index number |
| Select | `selected` | Boolean (on option) |
| Option | `text` | Display text |
| Option | `value` | Option value |

### 10.3 Form Events

| Event | Description |
|-------|-------------|
| `onsubmit` | Form submission |
| `onchange` | Value changed |
| `onblur` | Element loses focus |
| `onfocus` | Element gets focus |
| `onclick` | Element clicked |

### 10.4 Methods

```javascript
element.focus()           // Set focus
element.blur()            // Remove focus
form.submit()             // Submit form
form.reset()              // Reset form
```

---

## 11. Interview Questions

### Q1: How do you prevent form submission?
**Answer**: Return `false` from the `onsubmit` handler:
```html
<form onsubmit="return false">
```
Or in the validation function:
```javascript
function validate() {
    if (invalid) return false;
    return true;
}
```

### Q2: What's the difference between `this` and `this.form`?
**Answer**:
- `this` refers to the current element (e.g., button)
- `this.form` refers to the form containing the element

### Q3: How do you get all selected values from a multi-select?
**Answer**:
```javascript
var select = document.getElementById("mySelect");
var selected = [];
for (var i = 0; i < select.options.length; i++) {
    if (select.options[i].selected) {
        selected.push(select.options[i].value);
    }
}
```

### Q4: What does isNaN("5") return and why?
**Answer**: `false`, because JavaScript attempts to convert "5" to a number, and "5" successfully converts to the number 5.

### Q5: How do you programmatically submit a form?
**Answer**: Call the `submit()` method on the form:
```javascript
document.formName.submit();
// or
document.getElementById("formId").submit();
```

### Q6: What's the difference between `text` and `value` in a select option?
**Answer**:
- `text` is the visible display text between `<option>` tags
- `value` is the value attribute
```html
<option value="1">First Option</option>
<!-- text = "First Option", value = "1" -->
```

---

## Navigation

← Previous: [17_Date_and_Math_Functions.md](./17_Date_and_Math_Functions.md) | Next: Module 3 →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 04*
