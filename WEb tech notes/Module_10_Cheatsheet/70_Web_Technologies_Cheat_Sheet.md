# Web Technologies Master Cheat Sheet & Interview Reference

## Table of Contents
1.  [HTML5 & CSS3 Quick Ref](#1-html5--css3-quick-ref)
2.  [JavaScript (ES6+) Quick Ref](#2-javascript-es6-quick-ref)
3.  [Node.js & Express Quick Ref](#3-nodejs--express-quick-ref)
4.  [React & Redux Quick Ref](#4-react--redux-quick-ref)
5.  [jQuery Quick Ref](#5-jquery-quick-ref)
6.  [MASTER INTERVIEW Q&A INDEX](#6-master-interview-qa-index)

---

## 1. HTML5 & CSS3 Quick Ref

| Feature | Description | Code Snippet |
| :--- | :--- | :--- |
| **DocType** | HTML5 Declaration | `<!DOCTYPE html>` |
| **Semantic** | `<header>`, `<footer>`, `<nav>`, `<section>` | `<article>Content</article>` |
| **Storage** | **LocalStorage** (Persistent), **SessionStorage** (Session) | `localStorage.setItem('k','v')` |
| **Canvas** | Scriptable 2D Drawing | `ctx.fillRect(0,0,10,10)` |
| **Flexbox** | 1D Layout Model | `display: flex; justify-content: center;` |
| **Grid** | 2D Layout Model | `display: grid; grid-template-columns: 1fr 1fr;` |
| **Selectors** | Class (`.`), ID (`#`), Child (`>`), Descendant (` `) | `.class > p { color: red; }` |

---

## 2. JavaScript (ES6+) Quick Ref

| Concept | Description | Example |
| :--- | :--- | :--- |
| **Variables** | `let` (block), `const` (block, immutable ref), `var` (function) | `const PI = 3.14;` |
| **Arrows** | Concise function syntax, lexical `this` | `const add = (a,b) => a+b;` |
| **Destructuring** | Unpack values from arrays/objects | `const {name} = user;` |
| **Spread/Rest** | `...` Expand array / Collect args | `[...arr, 4]`, `function(...args){}` |
| **Promises** | Async value representation | `fetch().then(res => ...)` |
| **Async/Await** | Syntactic sugar for Promises | `const res = await fetch();` |
| **Classes** | OOP Syntax (Sugar over prototypes) | `class Car { constructor(){} }` |
| **Modules** | `import` / `export` | `export default App;` |

---

## 3. Node.js & Express Quick Ref

| Concept | Command / Note |
| :--- | :--- |
| **REPL** | Read-Eval-Print-Loop (Console) |
| **Global Objs** | `process`, `__dirname`, `module`, `require`, `Buffer` |
| **Core Modules**| `fs`, `http`, `path`, `events`, `os` |
| **NPM** | `npm init -y`, `npm i [pkg]` |
| **Server** | `const server = http.createServer((req, res) => ...)` |
| **Express App** | `const app = express(); app.listen(3000);` |
| **Middleware** | `app.use((req, res, next) => { next(); })` |
| **Routing** | `app.get('/', handler)`, `router.post('/login', handler)` |
| **Streams** | Readable, Writable, Duplex, Transform |
| **Events** | `emitter.on('event', cb)`, `emitter.emit('event')` |

---

## 4. React & Redux Quick Ref

| Concept | Description | Snippet |
| :--- | :--- | :--- |
| **Component** | Functional (Stateless/Hook) or Class | `function App() { return <h1>Hi</h1> }` |
| **JSX** | HTML-like syntax in JS | `<div className="box"></div>` |
| **Props** | Read-only inputs from parent | `function Welcome(props) { ... }` |
| **State** | Mutable internal data | `const [count, setCount] = useState(0)` |
| **Effect** | Side-effects (Mount/Update) | `useEffect(() => { ... }, [deps])` |
| **Ref** | Direct DOM access / Persistence | `const inputRef = useRef(null)` |
| **Context** | Global state without props drilling | `const val = useContext(MyContext)` |
| **Redux Store** | Single Source of Truth | `createStore(reducer)` |
| **Reducer** | `(state, action) => newState` | `switch(action.type) { ... }` |
| **Action** | Object describing change | `{ type: 'ADD', payload: 1 }` |
| **Dispatch** | Send action to reducer | `dispatch({ type: 'ADD' })` |
| **Provider** | Connects Store to React | `<Provider store={store}><App /></Provider>` |

---

## 5. jQuery Quick Ref

| Feature | Syntax | Example |
| :--- | :--- | :--- |
| **Ready** | `$(document).ready(fn)` | `$(function() { ... })` |
| **ID Select** | `$('#id')` | `$('#btn')` |
| **Class Select**| `$('.class')` | `$('.active')` |
| **Event** | `.on('event', fn)` | `$('#btn').click(fn)` |
| **Traverse** | `.parent()`, `.children()`, `.find()` | `$('ul').find('li')` |
| **Manipulate** | `.html()`, `.text()`, `.val()`, `.css()` | `$('#div').text('Hello')` |
| **Classes** | `.addClass()`, `.removeClass()` | `$(this).addClass('active')` |
| **AJAX** | `$.ajax({ url, method, success })` | `$.get('url', cb)` |

---

## 6. MASTER INTERVIEW Q&A INDEX

*Condensed answers for every question covered in Modules.*

### HTML5 & CSS
*   **HTML5 Features**: Canvas, Audio/Video, LocalStorage, Semantic Tags.
*   **Doctype**: Tells browser version (HTML5 standards mode).
*   **Canvas vs SVG**: Canvas is pixel-based (JS), SVG is vector-based (XML).
*   **Storage**: Session (Tab), Local (Permanent), Cookies (Server sent).

### JavaScript
*   **JS vs JScript**: JS (Netscape/Standard), JScript (Microsoft IE).
*   **`==` vs `===`**: Loose vs Strict equality (checks value & type).
*   **Closure**: Function remembering outer scope variables even after execution.
*   **Hoisting**: Vars/Functions moved to top. `var` is undefined, `let/const` in TDZ.
*   **Data Types**: String, Number, Boolean, Null, Undefined, Symbol, BigInt, Object.
*   **EventLoop**: Call Stack -> Web APIs -> Queue -> Loop -> Stack.
*   **BOM vs DOM**: Browser Object Model (Window, Nav) vs Document Object Model (HTML Tree).

### Node.js & Express
*   **What is Node?**: JS Runtime on V8. Single-threaded, Non-blocking I/O.
*   **Event Loop**: Handles async callbacks. Phases: Timers, IO, Poll, Check, Close.
*   **Middleware**: Functions executing between request and response (`req, res, next`).
*   **Streams**: Efficient data handling (Chunks). Pipe connects streams.
*   **NextTick vs SetImmediate**: NextTick (Microtask, before IO), SetImmediate (Macrotask, after IO).

### React.js
*   **VDOM**: Lightweight copy of DOM. React diffs VDOM to update Real DOM (Reconciliation).
*   **Hooks**: `useState` (State), `useEffect` (Lifecycle), `useRef` (DOM), `useContext` (Global).
*   **Keys**: Unique ID for optimization in Lists to identify changed items.
*   **Props vs State**: Props (External, Immutable), State (Internal, Mutable).
*   **HOC**: Function taking component -> returning new component.
*   **Controlled Comp**: React controls state (`value={state}`).

### Redux
*   **Principles**: Single Source, Read-only State, Pure Reducers.
*   **Data Flow**: Dispatch -> Action -> Reducer -> Store -> View.
*   **Thunk**: Middleware for async actions (function returning function).
*   **Connect**: HOC to bind Store state/dispatch to Component props.

---

*[End of Cheat Sheet]*
