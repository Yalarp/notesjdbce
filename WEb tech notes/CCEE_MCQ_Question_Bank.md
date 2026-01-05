# CCEE – Complete MCQ Question Bank (150 Questions)

## Module 1: JavaScript Fundamentals
### Easy
### Q1. Which of the following is NOT a primitive data type in JavaScript?
A. String  
B. Boolean  
C. Symbol  
D. Array  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** D  

**Explanation:**  
In JavaScript, Arrays are technically objects (Non-primitive). Primitives include String, Number, Boolean, Undefined, Null, Symbol, and BigInt.
</details>

### Q2. What keyword is used to declare a block-scoped variable that cannot be reassigned?
A. var  
B. let  
C. const  
D. static  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`const` declares a block-scoped variable that must be initialized immediately and cannot be reassigned. `let` is block-scoped but reassignable.
</details>

### Q3. What is the result of `typeof null` in JavaScript?
A. "null"  
B. "undefined"  
C. "object"  
D. "number"  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
This is a known legacy definition in JavaScript; `typeof null` returns "object".
</details>

### Medium
### Q4. What is the output of the following code?
```javascript
console.log("5" - 3);
```
A. "53"  
B. 2  
C. NaN  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The `-` operator triggers numeric conversion. The string "5" is converted to the number 5, and 5 - 3 = 2. (Unlike `+` which would concatenate).
</details>

### Q5. Which statement correctly converts a string "123.45" to a number in JavaScript?
A. `parseFloat("123.45")`  
B. `toNumber("123.45")`  
C. `Integer.parse("123.45")`  
D. `String.toNumber("123.45")`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`parseFloat()` is the standard global function to parse a string argument and return a floating-point number.
</details>

### Hard
### Q6. What is the output?
```javascript
let a = 10;
{
  let a = 20;
  console.log(a);
}
console.log(a);
```
A. 20 20  
B. 10 10  
C. 20 10  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`let` is block-scoped. The inner `a` (20) shadows the outer `a` only within the block. Outside the block, `a` remains 10.
</details>

---

## Module 2: Advanced JavaScript (DOM & Objects)
### Easy
### Q7. Which method allows you to select an element by its ID?
A. `document.querySelector()`  
B. `document.getElementById()`  
C. `document.getElementID()`  
D. `window.selectID()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`document.getElementById('id')` is the specific method for selecting a single element by its ID attribute.
</details>

### Q8. Which Window method is used to open a new browser tab or window?
A. `window.create()`  
B. `window.new()`  
C. `window.open()`  
D. `document.open()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`window.open(url, target)` loads a resource into a new or existing browsing context (tab or window).
</details>

### Medium
### Q9. What will the following code output?
```javascript
function sayHello() {
  console.log(this.name);
}
const obj = { name: "Alice" };
sayHello.call(obj);
```
A. undefined  
B. null  
C. "Alice"  
D. ""  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`call()` invokes the function with a specified `this` context. Here, `sayHello` is called with `obj` as `this`, so `this.name` is "Alice".
</details>

### Q10. What is a "Closure" in JavaScript?
A. A function that has finished executing.  
B. A function bundled with its lexical environment/scope.  
C. A method to close a browser window.  
D. An error when variable is not defined.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
A closure gives a function access to its outer scope's variable environment, even after the outer function has returned.
</details>

### Hard
### Q11. Identify the output:
```javascript
for (var i = 1; i <= 3; i++) {
  setTimeout(() => console.log(i), 100);
}
```
A. 1 2 3  
B. 1 2 3 4  
C. 4 4 4  
D. 3 3 3  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`var` is function-scoped (or global here), not block-scoped. By the time `setTimeout` callbacks run, the loop has finished and `i` has incremented to 4.
</details>

### Q12. How does the Event Loop handle promises compared to `setTimeout`?
A. Promises and timeouts are in the same queue.  
B. Promises go to the Microtask Queue; Timeouts go to the Macrotask (Callback) Queue.  
C. Timeouts are high priority.  
D. Promises are executed synchronously.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Promises use the Microtask Queue, which has higher priority and is processed immediately after the current script/stack empties, before the Macrotask (setTimeout) Queue.
</details>

---

## Module 3: ES6 & Asynchronous Programming
### Easy
### Q13. Which ES6 syntax allows unpacking values from arrays or objects into properties?
A. Spread Operator  
B. Rest Parameter  
C. Destructuring  
D. Cloning  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Destructuring assignment (`const {name} = obj;`) unpacks values from data structures into distinct variables.
</details>

### Q14. What does the `...` operator do in `function sum(...nums) {}`?
A. Spreads array  
B. Collects arguments into an array (Rest Parameter)  
C. Creates an object  
D. Throws Syntax Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
When used in a function definition, `...` acts as the Rest parameter, condensing multiple arguments into a single array.
</details>

