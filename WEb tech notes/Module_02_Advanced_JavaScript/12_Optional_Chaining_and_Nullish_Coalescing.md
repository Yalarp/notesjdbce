# Optional Chaining and Nullish Coalescing in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [The Non-Existing Property Problem](#2-the-non-existing-property-problem)
3. [Optional Chaining (?.)](#3-optional-chaining-)
4. [Optional Chaining with Functions](#4-optional-chaining-with-functions)
5. [Optional Chaining with Arrays](#5-optional-chaining-with-arrays)
6. [Nullish Coalescing Operator (??)](#6-nullish-coalescing-operator-)
7. [Comparison: ?? vs ||](#7-comparison--vs-)
8. [Practical Examples](#8-practical-examples)
9. [Quick Reference](#9-quick-reference)
10. [Interview Questions](#10-interview-questions)

---

## 1. Introduction

### 1.1 Definition
**Optional Chaining (`?.`)** is a safe way to access nested object properties, even when an intermediate property doesn't exist. **Nullish Coalescing (`??`)** is an operator that returns the right-hand operand when the left-hand operand is null or undefined.

### 1.2 Purpose
- Prevent errors when accessing properties of null/undefined
- Provide cleaner code for nested property access
- Handle default values more precisely
- Short-circuit evaluation for safer code

### 1.3 Key Benefits

| Feature | Benefit |
|---------|---------|
| `?.` | Prevents "Cannot read property of undefined" errors |
| `??` | Provides defaults only for null/undefined (not falsy values) |
| Short-circuit | Stops evaluation if left side is null/undefined |

---

## 2. The Non-Existing Property Problem

### 2.1 The Problem

```javascript
let user = {}; // a user without "address" property

alert(user.address.street); // Error!
```

**Error Message:**
```
TypeError: Cannot read property 'street' of undefined
```

### 2.2 Why This Happens

```javascript
user.address      // undefined
user.address.street  // ERROR: Cannot read 'street' of undefined
```

### 2.3 Traditional Solutions (Ugly)

**Using if statement:**
```javascript
let user = {};
if (user.address) {
    alert(user.address.street);
}
```

**Using ternary operator:**
```javascript
let user = {};
alert(user.address ? user.address.street : undefined);
```

**Deeply nested (horrible!):**
```javascript
let user = {};
alert(user.address ? (user.address.street ? user.address.street.name : null) : null);
```

---

## 3. Optional Chaining (?.)

### 3.1 Basic Syntax

```javascript
value?.prop
```

- If `value` exists (not null/undefined): returns `value.prop`
- If `value` is null/undefined: returns `undefined`

### 3.2 Basic Examples

**Without optional chaining (crashes):**
```javascript
<script>
let user;  // user has no address
alert(user.address);
document.write("ERR");  // Never reached
</script>
// Result: Application crash
```

**With optional chaining (safe):**
```javascript
<script>
let user;  // user has no address
alert(user?.address);  // undefined
document.write("Flow will go ahead");
</script>
// Output: undefined
// Flow will go ahead
```

### 3.3 With null Values

```javascript
<script>
let user = null;
alert(user?.address);  // undefined (no crash!)
document.write("flow will go ahead");
</script>
// Output: undefined
// flow will go ahead
```

### 3.4 Chaining Multiple Levels

```javascript
let user = {}; // user has no address

// Safe access to nested properties
alert(user?.address?.street); // undefined (no error)
```

### 3.5 Important Rules

**Rule 1: Variable must be declared**
```javascript
// ReferenceError: user is not defined
user?.address;  // ERROR if user is not declared!

// Correct:
let user;
user?.address;  // undefined (OK)
```

**Rule 2: Only makes left side optional**
```javascript
// ?. only makes 'user' optional, not 'address'
user?.address.street

// To make 'address' also optional:
user?.address?.street
```

**Rule 3: Cannot use for assignment**
```javascript
let user = null;
user?.name = "John"; // Error!
// Because it evaluates to: undefined = "John"
```

### 3.6 Short-Circuiting

When `?.` evaluates to undefined, further evaluation stops:

```javascript
let user = null;
let x = 0;

user?.sayHi(x++); // x++ never executes
alert(x); // 0, value not incremented
```

---

## 4. Optional Chaining with Functions

### 4.1 Syntax: ?.()

```javascript
obj.method?.()
```

Calls the method if it exists, returns undefined otherwise.

### 4.2 Example

```javascript
let userAdmin = {
    admin() {
        alert("I am admin");
    }
};

let userGuest = {};

userAdmin.admin?.(); // "I am admin"
userGuest.admin?.(); // Nothing (no error, method doesn't exist)
```

### 4.3 Calling Potentially Undefined Functions

```javascript
let apiResponse = {
    data: null,
    getData: function() {
        return this.data;
    }
};

// Safe function call
let result = apiResponse.getData?.();  // Works
let missing = apiResponse.getMissing?.();  // undefined (no error)
```

---

## 5. Optional Chaining with Arrays

### 5.1 Syntax: ?.[]

```javascript
obj?.[prop]
```

### 5.2 Example

```javascript
let key = "firstName";

let user1 = {
    firstName: "John"
};

let user2 = null;

alert(user1?.[key]); // "John"
alert(user2?.[key]); // undefined (no error)
```

### 5.3 With delete

```javascript
let user = { name: "John" };
delete user?.name; // Deletes user.name if user exists

let nullUser = null;
delete nullUser?.name; // Safe, does nothing
```

---

## 6. Nullish Coalescing Operator (??)

### 6.1 Syntax

```javascript
result = a ?? b;
```

- If `a` is defined (not null/undefined): returns `a`
- If `a` is null/undefined: returns `b`

### 6.2 Equivalent Code

```javascript
result = a ?? b;

// Is the same as:
result = (a !== null && a !== undefined) ? a : b;
```

### 6.3 Basic Examples

```javascript
let user;
alert(user ?? "Anonymous"); // "Anonymous"

let user = "John";
alert(user ?? "Anonymous"); // "John"
```

### 6.4 Use in Functions

```javascript
// Old way using ||
function add(a, b) {
    b = b || 1;  // Problem: 0 is falsy!
    return a + b;
}

add(5, 0);  // Returns 6, not 5! (0 is falsy, so b becomes 1)

// New way using ??
function add(a, b) {
    b = b ?? 1;  // Only replaces null/undefined
    return a + b;
}

add(5, 0);  // Returns 5 (0 is NOT null/undefined)
```

---

## 7. Comparison: ?? vs ||

### 7.1 Key Difference

| Operator | Returns right side when left is: |
|----------|----------------------------------|
| `||` | Falsy (false, 0, "", null, undefined, NaN) |
| `??` | Nullish (null, undefined only) |

### 7.2 Examples

```javascript
let height = 0;

console.log(height || 100);  // 100 (0 is falsy)
console.log(height ?? 100);  // 0 (0 is NOT nullish)

let name = "";

console.log(name || "Anonymous");  // "Anonymous" (empty string is falsy)
console.log(name ?? "Anonymous");  // "" (empty string is NOT nullish)
```

### 7.3 Choosing Between ?? and ||

| Use `??` when | Use `||` when |
|---------------|---------------|
| 0 is a valid value | 0 should be replaced |
| Empty string is valid | Empty string should be replaced |
| false is a valid value | false should be replaced |
| Only want to replace null/undefined | Want to replace all falsy values |

### 7.4 Practical Comparison

```javascript
let firstName = null;
let lastName = null;
let nickName = "Supercoder";

// Using || (shows first truthy value)
alert(firstName || lastName || nickName || "Anonymous"); // "Supercoder"

// Using ?? (shows first non-nullish value)
alert(firstName ?? lastName ?? nickName ?? "Anonymous"); // "Supercoder"
```

---

## 8. Practical Examples

### 8.1 API Response Handling

```javascript
function displayUser(response) {
    // Safe access to nested data
    const userName = response?.data?.user?.name ?? "Guest";
    const userEmail = response?.data?.user?.email ?? "No email";
    
    console.log(`User: ${userName}, Email: ${userEmail}`);
}

// Works with various response shapes:
displayUser({ data: { user: { name: "John", email: "john@test.com" } } });
displayUser({ data: null });
displayUser(null);
```

### 8.2 DOM Element Access

```javascript
// Safe DOM access
const element = document.querySelector('.elem');
const innerHTML = element?.innerHTML ?? "Element not found";

// Without optional chaining:
const innerHTML = element ? element.innerHTML : "Element not found";
```

### 8.3 Configuration Objects

```javascript
function initApp(config) {
    const port = config?.server?.port ?? 3000;
    const host = config?.server?.host ?? "localhost";
    const timeout = config?.settings?.timeout ?? 5000;
    
    console.log(`Starting on ${host}:${port}, timeout: ${timeout}ms`);
}

initApp({});  // Uses all defaults
initApp({ server: { port: 8080 } });  // Custom port, default host
```

### 8.4 Calling Optional Callbacks

```javascript
function fetchData(options) {
    const data = { id: 1, name: "Test" };
    
    // Call callback if provided
    options?.onSuccess?.(data);
    options?.onComplete?.();
}

// With callbacks
fetchData({
    onSuccess: (data) => console.log("Got data:", data),
    onComplete: () => console.log("Done")
});

// Without callbacks (no error)
fetchData({});
```

---

## 9. Quick Reference

### 9.1 Optional Chaining Syntax

```javascript
obj?.prop        // Property access
obj?.[expr]      // Dynamic property access
arr?.[index]     // Array access
func?.()         // Function call
```

### 9.2 Nullish Coalescing

```javascript
value ?? default   // Returns default only if value is null/undefined
```

### 9.3 Three Forms of ?.

| Form | Description |
|------|-------------|
| `obj?.prop` | Returns obj.prop if obj exists, otherwise undefined |
| `obj?.[prop]` | Returns obj[prop] if obj exists, otherwise undefined |
| `obj.method?.()` | Calls obj.method() if it exists, otherwise undefined |

### 9.4 Combining ?. and ??

```javascript
const value = obj?.prop?.nested ?? "default";
```

---

## 10. Interview Questions

### Q1: What is optional chaining and why was it introduced?
**Answer**: Optional chaining (`?.`) is a safe way to access nested object properties. It was introduced to prevent "Cannot read property of undefined" errors when accessing properties of potentially null/undefined values. It returns undefined instead of throwing an error.

### Q2: What's the difference between ?. and the && operator for checking properties?
**Answer**: 
- `obj?.prop` returns undefined if obj is null/undefined
- `obj && obj.prop` returns obj if it's falsy, or obj.prop if truthy
- `?.` is cleaner and specifically checks for null/undefined

### Q3: What's the difference between ?? and ||?
**Answer**:
- `||` returns right side for any falsy value (false, 0, "", null, undefined, NaN)
- `??` returns right side ONLY for null or undefined
- Use `??` when 0 or empty string are valid values

### Q4: Can you use ?. for assignment?
**Answer**: No. Optional chaining cannot be used on the left side of an assignment:
```javascript
user?.name = "John"; // Error!
```
This is because it would evaluate to `undefined = "John"` which is invalid.

### Q5: What happens to code after ?. if the value is null/undefined?
**Answer**: It short-circuits. The evaluation stops immediately and returns undefined without executing any further code:
```javascript
user?.method(x++); // x++ never runs if user is null
```

### Q6: Does the variable before ?. need to be declared?
**Answer**: Yes. If the variable is not declared at all, you'll get a ReferenceError:
```javascript
user?.address; // ReferenceError if 'user' is not declared
```

---

## Navigation

← Previous: [11_Exception_Handling.md](./11_Exception_Handling.md) | Next: [13_Generators_and_Iterators.md](./13_Generators_and_Iterators.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 03*
