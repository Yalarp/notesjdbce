# Web Programming Technologies Cheat Sheet

## Table of Contents
1. [HTML5 & CSS3](#1-html5--css3)
2. [JavaScript (ES6+)](#2-javascript-es6)
3. [Node.js & Express](#3-nodejs--express)
4. [React.js](#4-reactjs)
5. [Common Commands](#5-common-commands)

---

## 1. HTML5 & CSS3

### HTML Structural Tags
- `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`
- `<form action method>`, `<input type="text|password|email|number|date">`
- `<select><option>...</option></select>`
- `<table border> <tr> <th> <td>`

### CSS Selectors
- **ID**: `#id`
- **Class**: `.class`
- **Element**: `div`
- **Descendant**: `div p` (all p inside div)
- **Child**: `div > p` (direct child)
- **Pseudo**: `:hover`, `:nth-child(n)`, `:first-child`

### CSS Box Model
- `Content` -> `Padding` -> `Border` -> `Margin`
- `box-sizing: border-box` (Padding/Border included in width)

### Flexbox
- `display: flex`
- `justify-content: center | space-between | flex-start`
- `align-items: center | stretch`
- `flex-direction: row | column`

---

## 2. JavaScript (ES6+)

### Variables
- `var`: Function scope, hoisted.
- `let`: Block scope.
- `const`: Block scope, constant reference.

### Functions
```javascript
// Function Declaration
function add(a, b) { return a + b; }

// Arrow Function
const add = (a, b) => a + b;
```

### Async Operations
```javascript
// Promise
fetch(url).then(res => res.json()).then(data => console.log(data));

// Async/Await
async function getData() {
    const res = await fetch(url);
    const data = await res.json();
}
```

### DOM Manipulation
- `document.getElementById('id')`
- `document.querySelector('.class')`
- `element.addEventListener('click', () => {})`
- `element.innerHTML = 'New Content'`

---

## 3. Node.js & Express

### File System
```javascript
const fs = require('fs');
fs.readFile('file.txt', 'utf8', (err, data) => {});
fs.writeFileSync('file.txt', 'content');
```

### Simple Express Server
```javascript
const express = require('express');
const app = express();
app.use(express.json()); // Middleware

app.get('/', (req, res) => res.send('Hello'));
app.post('/user', (req, res) => {
    console.log(req.body);
    res.json({ status: 'ok' });
});

app.listen(3000);
```

### Middleware
```javascript
app.use((req, res, next) => {
    console.log('Time:', Date.now());
    next();
});
```

---

## 4. React.js

### Components
```jsx
// Functional Component
function Welcome({ name }) {
    return <h1>Hello, {name}</h1>;
}
```

### Hooks
-   `useState`: `const [count, setCount] = useState(0);`
-   `useEffect`:
    ```jsx
    useEffect(() => {
        // Runs on mount
        return () => { /* Cleanup */ };
    }, []); // Dependency array
    ```

### Routing (v6)
```jsx
<Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about/:id" element={<About />} />
</Routes>
```
-   `useNavigate()`: `const nav = useNavigate(); nav('/home');`
-   `useParams()`: `const { id } = useParams();`

### Redux Toolkit
-   `createSlice({ name, initialState, reducers })`
-   `configureStore({ reducer })`
-   `useSelector(state => state.val)`
-   `useDispatch()`

---

## 5. Common Commands

| Command | Description |
|---------|-------------|
| `npm init -y` | Initialize project |
| `npm install pkg` | Install package |
| `npm i -D pkg` | Install dev dependency |
| `npm start` | Run start script |
| `node app.js` | Run Node file |
| `npx create-react-app .` | Create React App |
| `npx vite@latest` | Create Vite App (Faster) |

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Summary*