### Medium
### Q15. Which method is used to handle a successful resolution of a Promise?
A. `.catch()`  
B. `.final()`  
C. `.then()`  
D. `.resolve()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`.then()` takes a callback function that executes when the Promise is fulfilled (resolved).
</details>

### Q16. What is the output?
```javascript
const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4];
console.log(arr2);
```
A. `[[1, 2], 3, 4]`  
B. `[1, 2, 3, 4]`  
C. `[1, 2, [3, 4]]`  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The Spread operator (`...`) expands `arr1` elements individually into `arr2`.
</details>

### Hard
### Q17. Async/Await is syntax sugar built on top of?
A. Callbacks  
B. Promises  
C. Generators  
D. Event Listeners  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Async functions (`async/await`) behave like generators but are built on top of Promises to write asynchronous code in a synchronous style.
</details>

---

## Module 4: Node.js Fundamentals
### Easy
### Q18. What is the default scope of a variable declared in a Node.js module?
A. Global  
B. Local to the module  
C. Local to the function  
D. Block scoped  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
In Node.js, every file is treated as a module. Variables are local to that module unless explicitly exported.
</details>

### Q19. Usage of `package.json`?
A. Stores project metadata and dependencies  
B. Executes JavaScript code  
C. Configures Database  
D. Stores HTML templates  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`package.json` holds metadata like project name, version, scripts, and the list of installed npm dependencies.
</details>

### Medium
### Q20. How do you export a function `add` in CommonJS?
A. `export default add`  
B. `module.exports = { add }`  
C. `exports.default = add`  
D. `require(add)`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
CommonJS (default Node.js module system) uses `module.exports` object to export values.
</details>

### Q21. Which core module handles File System operations?
A. `file`  
B. `fs`  
C. `path`  
D. `system`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The built-in `fs` module provides API to interact with the file system (read, write, delete).
</details>

### Hard
### Q22. Which phase of the Event Loop handles `setImmediate()`?
A. Timers  
B. Poll  
C. Check  
D. Close Callbacks  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`setImmediate()` callbacks are executed in the **Check** phase of the Node.js Event Loop, directly after the Poll phase.
</details>

### Q23. What is a "Stream" in Node.js?
A. A collection of Arrays  
B. An abstract interface for working with streaming data (chunks)  
C. A database connection  
D. A third-party library  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Streams allow reading/writing data piece by piece (chunks) without loading the whole file into memory, efficient for large data.
</details>

---

## Module 5: Express.js & MongoDB
### Easy
### Q24. What is the correct way to initialize an Express app?
A. `const app = new Express();`  
B. `const app = express();`  
C. `const app = init.express();`  
D. `import app from 'express';`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The `express` module exports a top-level function that we invoke to create an Express application: `const app = express();`.
</details>

### Q25. Which function parses incoming JSON payloads in Express?
A. `bodyParser.text()`  
B. `express.urlencoded()`  
C. `express.json()`  
D. `JSON.parse()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`express.json()` is a built-in middleware function in Express (v4.16+) used to parse incoming requests with JSON payloads.
</details>

### Medium
### Q26. What is "Middleware" in Express?
A. A database driver  
B. A function that has access to request, response, and next function  
C. A front-end framework  
D. A CSS library  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Middleware functions are functions that execute during the request-response cycle. They can modify req/res or end the cycle, or call `next()`.
</details>

### Q27. In `app.get('/user/:id', ...)`, how do you access `id`?
A. `req.query.id`  
B. `req.params.id`  
C. `req.body.id`  
D. `req.url.id`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Route parameters identified by a colon (e.g., `:id`) are accessible via `req.params`.
</details>

### Hard
### Q28. What is the role of `next()`?
A. Skips the current route  
B. Restarts the server  
C. Passes control to the next middleware function  
D. Sends response to client  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`next()` is a callback argument provided to middleware. Calling it passes control to the subsequent middleware function in the stack. If not called, the request hangs.
</details>

---

## Module 6: React.js Fundamentals
### Easy
### Q29. React Main Concept is?
A. Component-based architecture  
B. MVC Architecture  
C. Database Management  
D. Direct DOM manipulation  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
React is built around the concept of reusable **Components** that manage their own state and render UI.
</details>

### Q30. What is JSX?
A. JavaScript XML  
B. Java Standard Extension  
C. JSON Syntax  
D. Java Syntax Header  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
JSX (JavaScript XML) is a syntax extension for JavaScript that allows writing HTML-like code within JS.
</details>

### Medium
### Q31. Which hook is used to initialize state in a functional component?
A. `useEffect`  
B. `useContext`  
C. `useState`  
D. `useReducer`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`useState` is the standard Hook for adding state variables to functional components.
</details>

### Q32. How do you pass data from Parent to Child?
A. State  
B. Props  
C. Context  
D. Redux  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
**Props** (properties) are the mechanism to pass read-only data from a parent component down to a child component.
</details>

### Hard
### Q33. Why is the "key" prop important in Lists?
A. It styles the list item.  
B. It acts as a class name.  
C. It helps React identify which items have changed, added, or removed.  
D. It is mandatory for HTML compliance.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Keys provide a stable identity for DOM elements. React uses keys during the Reconciliation process to efficiently update only the modified items in a list.
</details>

