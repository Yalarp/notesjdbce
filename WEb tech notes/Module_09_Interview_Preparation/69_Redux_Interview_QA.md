# Redux & Advanced React Interview Questions

## Table of Contents
1. [Redux Fundamentals](#1-redux-fundamentals)
2. [Redux Middleware (Thunk/Saga)](#2-redux-middleware)
3. [React-Redux Bindings](#3-react-redux-bindings)
4. [Optimization & Selectors](#4-optimization--selectors)
5. [Context vs Redux](#5-context-vs-redux)
6. [Testing & Debugging](#6-testing--debugging)

---

## 1. Redux Fundamentals

### Q1: What is Redux?
**Answer**: Redux is a predictable state container for JavaScript apps. It helps write applications that behave consistently, run in different environments (client, server, native), and are easy to test.

### Q2: What are the Three Principles of Redux?
**Answer**:
1.  **Single Source of Truth**: The state of your whole application is stored in an object tree within a single **store**.
2.  **State is Read-Only**: The only way to change the state is to emit an **action**, an object describing what happened.
3.  **Changes are made with Pure Functions**: To specify how the state tree is transformed by actions, you write pure **reducers**.

### Q3: What is an Action in Redux?
**Answer**: An action is a plain JavaScript object that describes *what happened*. It must have a `type` property.
```javascript
const addTodoAction = {
  type: 'ADD_TODO',
  payload: 'Learn Redux'
}
```

### Q4: What is a Reducer?
**Answer**: A reducer is a pure function that takes the previous state and an action, and returns the next state.
`(previousState, action) => newState`
*Crucial*: Never mutate the state argument. Always return a new object.

---

## 2. Redux Middleware

### Q5: What is Middleware in Redux?
**Answer**: It provides a third-party extension point between dispatching an action and the moment it reaches the reducer. Used for logging, crash reporting, performing asynchronous tasks, etc.

### Q6: What is Redux Thunk?
**Answer**: A middleware that allows you to write action creators that return a *function* instead of an action. This function receives `dispatch` and `getState` as arguments.
**Use Case**: Async Logic (API calls).
```javascript
const fetchUser = (id) => (dispatch) => {
  dispatch({ type: 'FETCH_START' });
  api.getUser(id).then(user => dispatch({ type: 'FETCH_SUCCESS', payload: user }));
};
```

### Q7: Redux Thunk vs Redux Saga?
**Answer**:
-   **Thunk**: Simple, easy to learn, efficient for simple async logic. Functions returning functions.
-   **Saga**: Uses ES6 Generators. More powerful for complex async flows (cancellation, race conditions), easier to test, but higher learning curve.

---

## 3. React-Redux Bindings

### Q8: What is `Provider`?
**Answer**: A component from `react-redux` that makes the Redux store available to any nested components that need to access the Redux store.
```jsx
<Provider store={store}><App /></Provider>
```

### Q9: `useSelector` hook?
**Answer**: Allows you to extract data from the Redux store state, using a selector function.
`const count = useSelector(state => state.counter.value)`

### Q10: `useDispatch` hook?
**Answer**: Returns a reference to the `dispatch` function from the Redux store. Used to dispatch actions.
`const dispatch = useDispatch()`

---

## 4. Optimization & Selectors

### Q11: What is `reselect`?
**Answer**: A library for creating memoized "selector" functions. Commonly used with Redux.
-   Selectors can compute derived data, allowing Redux to store the minimal possible state.
-   Selectors are memoized: they don't recompute unless arguments change.

### Q12: Why is immutability important in Redux?
**Answer**:
1.  **Performance**: Redux uses shallow equality checking. If references change, it knows state changed.
2.  **Predictability**: Pure functions + Immutability = Predictable state updates.
3.  **Time-Travel Debugging**: Requires tracking distinct state versions.

---

## 5. Context vs Redux

### Q13: When to use Redux over Context API?
**Answer**:
-   **Context**: Passing data deep down without props drilling (Theme, Auth). Simple, low-frequency updates.
-   **Redux**: Complex state logic, many state slices, frequent updates, different parts of app needing same data, need for Middleware/DevTools.

---

## 6. Testing & Debugging

### Q14: What is Redux DevTools?
**Answer**: A browser extension that allows you to inspect every state and action payload. It lets you go back in time ("time travel") which makes debugging easy.

### Q15: How to test Reducers?
**Answer**: Since reducers are pure functions, you simply pass an initial state and an action, and assert the return value equals the expected new state.

---

## Navigation

← Previous: [68_React_Interview_QA.md](../Module_09_Interview_Preparation/68_React_Interview_QA.md) | Next: [70_Web_Technologies_Cheat_Sheet.md](../Module_10_Cheatsheet/70_Web_Technologies_Cheat_Sheet.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Redux Notes*
