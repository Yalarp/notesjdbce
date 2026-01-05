# Event Handling in React

## Table of Contents
1. [Introduction](#1-introduction)
2. [Handling Events](#2-handling-events)
3. [Event Object](#3-event-object)
4. [Passing Arguments](#4-passing-arguments)
5. [Common Events](#5-common-events)
6. [Practical Examples](#6-practical-examples)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 React Events vs HTML Events
Handling events with React elements is very similar to handling events on DOM elements, with some syntax differences:
1.  React events are named using **camelCase** (e.g., `onClick` instead of `onclick`).
2.  You pass a **function** as the event handler, rather than a string.

### 1.2 Synthetic Events
React uses a cross-browser wrapper around the browser's native event system called **SyntheticEvent**. This ensures that events behave consistently across all browsers (IE, Chrome, Firefox, etc.).

---

## 2. Handling Events

### 2.1 Basic Syntax

**HTML:**
```html
<button onclick="activateLasers()">
  Activate Lasers
</button>
```

**React:**
```jsx
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

### 2.2 Common Mistake: Invoking Function
Don't invoke the function when passing it.

**Wrong:**
```jsx
<button onClick={handleClick()}>Click me</button>
// This runs handleClick immediately during render!
```

**Right:**
```jsx
<button onClick={handleClick}>Click me</button>
// OR
<button onClick={() => handleClick()}>Click me</button>
```

---

## 3. Event Object

The event handler receives the `SyntheticEvent` object as its argument.

```jsx
function Button() {
    function handleClick(e) {
        e.preventDefault(); // Prevent default browser behavior
        console.log('Button clicked');
    }

    return (
        <a href="#" onClick={handleClick}>
            Click me
        </a>
    );
}
```

---

## 4. Passing Arguments

To pass an extra argument to an event handler, use an arrow function.

```jsx
<button onClick={(e) => deleteRow(id, e)}>Delete Row</button>
```

---

## 5. Common Events

| Event | Description |
|-------|-------------|
| `onClick` | Click event |
| `onChange` | Checkbox, text input, select changes |
| `onSubmit` | Form submission |
| `onMouseEnter` | Mouse hover |
| `onFocus` | Element gets focus |
| `onBlur` | Element loses focus |

---

## 6. Practical Examples

### 6.1 Click Event (Counter)
**Original Code (from `Counter.jsx`):**
```jsx
import { useState, useEffect } from 'react';

export default function Counter() {
    const [count, setCount] = useState(0);
    
    // ... useEffect code omitted ...

    return (
        <button onClick={() => setCount(count + 1)}>
            You clicked {count} times
        </button>
    );
}
```

**Explanation:**
- The `onClick` handler is an arrow function: `() => setCount(count + 1)`.
- When clicked, it updates the state, triggering a re-render.

### 6.2 input Change Event (Search)
**Original Code (from `Search.jsx`):**
```jsx
export function Search({ onQuery }) {
   function handelInput(e) {
      onQuery(e.target.value);
   }
   return (
      <div>
         <input type="text" onChange={handelInput} />
      </div>
   )
}
```

**Line-by-Line Explanation:**
| Line | Code | Explanation |
|------|------|-------------|
| 1 | `export function Search({ onQuery })` | Component receives `onQuery` prop (a callback function from parent). |
| 2 | `function handelInput(e)` | Local event handler function. |
| 3 | `onQuery(e.target.value)` | `e.target` refers to the input element. `e.target.value` gets the current text. Calls the parent's function. |
| 7 | `onChange={handelInput}` | Attaches the handler to the input's change event. |

**Execution Flow:**
1. User types in the input box.
2. `onChange` event fires.
3. `handelInput` function is called with the event object `e`.
4. `e.target.value` (typed text) is extracted.
5. `onQuery` (parent's function) is called with the text.
6. Parent component likely updates its state, causing data flow.

---

## 7. Quick Reference

### 7.1 Syntax Cheatsheet

```jsx
// No args
<button onClick={handler}>Click</button>

// With args
<button onClick={() => handler(id)}>Click</button>

// Event object
<input onChange={(e) => console.log(e.target.value)} />
```

### 7.2 Preventing Default

```jsx
// Checkbox or Link
function handleClick(e) {
    e.preventDefault();
}
```

---

## 8. Interview Questions

### Q1: What is a Synthetic Event in React?
**Answer**: A Synthetic Event is a cross-browser wrapper around the browser's native event. It has the same interface as the native event (e.g., `stopPropagation()`, `preventDefault()`) but works identically across all browsers.

### Q2: Why is `onClick={handleClick()}` incorrect?
**Answer**: Because it calls the function *immediately* when the component renders, instead of waiting for the click event. The correct way is `onClick={handleClick}` (passing the function reference).

### Q3: How do you pass a parameter to an event handler?
**Answer**: Wrap the handler in an arrow function: `onClick={() => handleDelete(id)}`.

### Q4: Can I use `return false` to prevent default behavior in React?
**Answer**: No, you must explicitly call `e.preventDefault()`. `return false` works in standard HTML/jQuery handlers but not in React.

---

## Navigation

← Previous: [44_Conditional_Rendering.md](./44_Conditional_Rendering.md) | Next: [46_Lists_and_Keys.md](./46_Lists_and_Keys.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 09*
