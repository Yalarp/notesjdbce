# REST API Development with Express

## Table of Contents
1. [Introduction](#1-introduction)
2. [REST Principles](#2-rest-principles)
3. [Building REST API](#3-building-rest-api)
4. [CRUD Operations](#4-crud-operations)
5. [Request Validation](#5-request-validation)
6. [API Response Format](#6-api-response-format)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 What is REST?
**REST** (Representational State Transfer) is an architectural style for designing networked applications. It uses HTTP requests to perform CRUD operations.

### 1.2 RESTful API
A RESTful API is an API that conforms to REST architectural constraints:
- Stateless
- Client-Server architecture
- Cacheable
- Uniform interface
- Layered system

---

## 2. REST Principles

### 2.1 HTTP Methods (CRUD)

| Method | Operation | Description |
|--------|-----------|-------------|
| GET | Read | Retrieve resource(s) |
| POST | Create | Create new resource |
| PUT | Update | Replace entire resource |
| PATCH | Update | Partial update |
| DELETE | Delete | Remove resource |

### 2.2 Status Codes

| Code | Category | Common Usage |
|------|----------|--------------|
| 200 | Success | OK |
| 201 | Success | Created |
| 204 | Success | No Content |
| 400 | Client Error | Bad Request |
| 401 | Client Error | Unauthorized |
| 403 | Client Error | Forbidden |
| 404 | Client Error | Not Found |
| 500 | Server Error | Internal Error |

### 2.3 URL Design

| Resource | Endpoint | Method |
|----------|----------|--------|
| All users | `/api/users` | GET |
| Single user | `/api/users/:id` | GET |
| Create user | `/api/users` | POST |
| Update user | `/api/users/:id` | PUT |
| Delete user | `/api/users/:id` | DELETE |

---

## 3. Building REST API

### 3.1 Project Setup

```bash
mkdir rest-api
cd rest-api
npm init -y
npm install express
```

### 3.2 Basic Structure

```javascript
const express = require('express');
const app = express();

// Middleware
app.use(express.json());

// In-memory data store
let users = [
    { id: 1, name: 'John', email: 'john@example.com' },
    { id: 2, name: 'Jane', email: 'jane@example.com' }
];

// Routes will go here

const PORT = 3000;
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

### 3.3 Complete API Example

```javascript
const express = require('express');
const app = express();

app.use(express.json());

let users = [
    { id: 1, name: 'John', email: 'john@example.com' },
    { id: 2, name: 'Jane', email: 'jane@example.com' }
];
let nextId = 3;

// GET all users
app.get('/api/users', (req, res) => {
    res.json(users);
});

// GET single user
app.get('/api/users/:id', (req, res) => {
    const user = users.find(u => u.id === parseInt(req.params.id));
    if (!user) {
        return res.status(404).json({ error: 'User not found' });
    }
    res.json(user);
});

// POST create user
app.post('/api/users', (req, res) => {
    const { name, email } = req.body;
    
    if (!name || !email) {
        return res.status(400).json({ error: 'Name and email required' });
    }
    
    const user = { id: nextId++, name, email };
    users.push(user);
    res.status(201).json(user);
});

// PUT update user
app.put('/api/users/:id', (req, res) => {
    const user = users.find(u => u.id === parseInt(req.params.id));
    if (!user) {
        return res.status(404).json({ error: 'User not found' });
    }
    
    const { name, email } = req.body;
    user.name = name || user.name;
    user.email = email || user.email;
    
    res.json(user);
});

// DELETE user
app.delete('/api/users/:id', (req, res) => {
    const index = users.findIndex(u => u.id === parseInt(req.params.id));
    if (index === -1) {
        return res.status(404).json({ error: 'User not found' });
    }
    
    users.splice(index, 1);
    res.status(204).send();
});

app.listen(3000);
```

---

## 4. CRUD Operations

### 4.1 Create (POST)

```javascript
app.post('/api/users', (req, res) => {
    const { name, email } = req.body;
    
    // Validation
    if (!name || !email) {
        return res.status(400).json({
            success: false,
            error: 'Name and email are required'
        });
    }
    
    // Create
    const newUser = {
        id: Date.now(),
        name,
        email,
        createdAt: new Date()
    };
    
    users.push(newUser);
    
    res.status(201).json({
        success: true,
        data: newUser
    });
});
```

### 4.2 Read (GET)

```javascript
// Get all with query filtering
app.get('/api/users', (req, res) => {
    let result = users;
    
    // Filter by name
    if (req.query.name) {
        result = result.filter(u => 
            u.name.toLowerCase().includes(req.query.name.toLowerCase())
        );
    }
    
    // Pagination
    const page = parseInt(req.query.page) || 1;
    const limit = parseInt(req.query.limit) || 10;
    const start = (page - 1) * limit;
    const end = start + limit;
    
    res.json({
        success: true,
        count: result.length,
        data: result.slice(start, end)
    });
});

// Get single
app.get('/api/users/:id', (req, res) => {
    const user = users.find(u => u.id === parseInt(req.params.id));
    
    if (!user) {
        return res.status(404).json({
            success: false,
            error: 'User not found'
        });
    }
    
    res.json({
        success: true,
        data: user
    });
});
```

### 4.3 Update (PUT/PATCH)

```javascript
// Full update (PUT)
app.put('/api/users/:id', (req, res) => {
    const index = users.findIndex(u => u.id === parseInt(req.params.id));
    
    if (index === -1) {
        return res.status(404).json({ error: 'User not found' });
    }
    
    // Replace entire object
    users[index] = {
        id: parseInt(req.params.id),
        ...req.body,
        updatedAt: new Date()
    };
    
    res.json({ success: true, data: users[index] });
});

// Partial update (PATCH)
app.patch('/api/users/:id', (req, res) => {
    const user = users.find(u => u.id === parseInt(req.params.id));
    
    if (!user) {
        return res.status(404).json({ error: 'User not found' });
    }
    
    // Update only provided fields
    Object.keys(req.body).forEach(key => {
        if (key !== 'id') {
            user[key] = req.body[key];
        }
    });
    
    user.updatedAt = new Date();
    res.json({ success: true, data: user });
});
```

### 4.4 Delete (DELETE)

```javascript
app.delete('/api/users/:id', (req, res) => {
    const index = users.findIndex(u => u.id === parseInt(req.params.id));
    
    if (index === -1) {
        return res.status(404).json({ error: 'User not found' });
    }
    
    const deleted = users.splice(index, 1);
    
    res.json({
        success: true,
        message: 'User deleted',
        data: deleted[0]
    });
    
    // OR return no content
    // res.status(204).send();
});
```

---

## 5. Request Validation

### 5.1 Basic Validation

```javascript
app.post('/api/users', (req, res) => {
    const { name, email, age } = req.body;
    const errors = [];
    
    if (!name || name.length < 2) {
        errors.push('Name must be at least 2 characters');
    }
    
    if (!email || !email.includes('@')) {
        errors.push('Valid email is required');
    }
    
    if (age && (typeof age !== 'number' || age < 0)) {
        errors.push('Age must be a positive number');
    }
    
    if (errors.length > 0) {
        return res.status(400).json({ errors });
    }
    
    // Proceed with creation
});
```

### 5.2 Validation Middleware

```javascript
const validateUser = (req, res, next) => {
    const { name, email } = req.body;
    
    if (!name) {
        return res.status(400).json({ error: 'Name is required' });
    }
    
    if (!email) {
        return res.status(400).json({ error: 'Email is required' });
    }
    
    next();
};

app.post('/api/users', validateUser, (req, res) => {
    // Handler code
});
```

---

## 6. API Response Format

### 6.1 Standard Response Structure

```javascript
// Success response
{
    "success": true,
    "data": { ... },
    "message": "Operation successful"
}

// Error response
{
    "success": false,
    "error": "Error message",
    "details": [ ... ]
}

// List response
{
    "success": true,
    "count": 10,
    "total": 100,
    "page": 1,
    "data": [ ... ]
}
```

### 6.2 Response Helper

```javascript
const sendResponse = (res, statusCode, data, message) => {
    res.status(statusCode).json({
        success: statusCode < 400,
        data,
        message
    });
};

const sendError = (res, statusCode, error) => {
    res.status(statusCode).json({
        success: false,
        error
    });
};

// Usage
app.get('/api/users/:id', (req, res) => {
    const user = users.find(u => u.id === parseInt(req.params.id));
    
    if (!user) {
        return sendError(res, 404, 'User not found');
    }
    
    sendResponse(res, 200, user, 'User retrieved');
});
```

---

## 7. Quick Reference

### 7.1 CRUD Routes

```javascript
app.get('/api/items', getAll);
app.get('/api/items/:id', getOne);
app.post('/api/items', create);
app.put('/api/items/:id', updateFull);
app.patch('/api/items/:id', updatePartial);
app.delete('/api/items/:id', remove);
```

### 7.2 Status Codes

```javascript
res.status(200).json(data);   // OK
res.status(201).json(data);   // Created
res.status(204).send();       // No Content
res.status(400).json(error);  // Bad Request
res.status(404).json(error);  // Not Found
res.status(500).json(error);  // Server Error
```

### 7.3 Request Data

```javascript
req.params.id    // URL parameters
req.query.name   // Query strings
req.body         // Request body (JSON)
req.headers      // Request headers
```

---

## 8. Interview Questions

### Q1: What is REST?
**Answer**: REST (Representational State Transfer) is an architectural style for designing APIs. It uses standard HTTP methods (GET, POST, PUT, DELETE) and is stateless, meaning each request contains all necessary information.

### Q2: What is the difference between PUT and PATCH?
**Answer**:
- **PUT**: Replaces the entire resource
- **PATCH**: Updates only specific fields

### Q3: What status code should you return after creating a resource?
**Answer**: 201 (Created), optionally with the created resource in the response body.

### Q4: How do you handle errors in a REST API?
**Answer**: Return appropriate HTTP status codes (4xx for client errors, 5xx for server errors) with a JSON error message describing the issue.

### Q5: What is the purpose of the 204 status code?
**Answer**: 204 (No Content) indicates success but with no response body. Commonly used for DELETE operations.

### Q6: How should you design REST API URLs?
**Answer**: Use nouns for resources (not verbs), use plural forms, nest resources for relationships, and use HTTP methods for actions.

---

## Navigation

← Previous: [38_Express_Middleware.md](./38_Express_Middleware.md) | Next: [40_MongoDB_Integration.md](./40_MongoDB_Integration.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 08*
