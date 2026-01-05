# Sibling Component Data Passing

## Table of Contents
1. [Introduction](#1-introduction)
2. [Lifting State Up](#2-lifting-state-up)
3. [The Problem with Siblings](#3-the-problem-with-siblings)
4. [Step-by-Step Implementation](#4-step-by-step-implementation)
5. [Practical Example](#5-practical-example)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 Data Flow in React
React has a **unidirectional (one-way) data flow**, meaning data flows down from parent to children via props.

### 1.2 The Challenge
Sibling components cannot directly pass data to each other. They don't share a direct connection.

```
    Parent
   /      \
Child A   Child B
```

If **Child A** has data that **Child B** needs, you cannot pass it directly from A to B.

---

## 2. Lifting State Up

### 2.1 The Solution
To share data between siblings, you must **lift the state up** to their closest common ancestor (Parent).

1.  Move the state to the **Parent**.
2.  Pass the state down to **Child B** (as a prop).
3.  Pass a function (callback) down to **Child A** (as a prop) to update the state.

---

## 3. The Problem with Siblings

Imagine two components: one for inputting text, and another for displaying it.

```jsx
// InputComponent (Sibling A)
function InputComponent() {
    const [text, setText] = useState(""); // State is local
    return <input onChange={e => setText(e.target.value)} />;
}

// DisplayComponent (Sibling B)
function DisplayComponent() {
    // Cannot access 'text' from Sibling A!
    return <p>Text: ???</p>;
}
```

---

## 4. Step-by-Step Implementation

### Step 1: Create State in Parent
```jsx
function Parent() {
    const [sharedData, setSharedData] = useState("");

    return (
        <div>
           <SiblingA onDataChange={setSharedData} />
           <SiblingB data={sharedData} />
        </div>
    );
}
```

### Step 2: Child A Updates Parent
```jsx
function SiblingA({ onDataChange }) {
    const handleChange = (e) => {
        // Call parent's function
        onDataChange(e.target.value);
    };

    return <input onChange={handleChange} />;
}
```

### Step 3: Child B Receives Data
```jsx
function SiblingB({ data }) {
    return <p>Received: {data}</p>;
}
```

---

## 5. Practical Example

This example demonstrates a "Search" component (Sibling A) filtering a "List" component (Sibling B).

**Code Structure:**
```
App (Parent) - Holds the 'query' state
├── SearchBar (Sibling A) - Updates 'query'
└── ProductList (Sibling B) - Displays items matching 'query'
```

**Implementation:**

```jsx
import { useState } from 'react';

// Sibling A: Input
function SearchBar({ onSearch }) {
    return (
        <div style={{ padding: '10px', background: '#eee' }}>
            <input 
                placeholder="Search products..." 
                onChange={(e) => onSearch(e.target.value)} 
            />
        </div>
    );
}

// Sibling B: List
function ProductList({ products, query }) {
    const filtered = products.filter(p => 
        p.name.toLowerCase().includes(query.toLowerCase())
    );

    return (
        <ul>
            {filtered.map(p => <li key={p.id}>{p.name}</li>)}
        </ul>
    );
}

// Parent: App
export default function App() {
    const [query, setQuery] = useState('');
    
    const products = [
        { id: 1, name: 'Apple' },
        { id: 2, name: 'Banana' },
        { id: 3, name: 'Cherry' },
        { id: 4, name: 'Date' }
    ];

    return (
        <div>
            <h1>Sibling Communication</h1>
            
            {/* Pass setter to A */}
            <SearchBar onSearch={setQuery} />
            
            {/* Pass state to B */}
            <ProductList products={products} query={query} />
        </div>
    );
}
```

**Execution Flow:**
1. User types "app" in `SearchBar`.
2. `onChange` fires, calling `onSearch("app")`.
3. `onSearch` is actually `setQuery` from `App`.
4. `App` state `query` updates to "app".
5. `App` re-renders.
6. `ProductList` receives new `query` prop ("app").
7. `ProductList` filters products and displays "Apple".

---

## 6. Quick Reference

| Component | Role | Action |
|-----------|------|--------|
| **Parent** | Mediator | Holds State, passes Down |
| **Sibling A** | Sender | Calls callback function |
| **Sibling B** | Receiver | Receives data as prop |

**Key Pattern:**
`Child A` -> `Parent (State)` -> `Child B`

---

## 7. Interview Questions

### Q1: How do you pass data between sibling components in React?
**Answer**: You cannot pass data directly between siblings. You must lift the state up to their closest common ancestor (parent). The parent holds the state and passes it down to the receiving sibling as props, and passes a callback function to the sending sibling to update the state.

### Q2: What is "Lifting State Up"?
**Answer**: It is the process of moving state from a child component to a parent component so that the state can be shared with other children (siblings).

### Q3: Can we use Context API for sibling communication?
**Answer**: Yes, for deeply nested components or avoiding "prop drilling", Context API is suitable. However, for direct siblings, lifting state up is simpler and preferred.

### Q4: Does lifting state cause re-renders?
**Answer**: Yes, when the state in the parent changes, the parent re-renders, which causes all its children (including the siblings) to re-render with the new props.

---

## Navigation

← Previous: [46_Lists_and_Keys.md](./46_Lists_and_Keys.md) | Next: [48_React_Router_v6.md](./48_React_Router_v6.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 10*
