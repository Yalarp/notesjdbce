# CCEE – Deep Dive Master Question Bank (150 Hard Questions)

**Scope:** Day 01 to Day 13 (Modules 1-8)
**Difficulty:** Hard / Conceptual
**Focus:** Code Analysis, Edge Cases, Internal Mechanics

---

## Part 1: JavaScript Core & Advanced (Day 1-4)

### Q1. What is the output of the following code?
```javascript
console.log([] + {});
console.log({} + []);
```
A. `"[object Object]"` and `0`  
B. `"[object Object]"` and `"[object Object]"`  
C. `"[object Object]"` and `0` (or `[object Object]` depending on browser/repl context)  
D. `""` and `NaN`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`[] + {}`: The array becomes `""`, adding object stringifies it to `"[object Object]"`. Result: `"[object Object]"`.  
`{} + []`: In many REPLs/consoles, the first `{}` is interpreted as an empty code block, so it becomes `+[]` which coerces `[]` to `0`. If evaluated as an expression (like in `console.log({} + [])`), it treats `{}` as an object, resulting in `"[object Object]"`. The trickiest part is the context-dependency.
</details>

### Q2. Consider the Temporal Dead Zone (TDZ). What happens here?
```javascript
let x = 10;
function test() {
    console.log(x);
    let x = 20;
}
test();
```
A. 10  
B. 20  
C. `undefined`  
D. ReferenceError  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** D  

**Explanation:**  
The `let x` inside the function shadows the outer `x`. However, variables declared with `let` are in the Temporal Dead Zone from the start of the block until the declaration is processed. Accessing `x` before `let x = 20` throws a `ReferenceError`.
</details>

### Q3. What is the output of this Immediately Invoked Function Expression (IIFE)?
```javascript
(function(x) {
    return (function(y) {
        console.log(x);
    })(2);
})(1);
```
A. 1  
B. 2  
C. `undefined`  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
The inner function forms a closure and has access to `x` from the outer function's scope. `x` is `1`.
</details>

### Q4. Precision issues: What is the result of `0.1 + 0.2 === 0.3`?
A. true  
B. false  
C. Error  
D. `NaN`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Due to floating-point precision standards (IEEE 754), `0.1 + 0.2` results in `0.30000000000000004`, which is not strictly equal to `0.3`.
</details>

### Q5. `delete` operator behavior:
```javascript
var output = (function(x) {
    delete x;
    return x;
})(0);
console.log(output);
```
A. `undefined`  
B. 0  
C. null  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The `delete` operator is used to remove properties from objects. It cannot delete local variables or function parameters. The operation `delete x` fails silently (returns false), and `x` remains `0`.
</details>

### Q6. Array methods: What does `[1, 2, 3, 4, 5].length = 2` do?
A. Throws an error  
B. Nothing  
C. Truncates the array to `[1, 2]`  
D. Makes the other elements `undefined`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Setting the `.length` property of an array to a value lower than its current length truncates the array.
</details>

### Q7. Prototypes:
```javascript
function Person() {}
Person.prototype.name = "Alice";
let p1 = new Person();
p1.name = "Bob";
delete p1.name;
console.log(p1.name);
```
A. `undefined`  
B. "Bob"  
C. "Alice"  
D. null  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`p1.name = "Bob"` creates an "own" property, shadowing the prototype property. `delete p1.name` removes the own property, revealing the prototype property "Alice" again.
</details>

### Q8. Event Loop Order:
```javascript
console.log(1);
setTimeout(() => console.log(2), 0);
Promise.resolve().then(() => console.log(3));
console.log(4);
```
A. 1 2 3 4  
B. 1 4 2 3  
C. 1 4 3 2  
D. 1 3 4 2  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
1. Sync: `1`, `4`.  
2. Microtasks (Promise): `3`.  
3. Macrotasks (Timeout): `2`.  
Result: 1 4 3 2.
</details>

### Q9. `this` context:
```javascript
const obj = {
  name: 'Obj',
  getName: function() {
    return this.name;
  }
};
const getName = obj.getName;
console.log(getName());
```
A. "Obj"  
B. `undefined` (or window.name/global)  
C. Error  
D. null  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
When `getName` is assigned to a variable and called as a standalone function `getName()`, the context (`this`) is lost (defaults to global object or undefined in strict mode), not `obj`.
</details>

### Q10. Hoisting Tricky Case:
```javascript
var a = 1;
function b() {
    a = 10;
    return;
    function a() {}
}
b();
console.log(a);
```
A. 1  
B. 10  
C. `undefined`  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Inside `b()`, the function declaration `function a() {}` is hoisted to the top of `b`'s scope, creating a local variable `a`. The assignment `a = 10` modifies this *local* `a`, leaving the global `a` (1) untouched.
</details>

### Q11. Coercion with `null`:
```javascript
console.log(null > 0);
console.log(null == 0);
console.log(null >= 0);
```
A. false, false, false  
B. false, true, true  
C. false, false, true  
D. true, true, true  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
1. `null > 0`: `null` converts to `0`. `0 > 0` is `false`.  
2. `null == 0`: Equality check with `null` only equals `undefined` or `null`. It does NOT convert to number. `false`.  
3. `null >= 0`: Relational operator converts `null` to `0`. `0 >= 0` is `true`.
</details>

### Q12. Sparse Arrays:
```javascript
let arr = [1, 2, , 4];
arr.forEach(i => console.log(i));
```
A. 1 2 undefined 4  
B. 1 2 4  
C. 1 2 NaN 4  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`forEach` (and `map`, `filter`) skips empty slots (holes) in sparse arrays. It prints 1, 2, then 4.
</details>

### Q13. Object Keys ordering:
```javascript
const obj = {
  "2": "a",
  "1": "b",
  "b": "c",
  "a": "d"
};
console.log(Object.keys(obj));
```
A. `["2", "1", "b", "a"]`  
B. `["1", "2", "b", "a"]`  
C. `["a", "b", "1", "2"]`  
D. `["1", "2", "a", "b"]` (Browser dependent but commonly B)  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
While historically unordered, modern JS engines sort integer-like keys in ascending order first, followed by string keys in insertion order.
</details>

