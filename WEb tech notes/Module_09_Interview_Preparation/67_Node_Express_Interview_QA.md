# Node.js & Express Interview Questions

## Table of Contents
1. [Node.js Fundamentals](#1-nodejs-fundamentals)
2. [Asynchronous Programming](#2-asynchronous-programming)
3. [Modules & Globals](#3-modules--globals)
4. [Streams & Buffers](#4-streams--buffers)
5. [Express.js](#5-expressjs)
6. [Angular Support (Legacy)](#6-angular-support-legacy)

---

## 1. Node.js Fundamentals

### Q1: What is Node.js?
**Answer**: Node.js is a JavaScript runtime built on Google Chrome’s V8 JavaScript engine. It allows executing JavaScript code on the server-side. It creates a single thread for event looping and uses non-blocking I/O to handle concurrent requests efficiently.

### Q2: Key features of Node.js?
**Answer**:
1.  **Asynchronous & Event Driven**: All APIs are non-blocking.
2.  **Fast**: Uses V8 Engine.
3.  **Single Threaded but Scalable**: Uses Event Loop.
4.  **No Buffering**: Outputs data in chunks.
5.  **Cross-Platform**.

### Q3: When to use Node.js?
**Answer**:
-   I/O bound applications.
-   Data Streaming (Netflix).
-   Real-time Chat/Games.
-   JSON APIs.
-   Single Page Applications (SPAs).
*Not suitable for CPU-intensive tasks.*

### Q4: How does Node.js work?
**Answer**: It uses a **Single Threaded Event Loop**.
1.  Receives request.
2.  Registers a callback.
3.  Delegates blocking operation to background workers (libuv).
4.  Moves to next request immediately (Non-Blocking).
5.  When operation completes, Event Loop triggers the callback.

### Q5: What is REPL?
**Answer**: **R**ead **E**val **P**rint **L**oop. A console environment to run JS commands.
-   Read input -> Evaluate -> Print result -> Loop.

### Q6: What are Globals?
**Answer**: Objects available in all modules.
-   `global` (like window in browser).
-   `process` (info about current process).
-   `__dirname`, `__filename`.
-   `Buffer`.

---

## 2. Asynchronous Programming

### Q7: What is a Callback?
**Answer**: A function passed as an argument to another function, to be executed continuously or after a task is completed. Node.js uses callbacks heavily for async operations.

### Q8: What is Callback Hell?
**Answer**: Heavily nested callbacks which make code unreadable and hard to maintain.
**Solution**:
1.  Modularize code.
2.  Use **Promises**.
3.  Use **Async/Await**.
4.  Use Generators.

### Q9: `process.nextTick()` vs `setImmediate()`?
**Answer**:
-   `nextTick` fires immediately after the current operation, before the Event Loop continues.
-   `setImmediate` fires in the check phase of the next Event Loop iteration.

---

## 3. Modules & Globals

### Q10: What is NPM?
**Answer**: Node Package Manager.
1.  Online repository of packages.
2.  CLI tool for version/dependency management.

### Q11: Local vs Global Installation?
**Answer**:
-   **Local** (`npm i pkg`): Installed in `node_modules` of current project. Required via `require()`.
-   **Global** (`npm i -g pkg`): Installed in system directory. Used as CLI tools (e.g., `nodemon`).

### Q12: What is `package.json`?
**Answer**: A JSON file containing metadata about the project (dependencies, scripts, version, author). Required for any Node module.

### Q13: `module.exports` vs `exports`?
**Answer**: `exports` is a helper reference to `module.exports`. `module.exports` is the actual object that gets returned by `require()`.

---

## 4. Streams & Buffers

### Q14: What are Streams? Types?
**Answer**: Objects that let you read/write data continuously.
1.  **Readable**: `fs.createReadStream`.
2.  **Writable**: `fs.createWriteStream`.
3.  **Duplex**: Both (Sockets).
4.  **Transform**: Modify data (zlib).

### Q15: What is a Buffer?
**Answer**: A generic container for raw binary data. Stored outside V8 heap. Used for TCP streams and file system operations.

### Q16: What is a Pipe?
**Answer**: Mechanism to connect output of one stream to input of another.
`readStream.pipe(writeStream);`

---

## 5. Express.js

### Q17: How to create a simple Server?
**Answer**:
```javascript
var http = require('http');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello World');
}).listen(8080);
```

### Q18: Difference between Node, AJAX, jQuery?
**Answer**:
-   **Node.js**: Server-side runtime.
-   **AJAX**: Client-side technique for async data fetching.
-   **jQuery**: Client-side library for DOM/AJAX.

### Q19: Handling POST data?
**Answer**: Use middleware like `body-parser` (or `express.json()`).
```javascript
app.post('/', function(req, res){
   console.log(req.body);
});
```

---

## 6. Angular Support (Legacy)

### Q20: Custom Directives in AngularJS (Context)?
**Answer**: *From Interview Doc*
-   Directives are markers on DOM elements.
-   Types: Element (E), Attribute (A), Class (C), Comment (M).
-   Created using `app.directive()`.

---

## Navigation

← Previous: [66_JavaScript_Interview_QA.md](./66_JavaScript_Interview_QA.md) | Next: [68_React_Interview_QA.md](./68_React_Interview_QA.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Notes_CCEE_InterviewQA_Web*