### Q34. What happens if you call `setState` (or set function) with the same value?
A. Rerender occurs  
B. React skips the rerender (Bailing out)  
C. Error is thrown  
D. Component unmounts  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
React uses `Object.is` comparison. If the new state value is identical to the current one, React "bails out" and skips rendering the component and its children.
</details>

---

## Module 7: Advanced React & Redux
### Easy
### Q35. What is the single source of truth in Redux?
A. View  
B. Action  
C. Store  
D. Reducer  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
In Redux, the entire state of the application is stored in a single object tree within a single **Store**.
</details>

### Q36. Which hook is used to perform side effects?
A. `usesideEffect`  
B. `useEffect`  
C. `useAction`  
D. `useLifeCycle`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`useEffect` lets you perform side effects (data fetching, subscriptions, DOM updates) in functional components.
</details>

### Medium
### Q37. What is "Prop Drilling"?
A. Passing props through multiple levels of intermediate components  
B. Modifying props inside a child  
C. Using props types  
D. Deleting props  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Prop Drilling occurs when you pass data via props through several layers of components just to reach a deeply nested child, even if intermediate components don't use it.
</details>

### Q38. `useRef` is primarily used for?
A. Triggering re-renders  
B. Routing  
C. Accessing DOM elements or storing mutable values without re-render  
D. Context API  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`useRef` returns a mutable ref object (`.current`). Changes to it do *not* output a re-render. Common usage: accessing input elements directly.
</details>

### Hard
### Q39. What is the purpose of `Redux Thunk`?
A. To optimize CSS  
B. To allow writing action creators that return a function (Async logic)  
C. To replace Reducers  
D. To connect React to Redux  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Standard Redux actions are plain objects. Thunk middleware allows an action creator to return a *function*, enabling asynchronous operations (like API calls) before dispatching the final action.
</details>

### Q40. Why shouldn't you mutate state directly in a Reducer?
A. It throws a syntax error.  
B. It breaks Time Travel debugging and React may not detect changes to re-render.  
C. Redux state is private.  
D. JavaScript doesn't support mutation.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Redux relies on shallow equality checks. If you mutate the object reference in place, Redux assumes the state hasn't changed and won't trigger listeners (UI updates). You must return a *new* object copy.
</details>

---

## Module 8: jQuery
### Easy
### Q41. Which sign is used as an alias for jQuery?
A. `%`  
B. `&`  
C. `$`  
D. `@`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`$` is the standard alias for the `jQuery` function. `$(selector)` is the most common usage.
</details>

### Q42. Which method hides an element?
A. `.hidden()`  
B. `.hide()`  
C. `.display(none)`  
D. `.remove()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`.hide()` is the jQuery effect method to hide matched elements (sets `display: none`).
</details>

### Medium
### Q43. What does `$(document).ready()` perform?
A. Loads images  
B. Waits until the HTML DOM is fully loaded and ready for manipulation  
C. Starts the server  
D. Creates a cookie  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
It ensures that the jQuery code runs only after the DOM is fully constructed (safe to access elements), even if images haven't finished loading.
</details>

### Q44. How to chain methods in jQuery?
A. `$("#p1").color("red").slideUp();`  
B. `$("#p1") + slideUp();`  
C. `chain($("#p1"), slideUp);`  
D. Impossible in jQuery  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Many jQuery methods return the jQuery object (`this`), allowing multiple methods to be called on the same element in a single line (Chaining).
</details>

### Hard
### Q45. Which method is used to perform an asynchronous HTTP request in jQuery?
A. `$.http()`  
B. `$.fetch()`  
C. `$.ajax()`  
D. `$.request()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
### Q45. Which method is used to perform an asynchronous HTTP request in jQuery?
A. `$.http()`  
B. `$.fetch()`  
C. `$.ajax()`  
D. `$.request()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`$.ajax()` is the core method for performing generic AJAX requests in jQuery. `$.get` and `$.post` are shorthands for it.
</details>


## Module 2 (Continued): Deep Dive
### Q46. What is the prototype chain?
A. A chain of function calls  
B. The mechanism by which objects allow inheritance of properties and methods  
C. A linked list data structure  
D. An HTML attribute  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Objects in JS have a link to a prototype object. When accessing a property, JS checks the object, then its prototype, and so on up the "prototype chain".
</details>

### Q47. How do you create an object without a prototype?
A. `Object.create(null)`  
B. `new Object()`  
C. `{}`  
D. `Object.null()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`Object.create(null)` creates an object with no `[[Prototype]]`, meaning it doesn't inherit basic methods like `toString()`.
</details>

### Q48. `JSON.stringify` converts a JS object into?
A. A binary buffer  
B. A JSON string  
C. An XML string  
D. An encrypted token  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`JSON.stringify()` takes a JavaScript object and transforms it into a JSON string serialization.
</details>

## Module 3 (Continued): Async Deep Dive
### Q49. What code runs first?
A. `console.log('A')`  
B. `setTimeout(() => console.log('B'), 0)`  
C. `Promise.resolve().then(() => console.log('C'))`  
D. Depends on OS  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Synchronous code (`A`) runs first. Then Microtasks (`C`, Promise). Then Macrotasks (`B`, Timeout).
</details>

