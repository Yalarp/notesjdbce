# Express Middleware

## Table of Contents
1. [Introduction](#1-introduction)
2. [Types of Middleware](#2-types-of-middleware)
3. [Writing Custom Middleware](#3-writing-custom-middleware)
4. [Built-in Middleware](#4-built-in-middleware)
5. [Third-Party Middleware](#5-third-party-middleware)
6. [Error Handling Middleware](#6-error-handling-middleware)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 What is Middleware?
Middleware functions are functions that have access to the request object (req), response object (res), and the next middleware function in the request-response cycle (next).

### 1.2 Middleware Flow

```
Request → Middleware 1 → Middleware 2 → Route Handler → Response
                ↓              ↓
              next()         next()
```

### 1.3 What Middleware Can Do
- Execute any code
- Modify request and response objects
- End the request-response cycle
- Call the next middleware

---

## 2. Types of Middleware

### 2.1 Classification

| Type | Description |
|------|-------------|
| Application-level | Bound to app instance |
| Router-level | Bound to router instance |
| Error-handling | For error handling |
| Built-in | Express built-in |
| Third-party | External packages |

### 2.2 Application-Level Middleware

```javascript
const express = require('express');
const app = express();

// Executes for every request
app.use((req, res, next) => {
    console.log('Time:', Date.now());
    next();
});

// Executes for specific path
app.use('/api', (req, res, next) => {
    console.log('API request');
    next();
});

// Executes for specific method and path
app.get('/users', (req, res, next) => {
    console.log('Users requested');
    next();
}, (req, res) => {
    res.send('Users');
});
```

### 2.3 Router-Level Middleware

```javascript
const router = express.Router();

// Applies to all routes in router
router.use((req, res, next) => {
    console.log('Router middleware');
    next();
});

// Applies to specific path
router.use('/:id', (req, res, next) => {
    console.log('ID:', req.params.id);
    next();
});
```

---

## 3. Writing Custom Middleware

### 3.1 Basic Structure

```javascript
const myMiddleware = (req, res, next) => {
    // Do something
    console.log('Middleware executed');
    
    // Call next to continue
    next();
};

app.use(myMiddleware);
```

### 3.2 Logger Middleware

```javascript
const logger = (req, res, next) => {
    const timestamp = new Date().toISOString();
    console.log(`[${timestamp}] ${req.method} ${req.url}`);
    next();
};

app.use(logger);
```

### 3.3 Authentication Middleware

```javascript
const authenticate = (req, res, next) => {
    const token = req.headers.authorization;
    
    if (!token) {
        return res.status(401).json({ error: 'No token provided' });
    }
    
    // Validate token
    if (token === 'valid-token') {
        req.user = { id: 1, name: 'John' };
        next();
    } else {
        res.status(403).json({ error: 'Invalid token' });
    }
};

// Protect routes
app.get('/protected', authenticate, (req, res) => {
    res.json({ user: req.user });
});
```

### 3.4 Configurable Middleware

```javascript
const roleCheck = (roles) => {
    return (req, res, next) => {
        if (roles.includes(req.user.role)) {
            next();
        } else {
            res.status(403).json({ error: 'Forbidden' });
        }
    };
};

// Usage
app.get('/admin', authenticate, roleCheck(['admin']), (req, res) => {
    res.send('Admin area');
});
```

---

## 4. Built-in Middleware

### 4.1 express.json()

Parses incoming JSON payloads.

```javascript
app.use(express.json());

app.post('/api/users', (req, res) => {
    console.log(req.body);  // Parsed JSON object
    res.json(req.body);
});
```

### 4.2 express.urlencoded()

Parses URL-encoded bodies (form data).

```javascript
app.use(express.urlencoded({ extended: true }));

app.post('/submit', (req, res) => {
    console.log(req.body);  // { name: 'John', email: '...' }
    res.json(req.body);
});
```

### 4.3 express.static()

Serves static files.

```javascript
// Serve files from 'public' directory
app.use(express.static('public'));

// With virtual path
app.use('/static', express.static('public'));

// Multiple directories
app.use(express.static('public'));
app.use(express.static('files'));
```

---

## 5. Third-Party Middleware

### 5.1 Popular Middleware

| Package | Purpose |
|---------|---------|
| `morgan` | HTTP request logger |
| `cors` | Enable CORS |
| `helmet` | Security headers |
| `compression` | Response compression |
| `cookie-parser` | Parse cookies |

### 5.2 Morgan Logger

```bash
npm install morgan
```

```javascript
const morgan = require('morgan');

// Development logging
app.use(morgan('dev'));

// Production logging
app.use(morgan('combined'));
```

### 5.3 CORS

```bash
npm install cors
```

```javascript
const cors = require('cors');

// Enable all CORS
app.use(cors());

// Specific origins
app.use(cors({
    origin: ['http://localhost:3000', 'https://mysite.com'],
    methods: ['GET', 'POST', 'PUT', 'DELETE'],
    credentials: true
}));
```

### 5.4 Helmet (Security)

```bash
npm install helmet
```

```javascript
const helmet = require('helmet');

app.use(helmet());
```

---

## 6. Error Handling Middleware

### 6.1 Error Handler Structure

Error middleware has **four** parameters:

```javascript
const errorHandler = (err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({ error: 'Something went wrong!' });
};

// Must be last middleware
app.use(errorHandler);
```

### 6.2 Complete Error Handling

```javascript
// Custom error class
class AppError extends Error {
    constructor(message, statusCode) {
        super(message);
        this.statusCode = statusCode;
    }
}

// Route that throws error
app.get('/error', (req, res, next) => {
    next(new AppError('Not found', 404));
});

// 404 handler
app.use((req, res, next) => {
    next(new AppError('Route not found', 404));
});

// Error handler
app.use((err, req, res, next) => {
    const status = err.statusCode || 500;
    res.status(status).json({
        error: err.message,
        status: status
    });
});
```

### 6.3 Async Error Handling

```javascript
// Wrapper function
const asyncHandler = (fn) => (req, res, next) => {
    Promise.resolve(fn(req, res, next)).catch(next);
};

// Usage
app.get('/users', asyncHandler(async (req, res) => {
    const users = await User.findAll();
    res.json(users);
}));
```

---

## 7. Quick Reference

### 7.1 Middleware Types

```javascript
// Application-level
app.use(middleware);
app.use('/path', middleware);

// Router-level
router.use(middleware);

// Error-handling (4 args)
app.use((err, req, res, next) => {});
```

### 7.2 Built-in Middleware

```javascript
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(express.static('public'));
```

### 7.3 Common Pattern

```javascript
// Middleware order matters
app.use(logger);
app.use(cors());
app.use(helmet());
app.use(express.json());

// Routes
app.use('/api', routes);

// Error handler (last)
app.use(errorHandler);
```

---

## 8. Interview Questions

### Q1: What is middleware in Express?
**Answer**: Middleware functions are functions that have access to req, res, and next. They can execute code, modify req/res, end the cycle, or call the next middleware.

### Q2: What is the difference between app.use() and app.get()?
**Answer**:
- `app.use()`: Matches all HTTP methods, prefix matching
- `app.get()`: Only matches GET requests, exact path matching

### Q3: What happens if you don't call next()?
**Answer**: The request-response cycle is halted and the request hangs unless you send a response. The next middleware or route handler won't execute.

### Q4: What's special about error-handling middleware?
**Answer**: Error-handling middleware has **four** parameters: `(err, req, res, next)`. It must be defined after all other middleware and routes.

### Q5: How do you pass data between middleware?
**Answer**: Attach data to the `req` object:
```javascript
req.customData = 'value';
```

### Q6: What is the order of middleware execution?
**Answer**: Middleware executes in the order they are defined using `app.use()`. First defined, first executed.

---

## Navigation

← Previous: [37_Express_Routing.md](./37_Express_Routing.md) | Next: [39_REST_API_Development.md](./39_REST_API_Development.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 08*
