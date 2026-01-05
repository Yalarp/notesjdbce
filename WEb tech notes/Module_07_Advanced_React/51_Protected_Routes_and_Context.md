# Protected Routes and Context

## Table of Contents
1. [Introduction](#1-introduction)
2. [Context API](#2-context-api)
3. [Component Composition](#3-component-composition)
4. [Protected Routes Implementation](#4-protected-routes-implementation)
5. [Practical Example](#5-practical-example)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 Authentication Flow
In modern web apps, certain pages (like "Dashboard" or "Profile") should only be accessible if the user is authenticated (logged in). "Protected Routes" are a pattern to handle this.

### 1.2 The Role of Context
React Context allows us to share global data (like `isSignedIn` status) across the entire application without passing props down manually at every level.

---

## 2. Context API

### 2.1 What is Context?
Context provides a way to pass data through the component tree without having to pass props down manually at every level.

### 2.2 useOutletContext
React Router v6 provides a specific hook `useOutletContext` to pass context from a parent route (Layout) to its child routes (Outlets).

```jsx
// Parent
<Outlet context={{ user }} />

// Child
const { user } = useOutletContext();
```

---

## 3. Component Composition

We create a wrapper component (often called `<Protected>` or `<PrivateRoute>`) that checks the authentication status.
- If authenticated: Render the children (the actual page).
- If not: Redirect to Login page using `<Navigate />`.

---

## 4. Protected Routes Implementation

### 4.1 The Protected Component
(Based on `Protected.jsx` from source)

```jsx
import { Navigate, useOutletContext } from "react-router-dom";

function Protected({ children }) {
    // 1. Get auth status from context
    const { isSignedIn } = useOutletContext();

    // 2. Check if signed in
    if (!isSignedIn) {
        alert("You must be signed in to view this page");
        // 3. Redirect if not auth
        return <Navigate to="/home" replace />;
    }

    // 4. Render children if auth
    return children;
}

export default Protected;
```

### 4.2 App Structure
(Based on `App.jsx` from source)

```jsx
function App() {
  const [isSignedIn, setIsSignedIn] = useState(false);
  
  return (
    <div>
       {/* Pass state to all children via Outlet */}
       <Outlet context={{ isSignedIn }} />
    </div>
  );
}
```

### 4.3 Route Definition
(Based on `main.jsx`)

```jsx
<Route path="Listproducts" element={
    <Protected>
        <Listproducts />
    </Protected>
} />
```

---

## 5. Practical Example

### 5.1 Full Flow
1. **Initial State**: `isSignedIn` is `false`.
2. **User Action**: User tries to visit `/Listproducts`.
3. **Router**: Matches route. Renders `<Protected><Listproducts /></Protected>`.
4. **Protected Component**:
   - Calls `useOutletContext()`, gets `{ isSignedIn: false }`.
   - Condition `if (!isSignedIn)` is true.
   - Shows alert.
   - Returns `<Navigate to="/home" />`.
5. **Result**: User is potentially redirected to Home page.

### 5.2 Sign In Logic
When user clicks "Sign In" button (in `App.jsx`):
1. `setIsSignedIn(true)` is called.
2. `App` re-renders.
3. New context `{ isSignedIn: true }` passed to Outlet.
4. User tries `/Listproducts` again.
5. **Protected Component**:
   - Gets `{ isSignedIn: true }`.
   - Returns `children` (`<Listproducts />`).
   - Page loads successfully.

---

## 6. Quick Reference

| Component | Purpose |
|-----------|---------|
| `<Navigate />` | Declarative redirect (component based) |
| `useOutletContext` | Access data passed from Parent Route |
| `<Outlet context={...} />` | Pass data to Child Routes |
| Wrapper Component | Encapsulates logic (Auth check) around a route |

---

## 7. Interview Questions

### Q1: How do you implement a private route in React Router v6?
**Answer**: By creating a wrapper component that checks the authentication status. If authenticated, it returns the `children` (or `Outlet`); otherwise, it renders a `<Navigate />` component to redirect the user to the login page.

### Q2: What is the difference between `useNavigate()` and `<Navigate />`?
**Answer**:
- `useNavigate()` is a **hook** used for imperative navigation (e.g., inside an event handler after form submission).
- `<Navigate />` is a **component** used for declarative navigation (e.g., inside the render return statement when redirecting based on a condition).

### Q3: What is Prop Drilling and how does Context solve it?
**Answer**: Prop drilling is the process of passing data from a parent to a deeply nested child through all intermediate components. Context solves this by allowing data to be "teleported" directly from a provider to any consumer in the tree, bypassing intermediate levels.

### Q4: Can `useOutletContext` be used outside of a Route?
**Answer**: No, it can only be used by components rendered by an `<Outlet />`.

---

## Navigation

← Previous: [50_Forms_in_React.md](../Module_06_React_Basics/50_Forms_in_React.md) | Next: [52_useRef_Hook.md](./52_useRef_Hook.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 11*
