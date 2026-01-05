# Route Parameters and Hooks

## Table of Contents
1. [Introduction](#1-introduction)
2. [Route Parameters](#2-route-parameters)
3. [Key Hooks](#3-key-hooks)
4. [Practical Examples](#4-practical-examples)
5. [Quick Reference](#5-quick-reference)
6. [Interview Questions](#6-interview-questions)

---

## 1. Introduction

### 1.1 Dynamic Routing
Dynamic routing allows you to define routes that match a pattern, capturing values from the URL (like an ID) to pass as parameters to your component.

### 1.2 Router Hooks
React Router v6 provides several hooks to access router state and perform navigation programmatically.

---

## 2. Route Parameters

### 2.1 Defining Parameters
In your Route definition, use a colon (`:`) to denote a parameter.

```jsx
<Route path="emp/:id" element={<Employee />} />
```

- Matches `/emp/1`, `/emp/123`, etc.
- `id` becomes a key in the `useParams` object.

### 2.2 Accessing Parameters
Use the `useParams` hook to access the parameters in your component.

---

## 3. Key Hooks

### 3.1 `useParams`
Returns an object of key/value pairs of URL parameters.

```jsx
import { useParams } from 'react-router-dom';

function Employee() {
  const { id } = useParams();
  return <h1>Employee ID: {id}</h1>;
}
```

### 3.2 `useNavigate`
Returns a function to navigate programmatically (replaces `history.push`).

```jsx
import { useNavigate } from 'react-router-dom';

function Login() {
  const navigate = useNavigate();

  const handleLogin = () => {
    // ... login logic ...
    navigate('/dashboard');
  };
}
```

- `navigate(to)`: Navigate to path
- `navigate(-1)`: Go back one page

### 3.3 `useLocation`
Returns the current location object (like `window.location`). Useful for accessing state passed via navigation or current path.

```jsx
import { useLocation } from 'react-router-dom';

function Page() {
  const location = useLocation();
  console.log(location.pathname);
  console.log(location.search); // ?query=...
}
```

---

## 4. Practical Examples

### 4.1 Fetching Data with Parameters
This example shows how to use `useParams` to fetch details for a specific employee.

**Original Code (from `Employee.jsx`):**
```jsx
// Imports
import React, { useState, useEffect } from "react";
import { useParams, Link } from "react-router-dom";

function Employee() {
  const [employee, setEmployee] = useState({});
  const { id } = useParams(); // Extract ID from URL

  useEffect(() => {
    // Fetch data using the ID
    fetch("https://localhost:7208/api/employee/" + id)
      .then((res) => res.json())
      .then((result) => setEmployee(result));
  }, [id]); // Re-run if ID changes

  return (
    <div>
      <h2>Employee Details</h2>
      <label>Id:</label> {employee.id} <br />
      <label>Name:</label> {employee.name} <br />
      {/* ... */}
      <Link to="/Listproducts">Back to List</Link>
    </div>
  );
}
```

**Execution Flow:**
1. User navigates to `/emp/5`.
2. Router matches path `emp/:id` and renders `Employee`.
3. `useParams` extracts `id = "5"`.
4. `useEffect` runs, fetching `.../api/employee/5`.
5. Data received, state updated, component re-renders with employee details.

### 4.2 Programmatic Navigation
This example shows `useNavigate` to redirect after form submission.

**Original Code (from `CreateEmp.jsx`):**
```jsx
import { useNavigate } from "react-router-dom";

export default function CreateEmp() {
    const navigate = useNavigate();
    // ... form logic ...
    
    const handleSubmit = async (event) => {
        event.preventDefault();
        try {
            const response = await fetch(".../api/Employee", { ... });
            if (!response.ok) throw new Error("Failed");
            
            // Navigate back to home/list after success
            navigate("/"); 
        } catch(error) {
            console.error(error);
        }
    }
    // ...
}
```

---

## 5. Quick Reference

| Hook | Purpose | Example |
|------|---------|---------|
| `useParams` | Get URL params | `const { id } = useParams();` |
| `useNavigate` | Change URL | `navigate('/home');` |
| `useLocation` | Get current URL info | `location.pathname` |
| `useSearchParams` | Get query strings | `const [params] = useSearchParams();` |

---

## 6. Interview Questions

### Q1: How do you access the dynamic part of a URL in React Router?
**Answer**: By defining a route parameter (e.g., `:id`) and using the `useParams` hook in the component to retrieve the value.

### Q2: What is the difference between `Link` and `useNavigate`?
**Answer**:
- `Link`: Declarative navigation (JSX element), used for clickable links.
- `useNavigate`: Imperative navigation (function), used in event handlers or logic (e.g., redirect after login).

### Q3: How do you go back to the previous page using React Router v6?
**Answer**: Use `navigate(-1)`.

### Q4: How do you pass state while navigating?
**Answer**: `navigate('/path', { state: { key: 'value' } })`. This can be accessed via `useLocation().state` in the destination component.

---

## Navigation

← Previous: [48_React_Router_v6.md](./48_React_Router_v6.md) | Next: [50_Forms_in_React.md](./50_Forms_in_React.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 10*
