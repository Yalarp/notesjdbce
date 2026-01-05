# useRef Hook

## Table of Contents
1. [Introduction](#1-introduction)
2. [Accessing DOM Elements](#2-accessing-dom-elements)
3. [Mutable Variables (No Re-render)](#3-mutable-variables)
4. [Difference vs useState](#4-difference-vs-usestate)
5. [Practical Example](#5-practical-example)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 What is useRef?
`useRef` is a built-in React Hook that returns a **mutable ref object** whose `.current` property is initialized to the passed argument (`initialValue`). The returned object persists for the full lifetime of the component.

### 1.2 Key Characteristics
1.  **Does NOT trigger re-renders** when the value changes.
2.  Used to access **DOM elements** directly.
3.  Used to store **mutable values** (like instance variables in class components).

---

## 2. Accessing DOM Elements

The most common use case is to allow a parent component to access a child DOM node (e.g., to focus an input).

```jsx
import { useRef, useEffect } from 'react';

function TextInputWithFocusButton() {
  const inputEl = useRef(null);

  const onButtonClick = () => {
    // `current` points to the mounted text input element
    inputEl.current.focus();
  };

  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

---

## 3. Mutable Variables

If you need to keep track of a value (like a timer ID or previous state) but don't want to cause a re-render when it changes, use `useRef`.

```jsx
function Timer() {
  const count = useRef(0);

  useEffect(() => {
    const interval = setInterval(() => {
        count.current = count.current + 1;
        console.log("Timer:", count.current);
        // Note: UI will NOT update because no state change
    }, 1000);

    return () => clearInterval(interval);
  }, []);

  return <h1>Check console for usage</h1>;
}
```

---

## 4. Difference vs useState

| Feature | `useState` | `useRef` |
|---------|------------|----------|
| **Re-render?** | Yes, triggers re-render on update | No, does not trigger re-render |
| **Storage** | For data rendered in UI | For data NOT rendered in UI (mostly) |
| **Update** | Asynchronous (batching) | Synchronous (immediate) |
| **Access** | `state` | `ref.current` |

---

## 5. Practical Example

### 5.1 Stopwatch (Preserving Interval ID)

We need to store the `intervalId` so we can clear it later. Storing it in a normal variable wouldn't work because it resets on every render. Storing it in `useState` would cause an extra render. `useRef` is perfect.

```jsx
import { useState, useRef } from 'react';

export default function Stopwatch() {
  const [startTime, setStartTime] = useState(null);
  const [now, setNow] = useState(null);
  
  // Store interval ID in ref
  const intervalRef = useRef(null);

  function handleStart() {
    setStartTime(Date.now());
    setNow(Date.now());

    clearInterval(intervalRef.current);
    intervalRef.current = setInterval(() => {
      setNow(Date.now());
    }, 10);
  }

  function handleStop() {
    clearInterval(intervalRef.current);
  }

  let seconds = 0;
  if (startTime != null && now != null) {
    seconds = (now - startTime) / 1000;
  }

  return (
    <>
      <h1>Time passed: {seconds.toFixed(3)}</h1>
      <button onClick={handleStart}>Start</button>
      <button onClick={handleStop}>Stop</button>
    </>
  );
}
```

---

## 6. Quick Reference

### 6.1 Creating a Ref
```jsx
const ref = useRef(initialValue);
```

### 6.2 Accessing Value
```jsx
const value = ref.current;
```

### 6.3 Updating Value
```jsx
ref.current = newValue; // No re-render
```

### 6.4 Attaching to DOM
```jsx
<div ref={myRef}></div>
```

---

## 7. Interview Questions

### Q1: Does updating `useRef` cause a re-render?
**Answer**: No. Changing `ref.current` does not notify React of any changes, so the component does not re-render.

### Q2: When should you use `useRef`?
**Answer**:
1. Managing focus, text selection, or media playback.
2. Triggering imperative animations.
3. Integrating with third-party DOM libraries (e.g., D3.js).
4. Storing mutable values that don't require re-renders (like IDs).

### Q3: Why not just use a global variable `let`?
**Answer**: `let` variables inside a function component are reset every time the component re-renders. `useRef` preserves the object between renders. `let` variables outside the component are global and shared by all instances, which causes bugs if you have multiple instances of the same component.

### Q4: Can I use `useRef` to store previous state?
**Answer**: Yes. You can update `ref.current` inside a `useEffect` to store the previous value of a prop or state variable.

---

## Navigation

← Previous: [51_Protected_Routes_and_Context.md](./51_Protected_Routes_and_Context.md) | Next: [53_Lazy_Loading.md](./53_Lazy_Loading.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 11*
