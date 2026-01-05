# React Introduction

## Table of Contents
1. [Introduction](#1-introduction)
2. [Getting Started](#2-getting-started)
3. [JSX Syntax](#3-jsx-syntax)
4. [Components](#4-components)
5. [Virtual DOM](#5-virtual-dom)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 What is React?
**React** is a JavaScript library for building user interfaces, developed and maintained by Facebook. It focuses on building reusable UI components.

### 1.2 Key Features

| Feature | Description |
|---------|-------------|
| Component-Based | Build encapsulated components |
| Declarative | Describe what UI should look like |
| Virtual DOM | Efficient DOM updates |
| One-Way Data Flow | Data flows from parent to child |
| JSX | JavaScript XML syntax |

### 1.3 Why React?
- Fast and efficient
- Reusable components
- Large ecosystem
- Strong community
- Used by major companies

---

## 2. Getting Started

### 2.1 Create React App

```bash
npx create-react-app my-app
cd my-app
npm start
```

### 2.2 Vite (Recommended)

```bash
npm create vite@latest my-app -- --template react
cd my-app
npm install
npm run dev
```

### 2.3 Project Structure

```
my-app/
├── node_modules/
├── public/
│   └── index.html
├── src/
│   ├── App.jsx
│   ├── App.css
│   ├── index.jsx
│   └── index.css
├── package.json
└── vite.config.js
```

### 2.4 First Component

```jsx
// src/App.jsx
function App() {
    return (
        <div>
            <h1>Hello, React!</h1>
        </div>
    );
}

export default App;
```

---

## 3. JSX Syntax

### 3.1 What is JSX?
JSX (JavaScript XML) is a syntax extension that allows writing HTML-like code in JavaScript.

```jsx
// JSX
const element = <h1>Hello, World!</h1>;

// Compiles to
const element = React.createElement('h1', null, 'Hello, World!');
```

### 3.2 JSX Rules

```jsx
// 1. Return single parent element
return (
    <div>
        <h1>Title</h1>
        <p>Content</p>
    </div>
);

// 2. Or use Fragment
return (
    <>
        <h1>Title</h1>
        <p>Content</p>
    </>
);

// 3. Close all tags
<img src="photo.jpg" />
<br />

// 4. Use className instead of class
<div className="container">

// 5. Use camelCase for attributes
<button onClick={handleClick}>

// 6. Use htmlFor instead of for
<label htmlFor="email">
```

### 3.3 JavaScript Expressions in JSX

```jsx
function Greeting() {
    const name = 'John';
    const age = 25;
    
    return (
        <div>
            <h1>Hello, {name}!</h1>
            <p>Age: {age}</p>
            <p>Next year: {age + 1}</p>
            <p>Uppercase: {name.toUpperCase()}</p>
        </div>
    );
}
```

### 3.4 Conditional Rendering

```jsx
function Message({ isLoggedIn }) {
    return (
        <div>
            {isLoggedIn ? (
                <h1>Welcome back!</h1>
            ) : (
                <h1>Please log in</h1>
            )}
        </div>
    );
}

// Short-circuit
function Alert({ show, message }) {
    return (
        <div>
            {show && <p className="alert">{message}</p>}
        </div>
    );
}
```

### 3.5 Lists and Keys

```jsx
function UserList() {
    const users = [
        { id: 1, name: 'John' },
        { id: 2, name: 'Jane' },
        { id: 3, name: 'Bob' }
    ];
    
    return (
        <ul>
            {users.map(user => (
                <li key={user.id}>{user.name}</li>
            ))}
        </ul>
    );
}
```

---

## 4. Components

### 4.1 Functional Components

```jsx
// Basic component
function Welcome() {
    return <h1>Hello!</h1>;
}

// Arrow function
const Welcome = () => {
    return <h1>Hello!</h1>;
};

// With props
function Greeting({ name }) {
    return <h1>Hello, {name}!</h1>;
}

// Usage
<Greeting name="John" />
```

### 4.2 Props

```jsx
// Passing props
function App() {
    return (
        <UserCard 
            name="John" 
            age={25} 
            isAdmin={true}
            hobbies={['reading', 'gaming']}
        />
    );
}

// Receiving props
function UserCard({ name, age, isAdmin, hobbies }) {
    return (
        <div>
            <h2>{name}</h2>
            <p>Age: {age}</p>
            <p>Admin: {isAdmin ? 'Yes' : 'No'}</p>
            <ul>
                {hobbies.map((hobby, i) => (
                    <li key={i}>{hobby}</li>
                ))}
            </ul>
        </div>
    );
}
```

### 4.3 Default Props

```jsx
function Button({ label = 'Click me', color = 'blue' }) {
    return (
        <button style={{ backgroundColor: color }}>
            {label}
        </button>
    );
}
```

### 4.4 Children Props

```jsx
function Card({ title, children }) {
    return (
        <div className="card">
            <h2>{title}</h2>
            <div className="card-body">
                {children}
            </div>
        </div>
    );
}

// Usage
<Card title="My Card">
    <p>This is card content</p>
    <button>Click me</button>
</Card>
```

---

## 5. Virtual DOM

### 5.1 What is Virtual DOM?
The Virtual DOM is a lightweight JavaScript representation of the actual DOM. React uses it to optimize updates.

### 5.2 How It Works

```
1. State changes in component
        ↓
2. New Virtual DOM tree created
        ↓
3. Diff with previous Virtual DOM
        ↓
4. Calculate minimal changes
        ↓
5. Update real DOM (Reconciliation)
```

### 5.3 Benefits

| Benefit | Description |
|---------|-------------|
| Performance | Minimal DOM manipulations |
| Batching | Groups multiple updates |
| Efficiency | Only changes what's needed |

---

## 6. Quick Reference

### 6.1 Create App

```bash
npx create-react-app my-app
# or
npm create vite@latest my-app -- --template react
```

### 6.2 Component Structure

```jsx
function Component({ prop1, prop2 }) {
    return (
        <div>
            {/* JSX content */}
        </div>
    );
}

export default Component;
```

### 6.3 JSX Rules

```jsx
// Single parent element
// Use className, htmlFor
// Close all tags
// camelCase attributes
// JavaScript in {}
```

### 6.4 Rendering Lists

```jsx
{items.map(item => (
    <Item key={item.id} data={item} />
))}
```

---

## 7. Interview Questions

### Q1: What is React?
**Answer**: React is a JavaScript library for building user interfaces. It's component-based, declarative, and uses a Virtual DOM for efficient rendering.

### Q2: What is JSX?
**Answer**: JSX (JavaScript XML) is a syntax extension that allows writing HTML-like code in JavaScript. It gets compiled to React.createElement() calls.

### Q3: What is the Virtual DOM?
**Answer**: The Virtual DOM is a lightweight JavaScript representation of the real DOM. React uses it to efficiently update only the parts of the UI that changed.

### Q4: What are props in React?
**Answer**: Props are read-only properties passed from parent to child components. They allow data to flow down the component tree.

### Q5: Why do we need keys in lists?
**Answer**: Keys help React identify which items changed, added, or removed. They optimize reconciliation by allowing React to reuse existing DOM elements.

### Q6: What is the difference between React and ReactDOM?
**Answer**:
- **React**: Core library for creating components
- **ReactDOM**: Library for rendering React to the DOM

---

## Navigation

← Previous: [40_MongoDB_Integration.md](../Module_05_Express_Framework/40_MongoDB_Integration.md) | Next: [42_React_State_and_Props.md](./42_React_State_and_Props.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 09-10*
