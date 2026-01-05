# Node.js Introduction

## Table of Contents
1. [Introduction](#1-introduction)
2. [Key Features](#2-key-features)
3. [How Node.js Works](#3-how-nodejs-works)
4. [When to Use Node.js](#4-when-to-use-nodejs)
5. [REPL Environment](#5-repl-environment)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 What is Node.js?
**Node.js** is a JavaScript runtime built on Google Chrome's V8 JavaScript engine. It allows executing JavaScript code on any machine outside a browser (server-side JavaScript).

### 1.2 Key Characteristics
- **Single-threaded**: Uses one thread with event loop
- **Non-blocking I/O**: Asynchronous processing
- **Cross-platform**: Runs on Windows, Linux, macOS
- **Open-source**: Free and community-driven
- **Fast**: Built on V8 engine

### 1.3 Use Cases
| Ideal For | Not Ideal For |
|-----------|---------------|
| I/O bound applications | CPU-intensive operations |
| Real-time applications | Heavy computation |
| Data streaming | Long processing tasks |
| JSON APIs | |
| Chat applications | |
| Single Page Applications | |

---

## 2. Key Features

### 2.1 Asynchronous Event-Driven I/O
- All APIs are asynchronous
- Node receives request → executes in background → continues processing other requests
- Doesn't wait for response from previous requests

### 2.2 Fast Code Execution
- Uses V8 JavaScript Runtime engine (same as Google Chrome)
- Wrapper over JS engine makes runtime faster

### 2.3 Single Threaded but Highly Scalable
- Uses single thread model for event looping
- Traditional servers create limited threads
- Node.js creates one thread serving many more requests

### 2.4 No Buffering
- Applications never buffer data
- Output data in chunks

### 2.5 Active Community
- Large NPM ecosystem
- Regular updates
- Extensive documentation

---

## 3. How Node.js Works

### 3.1 Event Loop Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      Node.js Application                      │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│    Request 1 ─────┐                                          │
│    Request 2 ─────┼───→ [Event Queue] → [Event Loop]        │
│    Request 3 ─────┘           ↓                              │
│                               ↓                              │
│                        ┌──────────────┐                      │
│                        │ Single Thread│                      │
│                        └──────┬───────┘                      │
│                               │                              │
│                    ┌──────────┴──────────┐                   │
│                    ↓                     ↓                   │
│              [Non-blocking]         [Blocking]               │
│              Execute & Return       Background Workers       │
│                                    (Thread Pool)             │
│                                          ↓                   │
│                                    Callback                  │
└─────────────────────────────────────────────────────────────┘
```

### 3.2 The Delivery Boy Analogy
Imagine a delivery boy:
1. Goes to each house to deliver packets
2. If house is not open, doesn't wait
3. Calls owner: "Call me when you're home"
4. Continues delivering to other houses
5. Returns when called back

**Node.js works the same way:**
- Doesn't wait for I/O operations to complete
- Attaches callback function
- Continues processing other requests
- Callback executes when operation completes

### 3.3 Callback Function Flow

```javascript
// Request comes in
app.get('/data', function(req, res) {
    // Node.js doesn't wait for database
    database.query('SELECT * FROM users', function(err, result) {
        // This callback runs when data is ready
        res.send(result);
    });
    // Continues to handle other requests immediately
});
```

---

## 4. When to Use Node.js

### 4.1 Perfect For

| Use Case | Why |
|----------|-----|
| Chat applications | Real-time, event-driven |
| Game servers | High concurrency |
| Collaborative tools | Event loop for changes |
| Advertisement servers | Handle thousands of requests |
| Streaming servers | Multimedia streaming |
| REST APIs | JSON handling |

### 4.2 Not Suitable For

| Avoid When | Reason |
|------------|--------|
| Heavy CPU computation | Blocks the event loop |
| Complex calculations | Single thread limitation |
| Image/video processing | CPU intensive |

---

## 5. REPL Environment

### 5.1 What is REPL?
**REPL** = Read Eval Print Loop

A simple program that:
1. **Read**: Reads user input, parses into JavaScript
2. **Eval**: Executes the data structure
3. **Print**: Prints the result
4. **Loop**: Repeats until Ctrl+C twice

### 5.2 Starting REPL

```bash
$ node
> 
```

### 5.3 REPL Commands

| Command | Description |
|---------|-------------|
| `.help` | Display help |
| `Tab` | List available commands |
| `Up/Down` | Previous commands |
| `.save filename` | Save session to file |
| `.load filename` | Load file into session |
| `Ctrl + C` | Terminate current command |
| `Ctrl + C (twice)` | Exit REPL |
| `Ctrl + D` | Exit REPL |
| `.break` | Exit multiline expression |
| `.clear` | Clear context |

### 5.4 REPL Examples

```javascript
> 1 + 2
3
> var x = 10
undefined
> x * 5
50
> console.log("Hello")
Hello
undefined
```

---

## 6. Quick Reference

### 6.1 Node.js Architecture

```
JavaScript Code
      ↓
   V8 Engine (C++)
      ↓
   libuv (C)
      ↓
Operating System
```

### 6.2 Key Concepts

| Concept | Description |
|---------|-------------|
| Event Loop | Handles async operations |
| Callback | Function executed on completion |
| Non-blocking | Doesn't wait for I/O |
| Single Thread | One thread for all requests |
| V8 Engine | JavaScript execution engine |

### 6.3 Node.js vs Browser JavaScript

| Feature | Browser | Node.js |
|---------|---------|---------|
| DOM | ✓ | ✗ |
| Window | ✓ | ✗ |
| File System | ✗ | ✓ |
| HTTP Server | ✗ | ✓ |
| Global object | window | global |

---

## 7. Interview Questions

### Q1: What is Node.js?
**Answer**: Node.js is a JavaScript runtime built on Chrome's V8 engine that allows executing JavaScript on the server-side. It's single-threaded, uses non-blocking I/O, and is event-driven.

### Q2: Why is Node.js single-threaded?
**Answer**: Node.js was designed as an experiment for async processing. It achieves better performance and scalability by doing async processing on a single thread under typical web loads.

### Q3: What is the event loop?
**Answer**: The event loop is a mechanism that handles and processes external events, converting them to callback invocations. It allows Node.js to perform non-blocking I/O operations.

### Q4: Can you access DOM in Node.js?
**Answer**: No, DOM is a browser API. Node.js runs on the server and doesn't have access to browser APIs like DOM, window, or document.

### Q5: What is a callback in Node.js?
**Answer**: A callback is a function passed as an argument to another function, which gets executed when an asynchronous operation completes. It's the foundation of Node.js's non-blocking architecture.

### Q6: When should you NOT use Node.js?
**Answer**: Don't use Node.js for CPU-intensive applications like heavy computation, image processing, or video encoding. These block the event loop and prevent handling other requests.

---

## Navigation

← Previous: [29_AJAX_XMLHttpRequest.md](../Module_03_ES6_and_Async_Programming/29_AJAX_XMLHttpRequest.md) | Next: [31_NPM_and_Package_Management.md](./31_NPM_and_Package_Management.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 07*
