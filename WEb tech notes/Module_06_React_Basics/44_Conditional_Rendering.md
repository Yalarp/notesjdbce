# Conditional Rendering in React

## Table of Contents
1. [Introduction](#1-introduction)
2. [Rendering Approaches](#2-rendering-approaches)
3. [Good Practices](#3-good-practices)
4. [Practical Example](#4-practical-example)
5. [Quick Reference](#5-quick-reference)
6. [Interview Questions](#6-interview-questions)

---

## 1. Introduction

### 1.1 What is Conditional Rendering?
Conditional rendering in React allows you to render different components or elements based on certain conditions (like state, props, or logic). It works the same way conditions work in JavaScript using `if` statements, ternary operators, and logical operators.

### 1.2 Purpose
- Show/hide elements (e.g., loading spinners, error messages)
- Toggle features (e.g., login/logout buttons)
- Render different views based on data

---

## 2. Rendering Approaches

### 2.1 Using `if` Statements
The most basic way is to use JavaScript `if` statements inside the component function to return different JSX blocks.

```jsx
function UserGreeting({ isLoggedIn }) {
    if (isLoggedIn) {
        return <h1>Welcome back!</h1>;
    }
    return <h1>Please sign in.</h1>;
}
```

### 2.2 Ternary Operator (`? :`)
Used for inline conditional rendering. Concise and commonly used for switching between two elements.

```jsx
// Syntax: condition ? trueElement : falseElement

function LoginButton({ isLoggedIn }) {
    return (
        <div>
            {isLoggedIn ? (
                <LogoutButton />
            ) : (
                <LoginButton />
            )}
        </div>
    );
}
```

### 2.3 Logical AND Operator (`&&`)
Used when you want to render something **only if the condition is true**, otherwise render nothing.

```jsx
// Syntax: condition && element

function Mailbox({ unreadMessages }) {
    return (
        <div>
            <h1>Hello!</h1>
            {unreadMessages.length > 0 && (
                <h2>
                    You have {unreadMessages.length} unread messages.
                </h2>
            )}
        </div>
    );
}
```

### 2.4 Nullish Coalescing (`??`)
Useful for checking if a value is `null` or `undefined` and providing a fallback.

```jsx
function Bio({ text }) {
    return <p>{text ?? "Loading..."}</p>;
}
```

### 2.5 Preventing Rendering (`return null`)
To hide a component completely, return `null`.

```jsx
function WarningBanner({ warn }) {
    if (!warn) {
        return null;
    }

    return <div className="warning">Warning!</div>;
}
```

---

## 3. Good Practices

### 3.1 Don't Put Numbers on the Left of `&&`
JavaScript evaluates `0` as falsy, but React renders the number `0`.

**Bad:**
```jsx
{count && <h1>Messages: {count}</h1>}
// If count is 0, renders "0"
```

**Good:**
```jsx
{count > 0 && <h1>Messages: {count}</h1>}
// If count is 0, renders nothing
```

### 3.2 Extract Complex Logic
If conditions are complex, extract them into a variable or a helper function.

```jsx
function Dashboard({ user }) {
    const showAdminControls = user.isAdmin && user.isActive;

    return (
        <div>
            {showAdminControls && <AdminPanel />}
        </div>
    );
}
```

---

## 4. Practical Example

This example demonstrates handling asynchronous data loading using conditional rendering approaches.

**Original Code (from `Page.jsx`):**
```jsx
import { useState, useEffect } from 'react';
import { fetchBio } from './api.js';

export default function Page() {
  const [person, setPerson] = useState('Alice');
  const [bio, setBio] = useState(null);

  useEffect(() => {
    let ignore = false;
    setBio(null);
    fetchBio(person).then(result => {
      if (!ignore) {
        setBio(result);
      }
    });
    return () => {
      ignore = true;
    }
  }, [person]);

  return (
    <>
      <select
        value={person}
        onChange={e => {
          setPerson(e.target.value);
        }}
      >
        <option value="Alice">Alice</option>
        <option value="Bob">Bob</option>
        <option value="Taylor">Taylor</option>
      </select>
      <hr />
      <p><i>{bio ?? 'Loading...'}</i></p>
    </>
  );
}
```

**Line-by-Line Explanation:**
| Line | Code | Explanation |
|------|------|-------------|
| 1-2 | Imports | Import hooks and API function. |
| 5 | `const [person...]` | State for selected person (default 'Alice'). |
| 6 | `const [bio...]` | State for bio text (default null). |
| 8-19 | `useEffect` | Fetches bio when `person` changes. |
| 10 | `setBio(null)` | Resets bio to null while loading new data. |
| 34 | `{bio ?? 'Loading...'}` | **Conditional Rendering**: Displays `bio` if it exists. If `bio` is null/undefined, displays "Loading...". |

**Execution Flow:**
1. Component mounts, `person` is 'Alice', `bio` is null.
2. `useEffect` runs, calls `fetchBio`.
3. Render: Displays dropdown and "Loading..." (because `bio` is null).
4. `fetchBio` resolves, `setBio` updates state.
5. Re-render: Displays dropdown and "This is Alice's bio.".
6. User selects 'Bob'. `setPerson` updates state.
7. Re-render: `bio` is still Alice's bio momentarily? No, `useEffect` will trigger.
   - *Wait, logic check:* `setPerson` triggers re-render 1. `useEffect` runs. `setBio(null)` triggers re-render 2.
   - So effectively, it shows "Loading..." again until response comes.

---

## 5. Quick Reference

| Approach | Syntax | Use Case |
|----------|--------|----------|
| **If/Else** | `if (cond) return <A/> else return <B/>` | Component-level logic |
| **Ternary** | `cond ? <A/> : <B/>` | Inline toggle between two |
| **Logical AND** | `cond && <A/>` | Show something or nothing |
| **Nullish** | `val ?? fallback` | Handle null/undefined values |
| **Return Null** | `return null` | Hide component completely |

---

## 6. Interview Questions

### Q1: Can I use `if-else` inside JSX?
**Answer**: No, strict `if-else` statements do not work inside JSX `{}` blocks because JSX is syntactic sugar for function calls, and `if` is a statement, not an expression. Use ternary operators or logical `&&` instead.

### Q2: What is the difference between `&&` and ternary `? :`?
**Answer**:
- `&&`: Renders the element if condition is true, nothing if false. (Be careful with 0).
- `? :`: Renders one element if true, and a different element (or null) if false.

### Q3: Why does `{count && <Component/>}` render "0" when count is 0?
**Answer**: JavaScript evaluates `0 && anything` as `0`. React renders the number `0` in the DOM. To fix this, force a boolean check using `count > 0 && ...` or `!!count && ...`.

### Q4: How do you hide a component?
**Answer**: By returning `null` from its render function (or functional component body).

---

## Navigation

← Previous: [43_React_Hooks.md](./43_React_Hooks.md) | Next: [45_Event_Handling_React.md](./45_Event_Handling_React.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 09*
