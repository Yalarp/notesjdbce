# HTTP Server Basics in Node.js

## Table of Contents
1. [Introduction](#1-introduction)
2. [Creating HTTP Server](#2-creating-http-server)
3. [Request and Response](#3-request-and-response)
4. [Routing](#4-routing)
5. [Serving HTML](#5-serving-html)
6. [Serving Static Files](#6-serving-static-files)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 The http Module
The `http` module is a core Node.js module that allows creating HTTP servers and making HTTP requests.

```javascript
const http = require('http');
```

### 1.2 How It Works

```
┌─────────────┐     Request     ┌─────────────────┐
│   Client    │ ───────────────→│   HTTP Server   │
│  (Browser)  │                 │    (Node.js)    │
│             │ ←───────────────│                 │
└─────────────┘    Response     └─────────────────┘
```

---

## 2. Creating HTTP Server

### 2.1 Basic Server

```javascript
const http = require('http');

const server = http.createServer((request, response) => {
    response.writeHead(200, {'Content-Type': 'text/plain'});
    response.end('Hello World!\n');
});

server.listen(3000, () => {
    console.log('Server running at http://localhost:3000/');
});
```

### 2.2 Server with Request Listener

```javascript
const http = require('http');

function requestListener(req, res) {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Welcome Viewers\n');
}

const server = http.createServer(requestListener);
server.listen(8080);
```

### 2.3 Understanding the Flow

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    // 1. Set response headers
    res.writeHead(200, {
        'Content-Type': 'text/html',
        'X-Custom-Header': 'MyValue'
    });
    
    // 2. Write response body
    res.write('<h1>Hello</h1>');
    res.write('<p>World</p>');
    
    // 3. End response
    res.end();
});

server.listen(3000, '127.0.0.1', () => {
    console.log('Server running on port 3000');
});
```

---

## 3. Request and Response

### 3.1 Request Object Properties

| Property | Description |
|----------|-------------|
| `req.url` | Request URL path |
| `req.method` | HTTP method (GET, POST) |
| `req.headers` | Request headers |
| `req.httpVersion` | HTTP version |

```javascript
http.createServer((req, res) => {
    console.log('URL:', req.url);
    console.log('Method:', req.method);
    console.log('Headers:', req.headers);
    
    res.end('Request received');
}).listen(3000);
```

### 3.2 Response Object Methods

| Method | Description |
|--------|-------------|
| `res.writeHead(status, headers)` | Set status and headers |
| `res.setHeader(name, value)` | Set single header |
| `res.write(data)` | Write to body |
| `res.end([data])` | End response |
| `res.statusCode` | Set status code |

### 3.3 Status Codes

| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 301 | Moved Permanently |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---

## 4. Routing

### 4.1 Basic Routing

```javascript
const http = require('http');

http.createServer((req, res) => {
    res.writeHead(200, {'Content-Type': 'text/html'});
    
    if (req.url === '/') {
        res.end('<h1>Home Page</h1>');
    } else if (req.url === '/about') {
        res.end('<h1>About Page</h1>');
    } else if (req.url === '/contact') {
        res.end('<h1>Contact Page</h1>');
    } else {
        res.writeHead(404);
        res.end('<h1>404 - Page Not Found</h1>');
    }
}).listen(3000);
```

### 4.2 Method-Based Routing

```javascript
http.createServer((req, res) => {
    if (req.url === '/api/users' && req.method === 'GET') {
        res.writeHead(200, {'Content-Type': 'application/json'});
        res.end(JSON.stringify([{id: 1, name: 'John'}]));
    } else if (req.url === '/api/users' && req.method === 'POST') {
        // Handle POST
        res.writeHead(201);
        res.end('User created');
    } else {
        res.writeHead(404);
        res.end('Not found');
    }
}).listen(3000);
```

---

## 5. Serving HTML

### 5.1 Inline HTML

```javascript
http.createServer((req, res) => {
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.end(`
        <!DOCTYPE html>
        <html>
        <head><title>My Page</title></head>
        <body>
            <h1>Welcome to Node.js</h1>
        </body>
        </html>
    `);
}).listen(3000);
```

### 5.2 Loading HTML from File

```javascript
const http = require('http');
const fs = require('fs');

http.createServer((req, res) => {
    fs.readFile('index.html', (err, data) => {
        if (err) {
            res.writeHead(500, {'Content-Type': 'text/plain'});
            res.end('Internal Server Error');
            return;
        }
        res.writeHead(200, {'Content-Type': 'text/html'});
        res.end(data);
    });
}).listen(3000);
```

### 5.3 Dynamic HTML

```javascript
const users = [{name: 'John'}, {name: 'Jane'}];

http.createServer((req, res) => {
    let html = '<ul>';
    users.forEach(user => {
        html += `<li>${user.name}</li>`;
    });
    html += '</ul>';
    
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.end(html);
}).listen(3000);
```

---

## 6. Serving Static Files

### 6.1 Basic Static File Server

```javascript
const http = require('http');
const fs = require('fs');
const path = require('path');

const mimeTypes = {
    '.html': 'text/html',
    '.css': 'text/css',
    '.js': 'text/javascript',
    '.json': 'application/json',
    '.png': 'image/png',
    '.jpg': 'image/jpeg'
};

http.createServer((req, res) => {
    let filePath = '.' + req.url;
    if (filePath === './') filePath = './index.html';
    
    const ext = path.extname(filePath);
    const contentType = mimeTypes[ext] || 'application/octet-stream';
    
    fs.readFile(filePath, (err, data) => {
        if (err) {
            res.writeHead(404);
            res.end('File not found');
            return;
        }
        res.writeHead(200, {'Content-Type': contentType});
        res.end(data);
    });
}).listen(3000);
```

### 6.2 Serving JSON

```javascript
const data = {
    name: 'Node.js',
    version: '18.0.0',
    features: ['async', 'event-driven', 'fast']
};

http.createServer((req, res) => {
    res.writeHead(200, {'Content-Type': 'application/json'});
    res.end(JSON.stringify(data));
}).listen(3000);
```

---

## 7. Quick Reference

### 7.1 Creating Server

```javascript
const http = require('http');

http.createServer((req, res) => {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Hello');
}).listen(3000);
```

### 7.2 Response Methods

```javascript
res.writeHead(statusCode, headers);
res.setHeader('Content-Type', 'text/html');
res.write(data);
res.end([data]);
res.statusCode = 200;
```

### 7.3 Request Properties

```javascript
req.url      // '/path'
req.method   // 'GET', 'POST'
req.headers  // { 'content-type': '...' }
```

### 7.4 Content Types

```javascript
'text/plain'
'text/html'
'text/css'
'text/javascript'
'application/json'
'image/png'
'image/jpeg'
```

---

## 8. Interview Questions

### Q1: How do you create an HTTP server in Node.js?
**Answer**:
```javascript
const http = require('http');
http.createServer((req, res) => {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Hello World');
}).listen(3000);
```

### Q2: What is the difference between res.write() and res.end()?
**Answer**:
- `res.write()`: Writes data to response body, can be called multiple times
- `res.end()`: Signals that all headers and body have been sent, must be called to finish response

### Q3: How do you set response headers?
**Answer**: Use `res.writeHead()` or `res.setHeader()`:
```javascript
res.writeHead(200, {'Content-Type': 'application/json'});
// or
res.setHeader('Content-Type', 'application/json');
res.statusCode = 200;
```

### Q4: How do you handle different routes in plain Node.js?
**Answer**: Check `req.url` and `req.method`:
```javascript
if (req.url === '/' && req.method === 'GET') {
    // Handle home route
}
```

### Q5: How do you serve HTML files?
**Answer**: Use fs.readFile to read HTML and set proper Content-Type:
```javascript
fs.readFile('page.html', (err, data) => {
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.end(data);
});
```

### Q6: What happens if you don't call res.end()?
**Answer**: The request will hang, the client will keep waiting for a response, and eventually timeout.

---

## Navigation

← Previous: [33_File_System_Operations.md](./33_File_System_Operations.md) | Next: [35_Events_and_EventEmitter.md](./35_Events_and_EventEmitter.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 07*
