# Express Routing

## Table of Contents
1. [Introduction](#1-introduction)
2. [Route Methods](#2-route-methods)
3. [Route Parameters](#3-route-parameters)
4. [Route Handlers](#4-route-handlers)
5. [Router Module](#5-router-module)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 What is Routing?
Routing refers to how an application's endpoints (URIs) respond to client requests. Each route can have one or more handler functions.

### 1.2 Route Definition Structure

```javascript
app.METHOD(PATH, HANDLER)
```

| Part | Description |
|------|-------------|
| `app` | Express instance |
| `METHOD` | HTTP method (get, post, put, delete) |
| `PATH` | URL path |
| `HANDLER` | Function executed when route matches |

---

## 2. Route Methods

### 2.1 Basic HTTP Methods

```javascript
const express = require('express');
const app = express();

// GET - Retrieve data
app.get('/users', (req, res) => {
    res.json([{ id: 1, name: 'John' }]);
});

// POST - Create data
app.post('/users', (req, res) => {
    res.status(201).json({ message: 'User created' });
});

// PUT - Update data (full)
app.put('/users/:id', (req, res) => {
    res.json({ message: `User ${req.params.id} updated` });
});

// PATCH - Update data (partial)
app.patch('/users/:id', (req, res) => {
    res.json({ message: `User ${req.params.id} patched` });
});

// DELETE - Remove data
app.delete('/users/:id', (req, res) => {
    res.json({ message: `User ${req.params.id} deleted` });
});
```

### 2.2 Special Methods

```javascript
// Handle ALL HTTP methods
app.all('/api/*', (req, res, next) => {
    console.log('API request received');
    next();
});

// Route for multiple methods
app.route('/book')
    .get((req, res) => res.send('Get book'))
    .post((req, res) => res.send('Add book'))
    .put((req, res) => res.send('Update book'));
```

---

## 3. Route Parameters

### 3.1 URL Parameters

```javascript
// Single parameter
app.get('/users/:id', (req, res) => {
    res.send(`User ID: ${req.params.id}`);
});

// Multiple parameters
app.get('/users/:userId/posts/:postId', (req, res) => {
    res.json({
        userId: req.params.userId,
        postId: req.params.postId
    });
});
```

### 3.2 Query Strings

```javascript
// URL: /search?q=node&limit=10
app.get('/search', (req, res) => {
    const { q, limit } = req.query;
    res.json({ query: q, limit: limit || 10 });
});
```

### 3.3 Optional Parameters

```javascript
// Optional parameter with ?
app.get('/users/:id/:name?', (req, res) => {
    res.json({
        id: req.params.id,
        name: req.params.name || 'Anonymous'
    });
});
```

### 3.4 Regular Expression Routes

```javascript
// Match routes ending in 'fly'
app.get(/.*fly$/, (req, res) => {
    res.send('Matched butterfly, dragonfly, etc.');
});

// Parameter with constraints
app.get('/users/:id([0-9]+)', (req, res) => {
    res.send(`User ID (numeric only): ${req.params.id}`);
});
```

---

## 4. Route Handlers

### 4.1 Single Handler

```javascript
app.get('/example', (req, res) => {
    res.send('Single handler');
});
```

### 4.2 Multiple Handlers

```javascript
// Multiple callbacks
app.get('/example', 
    (req, res, next) => {
        console.log('First handler');
        next();
    },
    (req, res) => {
        res.send('Second handler');
    }
);
```

### 4.3 Array of Handlers

```javascript
const handler1 = (req, res, next) => {
    console.log('Handler 1');
    next();
};

const handler2 = (req, res, next) => {
    console.log('Handler 2');
    next();
};

const handler3 = (req, res) => {
    res.send('Done');
};

app.get('/example', [handler1, handler2, handler3]);
```

### 4.4 Mixed Handlers

```javascript
const middleware = (req, res, next) => {
    console.log('Middleware');
    next();
};

app.get('/example', middleware, (req, res, next) => {
    console.log('First');
    next();
}, (req, res) => {
    res.send('Done');
});
```

---

## 5. Router Module

### 5.1 Creating a Router

```javascript
// routes/users.js
const express = require('express');
const router = express.Router();

// GET /users
router.get('/', (req, res) => {
    res.json([{ id: 1, name: 'John' }]);
});

// GET /users/:id
router.get('/:id', (req, res) => {
    res.json({ id: req.params.id });
});

// POST /users
router.post('/', (req, res) => {
    res.status(201).json({ message: 'Created' });
});

module.exports = router;
```

### 5.2 Using the Router

```javascript
// app.js
const express = require('express');
const app = express();
const userRouter = require('./routes/users');

// Mount router at /users
app.use('/users', userRouter);

// Now routes are:
// GET /users
// GET /users/:id
// POST /users

app.listen(3000);
```

### 5.3 Multiple Routers

```javascript
// app.js
const express = require('express');
const app = express();

const userRouter = require('./routes/users');
const productRouter = require('./routes/products');
const orderRouter = require('./routes/orders');

app.use('/api/users', userRouter);
app.use('/api/products', productRouter);
app.use('/api/orders', orderRouter);

app.listen(3000);
```

### 5.4 Router Middleware

```javascript
const express = require('express');
const router = express.Router();

// Middleware for all routes in this router
router.use((req, res, next) => {
    console.log('Time:', Date.now());
    next();
});

// Middleware for specific route
router.use('/:id', (req, res, next) => {
    console.log('Request ID:', req.params.id);
    next();
});

router.get('/', (req, res) => res.send('Home'));
router.get('/:id', (req, res) => res.send(`ID: ${req.params.id}`));

module.exports = router;
```

---

## 6. Quick Reference

### 6.1 Route Definition

```javascript
app.get('/path', handler);
app.post('/path', handler);
app.put('/path', handler);
app.delete('/path', handler);
app.all('/path', handler);
```

### 6.2 Route Parameters

```javascript
// URL params
app.get('/users/:id', handler);
req.params.id

// Query strings
// GET /search?q=node
req.query.q
```

### 6.3 Router Usage

```javascript
// Create router
const router = express.Router();

// Define routes on router
router.get('/', handler);
router.post('/', handler);

// Mount router
app.use('/prefix', router);
```

### 6.4 Route Chaining

```javascript
app.route('/book')
    .get(handler)
    .post(handler)
    .put(handler)
    .delete(handler);
```

---

## 7. Interview Questions

### Q1: What is routing in Express?
**Answer**: Routing refers to determining how an application responds to a client request at a particular endpoint (URI) and HTTP method. Each route can have one or more handler functions.

### Q2: What is the difference between req.params and req.query?
**Answer**:
- `req.params`: Route parameters (URL path segments) `/users/:id`
- `req.query`: Query string parameters `?name=value`

### Q3: What is express.Router()?
**Answer**: `express.Router()` creates a modular, mountable route handler. It's like a mini Express application that can have its own middleware and routes.

### Q4: How do you handle multiple handlers for a route?
**Answer**: Chain handlers with `next()`:
```javascript
app.get('/path', handler1, handler2, finalHandler);
```

### Q5: What does next() do in route handlers?
**Answer**: `next()` passes control to the next middleware or route handler in the chain. Without it, the request-response cycle is not completed.

### Q6: How do you define an optional route parameter?
**Answer**: Use `?` after the parameter name:
```javascript
app.get('/users/:id/:name?', handler);
```

---

## Navigation

← Previous: [36_Express_Introduction.md](./36_Express_Introduction.md) | Next: [38_Express_Middleware.md](./38_Express_Middleware.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 08*
