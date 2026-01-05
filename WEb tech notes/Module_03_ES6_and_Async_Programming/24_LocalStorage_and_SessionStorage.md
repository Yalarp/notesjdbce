# LocalStorage and SessionStorage

## Table of Contents
1. [Introduction](#1-introduction)
2. [LocalStorage](#2-localstorage)
3. [SessionStorage](#3-sessionstorage)
4. [Storage Methods](#4-storage-methods)
5. [Storing Complex Data](#5-storing-complex-data)
6. [Practical Examples](#6-practical-examples)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 Web Storage API
Web Storage provides two different storage areas that differ in scope and lifetime:
- **LocalStorage**: Persistent storage across sessions
- **SessionStorage**: Storage for a single session

### 1.2 Comparison

| Feature | LocalStorage | SessionStorage | Cookies |
|---------|--------------|----------------|---------|
| Capacity | ~5MB | ~5MB | ~4KB |
| Expires | Never (unless cleared) | Tab/window close | Set expiry |
| Accessible | All windows | Same tab only | All windows |
| Sent with requests | No | No | Yes |
| Storage location | Browser | Browser | Browser |

### 1.3 Key Points to Remember
- Data persists until explicitly deleted or browser cache is cleared (localStorage)
- Data persists until tab/window is closed (sessionStorage)
- Data stored by one browser is NOT accessible by another browser
- Objects should be stored as JSON strings
- Sensitive data should NOT be stored
- Storage changes trigger a "storage" event

---

## 2. LocalStorage

### 2.1 Definition
The `localStorage` object stores data with no expiration date. Data is NOT deleted when the browser is closed.

### 2.2 Benefits
- Long term data persistence
- No HTTP overhead (unlike cookies)
- Effective for storing user preferences
- Spans multiple windows/tabs
- Persists beyond current session

### 2.3 Basic Usage

```javascript
// Store data
localStorage.setItem("username", "John");

// Retrieve data
var name = localStorage.getItem("username");
console.log(name);  // "John"

// Remove specific item
localStorage.removeItem("username");

// Clear all data
localStorage.clear();
```

---

## 3. SessionStorage

### 3.1 Definition
The `sessionStorage` object stores data for only one session. Data is deleted when the browser tab is closed.

### 3.2 Use Cases
- Temporary form data
- Single-page application state
- Shopping cart (per tab)
- Login session data

### 3.3 Basic Usage

```javascript
// Store data
sessionStorage.setItem("tempData", "value");

// Retrieve data
var data = sessionStorage.getItem("tempData");

// Remove specific item
sessionStorage.removeItem("tempData");

// Clear all data
sessionStorage.clear();
```

---

## 4. Storage Methods

### 4.1 Methods Table

| Method | Description |
|--------|-------------|
| `setItem(key, value)` | Store key/value pair |
| `getItem(key)` | Get value by key |
| `removeItem(key)` | Remove specific item |
| `clear()` | Remove ALL items |
| `key(index)` | Get key at specified index |

### 4.2 Properties

| Property | Description |
|----------|-------------|
| `length` | Number of stored items |

### 4.3 Examples

```javascript
// Store
localStorage.setItem("name", "John");

// Retrieve
localStorage.getItem("name");  // "John"

// Length
console.log(localStorage.length);  // 1

// Get key by index
console.log(localStorage.key(0));  // "name"

// Remove
localStorage.removeItem("name");

// Clear all
localStorage.clear();
```

---

## 5. Storing Complex Data

### 5.1 The Problem
Storage only accepts strings. Complex objects must be converted.

```javascript
// This WON'T work correctly
localStorage.setItem("user", {name: "John"});
console.log(localStorage.getItem("user"));  // "[object Object]"
```

### 5.2 The Solution: JSON

```javascript
// Storing complex data
const userData = {
    job: "Programmer",
    skills: [
        { id: 4200, name: "Angular" },
        { id: 3000, name: "React" },
        { id: 8080, name: "Vue" }
    ]
};

// Store - convert to JSON string
localStorage.setItem("userData", JSON.stringify(userData));

// Retrieve - parse back to object
const data = localStorage.getItem("userData");
console.log("data:", JSON.parse(data));
```

### 5.3 Complete Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Storage Demo</title>
</head>
<body>
    <script>
        function Storedata() {
            const userData = {
                job: "Programmer",
                skills: [
                    { id: 4200, name: "Angular" },
                    { id: 3000, name: "React" },
                    { id: 8080, name: "Vue" }
                ]
            };
            // Store the object into storage
            localStorage.setItem("userData", JSON.stringify(userData));
        }
        
        function Getdata() {
            const data = localStorage.getItem("userData");
            console.log("data:", JSON.parse(data));
            
            let ta = document.getElementById("ta");
            let obj = JSON.parse(data);
            ta.innerHTML = JSON.stringify(obj);
        }
    </script>
    
    <input type="button" value="Store object" onclick="Storedata()" />
    <input type="button" value="Get object" onclick="Getdata()" />
    <textarea id="ta"></textarea>
</body>
</html>
```

---

## 6. Practical Examples

### 6.1 Remember User Preferences

```javascript
// Save theme preference
function saveTheme(theme) {
    localStorage.setItem("theme", theme);
    document.body.className = theme;
}

// Load theme on page load
function loadTheme() {
    const theme = localStorage.getItem("theme");
    if (theme) {
        document.body.className = theme;
    }
}

// Call on page load
window.onload = loadTheme;
```

### 6.2 Shopping Cart

```javascript
// Add item to cart
function addToCart(item) {
    let cart = JSON.parse(sessionStorage.getItem("cart")) || [];
    cart.push(item);
    sessionStorage.setItem("cart", JSON.stringify(cart));
}

// Get cart
function getCart() {
    return JSON.parse(sessionStorage.getItem("cart")) || [];
}

// Clear cart
function clearCart() {
    sessionStorage.removeItem("cart");
}
```

### 6.3 Form Auto-Save

```javascript
// Auto-save form data
document.getElementById("myForm").oninput = function() {
    const formData = {
        name: document.getElementById("name").value,
        email: document.getElementById("email").value
    };
    sessionStorage.setItem("formData", JSON.stringify(formData));
};

// Restore form data on page load
window.onload = function() {
    const saved = sessionStorage.getItem("formData");
    if (saved) {
        const formData = JSON.parse(saved);
        document.getElementById("name").value = formData.name;
        document.getElementById("email").value = formData.email;
    }
};
```

---

## 7. Quick Reference

### 7.1 LocalStorage

```javascript
// Store
localStorage.setItem("key", "value");

// Retrieve
localStorage.getItem("key");

// Remove
localStorage.removeItem("key");

// Clear all
localStorage.clear();

// Length
localStorage.length;

// Get key by index
localStorage.key(0);
```

### 7.2 SessionStorage

```javascript
// Store
sessionStorage.setItem("key", "value");

// Retrieve
sessionStorage.getItem("key");

// Remove
sessionStorage.removeItem("key");

// Clear all
sessionStorage.clear();
```

### 7.3 JSON Operations

```javascript
// Store object
localStorage.setItem("obj", JSON.stringify(myObject));

// Retrieve object
const obj = JSON.parse(localStorage.getItem("obj"));
```

### 7.4 When to Use Which

| Use Case | Storage Type |
|----------|--------------|
| User preferences | localStorage |
| Login tokens | sessionStorage |
| Shopping cart | sessionStorage |
| Theme settings | localStorage |
| Form draft | sessionStorage |
| Language preference | localStorage |

---

## 8. Interview Questions

### Q1: What is the difference between localStorage and sessionStorage?
**Answer**:
- **localStorage**: Data persists until explicitly deleted, available across all tabs/windows
- **sessionStorage**: Data persists only for the session, limited to the current tab/window

### Q2: What is the storage limit for Web Storage?
**Answer**: Typically around 5MB per origin, though this can vary by browser. This is much larger than cookies (4KB).

### Q3: How do you store objects in localStorage?
**Answer**: Use `JSON.stringify()` when storing and `JSON.parse()` when retrieving:
```javascript
localStorage.setItem("user", JSON.stringify(userObject));
const user = JSON.parse(localStorage.getItem("user"));
```

### Q4: Is Web Storage secure for storing sensitive data?
**Answer**: No. Web Storage is accessible via JavaScript, so any XSS attack could access the data. Sensitive information like passwords or tokens should not be stored.

### Q5: What happens when localStorage is full?
**Answer**: A `QuotaExceededError` exception is thrown. Always wrap storage operations in try-catch:
```javascript
try {
    localStorage.setItem("key", largeData);
} catch (e) {
    console.log("Storage full!");
}
```

### Q6: Can data from one domain access another domain's localStorage?
**Answer**: No. The Same-Origin Policy prevents this. Each domain has its own isolated storage.

---

## Navigation

← Previous: [23_JSON_Handling.md](./23_JSON_Handling.md) | Next: [25_Object_Destructuring.md](./25_Object_Destructuring.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 05*
