# React State and Props

## Table of Contents
1. [Introduction](#1-introduction)
2. [useState Hook](#2-usestate-hook)
3. [Props in Depth](#3-props-in-depth)
4. [State vs Props](#4-state-vs-props)
5. [Lifting State Up](#5-lifting-state-up)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 What is State?
**State** is data that changes over time within a component. When state changes, React re-renders the component.

### 1.2 What are Props?
**Props** (properties) are read-only data passed from parent to child components.

### 1.3 Comparison

| Feature | State | Props |
|---------|-------|-------|
| Mutable | Yes | No (read-only) |
| Owned by | Component itself | Parent component |
| Updates | Triggers re-render | Triggers re-render |
| Direction | Internal | Parent → Child |

---

## 2. useState Hook

### 2.1 Basic Syntax

```jsx
import { useState } from 'react';

function Counter() {
    const [count, setCount] = useState(0);
    
    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={() => setCount(count + 1)}>
                Increment
            </button>
        </div>
    );
}
```

### 2.2 Understanding useState

```jsx
const [value, setValue] = useState(initialValue);

// value: current state value
// setValue: function to update state
// initialValue: initial state value
```

### 2.3 Different Data Types

```jsx
// Number
const [count, setCount] = useState(0);

// String
const [name, setName] = useState('');

// Boolean
const [isOpen, setIsOpen] = useState(false);

// Array
const [items, setItems] = useState([]);

// Object
const [user, setUser] = useState({
    name: '',
    email: ''
});
```

### 2.4 Updating State

```jsx
function Example() {
    const [count, setCount] = useState(0);
    
    // Direct update
    const increment = () => {
        setCount(count + 1);
    };
    
    // Functional update (recommended)
    const incrementSafe = () => {
        setCount(prev => prev + 1);
    };
    
    return (
        <button onClick={incrementSafe}>
            Count: {count}
        </button>
    );
}
```

### 2.5 Updating Objects

```jsx
function UserForm() {
    const [user, setUser] = useState({
        name: '',
        email: '',
        age: 0
    });
    
    const updateName = (e) => {
        setUser({
            ...user,  // Spread existing properties
            name: e.target.value  // Update specific property
        });
    };
    
    // Or using functional update
    const updateEmail = (e) => {
        setUser(prev => ({
            ...prev,
            email: e.target.value
        }));
    };
    
    return (
        <form>
            <input value={user.name} onChange={updateName} />
            <input value={user.email} onChange={updateEmail} />
        </form>
    );
}
```

### 2.6 Updating Arrays

```jsx
function TodoList() {
    const [todos, setTodos] = useState([]);
    
    // Add item
    const addTodo = (text) => {
        setTodos([...todos, { id: Date.now(), text }]);
    };
    
    // Remove item
    const removeTodo = (id) => {
        setTodos(todos.filter(todo => todo.id !== id));
    };
    
    // Update item
    const updateTodo = (id, newText) => {
        setTodos(todos.map(todo => 
            todo.id === id ? { ...todo, text: newText } : todo
        ));
    };
    
    return (
        <ul>
            {todos.map(todo => (
                <li key={todo.id}>
                    {todo.text}
                    <button onClick={() => removeTodo(todo.id)}>×</button>
                </li>
            ))}
        </ul>
    );
}
```

---

## 3. Props in Depth

### 3.1 Passing Props

```jsx
// Parent component
function App() {
    const user = { name: 'John', age: 25 };
    
    return (
        <Profile 
            name={user.name}
            age={user.age}
            isAdmin={true}
            onLogout={() => console.log('Logout')}
        />
    );
}

// Child component
function Profile({ name, age, isAdmin, onLogout }) {
    return (
        <div>
            <h2>{name}</h2>
            <p>Age: {age}</p>
            {isAdmin && <span>Admin</span>}
            <button onClick={onLogout}>Logout</button>
        </div>
    );
}
```

### 3.2 Spread Props

```jsx
function App() {
    const props = {
        title: 'Welcome',
        message: 'Hello World',
        type: 'success'
    };
    
    return <Alert {...props} />;
}
```

### 3.3 Children Prop

```jsx
function Container({ children }) {
    return (
        <div className="container">
            {children}
        </div>
    );
}

// Usage
<Container>
    <h1>Title</h1>
    <p>Content goes here</p>
</Container>
```

### 3.4 Callback Props

```jsx
// Parent
function Parent() {
    const handleMessage = (msg) => {
        console.log('Received:', msg);
    };
    
    return <Child onSendMessage={handleMessage} />;
}

// Child
function Child({ onSendMessage }) {
    return (
        <button onClick={() => onSendMessage('Hello!')}>
            Send Message
        </button>
    );
}
```

---

## 4. State vs Props

### 4.1 Key Differences

| Aspect | State | Props |
|--------|-------|-------|
| Source | Created in component | Passed from parent |
| Mutability | Mutable via setState | Immutable |
| Purpose | Component's memory | Configure component |
| Changes | Re-renders component | Re-renders component |

### 4.2 When to Use

**Use State When:**
- Data changes over time
- User interaction changes data
- Data is component-specific

**Use Props When:**
- Passing data to child
- Configuring child behavior
- Sharing data between components

---

## 5. Lifting State Up

### 5.1 Concept
When multiple components need to share state, lift the state to their closest common ancestor.

### 5.2 Example

```jsx
// Parent manages shared state
function TemperatureConverter() {
    const [celsius, setCelsius] = useState(0);
    
    const fahrenheit = (celsius * 9/5) + 32;
    
    return (
        <div>
            <TemperatureInput
                scale="Celsius"
                value={celsius}
                onChange={setCelsius}
            />
            <TemperatureInput
                scale="Fahrenheit"
                value={fahrenheit}
                onChange={(f) => setCelsius((f - 32) * 5/9)}
            />
        </div>
    );
}

// Child component
function TemperatureInput({ scale, value, onChange }) {
    return (
        <div>
            <label>{scale}:</label>
            <input
                type="number"
                value={value}
                onChange={(e) => onChange(Number(e.target.value))}
            />
        </div>
    );
}
```

### 5.3 Data Flow

```
            ┌──────────────────┐
            │  Parent (State)  │
            └────────┬─────────┘
                     │ Props ↓
        ┌────────────┼────────────┐
        ↓            ↓            ↓
   ┌─────────┐  ┌─────────┐  ┌─────────┐
   │ Child 1 │  │ Child 2 │  │ Child 3 │
   └─────────┘  └─────────┘  └─────────┘
        │ Callback ↑
        └──────────┘
```

---

## 6. Quick Reference

### 6.1 useState

```jsx
const [value, setValue] = useState(initial);

// Update
setValue(newValue);
setValue(prev => prev + 1);
```

### 6.2 Props

```jsx
// Parent
<Child name="John" age={25} />

// Child
function Child({ name, age }) {
    return <p>{name} is {age}</p>;
}
```

### 6.3 Updating State

```jsx
// Objects
setUser({ ...user, name: 'Jane' });

// Arrays - Add
setItems([...items, newItem]);

// Arrays - Remove
setItems(items.filter(i => i.id !== id));

// Arrays - Update
setItems(items.map(i => i.id === id ? updated : i));
```

---

## 7. Interview Questions

### Q1: What is the difference between state and props?
**Answer**: State is mutable data managed within a component, while props are read-only data passed from parent to child. State changes trigger re-renders.

### Q2: Why should we use functional updates in setState?
**Answer**: When updates depend on previous state, functional updates ensure you're working with the latest state value, avoiding race conditions.

### Q3: Can we modify props directly?
**Answer**: No, props are read-only. To change data from child to parent, use callback functions passed as props.

### Q4: What is "lifting state up"?
**Answer**: Moving shared state to the closest common ancestor of components that need it, then passing state and updaters as props.

### Q5: Why do we spread objects when updating state?
**Answer**: React state updates must be immutable. Spreading creates a new object instead of mutating the existing one.

### Q6: What happens when state changes?
**Answer**: React re-renders the component and its children. The Virtual DOM diff determines what actually needs updating in the real DOM.

---

## Navigation

← Previous: [41_React_Introduction.md](./41_React_Introduction.md) | Next: [43_React_Hooks.md](./43_React_Hooks.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 09-10*
