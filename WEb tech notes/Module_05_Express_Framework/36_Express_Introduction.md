# Express.js Introduction

## Table of Contents
1. [Introduction](#1-introduction)
2. [Getting Started](#2-getting-started)
3. [Basic Application](#3-basic-application)
4. [Request and Response](#4-request-and-response)
5. [Application Structure](#5-application-structure)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 What is Express.js?
**Express.js** is a minimal, flexible, and fast web application framework for Node.js. It provides a robust set of features for web and mobile applications.

### 1.2 Why Express?
- Most popular Node.js framework
- Minimal and unopinionated
- Easy to learn
- Large ecosystem
- Middleware support
- Template engine integration

### 1.3 Features

| Feature | Description |
|---------|-------------|
| Routing | Define application endpoints |
| Middleware | Request processing pipeline |
| Template engines | Dynamic HTML rendering |
| Static files | Serve CSS, images, JS |
| Error handling | Built-in error handling |

---

## 2. Getting Started

### 2.1 Installation

```bash
# Create project folder
mkdir my-express-app
cd my-express-app

# Initialize npm
npm init -y

# Install Express
npm install express
```

### 2.2 Project Structure

```
my-express-app/
├── node_modules/
├── public/
│   ├── css/
│   ├── js/
│   └── images/
├── routes/
├── views/
├── app.js
└── package.json
```

---

## 3. Basic Application

### 3.1 Hello World

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
    res.send('Hello World!');
});

app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});
```

### 3.2 Running the Application

```bash
node app.js
```

### 3.3 Understanding the Code

```javascript
// 1. Import Express
const express = require('express');

// 2. Create Express application
const app = express();

// 3. Define route
app.get('/', (req, res) => {
    // Request handler
    res.send('Hello World!');
});

// 4. Start server
app.listen(3000);
```

---

## 4. Request and Response

### 4.1 Request Object (req)

| Property | Description |
|----------|-------------|
| `req.params` | Route parameters |
| `req.query` | Query string parameters |
| `req.body` | Request body (needs middleware) |
| `req.headers` | Request headers |
| `req.method` | HTTP method |
| `req.url` | Request URL |
| `req.path` | URL path |

### 4.2 Response Object (res)

| Method | Description |
|--------|-------------|
| `res.send()` | Send response |
| `res.json()` | Send JSON response |
| `res.render()` | Render template |
| `res.redirect()` | Redirect to URL |
| `res.status()` | Set status code |
| `res.sendFile()` | Send file |
| `res.download()` | Download file |

### 4.3 Response Examples

```javascript
// Plain text
res.send('Hello World');

// JSON
res.json({ message: 'Hello', status: 'success' });

// Status with JSON
res.status(201).json({ id: 1, name: 'Created' });

// Redirect
res.redirect('/login');

// Send file
res.sendFile(__dirname + '/public/index.html');

// Download
res.download('/path/to/file.pdf');

// Set header
res.set('Content-Type', 'text/plain');
res.send('Hello');
```

---

## 5. Application Structure

### 5.1 Basic Routes

```javascript
const express = require('express');
const app = express();

// GET request
app.get('/', (req, res) => {
    res.send('GET request');
});

// POST request
app.post('/submit', (req, res) => {
    res.send('POST request');
});

// PUT request
app.put('/update/:id', (req, res) => {
    res.send(`PUT request for ${req.params.id}`);
});

// DELETE request
app.delete('/delete/:id', (req, res) => {
    res.send(`DELETE request for ${req.params.id}`);
});

app.listen(3000);
```

### 5.2 Serving Static Files

```javascript
const express = require('express');
const app = express();
const path = require('path');

// Serve static files from 'public' directory
app.use(express.static('public'));

// Or with virtual path prefix
app.use('/static', express.static('public'));

// Absolute path (recommended)
app.use(express.static(path.join(__dirname, 'public')));

app.listen(3000);
```

### 5.3 Parsing Request Body

```javascript
const express = require('express');
const app = express();

// Parse JSON bodies
app.use(express.json());

// Parse URL-encoded bodies
app.use(express.urlencoded({ extended: true }));

app.post('/api/users', (req, res) => {
    console.log(req.body);  // { name: 'John', email: '...' }
    res.json(req.body);
});

app.listen(3000);
```

---

## 6. Quick Reference

### 6.1 Creating Application

```javascript
const express = require('express');
const app = express();

app.listen(3000, () => {
    console.log('Server running');
});
```

### 6.2 HTTP Methods

```javascript
app.get('/path', handler);
app.post('/path', handler);
app.put('/path', handler);
app.delete('/path', handler);
app.all('/path', handler);  // All methods
```

### 6.3 Response Methods

```javascript
res.send('text');
res.json({ data });
res.status(code);
res.redirect('url');
res.render('view');
res.sendFile(path);
```

### 6.4 Common Middleware

```javascript
// JSON body parser
app.use(express.json());

// URL-encoded parser
app.use(express.urlencoded({ extended: true }));

// Static files
app.use(express.static('public'));
```

---

## 7. Interview Questions

### Q1: What is Express.js?
**Answer**: Express.js is a minimal, fast, and flexible web application framework for Node.js. It provides features for building web applications and APIs, including routing, middleware, and template engines.

### Q2: Why use Express over plain Node.js HTTP?
**Answer**:
- Simplified routing
- Middleware support
- Built-in methods for common tasks
- Template engine integration
- Static file serving
- Better error handling

### Q3: What is the difference between res.send() and res.json()?
**Answer**:
- `res.send()`: Sends response of various types (string, object, buffer)
- `res.json()`: Specifically sends JSON response with proper Content-Type header

### Q4: How do you access URL parameters?
**Answer**:
```javascript
// Route: /users/:id
app.get('/users/:id', (req, res) => {
    console.log(req.params.id);
});
```

### Q5: How do you access query strings?
**Answer**:
```javascript
// URL: /search?q=node
app.get('/search', (req, res) => {
    console.log(req.query.q);  // 'node'
});
```

### Q6: How do you parse JSON request body?
**Answer**: Use the built-in middleware:
```javascript
app.use(express.json());
```

---

## Navigation

← Previous: [35_Events_and_EventEmitter.md](../Module_04_NodeJS_Fundamentals/35_Events_and_EventEmitter.md) | Next: [37_Express_Routing.md](./37_Express_Routing.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 08*