### Q50. `Promise.all` fails when?
A. All promises fail  
B. Any one promise fails (rejects)  
C. Half promises fail  
D. Never  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`Promise.all` rejects immediately if *any* of the input promises reject (fail-fast behavior).
</details>

## Module 4 (Continued): Node.js Core
### Q51. Which event is emitted when an unhandled exception occurs?
A. `error`  
B. `uncaughtException`  
C. `processExit`  
D. `fail`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The `uncaughtException` event is emitted on `process` when an exception bubbles all the way back to the event loop without being caught.
</details>

### Q52. What is `__dirname`?
A. Name of the directory of the current module  
B. Name of the current file  
C. Path to node executable  
D. Path to home directory  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`__dirname` is a global variable (in CommonJS) containing the absolute path of the directory containing the currently executing file.
</details>

### Q53. How to read a file synchronously?
A. `fs.readFile()`  
B. `fs.readSync()`  
C. `fs.readFileSync()`  
D. `fs.read()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`fs.readFileSync()` blocks execution until the file is read and returns the content.
</details>

### Q54. What class handles binary data in Node?
A. `Binary`  
B. `Stream`  
C. `Buffer`  
D. `Byte`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
The `Buffer` class is used to handle raw binary data (streams of octets) in Node.js.
</details>

## Module 5 (Continued): Express Scenarios
### Q55. Order of middleware execution?
A. Random  
B. Alphabetical  
C. Sequential (Order of definition)  
D. Priority based  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Middleware functions are executed in the sequence they are added using `app.use()`.
</details>

### Q56. How to serve static files?
A. `app.static('public')`  
B. `express.static('public')`  
C. `app.use(express.static('public'))`  
D. `app.files('public')`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
You must mount the built-in middleware using `app.use(express.static('folderName'))`.
</details>

### Q57. `res.send()` vs `res.json()`?
A. `json` converts to string, `send` does not  
B. `send` automatically sets Content-Type based on data, `json` enforces JSON  
C. No difference  
D. `send` is deprecated  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`res.json()` enforces the JSON content-type header and formats null/undefined. `res.send()` infers type (String -> HTML, Object -> JSON).
</details>

## Module 6 (Continued): React Patterns
### Q58. `useEffect(() => {}, [])` runs when?
A. Every render  
B. Only on Mount (and Unmount cleanup)  
C. On every update  
D. Never  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
An empty dependency array `[]` tells React to run the effect only once after the initial render (Mount).
</details>

### Q59. Function to update context value?
A. `Context.Update`  
B. `Provider` value prop  
C. `Consumer`  
D. `useUpdate`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The `value` prop in the `<MyContext.Provider value={...}>` component determines the value accessible to all consumers.
</details>

### Q60. "Controlled Component" means?
A. React controls the form input state  
B. The DOM controls the form input state  
C. Redux controls the component  
D. A component with strict types  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
In a controlled component, form data is handled by a React component's state (via `value` and `onChange`) rather than the DOM.
</details>

### Q61. `useContext` prevents?
A. State mutation  
B. Prop Drilling  
C. Re-renders  
D. Usage of Hooks  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Context allows sharing global data (theme, auth) without explicitly passing props through every level of the tree.
</details>

## Module 7 (Continued): Redux & Optimization
### Q62. What is "Dispatching" an action?
A. Deleting state  
B. Sending an action object to the Redux store  
C. Creating a component  
D. Rendering a view  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`dispatch(action)` is the only way to trigger a state change in Redux. It sends the action object to the store.
</details>

### Q63. What is the return value of a Reducer?
A. Nothing (void)  
B. The next state object  
C. A Promise  
D. A Component  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
A Reducer is a pure function `(state, action) => newState`. It must return the new state object.
</details>

### Q64. `React.memo` is used for?
A. Caching API calls  
B. Memoizing Functional Components to prevent unnecessary re-renders  
C. Memoizing values inside a component  
D. Redux state  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`React.memo` is a Higher Order Component that skips rendering the component if its props have not changed.
</details>

### Q65. `useMemo` vs `useCallback`?
A. `useMemo` returns a memoized value; `useCallback` returns a memoized function  
B. Same thing  
C. `useCallback` is for classes  
D. `useMemo` is for side effects  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`useMemo(() => val, [])` returns the result of the function. `useCallback(fn, [])` returns the function instance itself.
</details>

## Module 9: Tricky Interview Scenarios
### Q66. Output of `console.log(1 < 2 < 3)`?
A. true  
B. false  
C. Error  
D. NaN  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`1 < 2` is `true`. `true < 3` coerces `true` to `1`. `1 < 3` is `true`.
</details>

### Q67. Output of `console.log(3 > 2 > 1)`?
A. true  
B. false  
C. Error  
D. NaN  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`3 > 2` is `true`. `true > 1` coerces `true` to `1`. `1 > 1` is `false`.
</details>

### Q68. Can `const` objects be mutated?
A. No  
B. Yes, the reference is immutable but properties are mutable  
C. Only in strict mode  
D. Yes, fully reassignable  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`const` prevents reassigning the variable identifier. It does *not* make the value immutable. If it holds an object, properties can be changed.
</details>

### Q69. What is "Hoisting"?
A. Using a variable before declaration  
B. Lifting state up  
C. Moving declarations to the top of scope by the JS engine  
D. API requests  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Hoisting is the behavior where variable and function declarations are moved to the top of their containing scope during the compilation phase.
</details>

## Mixed Bag: Practical Application
### Q70. How to stop event propagation?
A. `event.stop()`  
B. `event.preventDefault()`  
C. `event.stopPropagation()`  
D. `event.halt()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`stopPropagation()` prevents the event from bubbling up the DOM tree. `preventDefault()` prevents the browser's default action (like form submission).
</details>

