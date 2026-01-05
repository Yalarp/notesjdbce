# AJAX and XMLHttpRequest

## Table of Contents
1. [Introduction](#1-introduction)
2. [XMLHttpRequest Object](#2-xmlhttprequest-object)
3. [Making GET Requests](#3-making-get-requests)
4. [Making POST Requests](#4-making-post-requests)
5. [Ready States and Status](#5-ready-states-and-status)
6. [Practical Examples](#6-practical-examples)
7. [AJAX vs Fetch](#7-ajax-vs-fetch)
8. [Quick Reference](#8-quick-reference)
9. [Interview Questions](#9-interview-questions)

---

## 1. Introduction

### 1.1 What is AJAX?
**AJAX** (Asynchronous JavaScript And XML) is not a programming language, but a technique for creating faster, more interactive web applications.

### 1.2 Key Features
- JavaScript can communicate directly with the server
- Uses XMLHttpRequest object
- Asynchronous data transfer
- Update parts of a page without reloading
- Browser technology independent of web server

### 1.3 AJAX Flow

```
1. Event occurs (page load, button click)
        ↓
2. XMLHttpRequest object created
        ↓
3. Request sent to web server
        ↓
4. Server processes request
        ↓
5. Server sends response (JSON/XML)
        ↓
6. JavaScript reads response
        ↓
7. JavaScript updates page (DOM)
```

### 1.4 AJAX is Based On
- JavaScript
- XML / JSON
- HTML
- CSS

---

## 2. XMLHttpRequest Object

### 2.1 Creating XMLHttpRequest

```javascript
var xhttp = new XMLHttpRequest();
```

### 2.2 Methods

| Method | Description |
|--------|-------------|
| `new XMLHttpRequest()` | Creates a new XMLHttpRequest object |
| `abort()` | Cancels the current request |
| `getAllResponseHeaders()` | Returns header information |
| `getResponseHeader()` | Returns specific header information |
| `open(method, url, async)` | Specifies the request |
| `send()` | Sends the request (GET) |
| `send(string)` | Sends the request with data (POST) |
| `setRequestHeader()` | Adds header to request |

### 2.3 Properties

| Property | Description |
|----------|-------------|
| `onreadystatechange` | Event handler for state changes |
| `readyState` | Status of XMLHttpRequest (0-4) |
| `responseText` | Response data as string |
| `responseXML` | Response data as XML |
| `status` | HTTP status code (200, 404, etc.) |
| `statusText` | HTTP status text |

---

## 3. Making GET Requests

### 3.1 The open() Method

```javascript
xhttp.open(method, url, async);
```

| Parameter | Description |
|-----------|-------------|
| `method` | GET or POST |
| `url` | Server URL |
| `async` | true (async) or false (sync) |

### 3.2 The send() Method

```javascript
xhttp.send();  // For GET requests
```

### 3.3 Complete GET Example

```javascript
function loadDoc() {
    var xhttp = new XMLHttpRequest();
    
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            document.getElementById("demo").innerHTML = this.responseText;
        }
    };
    
    xhttp.open("GET", "data.txt", true);
    xhttp.send();
}
```

---

## 4. Making POST Requests

### 4.1 When to Use POST
- Updating files/databases on server
- Sending large amounts of data (no size limits)
- Sending user input (more secure)
- Cached file is not an option

### 4.2 Setting Request Header for POST

```javascript
xhttp.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
```

### 4.3 Complete POST Example

```html
<form name='frm'>
    <label>Name</label><input name="name"/>
    <label>Email</label><input name="email"/>
    <label>Department</label><input name="department"/>
    <button type="button" onclick="loadDoc()">Send Form data</button>
</form>
<p id="demo"></p>

<script>
function loadDoc() {
    var form = document.querySelector('form');
    var data = {
        "name": form.name.value,
        "email": form.email.value,
        "department": form.department.value
    };
    
    let jdata = JSON.stringify(data);
    console.log(data);
    
    var xhttp = new XMLHttpRequest();
    
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            document.getElementById("demo").innerHTML = "Data inserted";
        }
    };
    
    xhttp.open("POST", "ejson.php", true);
    xhttp.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
    xhttp.send(jdata);
}
</script>
```

### 4.4 Using URL-Encoded Data

```javascript
var form = document.querySelector('form');
var data = new URLSearchParams(new FormData(form)).toString();
// Result: "name=Alice&age=25"

xhttp.open("POST", "ejson.php", true);
xhttp.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
xhttp.send(data);
```

---

## 5. Ready States and Status

### 5.1 readyState Values

| Value | State | Description |
|-------|-------|-------------|
| 0 | UNSENT | Request not initialized |
| 1 | OPENED | Server connection established |
| 2 | HEADERS_RECEIVED | Request has been sent |
| 3 | LOADING | Request is in process |
| 4 | DONE | Request is complete |

### 5.2 Common Status Codes

| Status | Meaning |
|--------|---------|
| 200 | OK |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

### 5.3 Checking Request Completion

```javascript
xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        // Request complete and successful
        console.log(this.responseText);
    }
};
```

---

## 6. Practical Examples

### 6.1 Reading JSON Data

```html
<button type="button" onclick="loadDoc()">Request data</button>
<p id="demo"></p>

<script>
function loadDoc() {
    var fd = "";
    var xhttp = new XMLHttpRequest();
    
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            let arr = JSON.parse(this.responseText);
            console.log(arr[0].code);
            
            for (let x of arr) {
                console.log(x);
                for (let b in x) {
                    console.log(x[b]);
                    fd += x[b] + "<br/>";
                }
                fd += "<hr/>";
            }
            document.getElementById("demo").innerHTML = fd;
        }
    };
    
    xhttp.open("GET", "ejson.json", true);
    xhttp.send();
}
</script>
```

### 6.2 Using Callback Functions

```html
<button onclick="loadDoc('ajax_info.txt', myFunction)">Get AJAX</button>
<button onclick="loadDoc('read_data.txt', go)">Read Data</button>

<div id="demo"></div>
<div id="dd"></div>

<script>
function loadDoc(url, cFunction) {
    var xhttp = new XMLHttpRequest();
    
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            cFunction(this);
        }
    };
    
    xhttp.open("GET", url, true);
    xhttp.send();
}

function myFunction(xhttp) {
    document.getElementById("demo").innerHTML = xhttp.responseText;
}

function go(xhttp) {
    document.getElementById("dd").innerHTML = xhttp.responseText;
}
</script>
```

---

## 7. AJAX vs Fetch

### 7.1 Comparison

| Feature | XMLHttpRequest | Fetch API |
|---------|----------------|-----------|
| Syntax | Verbose | Clean, Promise-based |
| Error handling | onreadystatechange | .catch() |
| Cancellation | abort() | AbortController |
| Progress | Supported | ReadableStream |
| JSON parsing | Manual | response.json() |
| Browser support | All | Modern browsers |

### 7.2 Content-Type Headers

| Content-Type | Usage |
|--------------|-------|
| `application/x-www-form-urlencoded` | Simple form submissions |
| `multipart/form-data` | File uploads |
| `application/json` | REST API, complex data |

---

## 8. Quick Reference

### 8.1 GET Request

```javascript
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        console.log(this.responseText);
    }
};
xhr.open("GET", "url", true);
xhr.send();
```

### 8.2 POST Request

```javascript
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        console.log(this.responseText);
    }
};
xhr.open("POST", "url", true);
xhr.setRequestHeader("Content-Type", "application/json");
xhr.send(JSON.stringify(data));
```

### 8.3 Key Events

```javascript
xhr.onreadystatechange  // State change
xhr.onload              // Load complete
xhr.onerror             // Error occurred
xhr.onprogress          // Progress update
```

---

## 9. Interview Questions

### Q1: What is AJAX?
**Answer**: AJAX (Asynchronous JavaScript And XML) is a technique for creating faster, more interactive web applications. It allows web pages to be updated asynchronously by exchanging data with a server behind the scenes, without reloading the page.

### Q2: What is the XMLHttpRequest object?
**Answer**: XMLHttpRequest is a browser API that provides an easy way to make HTTP requests from JavaScript. It's used to interact with servers, send data, and receive responses without refreshing the page.

### Q3: What are the ready states of XMLHttpRequest?
**Answer**:
- 0: UNSENT (request not initialized)
- 1: OPENED (connection established)
- 2: HEADERS_RECEIVED (request sent)
- 3: LOADING (processing)
- 4: DONE (complete)

### Q4: What is the difference between GET and POST in AJAX?
**Answer**:
- **GET**: Retrieves data, limited size, cached, visible in URL
- **POST**: Sends data, no size limit, not cached, more secure

### Q5: Why use Fetch instead of XMLHttpRequest?
**Answer**:
- Cleaner Promise-based syntax
- Better error handling
- Built-in JSON parsing
- More modern and readable

### Q6: What header is needed for sending JSON data?
**Answer**: `Content-Type: application/json`

---

## Navigation

← Previous: [28_Fetch_API.md](./28_Fetch_API.md) | Next: [30_NodeJS_Introduction.md](../Module_04_NodeJS_Fundamentals/30_NodeJS_Introduction.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 06*