### Q14. `JSON.stringify` with circular reference:
```javascript
const a = {};
const b = { a };
a.b = b;
JSON.stringify(a);
```
A. `{"b":{"a":{}}}`  
B. `[object Object]`  
C. Stack Overflow  
D. Throws TypeError: Converting circular structure to JSON  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** D  

**Explanation:**  
Standard `JSON.stringify` cannot handle circular references and throws an error.
</details>

### Q15. Generator flow:
```javascript
function* gen() {
  yield 1;
  yield 2;
  return 3;
}
const g = gen();
console.log([...g]);
```
A. `[1, 2, 3]`  
B. `[1, 2]`  
C. `[3]`  
D. `[1, 2, undefined]`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The spread operator consumes values yielded by the iterator. The `return` value of a generator finishes the iterator but is NOT included in the spread/iteration sequence.
</details>

## Part 2: ES6 & Async (Day 5-6)

### Q16. `Promise.race()` with rejection:
```javascript
const p1 = new Promise((_, reject) => setTimeout(() => reject('Error'), 100));
const p2 = new Promise(resolve => setTimeout(() => resolve('Success'), 200));

Promise.race([p1, p2]).then(console.log).catch(console.error);
```
A. "Success"  
B. "Error" (via console.error)  
C. Both  
D. Unhandled Rejection  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`Promise.race` settles as soon as the *first* promise settles, whether resolved or rejected. `p1` rejects first at 100ms, triggering the `.catch`.
</details>

