# Objects Basics in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Creating Objects](#2-creating-objects)
3. [Object Properties and Methods](#3-object-properties-and-methods)
4. [Literal Objects vs Constructor Objects](#4-literal-objects-vs-constructor-objects)
5. [The this Keyword](#5-the-this-keyword)
6. [Prototype and Prototype Methods](#6-prototype-and-prototype-methods)
7. [Object Copying (Shallow vs Deep)](#7-object-copying-shallow-vs-deep)
8. [Object Destructuring](#8-object-destructuring)
9. [call() and apply() Methods](#9-call-and-apply-methods)
10. [Quick Reference](#10-quick-reference)
11. [Interview Questions](#11-interview-questions)

---

## 1. Introduction

### 1.1 Definition
An object is a collection of related data and/or functionality, typically represented as key-value pairs called properties and methods.

### 1.2 Purpose
- Group related data together
- Model real-world entities
- Organize code into reusable units
- Enable Object-Oriented Programming patterns

### 1.3 Key Concept
In JavaScript, almost everything is an object. Even functions are objects (function objects). This is what makes JavaScript unique and powerful.

---

## 2. Creating Objects

### 2.1 Three Ways to Create Objects

| Method | Syntax | Use Case |
|--------|--------|----------|
| Object Constructor | `new Object()` | Dynamic property addition |
| Literal Notation | `{ key: value }` | Quick, simple objects |
| Constructor Function | `new FunctionName()` | Creating multiple similar objects |

### 2.2 Method 1: Using Object Constructor

```javascript
<script>
var obj = new Object();
obj.name = "vita";
obj.marks = 90;

document.write(obj);              // [object Object]
document.write(obj.constructor);  // function Object() { [native code] }
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 1 | `var obj = new Object()` | Creates new empty object using Object constructor |
| 2 | `obj.name = "vita"` | Adds property `name` with value "vita" |
| 3 | `obj.marks = 90` | Adds property `marks` with value 90 |
| 5 | `document.write(obj)` | Prints [object Object] (calls toString()) |
| 6 | `document.write(obj.constructor)` | Shows the constructor function |

**Memory Diagram:**
```
┌──────────────────────┐
│ obj                  │
├──────────────────────┤
│ name: "vita"         │
│ marks: 90            │
│ [[Prototype]]: Object│
└──────────────────────┘
```

### 2.3 Method 2: Literal Object

```javascript
<script>
var obj = {
    name: "raj",
    "2division": "A"    // Property name with number must be in quotes
};

obj.marks = 80;         // Adding property dynamically

alert(obj);                          // [object Object]
document.write(obj.constructor);     // function Object()
document.write(obj.name + "  " + obj["2division"]);  // raj  A
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 1-4 | `var obj = { ... }` | Creates object with literal notation |
| 3 | `"2division": "A"` | Property starting with number needs quotes |
| 6 | `obj.marks = 80` | Adds new property after creation |
| 10 | `obj["2division"]` | Access property with bracket notation |

**Two Ways to Access Properties:**
```javascript
obj.name        // Dot notation
obj["name"]     // Bracket notation

// Bracket notation REQUIRED when:
// - Property name has special characters
// - Property name starts with a number
// - Property name is stored in a variable
```

### 2.4 Method 3: Constructor Function (User-Defined Object)

```javascript
<script>
"use strict";
function person(nm, mks) {
    alert(this);           // Shows [object Object]
    this.name = nm;
    this.marks = mks;
}

var ob = new person("mona", 80);
document.write(ob);                    // [object Object]
document.write(ob.constructor);        // function person(nm, mks) {...}
document.write("<hr/>");
document.write(ob.name + " " + ob["name"]);  // mona mona

for (let pp in ob) {
    document.write(pp + "  " + ob[pp]);  // name mona, marks 80
}

document.write(ob instanceof person);  // true
document.write(ob instanceof Object);  // true

var ob1 = new person("Geeta", 900);
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 2 | `function person(nm, mks)` | Defines constructor function |
| 3 | `alert(this)` | `this` refers to the newly created object |
| 4-5 | `this.name = nm` | Creates instance properties |
| 8 | `new person("mona", 80)` | Creates new object using constructor |
| 10 | `ob.constructor` | Shows the constructor function used |
| 14-16 | `for (let pp in ob)` | Iterates over all properties |
| 18 | `ob instanceof person` | Checks if ob is instance of person |
| 19 | `ob instanceof Object` | All objects inherit from Object |

**Memory Diagram:**
```
┌──────────────────────┐     ┌──────────────────────┐
│ ob                   │     │ ob1                  │
├──────────────────────┤     ├──────────────────────┤
│ name: "mona"         │     │ name: "Geeta"        │
│ marks: 80            │     │ marks: 900           │
│ [[Prototype]]: person│     │ [[Prototype]]: person│
└──────────────────────┘     └──────────────────────┘
         │                           │
         └───────────┬───────────────┘
                     ↓
              ┌──────────────────┐
              │ person.prototype │
              ├──────────────────┤
              │ [[Prototype]]    │ → Object.prototype
              └──────────────────┘
```

---

## 3. Object Properties and Methods

### 3.1 Adding Methods to Literal Objects

```javascript
<script>
obj = {
    fname: "Raj",
    lname: "Mathur",
    age: 25,
    add: { d: "juhu" },           // Nested object
    fullname: function() {
        return this.fname + " " + this.lname;
    },
    toString: function() {
        return this.fullname() + "  " + this.age + " " + this.add.d;
    }
};

var f = obj.fullname();
document.write(f);                // Raj Mathur
document.write(obj);              // Raj Mathur  25 juhu
document.write(obj.toString());   // Raj Mathur  25 juhu
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 2-4 | Properties | Simple string and number properties |
| 5 | `add: { d: "juhu" }` | Nested object (address with district) |
| 6-8 | `fullname: function()` | Instance method that returns full name |
| 9-11 | `toString: function()` | Overrides Object's toString method |
| 11 | `this.add.d` | Accessing nested object property |
| 15 | `obj.fullname()` | Calling the method |
| 16 | `document.write(obj)` | Implicitly calls toString() |

**Memory Diagram:**
```
┌──────────────────────────────────┐
│ obj                              │
├──────────────────────────────────┤
│ fname: "Raj"                     │
│ lname: "Mathur"                  │
│ age: 25                          │
│ add: ──────────────→ { d: "juhu" }
│ fullname: ─────────→ function()  │
│ toString: ─────────→ function()  │
└──────────────────────────────────┘
```

### 3.2 Adding Methods to Constructor Functions

```javascript
<script>
"use strict";
function person(nm, ag) {
    this.name = nm;
    this.age = ag;
    this.speak = function() {      // Instance method
        return " hello " + this.name;
    };
    alert(this.constructor);
}

// Prototype methods - shared by all instances
person.prototype.walk = function() {
    return this.name + " can walk ";
};

person.prototype.toString = function() {
    return this.name + " " + this.age;
};

var obj1 = new person("raj", 80);
var x = new person("mona", 90);

document.write(obj1);             // raj 80
document.write(obj1.speak());     // hello raj
document.write(x);                // mona 90
document.write(x.speak());        // hello mona
document.write(x.walk());         // mona can walk
</script>
```

**Key Differences:**

| Instance Method | Prototype Method |
|----------------|------------------|
| `this.speak = function()` | `person.prototype.walk = function()` |
| Created for each object | Shared by all objects |
| Uses more memory | Uses less memory |
| Can access private variables | Cannot access private variables |
| Slower performance | Better performance |

---

## 4. Literal Objects vs Constructor Objects

### 4.1 Comparison Table

| Feature | Literal Object | Constructor Object |
|---------|---------------|-------------------|
| Syntax | `{ key: value }` | `new FunctionName()` |
| Separation | `:` (colon) | `=` (equals) |
| Property separator | `,` (comma) | `;` (semicolon) |
| Instances | Only one | Multiple |
| `this` keyword | Not used | Required |
| Use case | Single objects | Blueprints |

### 4.2 Example Comparison

```javascript
// LITERAL OBJECT
var literalPerson = {
    name: "Raj",     // colon and comma
    age: 25,
    greet: function() { return "Hi " + this.name; }
};
// Only ONE person created

// CONSTRUCTOR OBJECT
function Person(name, age) {
    this.name = name;   // equals and semicolon
    this.age = age;
    this.greet = function() { return "Hi " + this.name; };
}
var person1 = new Person("Raj", 25);    // First person
var person2 = new Person("Mona", 30);   // Second person
// MANY persons can be created
```

---

## 5. The this Keyword

### 5.1 What is this?
The `this` keyword refers to the object that is executing the current function.

### 5.2 this in Different Contexts

| Context | this refers to |
|---------|---------------|
| Global scope | `window` object |
| Object method | The object |
| Constructor (`new`) | The new object |
| Event handler | The element that received the event |
| Arrow function | Inherited from enclosing scope |

### 5.3 Calling Constructor Without new

**Without 'use strict' - DANGEROUS!**
```javascript
function person(nm, mks) {
    alert(this);           // Window [native code]
    this.name = nm;        // Creates window.name!
    this.marks = mks;      // Creates window.marks!
}

person("raj", 30);         // Called WITHOUT new
document.write(window.name);  // "raj" - Property added to window!
```

**With 'use strict' - SAFE**
```javascript
"use strict"
function person(nm, mks) {
    alert(this);           // undefined
    this.name = nm;        // TypeError: Cannot set property 'name' of undefined
}

person("raj", 30);         // Error thrown!
```

### 5.4 Protecting Constructor Functions

```javascript
"use strict"
function person(nm, ag) {
    if (this instanceof person) {
        this.name = nm;
        this.age = ag;
        return this;
    } else {
        throw new TypeError("Check: this is not a function");
    }
}

var obj = new person("raj", 80);  // Works
person("raj", 80);                // Throws error
```

---

## 6. Prototype and Prototype Methods

### 6.1 What is Prototype?
Every JavaScript object has a prototype. It's the mechanism by which JavaScript objects inherit features from one another.

### 6.2 Instance Methods vs Prototype Methods

```javascript
function person(nm, ag) {
    var x = "blue";        // Private variable
    
    this.name = nm;
    this.age = ag;
    
    // Instance method - can access private variable 'x'
    this.speak = function() {
        return " hello " + this.name + " " + x;
    };
}

// Prototype method - CANNOT access private variable 'x'
person.prototype.walk = function() {
    return this.name + " can walk ";
    // return x;  // ERROR: x is not defined
};

person.prototype.toString = function() {
    return this.name + " " + this.age;
};
```

**Key Difference:**
- Instance methods: Created separately for EACH object, CAN access private variables
- Prototype methods: Shared by ALL objects, CANNOT access private variables

**Memory Diagram:**
```
obj1 (person instance):      obj2 (person instance):
┌──────────────────┐        ┌──────────────────┐
│ name: "raj"      │        │ name: "mona"     │
│ age: 80          │        │ age: 90          │
│ speak: function()│        │ speak: function()│  ← Each has own copy
│ [[Prototype]] ───┼────┐   │ [[Prototype]] ───┼────┐
└──────────────────┘    │   └──────────────────┘    │
                        │                           │
                        └───────────┬───────────────┘
                                    ↓
                          person.prototype
                        ┌──────────────────┐
                        │ walk: function() │  ← Shared by all
                        │ toString: function()│
                        └──────────────────┘
```

---

## 7. Object Copying (Shallow vs Deep)

### 7.1 Reference Assignment (Not a Copy!)

```javascript
var ob = new person("mona", 80);
var cpy = ob;  // NOT a copy! Both point to same object

cpy.name = "geeta";

document.write(ob.name);   // "geeta" (original changed!)
document.write(cpy.name);  // "geeta"
```

**Diagram:**
```
ob ───────────→ { name: "geeta", marks: 80 }
                           ↑
cpy ──────────────────────┘
```

### 7.2 Object.assign() - Shallow Copy

```javascript
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);              // { a: 1, b: 4, c: 5 }
console.log(returnedTarget === target);  // true
```

**How Object.assign() Works:**
1. Copies all enumerable properties from source to target
2. Later properties overwrite earlier ones with same name
3. Returns the modified target object
4. It's a SHALLOW copy!

### 7.3 Shallow Copy Problem with Nested Objects

```javascript
const user = {
    name: 'Alex',
    address: { dd: 'juhu' },
    age: 43
};

const clone = {};
Object.assign(clone, user);

user.address.dd = "Andheri";

console.log(clone.address.dd);  // "Andheri" (also changed!)
```

**Why?** Nested objects are still referenced, not copied.

**Diagram:**
```
user:                           clone:
┌─────────────────┐            ┌─────────────────┐
│ name: "Alex"    │            │ name: "Alex"    │  (copied)
│ address: ───────┼─────┐      │ address: ───────┼────┐
│ age: 43         │     │      │ age: 43         │    │
└─────────────────┘     │      └─────────────────┘    │
                        │                             │
                        └─────────→ { dd: "Andheri" } ←┘
                                   (SHARED - not copied!)
```

### 7.4 Spread Operator for Copying

```javascript
const user = {
    name: 'Alex',
    address: '15th Park Avenue',
    age: 43
};

const clone = {...user};  // Shallow copy
console.log(clone === user);  // false (different objects)
```

**Adding Properties:**
```javascript
const updatedUser = {...user, salary: 12345};
// { name: "Alex", address: "15th Park Avenue", age: 43, salary: 12345 }
```

**Updating Properties:**
```javascript
const updatedUser = {...user, age: 56};
// { name: "Alex", address: "15th Park Avenue", age: 56 }
```

### 7.5 Deep Copy Solutions

**Using JSON (limited):**
```javascript
const deepClone = JSON.parse(JSON.stringify(original));
```
⚠️ Doesn't work with functions, undefined, circular references

**Using structuredClone (modern):**
```javascript
const deepClone = structuredClone(original);
```

---

## 8. Object Destructuring

### 8.1 Basic Destructuring

```javascript
let options = {
    title: "Menu",
    width: 100,
    height: 200
};

let { title, width, height } = options;

alert(title);   // Menu
alert(width);   // 100
alert(height);  // 200
```

### 8.2 Renaming During Destructuring

```javascript
let options = {
    title: "Menu",
    width: 100,
    height: 200
};

// { sourceProperty: targetVariable }
let { width: w, height: h, title } = options;

alert(title);  // Menu
alert(w);      // 100
alert(h);      // 200
```

### 8.3 Default Values

```javascript
let options = {
    title: "Menu"
};

let { width = 100, height = 200, title } = options;

alert(title);   // Menu
alert(width);   // 100 (default used)
alert(height);  // 200 (default used)
```

### 8.4 Rest Pattern in Destructuring

```javascript
let options = {
    title: "Menu",
    height: 200,
    width: 100
};

let { title, ...rest } = options;

alert(title);        // Menu
alert(rest.height);  // 200
alert(rest.width);   // 100
```

### 8.5 Nested Destructuring

```javascript
let options = {
    size: { width: 100, height: 200 },
    items: ["Cake", "Donut"],
    extra: true
};

let {
    size: { width, height },
    items: [item1, item2],
    title = "Menu"  // default for missing
} = options;

alert(title);   // Menu (default)
alert(width);   // 100
alert(height);  // 200
alert(item1);   // Cake
alert(item2);   // Donut
```

### 8.6 Destructuring Without let

```javascript
let title, width, height;

// ❌ Error - {} treated as code block
{title, width, height} = {title: "Menu", width: 200, height: 100};

// ✅ Correct - wrap in parentheses
({title, width, height} = {title: "Menu", width: 200, height: 100});

alert(title);  // Menu
```

---

## 9. call() and apply() Methods

### 9.1 Purpose
Allow you to call a function with a specified `this` value and arguments.

### 9.2 call() Method

```javascript
var objperson = {
    fullName: function() {
        return this.firstName + " " + this.lastName;
    }
};

var objperson1 = { firstName: "John", lastName: "Doe" };
var objperson2 = { firstName: "Mary", lastName: "Doe" };

objperson.fullName.call(objperson1);  // "John Doe"
objperson.fullName.call(objperson2);  // "Mary Doe"
```

**With Arguments:**
```javascript
var person = {
    fullName: function(city, country) {
        return this.firstName + " " + this.lastName + "," + city + "," + country;
    }
};

var person1 = { firstName: "John", lastName: "Doe" };

console.log(person.fullName.call(person1, "Mumbai", "India"));
// "John Doe,Mumbai,India"
```

### 9.3 apply() Method

Same as `call()` but takes arguments as an array:

```javascript
var person = {
    fullName: function(city, country) {
        return this.firstName + " " + this.lastName + "," + city + "," + country;
    }
};

var person1 = { firstName: "John", lastName: "Doe" };

console.log(person.fullName.apply(person1, ["Mumbai", "India"]));
// "John Doe,Mumbai,India"
```

### 9.4 call() vs apply()

| Feature | call() | apply() |
|---------|--------|---------|
| Arguments | Individual | Array |
| Syntax | `fn.call(this, arg1, arg2)` | `fn.apply(this, [arg1, arg2])` |
| Mnemonic | C for Comma-separated | A for Array |

---

## 10. Quick Reference

### 10.1 Object Creation Methods

```javascript
// Object constructor
var obj = new Object();
obj.prop = value;

// Literal notation
var obj = { prop: value };

// Constructor function
function ClassName(param) { this.prop = param; }
var obj = new ClassName(value);

// ES6 Class (covered later)
class ClassName { constructor(param) { this.prop = param; } }
```

### 10.2 Property Access

```javascript
obj.propertyName       // Dot notation
obj["propertyName"]    // Bracket notation
obj[variableName]      // Dynamic access
```

### 10.3 Object Methods

| Method | Purpose |
|--------|---------|
| `Object.assign(target, source)` | Copy properties (shallow) |
| `Object.keys(obj)` | Get array of keys |
| `Object.values(obj)` | Get array of values |
| `Object.entries(obj)` | Get array of [key, value] pairs |
| `Object.freeze(obj)` | Prevent modifications |
| `obj.hasOwnProperty(prop)` | Check if property exists |

---

## 11. Interview Questions

### Q1: What is the difference between dot notation and bracket notation?
**Answer**: 
- Dot notation: `obj.property` - Clean, only works with valid identifiers
- Bracket notation: `obj["property"]` - Works with any string, variables, special characters

### Q2: What is the difference between instance methods and prototype methods?
**Answer**:
- Instance methods are created for each object, use more memory, but can access private variables
- Prototype methods are shared among all instances, use less memory, but cannot access private variables

### Q3: What is a shallow copy vs deep copy?
**Answer**:
- Shallow copy copies only top-level properties; nested objects are still referenced
- Deep copy creates completely independent copies of all levels
- `Object.assign()` and spread operator create shallow copies

### Q4: What does `this` refer to in an object method?
**Answer**: In an object method, `this` refers to the object the method belongs to. However, it depends on how the function is called, not where it's defined.

### Q5: What happens when you call a constructor function without new?
**Answer**: Without strict mode, `this` refers to the global object (window), and properties are added to window. With strict mode, `this` is undefined and an error is thrown.

### Q6: What is Object.assign() used for?
**Answer**: `Object.assign()` copies enumerable own properties from source objects to a target object. It's commonly used for shallow cloning and merging objects.

### Q7: What is object destructuring?
**Answer**: Destructuring allows extracting properties from objects into distinct variables. Example: `const { name, age } = person;` extracts name and age properties into variables.

---

## Navigation

← Previous: [04_Anonymous_Functions_and_IIFE.md](./04_Anonymous_Functions_and_IIFE.md) | Next: [06_External_JS_and_Events.md](./06_External_JS_and_Events.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 01-02*
