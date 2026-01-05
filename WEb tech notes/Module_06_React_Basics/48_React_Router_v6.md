# React Router v6

## Table of Contents
1. [Introduction](#1-introduction)
2. [Installation](#2-installation)
3. [Core Components](#3-core-components)
4. [Setting Up Routes](#4-setting-up-routes)
5. [Navigation](#5-navigation)
6. [Nested Routes](#6-nested-routes)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 What is React Router?
**React Router** is a standard library for routing in React. It enables the navigation among views of various components in a React Application, allows changing the browser URL, and keeps the UI in sync with the URL.

### 1.2 Single Page Application (SPA)
In an SPA, the application loads a single HTML page and dynamically updates that page as the user interacts with the app. React Router handles this "simulated" navigation without a full page reload.

---

## 2. Installation

To use React Router v6, install the package:

```bash
npm install react-router-dom
```

---

## 3. Core Components

| Component | Description |
|-----------|-------------|
| `BrowserRouter` | Wraps the app to enable routing (uses HTML5 History API) |
| `Routes` | Container for all route definitions (replaces `Switch`) |
| `Route` | Defines a single route and the component to render |
| `Link` | Navigates to a route without reloading page |
| `Outlet` | Placeholder for nested route content |

---

## 4. Setting Up Routes

### 4.1 Basic Configuration
(Based on `main.jsx` from `reactcrud` project)

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import App from './App';
import Home from './components/Home';
import Contactus from './components/Contactus';
import Nopagefound from './components/Nopagefound';

const root = ReactDOM.createRoot(document.getElementById('root'));

root.render(
  <BrowserRouter>
    <Routes>
      <Route path="/" element={<App />}>
        {/* Index Route (Default) */}
        <Route index element={<Home />} />
        
        {/* Specific Routes */}
        <Route path="Home" element={<Home />} />
        <Route path="Contactus" element={<Contactus />} />
        
        {/* 404 Route */}
        <Route path="*" element={<Nopagefound />} />
      </Route>
    </Routes>
  </BrowserRouter>
);
```

### 4.2 Key Concepts
- **Nested Routes**: The `App` component wraps other routes. The child routes render inside `App`.
- **Index Route**: `<Route index />` specifies what to render at the parent's URL (`/`).
- **Wildcard Route**: `path="*"` catches any undefined URLs (404 page).

---

## 5. Navigation

### 5.1 Using `<Link>`
Use `Link` instead of `<a>` tags to prevent full page reloads.

```jsx
import { Link } from "react-router-dom";

function Navigation() {
  return (
    <nav>
      <Link to="/">Home</Link> | 
      <Link to="/Contactus">Contact Us</Link>
    </nav>
  );
}
```

### 5.2 Using `<NavLink>`
Similar to `Link`, but knows when it is active (useful for highlighting menu items).

```jsx
import { NavLink } from "react-router-dom";

<NavLink 
  to="/messages" 
  style={({ isActive }) => ({ color: isActive ? "red" : "blue" })}
>
  Messages
</NavLink>
```

---

## 6. Nested Routes

### 6.1 Using `<Outlet>`
When using nested routes, the parent component must render an `<Outlet />` to specify where the child components should appear.

**Parent Component (`App.jsx`):**
```jsx
import { Outlet, Link } from "react-router-dom";
import Header from "./components/Header";

function App() {
  return (
    <div>
      <Header /> {/* Always visible */}
      
      <nav>
        {/* Navigation links */}
      </nav>

      <hr />

      {/* Child routes render here */}
      <Outlet />
    </div>
  )
}
```

**Route Definition:**
```jsx
<Route path="/" element={<App />}>
  <Route path="Contactus" element={<Contactus />} />
</Route>
```

**Result:** When URL is `/Contactus`:
1. `App` renders.
2. `Contactus` renders inside the `<Outlet />` of `App`.

---

## 7. Quick Reference

### 7.1 Setup

```jsx
<BrowserRouter>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
  </Routes>
</BrowserRouter>
```

### 7.2 Navigation

```jsx
<Link to="/about">About</Link>
<NavLink to="/about" className={({isActive}) => isActive ? 'active' : ''}>About</NavLink>
```

### 7.3 404 Page

```jsx
<Route path="*" element={<NotFound />} />
```

---

## 8. Interview Questions

### Q1: What is the difference between `Link` and `<a>` tag?
**Answer**: `<a>` tag triggers a full page reload (server request), resetting standard state. `Link` uses the History API to change the URL and re-render components without refreshing the page, preserving state (SPA behavior).

### Q2: What is the purpose of `BrowserRouter`?
**Answer**: It uses the HTML5 history API (`pushState`, `replaceState`, `popstate`) to keep your UI in sync with the URL. It wraps the entire application.

### Q3: What is `<Outlet>`?
**Answer**: `Outlet` is a component used in parent routes to render their child route elements. It allows nested UI to show up when child routes are matched.

### Q4: How do you handle 404 pages in React Router v6?
**Answer**: By defining a route with `path="*"` at the end of your route list. This acts as a catch-all for any URL that doesn't match defined routes.

### Q5: What replaced `Switch` component in v6?
**Answer**: `Routes` replaced `Switch`. `Routes` is more intelligent and selects the best matching route automatically (no need for `exact` prop anymore).

---

## Navigation

← Previous: [47_Sibling_Data_Passing.md](./47_Sibling_Data_Passing.md) | Next: [49_Route_Parameters_and_Hooks.md](./49_Route_Parameters_and_Hooks.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 10*