### Q71. Which HTML5 tag is semantic?
A. `<div>`  
B. `<span>`  
C. `<article>`  
D. `<b>`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`<article>` clearly describes its content (a self-contained article), whereas `div` and `span` are generic containers.
</details>

### Q72. Correct way to merge two arrays `a` and `b`?
A. `a + b`  
B. `[...a, ...b]`  
C. `a.append(b)`  
D. `merge(a, b)`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The spread operator is the modern (ES6) way to merge arrays. `a.concat(b)` is the older way. `+` converts them to strings.
</details>

### Q73. In Node.js, `require('./module')` loads?
A. json  
B. js, json, or node file  
C. only js  
D. txt  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Node tries to resolve `.js`, then `.json`, then `.node` (compiled addon) if no extension is provided.
</details>

### Q74. `fs.writeFile` overwrites or appends by default?
A. Appends  
B. Overwrites  
C. Throws error if exists  
D. Prompts user  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`writeFile` replaces the file content if it exists. To append, usage of `fs.appendFile` or `{flag: 'a'}` is required.
</details>

### Q75. Express: `req.query` contains?
A. URL Route parameters  
B. URL Query string parameters (after ?)  
C. JSON Body  
D. Headers  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`req.query` captures the query string (e.g., `?name=bob` -> `{name: 'bob'}`).
</details>

### Q76. React: Why use `Fragment`?
A. To optimize CSS  
B. To avoid adding extra nodes to the DOM  
C. To use state  
D. To split code  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Fragments (`<></>`) grouping children without adding extra nodes (like a wrapper `div`) to the DOM.
</details>

### Q77. Redux: `connect` function comes from?
A. `redux`  
B. `react`  
C. `react-redux`  
D. `redux-thunk`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
The `connect` HOC (Higher Order Component) is part of the `react-redux` binding library, linking React components to the Redux store.
</details>

### Q78. jQuery: `$('.box')` selects?
A. Element with ID box  
B. All elements with class "box"  
C. First element with class "box"  
D. All div elements  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The `.` selector targets class names.
</details>

### Q79. JS: `NaN === NaN` is?
A. true  
B. false  
C. undefined  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
NaN is the only value in JavaScript that is not equal to itself. Identify using `isNaN()`.
</details>

### Q80. `Array.map()` returns?
A. A new array with transformed elements  
B. The same array modified  
C. undefined  
D. A boolean  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`.map()` creates a NEW array by applying the callback function to every element.
</details>

### Q81. `Array.forEach()` returns?
A. A new array  
B. undefined  
C. The original array  
D. The length  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`.forEach()` executes a function for each element but does not return a value (void/undefined).
</details>

### Q82. `Array.filter()` returns?
A. A new array with elements that pass the test  
B. The first matching element  
C. Boolean  
D. Count of matches  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`.filter()` creates a new array with all elements that pass the test implemented by the provided function.
</details>

### Q83. `Array.reduce()` is used for?
A. Filtering  
B. Accumulating values into a single result  
C. Sorting  
D. Deleting  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`.reduce()` executes a reducer function on each element of the array, resulting in a single output value.
</details>

### Q84. JS: `0` is?
A. Truthy  
B. Falsy  
C. Null  
D. Undefined  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The number `0` is one of the falsy values in JavaScript (along with `false`, `""`, `null`, `undefined`, `NaN`).
</details>

### Q85. JS: `[]` (Empty Array) is?
A. Truthy  
B. Falsy  
C. Null  
D. NaN  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Objects (including arrays) are truthy in JavaScript, even if empty.
</details>

### Q86. Node: `process.env` is used for?
A. File reading  
B. Environment variables  
C. Processes list  
D. Memory usage  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
It returns an object containing the user environment variables (like PATH, PORT, DB_URL).
</details>

### Q87. Express: `res.status(404)`?
A. Sends a 404 response  
B. Sets the HTTP status code to 404 but doesn't send response yet  
C. Stops the server  
D. Logs error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
It sets the status code. You usually chain it: `res.status(404).send('Not Found')`.
</details>

### Q88. React: Can you use Hooks in Class Components?
A. Yes  
B. No  
C. Only useState  
D. Only with adapters  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Hooks (`use...`) work *only* inside Functional Components.
</details>

### Q89. Redux: Where should async logic live?
A. Reducers  
B. Components  
C. Middleware (Thunk/Saga)  
D. Store  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Reducers must be pure (no side effects). Async logic belongs in Middleware like Thunk.
</details>

