# Forms in React

## Table of Contents
1. [Introduction](#1-introduction)
2. [Controlled Components](#2-controlled-components)
3. [Handling Multiple Inputs](#3-handling-multiple-inputs)
4. [Form Submission](#4-form-submission)
5. [Validation](#5-validation)
6. [Practical Example](#6-practical-example)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 HTML vs React Forms
In HTML, form elements (`<input>`, `<textarea>`, `<select>`) maintain their own state. In React, mutable state is properly kept in the `state` property of components, and updated only via `setState()`.

### 1.2 Controlled Components
A form element whose value is controlled by React in this way is called a **"controlled component"**. React is the "single source of truth".

---

## 2. Controlled Components

### 2.1 Basic Pattern

1.  **State**: Create state to hold the input value.
2.  **Value Prop**: Pass state to the input's `value` prop.
3.  **OnChange**: Update state in the `onChange` handler.

```jsx
function NameForm() {
    const [name, setName] = useState('');

    return (
        <input 
            value={name} 
            onChange={(e) => setName(e.target.value)} 
        />
    );
}
```

---

## 3. Handling Multiple Inputs

Instead of creating separate state and handlers for each input, you can use a single object state and a generic handler.

### 3.1 Generic Handler

```jsx
const [inputs, setInputs] = useState({});

const handleChange = (event) => {
    const name = event.target.name;
    const value = event.target.value;
    
    setInputs(values => ({...values, [name]: value}));
}
```

### 3.2 Usage

```jsx
<input 
    name="username" 
    value={inputs.username || ""} 
    onChange={handleChange} 
/>
<input 
    name="age" 
    value={inputs.age || ""} 
    onChange={handleChange} 
/>
```

---

## 4. Form Submission

Always prevent the default browser behavior (page reload) using `event.preventDefault()`.

```jsx
const handleSubmit = (event) => {
    event.preventDefault();
    // Submit logic here
}

<form onSubmit={handleSubmit}>...</form>
```

---

## 5. Validation

Simple validation can be done in the submit handler or interactively in the change handler.

```jsx
if (!formData.email.includes('@')) {
    setError('Invalid email');
    return;
}
```

---

## 6. Practical Example

This example demonstrates a complete "Create Employee" form with multiple inputs, validation, and API submission.

**Original Code (from `CreateEmp.jsx`):**
```jsx
// imports...
export default function CreateEmp() {
    // 1. Single state object for form data
    const [employee, setEmployee] = useState({name:"", email:"", departmentId:""});
    const [isSubmitting, setIsSubmitting] = useState(false);
    const navigate = useNavigate();

    // 2. Generic Change Handler
    const handleChange = (event) => {
        const { name, value } = event.target;
        // Update specific field while keeping others
        setEmployee((prev) => ({...prev, [name]: value}));
    }

    // 3. Submit Handler
    const handleSubmit = async (event) => {
        event.preventDefault(); // Stop reload

        // Validation
        if (!employee.name || !employee.email) {
            alert("name and email are required");
            return;
        }

        try {
            setIsSubmitting(true);
            const response = await fetch(".../api/Employee", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify(employee),
            });
            if (!response.ok) throw new Error("Failed");
            navigate("/");
        } catch (error) {
            console.error(error);
            alert("something went wrong!");
        } finally {
            setIsSubmitting(false);
        }
    }

    return (
        <form onSubmit={handleSubmit}>
            <input 
                name="name" 
                value={employee.name} 
                onChange={handleChange} 
                placeholder="Name" 
            />
            <input 
                name="email" 
                value={employee.email} 
                onChange={handleChange} 
                placeholder="Email" 
            />
            <input 
                name="departmentId" 
                value={employee.departmentId} 
                onChange={handleChange} 
                placeholder="Department" 
            />
            <button type="submit" disabled={isSubmitting}>
                {isSubmitting ? "Submitting..." : "Create Employee"}
            </button>
        </form>
    );
}
```

**Execution Flow:**
1. Form renders with empty inputs (state is empty).
2. User types in "Name". `handleChange` updates `employee.name`. React re-renders input with new value.
3. User clicks Submit. `handleSubmit` runs.
4. `preventDefault` stops reload.
5. Validation checks pass.
6. `fetch` sends POST request with JSON data.
7. On success, `navigate("/")` redirects user.

---

## 7. Quick Reference

### 7.1 Controlled Input Checklist
1. `value={state}`
2. `onChange={handler}`
3. Initialize state (don't use `null`, use `""`).

### 7.2 Updating Object State
```jsx
setUser(prev => ({ ...prev, [name]: value }))
```

### 7.3 `textarea` and `select`
In React, they work similarly to `input`.

```jsx
<textarea value={text} onChange={handleChange} />

<select value={selected} onChange={handleChange}>
    <option value="A">A</option>
</select>
```

---

## 8. Interview Questions

### Q1: What is a controlled component?
**Answer**: A component where React controls the value of the form element via state. The input's value is always driven by the React state.

### Q2: How do you handle multiple inputs with one handler?
**Answer**: By giving each input a `name` attribute matching the state property key, and using `e.target.name` to update the corresponding state field dynamically using computed property names: `[name]: value`.

### Q3: What is the alternative to controlled components?
**Answer**: **Uncontrolled components**, where form data is handled by the DOM itself. You use a `ref` to access form values when needed.

### Q4: Why do you need `e.preventDefault()` on form submit?
**Answer**: To prevent the browser's default behavior, which is to reload the page or send a standard GET/POST request, breaking the Single Page Application experience.

---

## Navigation

← Previous: [49_Route_Parameters_and_Hooks.md](./49_Route_Parameters_and_Hooks.md) | Next: [51_Protected_Routes_and_Context.md](../Module_07_Advanced_React/51_Protected_Routes_and_Context.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 10*
