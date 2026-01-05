# React Hooks

## Table of Contents
1. [Introduction](#1-introduction)
2. [useState](#2-usestate)
3. [useEffect](#3-useeffect)
4. [useContext](#4-usecontext)
5. [useRef](#5-useref)
6. [useMemo and useCallback](#6-usememo-and-usecallback)
7. [Custom Hooks](#7-custom-hooks)
8. [Quick Reference](#8-quick-reference)
9. [Interview Questions](#9-interview-questions)

---

## 1. Introduction

### 1.1 What are Hooks?
**Hooks** are functions that let you use state and other React features in functional components. Introduced in React 16.8.

### 1.2 Rules of Hooks
1. Only call hooks at the top level
2. Only call hooks inside React functions
3. Don't call hooks inside loops, conditions, or nested functions

### 1.3 Common Hooks

| Hook | Purpose |
|------|---------|
| useState | Add state to component |
| useEffect | Side effects |
| useContext | Access context |
| useRef | Reference DOM/values |
| useMemo | Memoize expensive calculations |
| useCallback | Memoize functions |

---

## 2. useState

### 2.1 Basic Usage

```jsx
import { useState } from 'react';

function Counter() {
    const [count, setCount] = useState(0);
    
    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={() => setCount(count + 1)}>+</button>
            <button onClick={() => setCount(c => c - 1)}>-</button>
        </div>
    );
}
```

### 2.2 Multiple State Variables

```jsx
function Form() {
    const [name, setName] = useState('');
    const [email, setEmail] = useState('');
    const [age, setAge] = useState(0);
    
    return (
        <form>
            <input value={name} onChange={e => setName(e.target.value)} />
            <input value={email} onChange={e => setEmail(e.target.value)} />
            <input type="number" value={age} onChange={e => setAge(+e.target.value)} />
        </form>
    );
}
```

---

## 3. useEffect

### 3.1 Basic Syntax

```jsx
import { useEffect } from 'react';

useEffect(() => {
    // Effect code
    
    return () => {
        // Cleanup (optional)
    };
}, [dependencies]);
```

### 3.2 Effect Types

```jsx
function Example() {
    // 1. Runs on every render
    useEffect(() => {
        console.log('Every render');
    });
    
    // 2. Runs once on mount
    useEffect(() => {
        console.log('Component mounted');
    }, []);
    
    // 3. Runs when dependency changes
    useEffect(() => {
        console.log('Value changed');
    }, [value]);
    
    // 4. With cleanup
    useEffect(() => {
        const handler = () => console.log('Scroll');
        window.addEventListener('scroll', handler);
        
        return () => {
            window.removeEventListener('scroll', handler);
        };
    }, []);
}
```

### 3.3 Fetching Data

```jsx
function UserProfile({ userId }) {
    const [user, setUser] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);
    
    useEffect(() => {
        const fetchUser = async () => {
            try {
                setLoading(true);
                const response = await fetch(`/api/users/${userId}`);
                const data = await response.json();
                setUser(data);
            } catch (err) {
                setError(err.message);
            } finally {
                setLoading(false);
            }
        };
        
        fetchUser();
    }, [userId]);
    
    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error}</p>;
    
    return <div>{user.name}</div>;
}
```

### 3.4 Cleanup Examples

```jsx
// Timer cleanup
useEffect(() => {
    const timer = setInterval(() => {
        console.log('Tick');
    }, 1000);
    
    return () => clearInterval(timer);
}, []);

// Subscription cleanup
useEffect(() => {
    const subscription = api.subscribe(data => {
        setData(data);
    });
    
    return () => subscription.unsubscribe();
}, []);
```

---

## 4. useContext

### 4.1 Creating Context

```jsx
import { createContext, useContext, useState } from 'react';

// Create context
const ThemeContext = createContext();

// Provider component
function ThemeProvider({ children }) {
    const [theme, setTheme] = useState('light');
    
    const toggleTheme = () => {
        setTheme(t => t === 'light' ? 'dark' : 'light');
    };
    
    return (
        <ThemeContext.Provider value={{ theme, toggleTheme }}>
            {children}
        </ThemeContext.Provider>
    );
}

// Using context
function ThemedButton() {
    const { theme, toggleTheme } = useContext(ThemeContext);
    
    return (
        <button 
            onClick={toggleTheme}
            style={{ background: theme === 'dark' ? '#333' : '#fff' }}
        >
            Toggle Theme
        </button>
    );
}

// App with provider
function App() {
    return (
        <ThemeProvider>
            <ThemedButton />
        </ThemeProvider>
    );
}
```

---

## 5. useRef

### 5.1 DOM Reference

```jsx
import { useRef } from 'react';

function TextInput() {
    const inputRef = useRef(null);
    
    const focusInput = () => {
        inputRef.current.focus();
    };
    
    return (
        <div>
            <input ref={inputRef} type="text" />
            <button onClick={focusInput}>Focus</button>
        </div>
    );
}
```

### 5.2 Mutable Value (No Re-render)

```jsx
function Timer() {
    const countRef = useRef(0);
    const [, forceUpdate] = useState();
    
    useEffect(() => {
        const interval = setInterval(() => {
            countRef.current += 1;
            console.log(countRef.current);
        }, 1000);
        
        return () => clearInterval(interval);
    }, []);
    
    return <p>Check console</p>;
}
```

### 5.3 Previous Value

```jsx
function Counter() {
    const [count, setCount] = useState(0);
    const prevCountRef = useRef();
    
    useEffect(() => {
        prevCountRef.current = count;
    });
    
    return (
        <div>
            <p>Now: {count}, Before: {prevCountRef.current}</p>
            <button onClick={() => setCount(c => c + 1)}>+</button>
        </div>
    );
}
```

---

## 6. useMemo and useCallback

### 6.1 useMemo (Memoize Values)

```jsx
import { useMemo } from 'react';

function ExpensiveComponent({ data }) {
    const processedData = useMemo(() => {
        // Expensive calculation
        return data.map(item => item * 2).filter(item => item > 10);
    }, [data]);  // Only recalculate when data changes
    
    return <div>{processedData.join(', ')}</div>;
}
```

### 6.2 useCallback (Memoize Functions)

```jsx
import { useCallback } from 'react';

function Parent() {
    const [count, setCount] = useState(0);
    
    // Without useCallback: new function on every render
    // With useCallback: same function reference
    const handleClick = useCallback(() => {
        console.log('Clicked');
    }, []);  // Dependencies
    
    return (
        <div>
            <p>{count}</p>
            <Child onClick={handleClick} />
            <button onClick={() => setCount(c => c + 1)}>+</button>
        </div>
    );
}

const Child = React.memo(({ onClick }) => {
    console.log('Child rendered');
    return <button onClick={onClick}>Click</button>;
});
```

---

## 7. Custom Hooks

### 7.1 Creating Custom Hook

```jsx
// useLocalStorage.js
import { useState, useEffect } from 'react';

function useLocalStorage(key, initialValue) {
    const [value, setValue] = useState(() => {
        const stored = localStorage.getItem(key);
        return stored ? JSON.parse(stored) : initialValue;
    });
    
    useEffect(() => {
        localStorage.setItem(key, JSON.stringify(value));
    }, [key, value]);
    
    return [value, setValue];
}

// Usage
function App() {
    const [name, setName] = useLocalStorage('name', '');
    
    return (
        <input 
            value={name} 
            onChange={e => setName(e.target.value)} 
        />
    );
}
```

### 7.2 useFetch Hook

```jsx
function useFetch(url) {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);
    
    useEffect(() => {
        const fetchData = async () => {
            try {
                setLoading(true);
                const response = await fetch(url);
                const json = await response.json();
                setData(json);
            } catch (err) {
                setError(err.message);
            } finally {
                setLoading(false);
            }
        };
        
        fetchData();
    }, [url]);
    
    return { data, loading, error };
}

// Usage
function Users() {
    const { data, loading, error } = useFetch('/api/users');
    
    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error}</p>;
    
    return <ul>{data.map(u => <li key={u.id}>{u.name}</li>)}</ul>;
}
```

---

## 8. Quick Reference

### 8.1 useState

```jsx
const [state, setState] = useState(initial);
setState(newValue);
setState(prev => prev + 1);
```

### 8.2 useEffect

```jsx
useEffect(() => {
    // effect
    return () => { /* cleanup */ };
}, [deps]);
```

### 8.3 useContext

```jsx
const value = useContext(MyContext);
```

### 8.4 useRef

```jsx
const ref = useRef(initialValue);
ref.current = newValue;
```

### 8.5 useMemo/useCallback

```jsx
const memoized = useMemo(() => compute(a, b), [a, b]);
const callback = useCallback(() => fn(a), [a]);
```

---

## 9. Interview Questions

### Q1: What are React Hooks?
**Answer**: Hooks are functions that let you use state and lifecycle features in functional components without writing classes.

### Q2: What is the difference between useEffect with [] and without dependencies?
**Answer**:
- `useEffect(() => {})`: Runs after every render
- `useEffect(() => {}, [])`: Runs only on mount
- `useEffect(() => {}, [dep])`: Runs when dep changes

### Q3: Why do we need cleanup in useEffect?
**Answer**: Cleanup prevents memory leaks by removing event listeners, canceling subscriptions, or clearing timers when component unmounts.

### Q4: What is the difference between useMemo and useCallback?
**Answer**:
- `useMemo`: Memoizes a computed value
- `useCallback`: Memoizes a function reference

### Q5: Can we call hooks conditionally?
**Answer**: No, hooks must be called at the top level, not inside conditions, loops, or nested functions.

### Q6: What is useRef used for?
**Answer**: useRef provides a way to access DOM elements directly and store mutable values that persist across renders without triggering re-renders.

---

## Navigation

← Previous: [42_React_State_and_Props.md](./42_React_State_and_Props.md) | Next: [44_React_Event_Handling.md](./44_React_Event_Handling.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 09-10*