### Q90. jQuery: `$(this)` refers to?
A. The jQuery object wrapper of the current element  
B. The raw DOM element  
C. The document  
D. The window  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`this` is the raw DOM element; `$(this)` wraps it to enable jQuery methods.
</details>

### Q91. What is the Time Complexity of accessing an Array item by index?
A. O(1)  
B. O(n)  
C. O(log n)  
D. O(n^2)  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Array access by index is a constant time operation.
</details>

### Q92. `Set` in JavaScript stores?
A. Key-Value pairs  
B. Unique values  
C. Duplicate values  
D. Ordered map  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The `Set` object lets you store unique values of any type. Duplicates are automatically removed.
</details>

### Q93. `Map` vs `Object` keys?
A. Object keys must be Strings/Symbols; Map keys can be anything  
B. No difference  
C. Object keys are ordered  
D. Map keys are restricted  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Maps allow keys of any type (objects, functions, primitives). Objects traditionally only support Strings and Symbols as keys.
</details>

### Q94. JS: `call` vs `apply`?
A. `call` takes array of args; `apply` takes comma-separated args  
B. `call` takes comma-separated args; `apply` takes array of args  
C. `call` is async  
D. `apply` creates a new function  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Both invoke the function with a given context. `call(this, arg1, arg2)`. `apply(this, [args])`.
</details>

### Q95. JS: `bind`?
A. Invokes immediately  
B. Returns a new function with `this` bound  
C. Merges arrays  
D. Links HTML  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`bind()` returns a NEW function instance with a fixed `this` contexts, which can be called later.
</details>

### Q96. Node: `path.join('/a', '/b')` on Windows returns?
A. `\a\b`  
B. `/a/b`  
C. `a/b`  
D. `Error`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`path.join` uses the platform-specific separator. On Windows, it uses backslashes.
</details>

### Q97. Express: `app.use(cors())` enables?
A. Cookies  
B. Cross-Origin Resource Sharing  
C. Compression  
D. Caching  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
CORS middleware allows restricts/allows requests from different domains (origins).
</details>

### Q98. React: "Lifting State Up" means?
A. Using Redux  
B. Moving state to the closest common ancestor of components that need it  
C. Hoisting variables  
D. Using Server Side Rendering  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Standard React pattern to share state between siblings by moving it to their parent.
</details>

### Q99. React: `StrictMode` in development?
A. Throws errors for unsafe lifecycles and runs effects twice  
B. Makes app faster  
C. Disables console logs  
D. Enforces TypeScript  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
It intentionally invokes methods twice to detect side effects and warns about deprecated features.
</details>

### Q100. jQuery: `addClass` usage?
A. `$('div').addClass('.active')`  
B. `$('div').addClass('active')`  
C. `$('div').class('active')`  
D. `$('div').active(true)`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
You pass the class name *without* the dot to `addClass()`.
</details>

### Q101. JS: `let a = {x:1}; let b = a; b.x = 2;` Value of `a.x`?
A. 1  
B. 2  
C. undefined  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Objects are assigned by reference. `b` points to same object as `a`. Changing `b` changes `a`.
</details>

### Q102. JS: `3 + 2 + "7"`?
A. "57"  
B. "12"  
C. "327"  
D. NaN  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Left-to-right: `3+2=5`. Then `5+"7" = "57"` (String concatenation).
</details>

### Q103. JS: `"3" + 2 + 7`?
A. "327"  
B. "12"  
C. "57"  
D. NaN  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`"3"+2 = "32"`. `"32"+7 = "327"`. All become string concatenation.
</details>

### Q104. JS: `!!` operator?
A. Logical OR  
B. Converts to Boolean (Double Negation)  
C. Checks equality  
D. Bitwise OR  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`!` negates truthiness. `!!` negates it back, effectively casting a value to its boolean equivalent (`true`/`false`).
</details>

### Q105. Node: `os.cpus()`?
A. Returns CPU info array  
B. Returns CPU temperature  
C. Returns CPU usage percentage  
D. Returns number of processes  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Returns an array of objects containing information about each logical CPU core.
</details>

