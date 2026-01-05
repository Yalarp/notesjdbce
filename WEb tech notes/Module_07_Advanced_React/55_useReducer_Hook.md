# useReducer Hook

## Table of Contents
1. [Introduction](#1-introduction)
2. [When to use useReducer](#2-when-to-use-usereducer)
3. [Syntax and Structure](#3-syntax-and-structure)
4. [Practical Example](#4-practical-example)
5. [Comparison with useState](#5-comparison-with-usestate)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 What is useReducer?
`useReducer` is a React Hook that is an alternative to `useState`. It allows you to manage complex state logic in function components using the **reducer pattern** (similar to Redux), where state transitions are explicit and determined by "actions".

---

## 2. When to use useReducer

Prefer `useReducer` over `useState` when:
1.  **Complex State Logic**: State involves multiple sub-values or complex objects.
2.  **Dependent Updates**: The next state depends on the previous state in complex ways.
3.  **Similar to Redux**: You want to organize logic cleanly or prepare for Redux.

---

## 3. Syntax and Structure

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

- **state**: The current state.
- **dispatch**: Function to send actions to the reducer.
- **reducer**: Function `(state, action) => newState`.
- **initialState**: The starting value.

---

## 4. Practical Example

### 4.1 Counter with Complex Actions

Unlike a simple counter, let's say we have actions to increment, decrement, and reset.

```jsx
import React, { useReducer } from 'react';

// 1. Define Initial State
const initialState = { count: 0 };

// 2. Define Reducer Function
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    case 'reset':
      return { count: 0 };
    default:
      throw new Error();
  }
}

// 3. Component
function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <>
      <h1>Count: {state.count}</h1>
      {/* Dispatch actions on click */}
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'reset' })}>Reset</button>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
    </>
  );
}
```

### 4.2 Handling Form State (Object)

Managing a form with many fields using `useReducer` keeps logic cleaner.

```jsx
const initialState = {
  username: '',
  email: '',
  loading: false,
};

function formReducer(state, action) {
  switch (action.type) {
    case 'INPUT_CHANGE':
      return { ...state, [action.field]: action.value };
    case 'TOGGLE_LOADING':
      return { ...state, loading: !state.loading };
    default:
      return state;
  }
}
```

---

## 5. Comparison with useState

| Feature | `useState` | `useReducer` |
|---------|------------|--------------|
| **Best for** | Simple values (numbers, strings, booleans) | Complex objects, deeply nested state |
| **Logic** | Logic inside event handler | Logic separated in reducer function |
| **Testing** | Harder to isolate logic | Reducer is a pure function (easy to test) |
| **Code Size** | Concise | More boilerplate |

---

## 6. Quick Reference

```jsx
// Reducer
const reducer = (state, action) => {
    if (action.type === 'ADD') return state + 1;
    return state;
};

// Hook
const [count, dispatch] = useReducer(reducer, 0);

// Dispatch
dispatch({ type: 'ADD' });
```

---

## 7. Interview Questions

### Q1: What is the third argument of useReducer for?
**Answer**: It is an optional **init function** for lazy initialization. If passed, the initial state is set to `init(initialArg)`. This is useful for calculating initial state based on props which might be expensive.

### Q2: Is useReducer part of Redux?
**Answer**: No. It is a built-in React Hook. However, it implements the same *patterns* (Reducer, Action, Dispatch) and principles as Redux, but for local component state.

### Q3: Can useReducer replace Redux?
**Answer**: For local or moderately shared state (with Context), yes. But for large-scale global state management, Redux (or Redux Toolkit) offers more features like DevTools, middleware (Thunk/Saga), and performance optimizations.

---

## Navigation

← Previous: [54_Redux_Introduction.md](./54_Redux_Introduction.md) | Next: [56_Redux_Demo_and_Practice.md](./56_Redux_Demo_and_Practice.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 11*