### Q17. Arrow function `arguments`:
```javascript
const fn = () => {
    console.log(arguments);
};
fn(1, 2, 3);
```
A. `[1, 2, 3]`  
B. `{ '0':1, '1':2, '2':3 }`  
C. ReferenceError  
D. `undefined`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Arrow functions do not satisfy the `arguments` object. Accessing it throws a ReferenceError (unless wrapped in a regular function where it accesses the parent's arguments).
</details>

### Q18. Object Destructuring with Aliasing and Default:
```javascript
const { a: x = 10 } = { a: undefined };
console.log(x);
```
A. `undefined`  
B. 10  
C. null  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Destructuring defaults trigger if the value is strictly `undefined`. Here `a` is `undefined`, so `x` takes the default value `10`.
</details>

### Q19. `Set` with objects:
```javascript
const s = new Set();
s.add({a: 1});
s.add({a: 1});
console.log(s.size);
```
A. 1  
B. 2  
C. 0  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Objects are stored by reference. Two distinct object literals `{a:1}` and `{a:1}` are different references in memory, so both are added to the Set.
</details>

### Q20. `map` vs `forEach` return:
```javascript
const arr = [1, 2, 3];
const res = arr.forEach(x => x * 2);
console.log(res);
```
A. `[2, 4, 6]`  
B. `[1, 2, 3]`  
C. `undefined`  
D. `true`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`forEach` always returns `undefined`. It is for side effects, not transformation.
</details>

### Q21. Symbol key visibility:
```javascript
const sym = Symbol('foo');
const obj = { [sym]: 'bar', a: 1 };
console.log(Object.keys(obj));
```
A. `['a', Symbol(foo)]`  
B. `['a', 'bar']`  
C. `['a']`  
D. `[]`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`Object.keys` (and `JSON.stringify`) skips Symbol properties. Use `Object.getOwnPropertySymbols()` to see them.
</details>

### Q22. WeakMap keys:
A. Can be primitives  
B. Must be Objects  
C. Can be Global  
D. Are iterable  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`WeakMap` keys *must* be objects (or non-registered Symbols). They are held weakly, allowing garbage collection if no other reference exists.
</details>

### Q23. Regex: What does `/^a.*z$/` match?
A. String starting with 'a' OR ending with 'z'  
B. String starting with 'a', any chars, ending with 'z'  
C. Only 'az'  
D. 'a' followed by dots then 'z'  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`^` (start), `a` (literal), `.*` (any char 0 or more times), `z` (literal), `$` (end).
</details>

### Q24. Async function return:
```javascript
async function foo() {
    return 1;
}
console.log(foo());
```
A. 1  
B. Promise { 1 }  
C. undefined  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Async functions always return a Promise. If the function returns a value, the promise is resolved with that value.
</details>

### Q25. `NaN` in Arrays:
```javascript
console.log([NaN].indexOf(NaN));
console.log([NaN].includes(NaN));
```
A. -1, true  
B. -1, false  
C. 0, true  
D. 0, false  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`indexOf` uses strict equality (`===`), so `NaN === NaN` is false (returns -1). `includes` uses `SameValueZero` algorithm, which considers `NaN` equal to `NaN` (returns true).
</details>

## Part 3: Node.js & Modules (Day 7-8)

### Q26. `require` caching:
```javascript
// counter.js
let count = 0;
module.exports = { inc: () => count++ };

// main.js
const c1 = require('./counter');
c1.inc();
const c2 = require('./counter');
c2.inc();
// What is count now?
```
A. 1  
B. 2  
C. 0  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Modules are cached after the first load. `c1` and `c2` refer to the *same* exported object from the cached module. The state `count` is shared.
</details>

### Q27. `fs.readFile` encoding:
```javascript
fs.readFile('test.txt', (err, data) => {
    console.log(typeof data);
});
// Assuming no options passed
```
A. string  
B. object (Buffer)  
C. array  
D. null  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Without an encoding (like 'utf8') passed as the second argument, `fs.readFile` returns the raw `Buffer` object (which is `typeof object`).
</details>

### Q28. Node Event Emitter synchronous behavior:
```javascript
const EventEmitter = require('events');
const ee = new EventEmitter();
ee.on('event', () => console.log('A'));
console.log('B');
ee.emit('event');
console.log('C');
```
A. B A C  
B. B C A  
C. A B C  
D. B A C (if async) / B C A (if sync)  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`EventEmitter` emits are synchronous by default. When `emit` is called, all listeners run immediately before `emit` returns.
</details>

### Q29. `setImmediate` vs `setTimeout(..., 0)` inside I/O:
```javascript
const fs = require('fs');
fs.readFile(__filename, () => {
    setTimeout(() => console.log('timeout'), 0);
    setImmediate(() => console.log('immediate'));
});
```
A. timeout, immediate  
B. immediate, timeout  
C. Random  
D. Concurrent  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Inside an I/O callback (like readFile), the Event Loop is in the **Poll** phase. The next phase is **Check** (`setImmediate`), followed by closing callbacks, and then it loops to **Timers** (`setTimeout`). So `setImmediate` is guaranteed to run first.
</details>

### Q30. Buffer Iteration:
```javascript
const buf = Buffer.from([1, 2, 3]);
for (const b of buf) console.log(b);
```
A. Prints 1, 2, 3  
B. Error: Buffer not iterable  
C. Prints hex values  
D. Prints binary  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Buffers are subclasses of `Uint8Array` and are iterable. They yield the byte values (integers).
</details>

### Q31. What happens if you `exports = { a: 1 }` instead of `module.exports = { a: 1 }`?
A. It works fine  
B. It exports the object  
C. It breaks the export ref; module exports empty object  
D. It throws error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`exports` is just a reference to `module.exports`. Reassigning `exports` to a new object breaks the link; `module.exports` remains `{}`.
</details>

### Q32. `process.nextTick` queue priority:
A. Before Microtasks  
B. After Macrotasks  
C. Before Macrotasks, essentially "Starving" I/O if recursive  
D. Same as SetImmediate  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`nextTick` queue is processed immediately after the current operation finishes, even before Promise microtasks and well before any I/O or timers. Recursive nextTicks can block the event loop indefinitely.
</details>

### Q33. `path.resolve('/a', '/b', 'c')`?
A. `/a/b/c`  
B. `/b/c`  
C. `c`  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`path.resolve` processes right-to-left. If it encounters an absolute path (`/b`), it ignores preceding paths (`/a`). Result represents absolute path to `/b/c`.
</details>

### Q34. HTTP Module: `req` object class?
A. `Object`  
B. `http.IncomingMessage`  
C. `http.ClientRequest`  
D. `Stream`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
On the server side, the request argument passed to the request listener is an instance of `http.IncomingMessage` (which is a Readable Stream).
</details>

### Q35. Piping streams:
```javascript
readStream.pipe(writeStream);
// Does this close writeStream automatically?
```
A. No  
B. Yes, unless `{ end: false }` is passed  
C. Only on error  
D. Only on Windows  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
By default, `pipe()` calls `stream.end()` on the destination when the source stream emits 'end'. Can be disabled with option `{ end: false }`.
</details>

## Part 4: Express & Middleware (Day 8)

### Q36. Middleware Error Handling Signature:
A. `(err, req, res)`  
B. `(req, res, err)`  
C. `(err, req, res, next)`  
D. `(req, res, next, err)`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Error-handling middleware MUST have exactly 4 arguments: `(err, req, res, next)`. If `next` is missing, Express treats it as a regular middleware.
</details>

### Q37. `app.use('/api', mw)` vs `app.use(mw)`?
A. No difference  
B. First runs only for /api routes, second for all  
C. First runs for all, second for /api  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The first argument is an optional path mount point. If omitted, it defaults to `'/'`, matching all requests.
</details>

### Q38. `express.urlencoded({ extended: true })` meaning?
A. Uses `qs` library (nested objects supported)  
B. Uses `querystring` library (flat objects only)  
C. Allows large bodies  
D. Encrypts URL  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`extended: true` uses the `qs` library which allows rich objects and arrays to be encoded into the URL-encoded format. `false` uses `querystring` (native Node).
</details>

### Q39. What happens if you forget `next()` in middleware?
A. Server crashes  
B. 404 sent  
C. Request hangs (loads indefinitely)  
D. Next route runs automatically  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Since the request is not terminated (`res.send`) and control is not passed (`next()`), the client connection remains open until it times out.
</details>

### Q40. `res.locals` usage?
A. Store local variables for the current request context (passed to views)  
B. Store global variables  
C. Store user session  
D. Database cache  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`res.locals` is an object scoped to the request responsible for passing data to the view rendering engine. It does not persist across requests.
</details>

### Q41. `app.param()` function?
A. Reads query params  
B. Triggers callback when a specific route parameter is detected  
C. Sets a global param  
D. Validates body  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Used to register a middleware that runs only when a specific parameter (e.g., `:userId`) is present in the route path. Useful for pre-loading data.
</details>

### Q42. Difference between `router` and `app`?
A. `router` is a mini-app (isolated middleware/routes) capable of mounting  
B. `router` is faster  
C. `app` cannot handle routing  
D. `router` connects to DB  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
An `express.Router()` object is an isolated instance of middleware and routes. It is a "mini-application" capable of performing middleware and routing functions.
</details>

### Q43. Express response: `res.format()`?
A. Formats hard drive  
B. Performs Content Negotiation based on Accept header  
C. Formats Date  
D. Formats JSON  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
It allows you to define different response logic (HTML, JSON, Text) based on the `Accept` HTTP header sent by the client.
</details>

### Q44. `cookie-parser` signed cookies?
A. Encrypted cookies  
B. Hashed/MAC verified cookies to prevent tampering  
C. HTTPS only cookies  
D. Large cookies  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Signed cookies are not encrypted (visible text) but include a signature (HMAC) to verify integrity. Accessed via `req.signedCookies`.
</details>

### Q45. MongoDB: `findByIdAndUpdate` default behavior?
A. Returns the NEW updated document  
B. Returns the OLD document (before update)  
C. Returns boolean  
D. Returns error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
By default, Mongoose returns the original document. You must pass `{ new: true }` option to get the updated document.
</details>

### Q46. Mongoose "Virtuals"?
A. Fields that exist in DB but not in Schema  
B. Fields that exist in Schema/Code but are NOT persisted to DB  
C. Virtual Tables  
D. Cache  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Virtuals are document properties that you can get and set but that do not get persisted to MongoDB (e.g., `fullName` derived from `first` + `last`).
</details>

### Q47. REST: Idempotent methods?
A. GET, PUT, DELETE  
B. POST only  
C. GET only  
D. None  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Idempotent methods can be called multiple times with the same outcome. POST is NOT idempotent (creates multiple resources). GET, PUT, DELETE are.
</details>

### Q48. `req.body` is `undefined`?
A. Node is broken  
B. Forgot `express.json()` or body-parser middleware  
C. GET request  
D. Client error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Express does not parse the body by default. You must configure body-parsing middleware to populate `req.body`.
</details>

### Q49. Wildcard route order:
```javascript
app.get('/users/:id', ...);
app.get('/users/profile', ...);
// Request: /users/profile
```
A. Matches `/users/profile`  
B. Matches `/users/:id` (`id` becomes "profile")  
C. Error  
D. Matches both  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Routes are matched in order of definition. `:id` is a wildcard matching anything, so it intercepts "profile". Specific routes must come *before* parameter routes.
</details>

### Q50. CORS preflight request method?
A. GET  
B. POST  
C. OPTIONS  
D. HEAD  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Browsers send an HTTP `OPTIONS` request first (Preflight) for complex cross-origin requests to check permissions before sending the actual request.
</details>

---

## Part 5: React Internals & Hooks (Day 9-10)

### Q51. React `setState` asynchronous behavior:
```javascript
handleClick = () => {
    this.setState({ count: this.state.count + 1 });
    this.setState({ count: this.state.count + 1 });
    this.setState({ count: this.state.count + 1 });
};
// Initial count: 0. Final count?
```
A. 3  
B. 1  
C. 0  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
React batches state updates. Since object syntax relies on `this.state.count` (which hasn't updated yet in the same cycle), all three calls see `0`. Result is 1. To fix, use functional update: `setState(prev => ({ count: prev.count + 1 }))`.
</details>

### Q52. Stale Closure in `useEffect`:
```javascript
const [count, setCount] = useState(0);
useEffect(() => {
    const id = setInterval(() => {
        console.log(count);
    }, 1000);
    return () => clearInterval(id);
}, []); // Empty deps
// What gets logged?
```
A. 0, 1, 2, 3...  
B. 0, 0, 0, 0...  
C. 1, 1, 1, 1...  
D. Nothing  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The effect runs only once (mount). The closure captures the initial value of `count` (0). The interval callback always sees that captured `0` because the effect doesn't re-run to capture new scope.
</details>

### Q53. React Keys & Index:
Why is using `index` as a key in a list typically bad?
A. It throws an error  
B. It breaks CSS  
C. It causes performance issues and state bugs when items are reordered/inserted  
D. Indexes start at 0  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Keys tell React which elements are stable. If index is used, and an item is inserted at top, all indexes shift. React thinks *all* components changed, or worse, reuses component state for the wrong data (e.g., input text stays in row 1 even if data moved to row 2).
</details>

### Q54. `useEffect` Cleanup function timing:
A. Runs before every render  
B. Runs after the component unmounts AND before the effect re-runs (on update)  
C. Runs only on unmount  
D. Runs synchronously  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The cleanup function runs to clean up the *previous* effect before applying the *new* one (if dependencies changed), and finally when the component unmounts.
</details>

### Q55. Synthetic Events vs Native Events:
A. Synthetic is slower  
B. Synthetic Events are a cross-browser wrapper around the browser’s native event system  
C. Synthetic Events don't bubble  
D. They are deprecated  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
React normalizes events so they have consistent properties across different browsers. They are pooled (in older React, though pooling was removed in v17) and delegated to root.
</details>

### Q56. Calling Hooks inside a loop/condition?
A. Allowed  
B. Allowed only in useEffect  
C. Strict Violation of Rules of Hooks  
D. Warnings only  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Hooks must be called in the exact same order on every render. Loops/conditions change the order/number of calls, breaking React's internal state array tracking.
</details>

### Q57. `useLayoutEffect` vs `useEffect` timing:
A. `useLayoutEffect` fires *after* paint (async); `useEffect` fires *before* paint (sync)  
B. `useLayoutEffect` fires synchronously *after* DOM mutations but *before* browser paint  
C. Same timing  
D. `useLayoutEffect` is for layout engines only  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`useLayoutEffect` blocks visual updates. Use it to measure DOM or mutate DOM before the user sees it, preventing flicker. `useEffect` is deferred until after paint.
</details>

### Q58. `React.memo` default comparison:
A. Deep equality  
B. Shallow equality of props  
C. Referenced equality  
D. Always returns true  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`React.memo` checks if current props are shallowly equal to next props. If `props.user` is a new object reference (even with same data), it re-renders.
</details>

### Q59. What triggers a React re-render?
A. Props change, State change, Parent re-render, Context change  
B. only State change  
C. Changing a `useRef` value  
D. Timer functions  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
All listed in 'A' trigger updates. Notably, changing a `ref.current` does *not* trigger a re-render.
</details>

### Q60. Lazy Initialization of State:
```javascript
const [val, setVal] = useState(() => expensiveComputation());
```
vs
```javascript
const [val, setVal] = useState(expensiveComputation());
```
Difference?
A. None  
B. Second one runs computation on *every* render; First one runs only on Mount  
C. First one is invalid syntax  
D. Second one is faster  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Passing a function to `useState` (Lazy Init) runs it only once. Calling the function directly inside `useState(...)` executes it on every render, even though React ignores the result on subsequent renders.
</details>

### Q61. React Portals event bubbling:
A. Events bubble to the React entry point (Parent), even if Portal is somewhere else in DOM  
B. Events bubble to the DOM parent only  
C. No bubbling  
D. Bubbling is disabled  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Even if a Portal renders a child into `document.body`, an event fired from it will bubble up to its *React* parent component, preserving the React tree structure over the DOM structure.
</details>

### Q62. `useReducer` dispatch stability:
A. `dispatch` function changes on every render  
B. `dispatch` identity is stable and guaranteed not to change  
C. `dispatch` changes if reducer changes  
D. Depends on dependency array  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
React guarantees that `dispatch` is stable. You don't need to add it to generic `useEffect` dependency lists (though linter might not complain).
</details>

### Q63. Controlled Input with `value={undefined}`?
```javascript
<input value={undefined} onChange={...} />
```
A. Controlled  
B. Uncontrolled  
C. Throws Error  
D. Read only  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
If `value` is undefined (or null), React treats it as an *uncontrolled* component. Input becomes editable. Switching from defined to undefined throws a warning about switching controlled to uncontrolled.
</details>

### Q64. `useCallback` with empty deps `[]`:
A. Recurs every render  
B. Returns the exact same function instance across renders  
C. Does nothing  
D. Invalid  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
It memoizes the function once on mount and returns that same instance forever (unless component unmounts).
</details>

### Q65. `forwardRef` usage:
A. forwarding props  
B. passing a ref from a parent to a child’s DOM node  
C. forwarding routing  
D. optimizing refs  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Functional components don't accept `ref` by default. `forwardRef` allows a parent to get a ref to a DOM node inside the child component.
</details>

### Q66. Conditional Rendering pitfall:
```javascript
{ count && <Component /> }
```
If `count` is `0`, what renders?
A. Nothing  
B. `0`  
C. `<Component />`  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`0` is falsy. The logical AND operator returns the falsy value (`0`). React renders number `0` in the UI. Better to use `count > 0 && ...` or `!!count && ...`.
</details>

### Q67. `capture` phase event handling in React?
A. `onClickCapture`  
B. `onClick` with flag  
C. `onCapture`  
D. Impossible  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Append `Capture` to event names, e.g., `onClickCapture`, to handle events in the capture phase (downwards) instead of bubbling phase.
</details>

### Q68. Context API performance issue:
A. Context is slow in general  
B. Updating context value triggers re-render in ALL consumers, even if they only use part of the data  
C. Context cannot hold objects  
D. Limited to Strings  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Any change in the Context Provider `value` triggers a re-render in every `useContext` consumer. Optimization often involves splitting context or memoization.
</details>

### Q69. `useRef` for previous value:
```javascript
const ref = useRef();
useEffect(() => { ref.current = value; }, [value]);
const prev = ref.current;
```
A. `prev` is current value  
B. `prev` is value from previous render  
C. `prev` is undefined always  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Since `useEffect` runs *after* render, `ref.current` is updated after the render output is calculated. During the render, `ref.current` still holds the old value.
</details>

### Q70. React Fiber?
A. New styling engine  
B. New Reconciliation engine enabling features like Suspense/Concurrent Mode  
C. Database  
D. Build tool  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Fiber is the reimplementation of React's core algorithm, allowing work splitting (time slicing) and pausing re-renders.
</details>

### Q71. Error Boundary limitations?
A. Catches all errors  
B. Cannot catch errors in Event Handlers, Async code, or SSR  
C. Only works in functional components  
D. Deprecated  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Error Boundaries only catch errors in render, lifecycle, and constructors. They do NOT catch errors in `onClick`, `setTimeout`, etc.
</details>

### Q72. Correct way to reset state from props?
A. `getDerivedStateFromProps`  
B. `useEffect` with dependency on prop OR using a `key` on the component  
C. Constructor  
D. `componentWillReceiveProps`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The modern/cleanest way to fully reset a component when an ID changes is to pass a different `key` to it (remounts it). Alternatively, use `useEffect` to sync (but try to avoid derived state).
</details>

### Q73. JSX Children constraint:
A. Can be String, Number, Element, Array  
B. Can be Object  
C. Objects are not valid as a React child  
D. Booleans render as text  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Objects (e.g., `<div >{{ a:1 }}</div>`) are valid in props but invalid as direct children. It throws "Objects are not valid as a React child".
</details>

### Q74. `PureComponent` comparison depth?
A. Deep  
B. Shallow  
C. None  
D. Reference only  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`PureComponent` implements `shouldComponentUpdate` with a shallow prop and state comparison.
</details>

### Q75. Hook Rule: Why not in nested function?
A. Performance  
B. Variable scoping  
C. React relies on execution order index which would get messed up  
D. Syntax Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
React stores hooks in a linked list/array associated with the component. It relies on the index/order stability to know which state belongs to which `useState` call.
</details>

## Part 6: Redux & Advanced Integrations (Day 11-13)

### Q76. Redux Reducer: `(state = initialState, action)` default arg?
A. Sets state if it is explicitly `null`  
B. Sets state if it is `undefined` (e.g., first run)  
C. Always overrides state  
D. Invalid syntax  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The ES6 default parameter syntax initializes state when Redux sends `undefined` (classic initialization step).
</details>

### Q77. Redux Middleware signature?
A. `store => next => action => {}`  
B. `action => next => store => {}`  
C. `(store, action, next) => {}`  
D. `state => action => {}`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
It's a curried function chain: `storeInstance => nextMiddleware => action => { ... }`.
</details>

### Q78. Connected Component and `ownProps`:
A. `mapStateToProps(state, ownProps)`  
B. `ownProps` is not available  
C. `connect` deletes ownProps  
D. Props are merged randomly  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
If specified, `mapStateToProps` receives `ownProps` (props passed to the wrapper component) as the second argument. Useful for selecting data based on an ID passed as prop.
</details>

### Q79. Reselect library purpose:
A. AJAX  
B. Memoized Selectors to prevent recalculation derived data  
C. Selecting DOM nodes  
D. Routing  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
It caches the result of selectors. If state args haven't changed, it returns the cached object ref, helping avoid re-renders (referential equality).
</details>

### Q80. Redux "Ducks" pattern?
A. Animal sounds  
B. Bundling reducers, actions, and types in a single file per feature  
C. Splitting everything into separate folders  
D. Using Context  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
A popular community proposal for modularizing Redux: keeps logic for a widget self-contained.
</details>

### Q81. Redux DevTools Time Travel depends on?
A. Mutations  
B. State Immutability and Pure Reducers  
C. LocalStorage  
D. Server Side Rendering  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Because state is never mutated (always replaced), DevTools can store snapshots of previous states and swap the current state pointer to jump back/forth.
</details>

### Q82. `useSelector` equality check?
A. Shallow Equality (===) of the returned value  
B. Deep Equality  
C. No check  
D. Key check  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`useSelector` compares the *result* of the selector function using strict reference equality (`===`). If you return a new object every time `=> ({ a: state.a })`, it will force a re-render every time.
</details>

### Q83. jQuery `prop()` vs `attr()`?
A. `attr` for HTML attributes, `prop` for DOM properties (live values)  
B. Same  
C. `prop` is deprecated  
D. `attr` is faster  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Crucial distinction: A checkbox `checked` attribute is the initial value. The `checked` property is the current live state (true/false) after user interaction. Use `prop()` for booleans.
</details>

### Q84. jQuery Event Delegation:
```javascript
$('ul').on('click', 'li', handler);
```
Why do this instead of `$('li').click(handler)`?
A. Syntax preference  
B. Works for dynamically added `li` elements (future elements)  
C. Slower  
D. Only works for ul  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The listener is attached to `ul`. It checks if the click target matches `'li'` at bubbling time. Allows handling clicks on `li`s that didn't exist when code ran.
</details>

### Q85. `$(this)` inside arrow function in jQuery?
A. The element  
B. The window/parent context (lexical this)  
C. The jQuery object  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Arrow functions do not bind their own `this`; they inherit it. `$(...)...( () => this )`: `this` will likely be Window, breaking typical jQuery patterns where `this` is expected to be the DOM element.
</details>

### Q86. Axios vs Fetch (Error Handling):
A. Both throw on 404  
B. Fetch does NOT reject on HTTP 404/500; Axios does  
C. Axios does NOT reject on 404  
D. Fetch throws on 404  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Fetch only rejects on network failure. You must check `response.ok`. Axios automatically rejects the promise if the status code falls outside the 2xx range.
</details>

### Q87. CommonJS circular dependency resolution?
A. Infinite loop  
B. Returns incomplete copy of exports  
C. Throws Error  
D. Waits forever  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Node returns the `exports` object as it exists *at the moment require is called*. If the cycle is not carefully managed, one module might get an empty object.
</details>

### Q88. `module.exports` vs `exports` mutation:
```javascript
exports.a = 1;
module.exports = { b: 2 };
```
What is exported?
A. `{ a: 1, b: 2 }`  
B. `{ a: 1 }`  
C. `{ b: 2 }`  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
`exports` initially points to `module.exports`. Reassigning `module.exports` breaks that link. Node returns `module.exports`, so only `{ b: 2 }` is exported.
</details>

### Q89. `process.env` types?
A. All values are Strings  
B. Preserves Types (Number, Bool)  
C. Objects  
D. Binary  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Environment variables are always strings. `PORT=3000` -> `process.env.PORT` is `"3000"`.
</details>

### Q90. React `flushSync`?
A. Flushes the toilet  
B. Forces simplified rendering  
C. Forces React to flush updates synchronously  
D. Clears cache  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Rarely used. It forces React to perform the update immediately (breaking batching) before the line of code finishes.
</details>

### Q91. React: Why not mutate `this.state` directly?
A. JS forbids it  
B. React won't know state changed (no `setState` call) -> No Re-render  
C. It crashes  
D. Security risk  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
React does not observe object properties. It relies on `setState` to trigger the reconciliation queue.
</details>

### Q92. `dangerouslySetInnerHTML` purpose?
A. To set HTML from string  
B. To create error  
C. To hack site  
D. To set styles  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
React's replacement for `innerHTML`. Named dangerously to remind developers of XSS risks.
</details>

### Q93. React Router `<Link>` vs `<a>`?
A. No difference  
B. `<a>` reloads the page (full refresh); `<Link>` handles routing internally (SPA navigation)  
C. `<Link>` is slower  
D. `<a>` is deprecated  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`<Link>` uses History API `pushState` to change URL without triggering a browser page load request.
</details>

### Q94. Redux Toolkit `createSlice` uses Immer. What does Imner do?
A. Allows writing "mutating" logic that actually produces immutable updates  
B. Validates types  
C. Connects to API  
D. Logs actions  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Immer uses Proxies to record mutations (`state.count++`) and produces a new immutable state tree automatically, simplifying reducer logic.
</details>

### Q95. Node Stream `backpressure`?
A. Gas leak  
B. When WriteStream cannot consume data as fast as ReadStream produces it  
C. Network error  
D. CPU overload  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Crucial concept. If the internal buffer fills (`write()` returns false), the readable stream should pause until the drain event to avoid implicit memory overflow.
</details>

### Q96. Buffer `allocUnsafe` vs `alloc`?
A. `allocUnsafe` is slower  
B. `allocUnsafe` does not zero-fill memory (may contain old sensitive data)  
C. `alloc` uses GPU  
D. No difference  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`alloc` zeroes out memory (safe but slower). `allocUnsafe` grabs uninitialized memory (fast but risky).
</details>

### Q97. `cluster.fork()` sharing?
A. Shares memory  
B. Shares nothing (separate processes), but shares server handle (port)  
C. Shares variables  
D. Shares event loop  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Worker processes are distinct OS processes with their own V8 instance/Memory. They communicate via IPC. They can share a TCP connection (the port).
</details>

### Q98. Express Error Handler position?
A. Top of file  
B. Before routes  
C. Last middleware (After all routes)  
D. Doesn't matter  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
It must be defined last. If a route sends a response, it stops. If a route calls `next(err)`, control skips strictly to error handlers defined *after* it.
</details>

### Q99. What returns a Promise?
A. `setTimeout`  
B. `fs.readFile`  
C. `fetch` or `async function`  
D. `Array.map`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Standard async APIs and async functions return Promises. Callbacks (A, B) do not.
</details>

### Q100. `Promise.allSettled` vs `Promise.all`?
A. `allSettled` waits for all to finish regardless of status; `all` fails fast  
B. Same  
C. `allSettled` is faster  
D. `all` waits for all  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`allSettled` returns an array of status objects matching each input promise, never rejecting (unless input is invalid). `all` rejects on first error.
</details>


## Part 7: Advanced Patterns, Security & Optimization

### Q101. HOC (Higher-Order Component) definition?
A. A component that renders high up in the tree  
B. A function that takes a component and returns a new component  
C. A Redux store  
D. A Parent component  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Pattern for reusing component logic. `const Enhanced = withAuth(WrappedComponent)`.
</details>

### Q102. Render Props pattern?
A. Passing a function as a prop (often named `render`) that returns a React element  
B. Rendering props to the DOM  
C. Passing props to render method  
D. Deprecated  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Allows sharing code between React components using a prop whose value is a function. `<DataProvider render={data => <Display data={data} />} />`.
</details>

### Q103. React: `key` prop on `<Fragment>`?
A. Impossible  
B. Allowed only with explicit syntax `<React.Fragment key={id}>`  
C. Allowed with short syntax `<>key={id}</>`  
D. Fragments don't need keys  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The shorthand `<>` does not support attributes. You must use `<React.Fragment key={...}>` if you are mapping a list of fragments.
</details>

### Q104. Preventing XSS in React?
What is typically the only way XSS happens in React?
A. Using `{}`  
B. Using `dangerouslySetInnerHTML` or user-provided entries in `href` (javascript: URI)  
C. Using Props  
D. Using State  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
React escapes values by default. The risk opens up when bypassing this protection explicitly or allowing execution via attributes like `href="javascript:..."`.
</details>

### Q105. CSRF (Cross-Site Request Forgery) mitigation?
A. Use HTTPS  
B. Anti-CSRF Tokens (Double Submit Cookie or Synchronizer Token)  
C. Use JWT  
D. Limit file size  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Ensures that the request comes from your own authenticated frontend, often by verifying a token hidden in a form or header that a separate site cannot read.
</details>

### Q106. JWT storage best practice (XSS safe)?
A. LocalStorage  
B. SessionStorage  
C. HttpOnly Cookie  
D. Redux State  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
LocalStorage is accessible by JS, making it vulnerable to XSS. HttpOnly cookies cannot be accessed by client-side JS, mitigating XSS token theft.
</details>

### Q107. Node: `child_process.exec` vs `spawn`?
A. `exec` buffers output (good for small data); `spawn` streams output (good for large data/long process)  
B. `spawn` is synchronous  
C. `exec` is faster  
D. `spawn` creates threads  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`exec` runs a command in a shell and buffers the output (max 200kb default). `spawn` launches a new process and streams stdout/stderr, better for heavy loads.
</details>

### Q108. Express: Rate Limiting purpose?
A. Save money  
B. Prevent DDOS and Brute Force attacks  
C. Make site faster  
D. Limit database size  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Restricts the number of requests a client can make in a given timeframe (`express-rate-limit`).
</details>

### Q109. Database Indexing trade-off?
A. Faster reads, Slower writes  
B. Slower reads, Faster writes  
C. Faster everything  
D. Slower everything  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Indexes speed up search (SELECT) but must be updated whenever data changes (INSERT/UPDATE/DELETE), adding overhead to writes.
</details>

### Q110. React `useImperativeHandle`?
A. Handles errors  
B. Customizes the instance value that is exposed to parent components when using `ref`  
C. Forces imperative code  
D. DOM manipulation  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Used with `forwardRef` to hide internal DOM nodes and only expose specific methods (like `focus()`) to the parent.
</details>

### Q111. `Object.seal()` vs `Object.freeze()`?
A. `seal` prevents adding/deleting properties but allows modifying existing values; `freeze` makes it fully immutable  
B. `freeze` allows modification  
C. Same  
D. `seal` is for arrays  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`seal`: existing props are mutable. `freeze`: read-only everywhere.
</details>

### Q112. What is a "Thunk"?
A. A noise  
B. A function returned by another function to delay computation (middleware for async Redux)  
C. A database  
D. An error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
In Redux, a Thunk is an action creator that returns a function (`dispatch => ...`) instead of an action object, allowing side effects.
</details>

### Q113. Redux Saga uses?
A. Generators (`function*`)  
B. Promises only  
C. Callbacks  
D. Observable  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Saga leverages ES6 Generators to make async flows read like synchronous code (`yield call(...)`).
</details>

### Q114. Node: `process.memoryUsage().heapUsed`?
A. Total memory on PC  
B. Memory used by V8 for objects/variables (GC managed)  
C. C++ memory  
D. Buffer memory  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Refers to the actual memory used by JS objects. Key metric for leak detection.
</details>

### Q115. `Function.prototype.call` first arg?
A. The arguments  
B. The `this` context  
C. The function name  
D. The return value  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
The first argument to `call`, `apply`, and `bind` is always the object to be used as `this`.
</details>

### Q116. JS: `(function(){})()` pattern name?
A. Callback  
B. IIFE (Immediately Invoked Function Expression)  
C. Closure  
D. Module  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Used to create a private scope and avoid polluting global namespace.
</details>

### Q117. React: What is "Reconciliation"?
A. The diffing algorithm React uses to decide which parts of the DOM need updating  
B. API fetching  
C. CSS layout  
D. Error checking  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
React compares the new Element tree with the previous one to determine the minimum operations to update the real DOM.
</details>

### Q118. `Promise.resolve(5).then(v => v*2).then(v => { throw new Error(v) }).catch(e => console.log(e.message))`?
A. 5  
B. 10  
C. Error  
D. Uncaught exception  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Chain: 5 -> 10 -> Error(10) -> Catch logs message "10".
</details>

### Q119. Browser Storage Limit (LocalStorage)?
A. ~5MB-10MB per origin  
B. Unlimited  
C. 1KB  
D. 1GB  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Typically around 5MB string data. Varies slightly by browser.
</details>

### Q120. `3` in `[3]`?
A. Check Index  
B. Check Value (includes)  
C. Syntax Error  
D. `in` operator checks if property/index exists  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** D  

**Explanation:**  
`3 in [1, 2, 3]` is `false` because the array has indices 0, 1, 2. Index 3 does not exist. `0 in [1]` is true.
</details>

### Q121. Semantic Versioning `^1.2.3`?
A. Exactly 1.2.3  
B. Compatible with 1.2.3 (updates minor/patch: < 2.0.0)  
C. Compatible with 1.2.3 (updates patch only: < 1.3.0)  
D. Latest  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Caret (`^`) allows changes that do not modify the left-most non-zero digit. For 1.x, it allows 1.9.9 but not 2.0.0.
</details>

### Q122. `npm ci` vs `npm install`?
A. `ci` is for Continuous Integration (clean install from lockfile only)  
B. `ci` is interactive  
C. `install` is faster  
D. `ci` updates packages  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
`ci` deletes `node_modules`, strictly installs from `package-lock.json`, and errors if `package.json` mismatches. Faster and reliable for builds.
</details>

### Q123. Node `crypto` module use?
A. Mining bitcoin  
B. Hashing, Encryption, Random bytes  
C. Currency conversion  
D. Compression  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Standard library for secure cryptographic operations (hash passwords, tokens).
</details>

### Q124. React `Prop Drilling` solution?
A. Use `Context` or Redux  
B. Use `props`  
C. Use `html`  
D. Use `global`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Passing props through many intermediate components is tedious. State management tools solve this.
</details>

### Q125. `Math.max()` with no args?
A. 0  
B. Infinity  
C. -Infinity  
D. NaN  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
It returns -Infinity so that any number compared to it will be larger (identity for max). `Math.min()` returns Infinity.
</details>

### Q126. `[1, 2] + [3, 4]`?
A. `[1, 2, 3, 4]`  
B. `"1,23,4"`  
C. Error  
D. `NaN`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Both arrays convert to strings: `"1,2"` and `"3,4"`. Then concatenation occurs: `"1,2" + "3,4"` -> `"1,23,4"`.
</details>

### Q127. Check if variable is Array?
A. `typeof var === 'array'`  
B. `Array.isArray(var)`  
C. `var instanceof Array` (fails across iframes)  
D. `var.type === 'Array'`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`typeof` returns 'object'. `Array.isArray()` is the robust standard method.
</details>

### Q128. `NaN` type check?
A. `typeof NaN === 'number'`  
B. `typeof NaN === 'NaN'`  
C. `typeof NaN === 'undefined'`  
D. `typeof NaN === 'object'`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
It stands for Not-a-Number, but it is a numeric type value.
</details>

### Q129. Node: `__filename` vs `__dirname`?
A. `__filename` includes the file name; `__dirname` is just the folder path  
B. Same  
C. Opposite  
D. `__filename` is relative  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Standard CommonJS globals for absolute paths.
</details>

### Q130. jQuery `$(document).ready()` replacement?
A. `$(function() { ... })`  
B. `document.ready = ...`  
C. `window.onload`  
D. `wait()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Pass a function directly to `$()` is the shorthand for the ready event.
</details>

### Q131. React: `class` attribute in JSX?
A. `class="..."`  
B. `className="..."`  
C. `style="..."`  
D. `css="..."`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`class` is a reserved keyword in JS. React uses `className` which compiles to the class attribute.
</details>

### Q132. `let` scoping?
A. Function scope  
B. Block scope  
C. Global scope only  
D. Module scope  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`let` and `const` adhere to the block `{}` they are defined in. `var` ignores blocks (function scope).
</details>

### Q133. JS: `String` immutability?
A. Strings can be changed in place  
B. Strings are immutable; methods return new strings  
C. Depends on `const`  
D. Only in strict mode  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Primitives (Strings, Numbers) cannot be mutated. `str[0] = 'a'` does nothing. You must reassign.
</details>

### Q134. Express: `res.json(body)` calls `res.send`?
A. No  
B. Yes, internally  
C. Error  
D. Opposite  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
`res.json` sets the header and then calls `res.send` with the stringified JSON.
</details>

### Q135. React: `style` prop format?
A. String `"color: red"`  
B. Object `{{ color: 'red', fontSize: '10px' }}`  
C. Array  
D. CSS file  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
CamelCased properties in a JS object.
</details>

### Q136. `Array.splice` vs `Array.slice`?
A. `splice` mutates array (removes/adds); `slice` returns a copy (subarray)  
B. `splice` is copy; `slice` is mutation  
C. Same  
D. `splice` joins strings  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Tricky interview favorite. `splice` changes original array. `slice` is pure.
</details>

### Q137. React: Unique Key Requirement scope?
A. Global  
B. Across the entire app  
C. Among siblings in the same list  
D. Random  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C  

**Explanation:**  
Keys must be unique only among siblings. Different lists can use the same keys.
</details>

### Q138. Redux: How to handle multiple reducers?
A. `combineReducers`  
B. `mergeReducers`  
C. `arrayReducers`  
D. `loops`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Combines slice reducers into a single root reducer function.
</details>

### Q139. Node: Reading large files without RAM crash?
A. `fs.readFileSync`  
B. `fs.createReadStream` (Streams)  
C. `fs.readFile`  
D. Increase RAM download  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Streams allow processing data chunk by chunk (small memory footprint).
</details>

### Q140. JS: `new Set([1, 1, 2, 2]).size`?
A. 4  
B. 2  
C. 1  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Sets remove duplicates. `{1, 2}` remains.
</details>

### Q141. React: `useState` initial value callback vs value?
A. `useState(fn)` calls fn on every render  
B. `useState(() => val)` calls fn ONLY on mount (lazy init)  
C. `useState(fn())` calls fn on mount  
D. `useState` has no callback  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Lazy initialization prevents expensive calculations from running on every re-render.
</details>

### Q142. JS: `Object.assign({}, target)`?
A. Shallow Copy  
B. Deep Copy  
C. Reference Copy  
D. Error  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Copies enumerable own properties. Nested objects are still referenced.
</details>

### Q143. Express: Middleware that parses JSON?
A. `express.json()`  
B. `express.body()`  
C. `JSON.parse()`  
D. `body-parser.all()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Built-in middleware (based on body-parser) available in Express 4.16+.
</details>

### Q144. `useEffect` empty dependency array `[]` simulates?
A. `componentDidMount` (and `componentWillUnmount` for return)  
B. `componentDidUpdate`  
C. `render`  
D. `shouldComponentUpdate`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Runs once after initial render.
</details>

### Q145. JS: `typeof null`?
A. `null`  
B. `object`  
C. `undefined`  
D. `0`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Famous JS bug/legacy behavior. `null` is a primitive, but `typeof` says object.
</details>

### Q146. `bind` returns?
A. Execution result  
B. A function  
C. `this`  
D. undefined  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Creates a new function that, when called, has its `this` keyword set to the provided value.
</details>

### Q147. What represents `false` in JS?
A. `false`, `0`, `""`, `null`, `undefined`, `NaN`  
B. Only `false`  
C. `false` and `0`  
D. `false`, `-1`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
The complete list of "falsy" values. Everything else is truthy.
</details>

### Q148. React: Uncontrolled component data access?
A. `state`  
B. `ref` (DOM access)  
C. `props`  
D. `context`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
You access the current value of the DOM node directly using a Ref, instead of through React state.
</details>

### Q149. Node: `process.stdin` is?
A. Writable Stream  
B. Readable Stream  
C. File  
D. String  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B  

**Explanation:**  
Standard Input. You can listen for 'data' events on it.
</details>

### Q150. Final: The "Throttling" technique?
A. Calling function only once in a specified time interval (e.g., once every 100ms)  
B. Delaying function until user stops typing (Debounce)  
C. Crashing server  
D. Speeding up CPU  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A  

**Explanation:**  
Ensures function doesn't run more often than X times per second (e.g., scroll handlers). Distinct from Debouncing (which waits for pause).
</details>

---

# Completion Confirmation
I confirm that this second Question Bank ("Deep Dive") contains 150 additional, harder questions strictly derived from the Day 01-13 syllabus, focusing on edge cases, internals, and architectural concepts. No external topics were added.


