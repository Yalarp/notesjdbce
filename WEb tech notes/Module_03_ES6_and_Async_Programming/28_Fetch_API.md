# Fetch API in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Basic Fetch Syntax](#2-basic-fetch-syntax)
3. [Response Object](#3-response-object)
4. [Reading Response Body](#4-reading-response-body)
5. [POST Requests](#5-post-requests)
6. [Request Headers](#6-request-headers)
7. [Practical Examples](#7-practical-examples)
8. [Quick Reference](#8-quick-reference)
9. [Interview Questions](#9-interview-questions)

---

## 1. Introduction

### 1.1 What is Fetch API?
The **Fetch API** provides a modern, versatile way to send network requests from JavaScript. It's Promise-based and is the standard replacement for XMLHttpRequest.

### 1.2 AJAX
**AJAX** (Asynchronous JavaScript And XML) is an umbrella term for network requests from JavaScript. Despite the name, we don't have to use XML - the term comes from old times.

### 1.3 Use Cases
- Submit an order
- Load user information
- Receive latest updates from the server
- All without reloading the page!

---

## 2. Basic Fetch Syntax

### 2.1 Basic Syntax

```javascript
let promise = fetch(url, [options]);
```

| Parameter | Description |
|-----------|-------------|
| `url` | The URL to access |
| `options` | Optional: method, headers, body, etc. |

### 2.2 Simple GET Request

```javascript
// Without options, this is a simple GET request
let response = await fetch('https://api.example.com/data');
```

### 2.3 Two-Stage Process

Getting a response is usually a two-stage process:

**Stage 1:** Promise resolves with Response object (headers received)
```javascript
let response = await fetch(url);
// At this stage: headers available, no body yet
```

**Stage 2:** Read the body using additional method
```javascript
let data = await response.json();
// Now we have the data
```

---

## 3. Response Object

### 3.1 Response Properties

| Property | Description |
|----------|-------------|
| `response.status` | HTTP status code (e.g., 200) |
| `response.ok` | `true` if status is 200-299 |
| `response.headers` | Headers object |
| `response.body` | ReadableStream object |

### 3.2 Checking Response Status

```javascript
let response = await fetch(url);

if (response.ok) {
    // HTTP status is 200-299
    let json = await response.json();
} else {
    alert("HTTP-Error: " + response.status);
}
```

### 3.3 Response Headers

```javascript
let response = await fetch('ejson.json');

// Get one header
alert(response.headers.get('Content-Type'));
// application/json; charset=utf-8

// Iterate over all headers
for (let [key, value] of response.headers) {
    alert(`${key} = ${value}`);
}
```

---

## 4. Reading Response Body

### 4.1 Response Methods

| Method | Returns |
|--------|---------|
| `response.text()` | Response as text |
| `response.json()` | Response parsed as JSON |
| `response.formData()` | Response as FormData |
| `response.blob()` | Response as Blob (binary) |
| `response.arrayBuffer()` | Response as ArrayBuffer |

### 4.2 Reading JSON

```javascript
let response = await fetch('https://api.example.com/data');
let data = await response.json();
console.log(data);
```

### 4.3 Reading Text

```javascript
let response = await fetch('https://api.example.com/page');
let text = await response.text();
alert(text.slice(0, 80) + '...');
```

### 4.4 Using Promises (no await)

```javascript
fetch('ejson.json')
    .then(response => response.json())
    .then(data => alert(data[0].name));
```

### 4.5 Important: Choose One Method

You can only read the body once:

```javascript
let text = await response.text();  // body consumed
let parsed = await response.json(); // ERROR! Already consumed
```

---

## 5. POST Requests

### 5.1 POST with JSON Body

```javascript
let user = {
    name: 'John',
    surname: 'Smith'
};

let response = await fetch('http://localhost:5500/api/product', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json;charset=utf-8'
    },
    body: JSON.stringify(user)
});

let result = await response.json();
```

### 5.2 Fetch Options

| Option | Description |
|--------|-------------|
| `method` | HTTP method (GET, POST, PUT, DELETE) |
| `headers` | Request headers object |
| `body` | Request body (string, FormData, Blob, etc.) |
| `mode` | cors, no-cors, same-origin |
| `credentials` | include, same-origin, omit |

### 5.3 Body Types

| Type | Use Case |
|------|----------|
| String | JSON-encoded data |
| FormData | Form data (multipart) |
| Blob | Binary data |
| URLSearchParams | URL-encoded data |

---

## 6. Request Headers

### 6.1 Setting Headers

```javascript
let response = await fetch(protectedUrl, {
    headers: {
        'Authentication': 'secret',
        'Content-Type': 'application/json'
    }
});
```

### 6.2 Forbidden Headers

Some headers cannot be set for security reasons:
- Accept-Charset, Accept-Encoding
- Connection, Content-Length
- Cookie, Cookie2
- Host, Origin, Referer
- And others...

These are controlled exclusively by the browser.

---

## 7. Practical Examples

### 7.1 Fetching and Displaying JSON

```html
<p id="p"></p>
<script>
async function getdata() {
    let res = await fetch('ejson.json');
    let data = await res.json();
    
    let fd = "";
    for (let x of data) {
        console.log(x);
        for (let b in x) {
            console.log(x[b]);
            fd += x[b] + "<br/>";
        }
        fd += "<hr/>";
    }
    document.getElementById('p').innerHTML = fd;
}

getdata();
</script>
```

### 7.2 Error Handling

```javascript
async function fetchData() {
    try {
        let response = await fetch('https://api.example.com/data');
        
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        let data = await response.json();
        return data;
    } catch (error) {
        console.error('Fetch failed:', error);
    }
}
```

### 7.3 Complete POST Example

```javascript
async function postData(url, data) {
    const response = await fetch(url, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
    });
    
    if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    return await response.json();
}

// Usage
postData('/api/users', { name: 'John', age: 30 })
    .then(data => console.log(data))
    .catch(error => console.error(error));
```

---

## 8. Quick Reference

### 8.1 GET Request

```javascript
// With async/await
async function getData() {
    let response = await fetch(url);
    let data = await response.json();
    return data;
}

// With Promises
fetch(url)
    .then(response => response.json())
    .then(data => console.log(data));
```

### 8.2 POST Request

```javascript
fetch(url, {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify(data)
});
```

### 8.3 Response Reading

```javascript
// JSON
let json = await response.json();

// Text
let text = await response.text();

// Blob
let blob = await response.blob();
```

### 8.4 Error Handling

```javascript
try {
    let response = await fetch(url);
    if (!response.ok) {
        throw new Error(`HTTP Error: ${response.status}`);
    }
    let data = await response.json();
} catch (error) {
    console.error('Error:', error);
}
```

---

## 9. Interview Questions

### Q1: What is the Fetch API?
**Answer**: The Fetch API is a modern interface for making HTTP requests in JavaScript. It's Promise-based and provides a more powerful and flexible way to send network requests compared to XMLHttpRequest.

### Q2: What does fetch() return?
**Answer**: `fetch()` returns a Promise that resolves to a Response object representing the response to the request.

### Q3: How do you read JSON from a fetch response?
**Answer**: Use the `.json()` method:
```javascript
let response = await fetch(url);
let data = await response.json();
```

### Q4: Does fetch reject on HTTP errors like 404 or 500?
**Answer**: No. Fetch only rejects on network failures. For HTTP errors, you must check `response.ok` or `response.status`.

### Q5: How do you send a POST request with fetch?
**Answer**:
```javascript
fetch(url, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(data)
});
```

### Q6: Can you read the response body multiple times?
**Answer**: No. The response body can only be consumed once. Calling `response.json()` after `response.text()` will fail.

---

## Navigation

← Previous: [27_Async_Await.md](./27_Async_Await.md) | Next: [29_AJAX_XMLHttpRequest.md](./29_AJAX_XMLHttpRequest.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 06*