### Q106. Express: How to handle 404 (Not Found)?
A. It's automatic  
B. Add a middleware at the very end that sends error  
C. Check in every route  
D. Use `app.notFound()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Express tries to match routes sequentially. If none match, execution reaches the final middleware, which is conventionally used to handle 404s.
</details>

### Q107. React: What prevents XSS in JSX?
A. Manual escaping  
B. React escapes values by default before rendering  
C. Cookies  
D. HTTPS  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
By default, React DOM escapes any values embedded in JSX before rendering them, effectively preventing injection attacks.
</details>

### Q108. React: `lazy` loading?
A. `React.lazy(() => import('./Comp'))`  
B. `import.lazy('./Comp')`  
C. `lazy('./Comp')`  
D. `require.lazy('./Comp')`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`React.lazy` lets you define a component that is loaded dynamically from an import(). Must be used with `<Suspense>`.
</details>

### Q109. Redux: `combineReducers`?
A. Merges two stores  
B. Combines multiple slice reducers into a single root reducer  
C. Connects react to redux  
D. Filters actions  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Used to split the root reducer into smaller reducers that manage independent parts of the state tree.
</details>

### Q110. JS: What is `Promise.race`?
A. Runs promises in parallel and waits for all  
B. Returns a promise that settles as soon as the first promise settles (resolves/rejects)  
C. Races CPU threads  
D. Sorts promises  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
It settles with the result/error of the *first* promise that finishes.
</details>

### Q111. JS: `Symbol` uniqueness?
A. `Symbol('foo') === Symbol('foo')` is true  
B. `Symbol('foo') === Symbol('foo')` is false  
C. Symbols are strings  
D. Symbols are shared by default  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Every `Symbol()` call creates a unique primitive value, even if the description string is the same.
</details>

### Q112. Node: `process.argv`?
A. Environment variables  
B. Command line arguments array  
C. Process ID  
D. File path  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Contains the command-line arguments. Index 0 is node, 1 is script path, 2+ are user args.
</details>

### Q113. Express: `.route()`?
A. Create chained route handlers for a route path  
B. Defines a new router  
C. Deletes a route  
D. Middleware  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`app.route('/book').get(...).post(...)` allows chaining handlers for the same path.
</details>

### Q114. React: `useReducer` resembles?
A. `useState` only  
B. Redux reducer pattern  
C. Context  
D. Router  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`useReducer(reducer, initial)` is preferable for complex state logic, mirroring Redux's (state, action) pattern.
</details>

### Q115. Redux: `Provider` usage?
A. Inside Reducers  
B. Wraps the root App component  
C. Wraps individual buttons  
D. Used in Actions  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`<Provider store={store}>` wraps the app to inject the store into the component tree.
</details>

### Q116. JS: `delete` operator?
A. Deletes a variable  
B. Deletes a property from an object  
C. Deletes a file  
D. Frees memory explicitly  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`delete obj.prop` removes the property from the object. It does not delete variables or objects themselves (GC does that).
</details>

### Q117. JS: `Object.keys()` returns?
A. Array of values  
B. Array of enumerable property names (keys)  
C. String representation  
D. Prototype  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Returns an array of a given object's own enumerable string-keyed property names.
</details>

### Q118. JS: `Object.freeze()`?
A. Makes object const  
B. Prevents adding/removing/modifying properties of an object  
C. Pauses execution  
D. Converts to JSON  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Standard method to make an object immutable.
</details>

### Q119. Node: Circular dependency in CommonJS?
A. Throws Error  
B. Returns empty object  
C. Returns a partially loaded object  
D. Crashes Loop  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Node.js allows circular dependencies but may return a partially loaded copy of the module to resolve the cycle.
</details>

### Q120. Express: `res.redirect('/home')` status code?
A. 200  
B. 302 (Found) default  
C. 404  
D. 500  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Redirects map to 302 by default (Temporary Redirect).
</details>

### Q121. React: `defaultProps`?
A. Define default values for props  
B. Check types  
C. Define state  
D. Define context  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Static property to define default values if props are undefined. (Being deprecated in function components in favor of default params).
</details>

### Q122. Redux: `mapStateToProps`?
A. Argument to reducer  
B. Function to select parts of state to pass as props in `connect`  
C. Lifecycle method  
D. Action creator  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Used in `connect(mapStateToProps)` to subscribe to store updates and map state to component props.
</details>

### Q123. jQuery: `append()` vs `prepend()`?
A. End of element vs Start of element  
B. Outside element vs Inside  
C. Before vs After  
D. Replace vs Remove  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`append` inserts content *inside* the element as the *last* child. `prepend` inserts as *first* child.
</details>

### Q124. JS: `parseInt("10px")`?
A. NaN  
B. 10  
C. Error  
D. "10px"  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`parseInt` parses until it hits a non-numeric character.
</details>

### Q125. JS: `Number("10px")`?
A. 10  
B. NaN  
C. Error  
D. "10"  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`Number()` is stricter than `parseInt`; if the string contains non-whitespace non-numeric chars, it returns NaN.
</details>

### Q126. JS: Is Array an Object?
A. Yes  
B. No  
C. Only in ES6  
D. Only on Windows  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`typeof []` is "object". Arrays are specialized objects with length property and index keys.
</details>

### Q127. Node: default package manager?
A. yarn  
B. npm  
C. pip  
D. maven  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
npm is bundled with Node.js.
</details>

### Q128. Express: `app.listen()`?
A. Starts the HTTP server listening for connections  
B. Listens for events  
C. Listens for errors  
D. Listens to music  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Binds and listens for connections on the specified host and port.
</details>

### Q129. React: Virtual DOM is faster because?
A. It bypasses the browser  
B. It minimizes direct manipulation of the heavy/slow Real DOM  
C. It runs on GPU  
D. It is written in C++  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Batching updates and diffing in memory (VDOM) is much faster than touching the actual DOM for every state change.
</details>

### Q130. Redux: Store methods?
A. `getState()`, `dispatch()`, `subscribe()`  
B. `get()`, `set()`, `listen()`  
C. `push()`, `pop()`  
D. `run()`, `stop()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
The core API of a Redux store.
</details>

