# Redux Demo and Practice

## Table of Contents
1. [Introduction](#1-introduction)
2. [Setup (Redux Toolkit)](#2-setup-redux-toolkit)
3. [Implementation Steps](#3-implementation-steps)
4. [Complete Example (Counter)](#4-complete-example-counter)
5. [Interview Questions](#5-interview-questions)

---

## 1. Introduction

We will implement a simple Redux application using **Redux Toolkit (RTK)**, which is the modern standard way to write Redux logic. It simplifies the setup by including sensible defaults and reducing boilerplate.

---

## 2. Setup (Redux Toolkit)

Install the necessary packages:

```bash
npm install @reduxjs/toolkit react-redux
```

---

## 3. Implementation Steps

1.  **Create Slice**: Define state and reducers.
2.  **Configure Store**: Create the store with the slice.
3.  **Provide Store**: Wrap the app with `<Provider>`.
4.  **Use Hooks**: `useSelector` (read) and `useDispatch` (write) in components.

---

## 4. Complete Example (Counter)

### Step 1: Create Slice (`counterSlice.js`)

```javascript
import { createSlice } from '@reduxjs/toolkit';

export const counterSlice = createSlice({
  name: 'counter',
  initialState: {
    value: 0,
  },
  reducers: {
    increment: (state) => {
      // RTK allows "mutating" logic in reducers using Immer library
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;

export default counterSlice.reducer;
```

### Step 2: Configure Store (`store.js`)

```javascript
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './counterSlice';

export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

### Step 3: Provide Store (`main.jsx`)

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import { store } from './store';
import { Provider } from 'react-redux';

ReactDOM.createRoot(document.getElementById('root')).render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

### Step 4: Use in Component (`Counter.jsx`)

```jsx
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement } from './counterSlice';

export function Counter() {
    // 1. Read state
    const count = useSelector((state) => state.counter.value);
    
    // 2. Init dispatch
    const dispatch = useDispatch();

    return (
        <div>
            <h1>Count: {count}</h1>
            <button onClick={() => dispatch(increment())}>
                Increment
            </button>
            <button onClick={() => dispatch(decrement())}>
                Decrement
            </button>
        </div>
    );
}
```

---

## 5. Interview Questions

### Q1: What is `createSlice` in Redux Toolkit?
**Answer**: It is a function that accepts an initial state, an object of reducer functions, and a "slice name", and automatically generates action creators and action types that correspond to the reducers and state.

### Q2: How do you read data from the store in a functional component?
**Answer**: Using the `useSelector` hook.
`const data = useSelector(state => state.property);`

### Q3: How do you update data in the store from a component?
**Answer**: By using the `useDispatch` hook to get the dispatch function, and then calling it with an action.
`dispatch(increment())`

### Q4: Why is Redux Toolkit preferred over "Vanilla" Redux?
**Answer**:
- **Less Boilerplate**: No need to manually create action types, action creators, and switch statements.
- **Immutability**: RTK uses ImmerJS, allowing you to write "mutating" syntax (`state.value++`) which is safer and easier.
- **Built-in Thunk**: Includes redux-thunk for async logic out of the box.

---

## Navigation

← Previous: [55_useReducer_Hook.md](./55_useReducer_Hook.md) | Next: [57_React_Bootstrap.md](./57_React_Bootstrap.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 11*
