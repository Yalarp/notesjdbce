# jQuery AJAX

## Table of Contents
1. [Introduction](#1-introduction)
2. [The load() Method](#2-the-load-method)
3. [The get() and post() Methods](#3-the-get-and-post-methods)
4. [The ajax() Method](#4-the-ajax-method)
5. [Practical Example](#5-practical-example)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 What is AJAX?
AJAX = Asynchronous JavaScript And XML. It allows you to load data in the background and display it on the webpage, without reloading the whole page.

### 1.2 jQuery vs Raw JavaScript
Writing AJAX code in raw JavaScript involves tricky logic with `XMLHttpRequest` or `Fetch API`. jQuery provides a set of simple methods that handle browser differences and simplify the code.

---

## 2. The load() Method

The `load()` method loads data from a server and puts the returned data into the selected element.

**Syntax:**
```javascript
$(selector).load(URL, data, callback);
```

**Example:**
```javascript
$("#div1").load("demo_test.txt");
```

---

## 3. The get() and post() Methods

The `$.get()` and `$.post()` methods are used to request data from the server with an HTTP GET or POST request.

### 3.1 $.get()

```javascript
$.get("demo_test.asp", function(data, status){
    alert("Data: " + data + "\nStatus: " + status);
});
```

### 3.2 $.post()

```javascript
$.post("demo_test_post.asp",
{
    name: "Donald Duck",
    city: "Duckburg"
},
function(data, status){
    alert("Data: " + data + "\nStatus: " + status);
});
```

---

## 4. The ajax() Method

The `$.ajax()` method is the core method for performing AJAX requests. It offers full control over settings.

**Syntax:**
```javascript
$.ajax({name:value, name:value, ... });
```

**Common Options:**
- `url`: The URL to send the request to.
- `type`: "GET" or "POST".
- `data`: Data to be sent to the server.
- `success(result, status, xhr)`: Function to run on success.
- `error(xhr, status, error)`: Function to run on error.

```javascript
$.ajax({
    url: "demo_test.txt", 
    success: function(result){
        $("#div1").html(result);
    },
    error: function(xhr){
        alert("An error occured: " + xhr.status + " " + xhr.statusText);
    }
});
```

---

## 5. Practical Example

This example demonstrates loading a text file into a div using the `load()` method.

**Original Code Structure (Based on `demo_test.txt` example):**

**HTML:**
```html
<script>
$(document).ready(function(){
  $("button").click(function(){
    // Load content of demo_test.txt into #div1
    $("#div1").load("demo_test.txt", function(responseTxt, statusTxt, xhr){
        if(statusTxt == "success")
            alert("External content loaded successfully!");
        if(statusTxt == "error")
            alert("Error: " + xhr.status + ": " + xhr.statusText);
    });
  });
});
</script>

<div id="div1"><h2>Let jQuery AJAX Change This Text</h2></div>
<button>Get External Content</button>
```

**Execution Flow:**
1. User clicks the button.
2. `$("#div1").load("demo_test.txt")` is executed.
3. Browser sends an async HTTP GET request for `demo_test.txt`.
4. **On Success**: The content of `#div1` is replaced with the file content. "External content loaded successfully!" alert is shown.
5. **On Error** (e.g., file not found): Error alert is shown.

---

## 6. Quick Reference

| Method | Description |
|--------|-------------|
| `load()` | Load data into an element |
| `$.get()` | Load data using GET |
| `$.post()` | Load data using POST |
| `$.ajax()` | Perform async AJAX request with full control |
| `$.getJSON()` | Load JSON-encoded data using a GET request |

---

## 7. Interview Questions

### Q1: What is the difference between `load()` and `$.get()`?
**Answer**:
- `load()` is a specific method designed to fetch HTML/text and directly inject it **into a selected DOM element**.
- `$.get()` is a general global method to fetch data, which you then have to handle manually in a callback (parse it, insert it, etc.).

### Q2: How do you handle errors in jQuery AJAX?
**Answer**:
- In `$.ajax()`, use the `error` callback option.
- In `load()`, use the callback function and check the `statusTxt` parameter.
- Globally, you can use `.fail()` on the promise returned by methods like `$.get()`.

### Q3: What is JSONP?
**Answer**: JSON with Padding. It is a technique used to overcome the cross-domain restrictions (CORS) in older browsers. In jQuery, you can set `dataType: "jsonp"`.

---

## Navigation

← Previous: [64_jQuery_Forms.md](./64_jQuery_Forms.md) | Next: [66_JavaScript_Interview_QA.md](../Module_09_Interview_Preparation/66_JavaScript_Interview_QA.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 13*
