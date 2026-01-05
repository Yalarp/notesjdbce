# jQuery Form Handling

## Table of Contents
1. [Introduction](#1-introduction)
2. [Get/Set Values](#2-getset-values)
3. [Form Events](#3-form-events)
4. [Validating Forms](#4-validating-forms)
5. [Practical Example](#5-practical-example)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

jQuery simplifies form handling by providing easy methods to get and set values of form controls (inputs, textareas, selects, checkboxes, radios) and handle events like submission and changes.

---

## 2. Get/Set Values

The primary method for form elements is `.val()`.

### 2.1 Get Value
```javascript
var name = $("#name").val();
```

### 2.2 Set Value
```javascript
$("#name").val("New Name");
```

---

## 3. Form Events

| Event | Triggers When |
|-------|---------------|
| `submit()` | Form is submitted |
| `change()` | Input value changes (and loses focus) |
| `focus()` | Element gets focus |
| `blur()` | Element loses focus |
| `select()` | Text is selected in input/textarea |

---

## 4. Validating Forms

While there are plugins (like jQuery Validation), basic validation is often done manually on submit.

```javascript
$("form").submit(function(event){
    var name = $("#name").val();
    if(name == "") {
        alert("Name required");
        event.preventDefault(); // Stop submission
    }
});
```

---

## 5. Practical Example

This example demonstrates handling text inputs and checkboxes.

### 5.1 Handling Text Input
**Original Code (Based on `01_frm_text.html`):**

```html
<script>
$(document).ready(function(){
  $("#b1").click(function(){
      // Get value from input
      var data = $("#t1").val();
      // Set value to div
      $("#d1").html(data);
  });
});
</script>

<input type="text" id="t1" />
<button id="b1">Show Value</button>
<div id="d1"></div>
```

### 5.2 Handling Checkboxes
**Original Code (Based on `02_frm_checkbox.html`):**

```html
<script>
$(document).ready(function(){
  $("#btn").click(function(){
      var str = "";
      
      // Select all checked checkboxes with name 'chk'
      $("input[name='chk']:checked").each(function(){
          // Append value to string
          str += $(this).val() + " ";
      });
      
      // Display result
      $("#result").html(str);
  });
});
</script>

<input type="checkbox" name="chk" value="Java"> Java
<input type="checkbox" name="chk" value="PHP"> PHP
<input type="checkbox" name="chk" value=".NET"> .NET
<button id="btn">Get Selected</button>
<div id="result"></div>
```

**Execution Flow:**
1. User checks "Java" and ".NET".
2. User clicks "Get Selected".
3. Selector `$("input[name='chk']:checked")` finds the two checked elements.
4. `.each()` loop iterates over them.
5. `str` becomes "Java .NET ".
6. Result displayed in `#result`.

---

## 6. Quick Reference

| Control | Get Value | Set Value |
|---------|-----------|-----------|
| **Input (Text)** | `$(sel).val()` | `$(sel).val("txt")` |
| **Checkbox** | `$(sel).is(":checked")` | `$(sel).prop("checked", true)` |
| **Radio** | `$("input[name='n']:checked").val()` | `...prop("checked", true)` |
| **Select** | `$(sel).val()` | `$(sel).val("opt-val")` |

---

## 7. Interview Questions

### Q1: How do you get the value of a selected radio button?
**Answer**: By using the `:checked` selector on the group name.
`var val = $("input[name='gender']:checked").val();`

### Q2: What is difference between `.val()` and `.attr('value')`?
**Answer**:
- `.val()` returns the **current property** (state) of the input (what the user typed).
- `.attr('value')` returns the **initial attribute** value from the HTML source (what was there at load).

### Q3: How do you check if a checkbox is checked?
**Answer**:
- `if($("#chk").is(":checked")) { ... }`
- OR `if($("#chk").prop("checked")) { ... }`

### Q4: How do you prevent a form from submitting if validation fails?
**Answer**: Use `event.preventDefault()` inside the submit handler.

---

## Navigation

← Previous: [63_jQuery_Effects.md](./63_jQuery_Effects.md) | Next: [65_jQuery_AJAX.md](./65_jQuery_AJAX.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 13*
