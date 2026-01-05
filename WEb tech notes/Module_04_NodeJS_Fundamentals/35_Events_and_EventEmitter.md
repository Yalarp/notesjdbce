# Events and EventEmitter in Node.js

## Table of Contents
1. [Introduction](#1-introduction)
2. [EventEmitter Class](#2-eventemitter-class)
3. [Creating Events](#3-creating-events)
4. [Event Methods](#4-event-methods)
5. [Practical Examples](#5-practical-examples)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 Event-Driven Architecture
Node.js is built around an event-driven architecture where certain objects emit events that can be listened to by callback functions.

### 1.2 The events Module
```javascript
const events = require('events');
```

### 1.3 Key Concepts

| Concept | Description |
|---------|-------------|
| Event | Something that happens |
| Emitter | Object that emits events |
| Listener | Function that responds to events |
| Handler | Same as listener |

---

## 2. EventEmitter Class

### 2.1 Creating an EventEmitter

```javascript
const events = require('events');

// Create an eventEmitter object
const eventEmitter = new events.EventEmitter();
```

### 2.2 Basic Usage

```javascript
const EventEmitter = require('events');
const emitter = new EventEmitter();

// Register listener
emitter.on('greet', () => {
    console.log('Hello, world!');
});

// Emit event
emitter.emit('greet');  // Output: Hello, world!
```

### 2.3 Passing Data with Events

```javascript
const EventEmitter = require('events');
const emitter = new EventEmitter();

// Listener with arguments
emitter.on('userCreated', (user) => {
    console.log('User created:', user.name);
});

// Emit with data
emitter.emit('userCreated', { name: 'John', email: 'john@example.com' });
// Output: User created: John
```

---

## 3. Creating Events

### 3.1 Register Event Listener

```javascript
const EventEmitter = require('events');
const emitter = new EventEmitter();

// Method 1: on()
emitter.on('event', () => {
    console.log('Event fired!');
});

// Method 2: addListener() (same as on)
emitter.addListener('event', () => {
    console.log('Event fired!');
});

// Method 3: once() - fires only once
emitter.once('singleEvent', () => {
    console.log('This only runs once!');
});
```

### 3.2 Multiple Listeners

```javascript
emitter.on('message', (msg) => {
    console.log('Listener 1:', msg);
});

emitter.on('message', (msg) => {
    console.log('Listener 2:', msg);
});

emitter.emit('message', 'Hello');
// Output:
// Listener 1: Hello
// Listener 2: Hello
```

### 3.3 Built-in Events

```javascript
const emitter = new EventEmitter();

// Fired when new listener is added
emitter.on('newListener', (event) => {
    console.log('New listener added for:', event);
});

// Fired when listener is removed
emitter.on('removeListener', (event) => {
    console.log('Listener removed for:', event);
});
```

---

## 4. Event Methods

### 4.1 Core Methods

| Method | Description |
|--------|-------------|
| `on(event, listener)` | Register listener |
| `once(event, listener)` | One-time listener |
| `emit(event, [args])` | Trigger event |
| `removeListener(event, listener)` | Remove specific listener |
| `removeAllListeners([event])` | Remove all listeners |
| `listeners(event)` | Get all listeners |
| `listenerCount(event)` | Count listeners |

### 4.2 Examples

```javascript
const EventEmitter = require('events');
const emitter = new EventEmitter();

// Define listener function
function onMessage(msg) {
    console.log('Message:', msg);
}

// Add listener
emitter.on('message', onMessage);

// Check listener count
console.log(emitter.listenerCount('message'));  // 1

// Get listeners
console.log(emitter.listeners('message'));  // [function onMessage]

// Remove listener
emitter.removeListener('message', onMessage);

// Remove all listeners for an event
emitter.removeAllListeners('message');
```

### 4.3 Error Handling

```javascript
const emitter = new EventEmitter();

// Always handle error events
emitter.on('error', (err) => {
    console.error('An error occurred:', err);
});

// Emit error
emitter.emit('error', new Error('Something went wrong'));
```

**Important**: If no listener is registered for 'error' event, Node.js will throw the error and crash.

---

## 5. Practical Examples

### 5.1 Custom Class with EventEmitter

```javascript
const EventEmitter = require('events');

class Logger extends EventEmitter {
    log(message) {
        console.log(message);
        this.emit('logged', { message, timestamp: new Date() });
    }
}

const logger = new Logger();

logger.on('logged', (data) => {
    console.log('Log saved:', data);
});

logger.log('Hello World');
// Output:
// Hello World
// Log saved: { message: 'Hello World', timestamp: ... }
```

### 5.2 Order Processing System

```javascript
const EventEmitter = require('events');

class OrderSystem extends EventEmitter {
    placeOrder(order) {
        console.log('Processing order:', order.id);
        
        // Simulate processing
        setTimeout(() => {
            this.emit('orderPlaced', order);
        }, 1000);
    }
}

const orderSystem = new OrderSystem();

// Email service listener
orderSystem.on('orderPlaced', (order) => {
    console.log('Email sent for order:', order.id);
});

// Inventory listener
orderSystem.on('orderPlaced', (order) => {
    console.log('Inventory updated for:', order.id);
});

orderSystem.placeOrder({ id: 123, item: 'Book' });
```

### 5.3 HTTP Server Events

```javascript
const http = require('http');

const server = http.createServer();

server.on('request', (req, res) => {
    console.log('Request received:', req.url);
    res.end('Hello');
});

server.on('listening', () => {
    console.log('Server is listening');
});

server.on('close', () => {
    console.log('Server closed');
});

server.listen(3000);
```

---

## 6. Quick Reference

### 6.1 Creating Events

```javascript
const EventEmitter = require('events');
const emitter = new EventEmitter();

// Register
emitter.on('event', callback);
emitter.once('event', callback);

// Emit
emitter.emit('event', data);
```

### 6.2 Managing Listeners

```javascript
// Add
emitter.on('event', listener);
emitter.addListener('event', listener);

// Remove
emitter.removeListener('event', listener);
emitter.off('event', listener);
emitter.removeAllListeners('event');

// Info
emitter.listenerCount('event');
emitter.listeners('event');
```

### 6.3 Extending EventEmitter

```javascript
class MyEmitter extends EventEmitter {
    doSomething() {
        this.emit('done', 'result');
    }
}
```

---

## 7. Interview Questions

### Q1: What is EventEmitter in Node.js?
**Answer**: EventEmitter is a class in the events module that allows objects to emit events and attach listener functions to those events. It's the foundation of Node.js's event-driven architecture.

### Q2: What is the difference between on() and once()?
**Answer**:
- `on()`: Registers a listener that fires every time the event is emitted
- `once()`: Registers a listener that fires only the first time, then automatically removed

### Q3: What happens if an error event is emitted without a listener?
**Answer**: If no listener is registered for the 'error' event, Node.js will throw the error as an unhandled exception and crash the application.

### Q4: How do you pass data when emitting an event?
**Answer**: Pass additional arguments after the event name:
```javascript
emitter.emit('data', arg1, arg2, arg3);
```

### Q5: How do you create a custom event emitter class?
**Answer**: Extend the EventEmitter class:
```javascript
class MyClass extends EventEmitter {
    myMethod() {
        this.emit('myEvent', data);
    }
}
```

### Q6: What are the built-in events of EventEmitter?
**Answer**:
- `newListener`: Fired when a listener is added
- `removeListener`: Fired when a listener is removed

---

## Navigation

← Previous: [34_HTTP_Server_Basics.md](./34_HTTP_Server_Basics.md) | Next: [36_Express_Introduction.md](../Module_05_Express_Framework/36_Express_Introduction.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 07*
