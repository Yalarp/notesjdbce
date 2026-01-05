# React & Redux Interview Questions

## Table of Contents
1. [React Fundamentals](#1-react-fundamentals)
2. [Components & Lifecycle](#2-components--lifecycle)
3. [Hooks (Functional Components)](#3-hooks-functional-components)
4. [State Management (Redux)](#4-state-management-redux)
5. [Router & Advanced Topics](#5-router--advanced-topics)

---

## 1. React Fundamentals

### Q1: What is React?
**Answer**: React is a JavaScript library for building user interfaces, developed by Facebook. It is component-based, declarative, and uses a Virtual DOM for efficient rendering.

### Q2: Features of React?
**Answer**:
1.  **Virtual DOM**: Performance optimization.
2.  **One-way Data Binding**: Data flows down (parent to child).
3.  **Components**: Reusable UI building blocks.
4.  **JSX**: JavaScript Syntax Extension (HTML-in-JS).

### Q3: What is the Virtual DOM?
**Answer**: An in-memory representation of the real DOM. React creates a tree of objects (VDOM). When state changes, it creates a new tree, compares it with the old one (**Diffing**), and updates only the changed nodes in the real DOM (**Reconciliation**).

### Q4: JSX vs HTML?
**Answer**:
-   JSX is not valid JS; it must be transpiled (by Babel).
-   Attributes use camelCase (`className` instead of `class`, `onClick` instead of `onclick`).
-   Tags must be closed.

### Q5: Props vs State?
**Answer**:
-   **Props** (Properties): Immutable, passed from parent to child. Used for configuration.
-   **State**: Mutable, managed within the component. Triggers re-render when changed.

---

## 2. Components & Lifecycle

### Q6: Functional vs Class Components?
**Answer**:
-   **Class**: Extend `React.Component`, have `render()`, use `this.state` and Lifecycle methods.
-   **Functional**: Plain JS functions, use **Hooks** for state/lifecycle. Simpler and preferred in modern React.

### Q7: Lifecycle Methods (Class)?
**Answer**:
1.  **Mounting**: `constructor()`, `static getDerivedStateFromProps()`, `render()`, `componentDidMount()`.
2.  **Updating**: `shouldComponentUpdate()`, `render()`, `componentDidUpdate()`.
3.  **Unmounting**: `componentWillUnmount()`.

### Q8: What is `PureComponent`?
**Answer**: A class component that implements `shouldComponentUpdate` with a shallow prop/state comparison. It prevents unnecessary re-renders if props/state haven't changed.

### Q9: What are Higher-Order Components (HOC)?
**Answer**: A function that takes a component and returns a new component (e.g., `connect` in Redux, `withRouter`). Used for logic reuse.

---

## 3. Hooks (Functional Components)

### Q10: What are Hooks?
**Answer**: Functions that let you "hook into" React state and lifecycle features from functional components. (Added in React 16.8).

### Q11: Common Hooks?
**Answer**:
-   `useState`: Manage local state.
-   `useEffect`: Manage side-effects (API calls, subscriptions). Replaces `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`.
-   `useContext`: Consume context without wrapping.
-   `useRef`: Access DOM elements or persist values without re-render.
-   `useReducer`: Complex state logic (Redux-like).
-   `useMemo`, `useCallback`: Performance optimization.

### Q12: `useEffect` Dependency Array?
**Answer**:
-   `[]`: Runs once (Mount).
-   `[prop]`: Runs when `prop` changes (Update).
-   No array: Runs on *every* render.

---

## 4. State Management (Redux)

### Q13: What is Redux?
**Answer**: A predictable state container for JavaScript apps. It enables managing global state in a single place (Store).

### Q14: Core Principles of Redux?
**Answer**:
1.  **Single Source of Truth**: One store for the whole app.
2.  **State is Read-Only**: The only way to change state is to emit an **Action**.
3.  **Changes are made with Pure Functions**: **Reducers** take previous state and action, and return new state.

### Q15: Redux Data Flow?
**Answer**: View -> Dispatch(Action) -> Middleware -> Reducer -> Store (State Update) -> View (Subscribe).

### Q16: What is a Reducer?
**Answer**: A pure function `(state, action) => newState`. It must *not* mutate the state; it returns a new copy.

### Q17: `mapStateToProps` and `mapDispatchToProps`?
**Answer**:
-   `mapState`: Selects part of the global state to pass as props.
-   `mapDispatch`: Maps action creators to props.
*(Modern Redux uses `useSelector` and `useDispatch` hooks instead).*

### Q18: Redux Thunk?
**Answer**: Middleware that allows action creators to return a *function* instead of an object. This function can perform async operations (e.g., Fetch API) and then dispatch a sync action.

---

## 5. Router & Advanced Topics

### Q19: What is React Router?
**Answer**: Standard routing library for React. Enables navigation among views without refreshing the page.
Components: `<BrowserRouter>`, `<Routes>`, `<Route>`, `<Link>`, `<NavLink>`.

### Q20: `useNavigate` vs `useHistory`?
**Answer**: `useHistory` was used in v5. `useNavigate` is the hook in v6.
`const navigate = useNavigate(); navigate('/home');`

### Q21: What are Fragment?
**Answer**: `<React.Fragment>` or `<>...</>` allows grouping a list of children without adding extra nodes to the DOM.

### Q22: Error Boundaries?
**Answer**: React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI. (Must use Class Component: `componentDidCatch`).

### Q23: Portals?
**Answer**: Way to render children into a DOM node that exists outside the DOM hierarchy of the parent component (e.g., Modals, Tooltips).

### Q24: Controlled vs Uncontrolled Components?
**Answer**:
-   **Controlled**: React handles state (`value={state}`).
-   **Uncontrolled**: internal DOM handles state (accessed via `ref`).

---

## Navigation

← Previous: [67_Node_Express_Interview_QA.md](./67_Node_Express_Interview_QA.md) | Next: [69_Web_Technologies_Cheat_Sheet.md](../Module_10_Cheatsheet/69_Web_Technologies_Cheat_Sheet.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Notes_CCEE_InterviewQA_Web (Simulated)*