### Q131. JS: `setTimeout(fn, 0)` guarantees execution in 0ms?
A. Yes  
B. No, it guarantees *minimum* delay, runs after stack clears  
C. Yes, interrupts current code  
D. Runs immediately  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
It places the callback in the queue. It runs only when the call stack is empty, which might take > 0ms.
</details>

### Q132. JS: `1/0` in JS?
A. Error  
B. Infinity  
C. NaN  
D. 0  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Division by zero returns `Infinity` (or `-Infinity`) in JS, not an error.
</details>

### Q133. DOM: `innerHTML` vs `innerText`?
A. `innerHTML` parses HTML tags; `innerText` treats them as text  
B. Same  
C. `innerText` parses tags  
D. `innerHTML` includes CSS  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Security risk: `innerHTML` allows XSS if not sanitized. `innerText` is safe for plain text.
</details>

### Q134. CSS: Box Model components?
A. Content, Padding, Border, Margin  
B. Content, Color, Font, Background  
C. Header, Body, Footer  
D. Margin, Padding, Float  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
From inside to outside.
</details>

### Q135. Node: `module.exports` initial value?
A. `null`  
B. `{}` (Empty Object)  
C. `undefined`  
D. `function`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
It starts as an empty object, which you can attach properties to or replace entirely.
</details>

### Q136. React: `e.target` vs `e.currentTarget`?
A. `target` is element that triggered event; `currentTarget` is element listener is attached to  
B. Same  
C. `target` is parent; `currentTarget` is child  
D. Opposite of A  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Important for event delegation.
</details>

### Q137. Redux: What is a "Slice"?
A. A part of the state tree and its associated reducers/actions  
B. A UI component  
C. A Pizza  
D. A server route  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Term popularized by Redux Toolkit to refer to the logic (reducer+actions) for a specific feature.
</details>

### Q138. jQuery: `remove()` vs `empty()`?
A. `remove` deletes element; `empty` deletes its children  
B. `remove` deletes children; `empty` deletes element  
C. Same  
D. `empty` hides  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`remove()` takes the element out of DOM. `empty()` clears its inner HTML but leaves the tag.
</details>

### Q139. JS: `typeof []`?
A. array  
B. list  
C. object  
D. collection  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Arrays are objects. Use `Array.isArray()` to distinguish.
</details>

### Q140. JS: `typeof NaN`?
A. number  
B. nan  
C. undefined  
D. error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
IEEE 754 standard defines NaN as a numeric value.
</details>

### Q141. Node: `fs.createReadStream` vs `readFile`?
A. Streams are memory efficient for large files  
B. `readFile` is faster  
C. Streams are synchronous  
D. `readFile` creates chunks  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`readFile` buffers the whole file into RAM. Streams read it in chunks, allowing processing of files larger than RAM.
</details>

### Q142. Express: `app.all('*')`?
A. Matches all HTTP methods and all paths (Catch-all)  
B. Matches all GET requests  
C. Matches nothing  
D. Syntax error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Often used for 404 handling or global logic.
</details>

### Q143. React: `useLayoutEffect`?
A. Runs synchronously after DOM mutation but before paint  
B. Same as useEffect  
C. Runs after paint  
D. Runs in background  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Used when you need to measure DOM layout/position synchronously to prevent visual flickering.
</details>

### Q144. JS: `void 0`?
A. Returns `undefined`  
B. Returns 0  
C. Returns null  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`void` operator evaluates an expression and returns undefined. `void 0` is a safe way to get `undefined`.
</details>

### Q145. JS: Generator function syntax?
A. `function* name() {}`  
B. `function name*() {}`  
C. `generator name() {}`  
D. `async function name() {}`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Asterisk `*` after `function` keyword denotes a generator.
</details>

### Q146. JS: `yield` keyword?
A. Pauses generator execution and returns value  
B. Stops function forever  
C. Returns promise  
D. Declares variable  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Used inside generators to pause execution and produce a value to the iterator.
</details>

### Q147. Node: `cluster` module?
A. Enables multi-core scalability (forking processes)  
B. Clusters database  
C. groups files  
D. Networking  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Allows creating child processes (workers) that share server ports, utilizing all CPU cores.
</details>

### Q148. Express: `res.render()`?
A. Renders a view template (Pug, EJS)  
B. Renders JSON  
C. Renders React  
D. Downloads file  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Used with template engines to generate HTML on the server.
</details>

### Q149. React: `Suspense` component?
A. Wraps lazy-loaded components to show fallback UI  
B. Suspends execution  
C. Handles errors  
D. Redux middleware  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Shows a fallback (like a spinner) while the lazy component is loading.
</details>

### Q150. Final: What is "Callback Hell"?
A. Deeply nested callbacks making code unreadable  
B. A function calling itself  
C. An infinite loop  
D. A database error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
The Pyramid of Doom caused by dependent asynchronous operations in Node.js/JS. Solved by Promises/Async-Await.
</details>

---

# Completion Confirmation
I confirm that all notes were fully analyzed and approximately 150 MCQs were generated covering every concept, with answers hidden and no syllabus deviation.
