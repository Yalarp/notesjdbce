# Rendering Lists and Keys

## Table of Contents
1. [Introduction](#1-introduction)
2. [Rendering Multiple Components](#2-rendering-multiple-components)
3. [The `key` Prop](#3-the-key-prop)
4. [Keys Anti-Pattern](#4-keys-anti-pattern)
5. [Practical Example](#5-practical-example)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 Rendering Lists in React
In React, you transform arrays of data into arrays of elements using JavaScript's map() function. You can run `map()` over an array and return an element (often a JSX element) for each item.

### 1.2 Unordered List Example

```jsx
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);

return <ul>{listItems}</ul>;
```

---

## 2. Rendering Multiple Components

You typically render lists inside a component.

```jsx
function NumberList({ numbers }) {
    return (
        <ul>
            {numbers.map((number) => (
                <li key={number.toString()}>
                    {number}
                </li>
            ))}
        </ul>
    );
}
```

---

## 3. The `key` Prop

### 3.1 Why Keys are Important?
Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity.

### 3.2 Key Rules
1. **Unique**: Keys must be unique among siblings. They don't need to be globally unique.
2. **Stable**: Keys must not change over time (don't use `Math.random()`).
3. **String/Number**: Best to use IDs from your data string or number.

### 3.3 Picking a Key
The best key is a unique ID from your data (e.g., database ID).

```jsx
// Good
todos.map((todo) => <li key={todo.id}>{todo.text}</li>);
```

---

## 4. Keys Anti-Pattern

### 4.1 Using Index as Key
Using the array index as a key is **not recommended** if the order of items may change.

**Bad Example:**
```jsx
// Avoid this if list can be reordered
items.map((item, index) => (
    <li key={index}>{item.name}</li>
));
```

**Why it's bad:**
- If an item is inserted at the beginning, all indexes shift.
- React thinks all items changed, leading to full re-render.
- Can cause issues with component state (e.g., unchecked checkboxes checking wrong item).

**When is it okay?**
- List and items are static (never change).
- List is never filtered or reordered.
- Items represent no own state (stateless).

---

## 5. Practical Example

This example demonstrates rendering a dynamic table of employees fetching from an API.

**Original Code (from `Listproducts.jsx`):**
```jsx
{employees.map((emp) => (
  <tr
    key={emp.id}
    style={rowHover}
    onMouseEnter={(e) => (e.currentTarget.style.background = "#f2f8ff")}
    onMouseLeave={(e) => (e.currentTarget.style.background = "white")}
  >
    <td style={tdStyle}>{emp.id}</td>
    <td style={tdStyle}>{emp.name}</td>
    <td style={tdStyle}>{emp.email}</td>
    <td style={tdStyle}>{emp.departmentId}</td>

    <td style={tdStyle}>
      <Link to={`/emp/${emp.id}`}>Display</Link>
    </td>
    <td style={tdStyle}>
      <Link to={`/empup/${emp.id}`}>Edit</Link>
    </td>
    <td style={tdStyle}>
      <Link to={`/empdel/${emp.id}`}>Delete</Link>
    </td>
  </tr>
))}
```

**Line-by-Line Explanation:**
| Line | Code | Explanation |
|------|------|-------------|
| 1 | `{employees.map((emp) => (` | Iterating over the `employees` array. |
| 3 | `key={emp.id}` | Assigning a unique ID as the key (Best Practice). |
| 116 | `<td...>{emp.id}</td>` | Displaying employee data. |
| 122 | `<Link...>` | Creating links for each row item. |

**Execution Flow:**
1. Component receives `employees` array (e.g., `[{id: 1, name: 'Alice'}, {id: 2, name: 'Bob'}]`).
2. `map()` runs for each user.
3. React creates a `<tr>` element for each user.
4. React assigns the `key` to each `<tr>` internally.
5. If the array updates (e.g., sorting), React uses keys to reorder existing DOM nodes instead of recreating them.

---

## 6. Quick Reference

| Concept | Description |
|---------|-------------|
| `map()` | Method used to transform data array to element array |
| `key` | Special string attribute for identifying items |
| `key={id}` | Recommended (Database ID) |
| `key={index}` | Discouraged (Use only for static lists) |
| `Math.random()` | **NEVER** use as key (causes full re-render) |

---

## 7. Interview Questions

### Q1: Why do we need keys in React lists?
**Answer**: Keys help React identify which items have changed, are added, or are removed. This allows React to optimize rendering by recycling existing DOM elements instead of destroying and recreating them during updates.

### Q2: Can we use array index as a key?
**Answer**: It is possible but generally discouraged. It can lead to performance issues and bugs with component state if the list items can be reordered, filtered, or inserted/deleted. It is only safe for static lists.

### Q3: Do keys need to be globally unique?
**Answer**: No, keys only need to be unique among siblings (items in the same array). Different lists can use the same keys.

### Q4: How do you render a list of components?
**Answer**: By using `array.map()` inside curly braces `{}` within the JSX.
```jsx
{items.map(item => <MyComponent key={item.id} data={item} />)}
```

---

## Navigation

← Previous: [45_Event_Handling_React.md](./45_Event_Handling_React.md) | Next: [47_Sibling_Data_Passing.md](./47_Sibling_Data_Passing.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 09*
