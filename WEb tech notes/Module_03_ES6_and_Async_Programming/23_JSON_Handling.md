# JSON Handling in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [JSON Syntax](#2-json-syntax)
3. [JSON Data Types](#3-json-data-types)
4. [JSON.stringify()](#4-jsonstringify)
5. [JSON.parse()](#5-jsonparse)
6. [Working with Nested JSON](#6-working-with-nested-json)
7. [JSON vs XML](#7-json-vs-xml)
8. [Quick Reference](#8-quick-reference)
9. [Interview Questions](#9-interview-questions)

---

## 1. Introduction

### 1.1 Definition
**JSON** (JavaScript Object Notation) is a lightweight data-interchange format that is easy for humans to read and write, and easy for machines to parse and generate.

### 1.2 Key Features
- Lightweight data-interchange format
- Self-describing and easy to understand
- Language independent (works with most languages)
- Based on JavaScript object notation
- Text format

### 1.3 Why JSON?
- Simpler than XML
- Faster to parse (no DOM traversal needed)
- Uses JavaScript syntax
- Works directly with AJAX
- No reserved words

---

## 2. JSON Syntax

### 2.1 Basic Structure

**Object:**
```json
{
    "name": "Vita",
    "age": 30,
    "city": "Mumbai"
}
```

**Array:**
```json
{
    "employees": ["Raj", "Mona", "Geeta"]
}
```

### 2.2 Rules
1. Data is in name/value pairs
2. Data is separated by commas
3. Objects are in curly braces `{}`
4. Arrays are in square brackets `[]`
5. **Keys MUST be strings with double quotes**

### 2.3 JSON Structure Diagram

```
Object:
{ name : value }
   ↓
  ","
   ↓
{ name : value }

Array:
[ value , value , value ]
```

---

## 3. JSON Data Types

### 3.1 Valid JSON Types

| Type | Example |
|------|---------|
| String | `{ "name": "Vita" }` |
| Number | `{ "age": 30 }` |
| Object | `{ "employee": { "name": "Vita" } }` |
| Array | `{ "employees": ["Raj", "Mona"] }` |
| Boolean | `{ "sale": true }` |
| null | `{ "middlename": null }` |

### 3.2 NOT Valid in JSON (Valid in JavaScript)

| Type | Note |
|------|------|
| Function | Not allowed |
| Date | Must be string |
| undefined | Not allowed |

---

## 4. JSON.stringify()

### 4.1 Definition
Converts a JavaScript object to a JSON string.

### 4.2 Basic Usage

```javascript
var myObj = { name: "John", age: 31, city: "New York" };
var myJSON = JSON.stringify(myObj);
console.log(myJSON);
// '{"name":"John","age":31,"city":"New York"}'
console.log(typeof myJSON);  // "string"
```

### 4.3 Storing Objects in localStorage

```javascript
// Storing data
myObj = { name: "John", age: 31, city: "New York" };
myJSON = JSON.stringify(myObj);
localStorage.setItem("testJSON", myJSON);
```

### 4.4 Stringifying Arrays

```javascript
var arr = ["John", "Peter", "Sally", "Jane"];
var myJSON = JSON.stringify(arr);
console.log(myJSON);  // '["John","Peter","Sally","Jane"]'
```

---

## 5. JSON.parse()

### 5.1 Definition
Converts a JSON string back into a JavaScript object.

### 5.2 Basic Usage

```javascript
var myJSON = '{"name":"John","age":31,"city":"New York"}';
var myObj = JSON.parse(myJSON);
console.log(myObj.name);  // "John"
console.log(typeof myObj);  // "object"
```

### 5.3 Retrieving from localStorage

```javascript
// Retrieving data
text = localStorage.getItem("testJSON");
obj = JSON.parse(text);
document.getElementById("demo").innerHTML = obj.name + " " + obj.age;
```

### 5.4 Complete Example

```html
<h2>Store and retrieve data from local storage.</h2>
<p id="demo"></p>
<button onclick="go()">Set JSON String</button>
<button onclick="getdata()">Get Object</button>

<script>
var myObj, myJSON, text, obj;

function go() {
    // Storing data
    myObj = { name: "John", age: 31, city: "New York" };
    myJSON = JSON.stringify(myObj);
    localStorage.setItem("testJSON", myJSON);
}

function getdata() {
    // Retrieving data
    text = localStorage.getItem("testJSON");
    obj = JSON.parse(text);
    document.getElementById("demo").innerHTML = obj.name + " " + obj.age;
}
</script>
```

---

## 6. Working with Nested JSON

### 6.1 Accessing Nested Objects

```javascript
var myobj = {
    "name": "John",
    "age": 30,
    "cars": {
        "car1": "Ford",
        "car2": "BMW",
        "car3": "Fiat"
    }
};

// Access nested object
console.log(myobj.cars.car2);      // "BMW"
console.log(myobj.cars["car2"]);   // "BMW"
```

### 6.2 Iterating Nested Objects

```javascript
function readdata() {
    for (let x in myobj) {
        console.log(typeof(myobj[x]));
        
        if (typeof(myobj[x]) != "object") {
            document.getElementById("demo").innerHTML += myobj[x];
        } else {
            for (let subx in myobj[x]) {
                document.getElementById("demo").innerHTML += myobj[x][subx];
            }
        }
    }
}
```

### 6.3 Nested Arrays

```javascript
var myobj = [
    ["Power Steering", "Front and rear power windows", "Anti-lock braking system"],
    ["Power Windows", "Automatic Climate Control"],
    ["Alloy Wheels", "Driver Airbag"],
    [null],
    [null]
];

function readdata() {
    for (let x of myobj) {
        for (let subx of x) {
            document.getElementById("demo").innerHTML += subx + "<br/>";
        }
    }
}
```

---

## 7. JSON vs XML

### 7.1 Similarities

| Feature | Both |
|---------|------|
| Plain text | ✓ |
| Self-describing | ✓ |
| Hierarchical | ✓ |
| Can be parsed | ✓ |
| Used with AJAX | ✓ |

### 7.2 Differences

| Feature | JSON | XML |
|---------|------|-----|
| End tag | No | Yes |
| Length | Shorter | Longer |
| Read/Write | Quicker | Slower |
| Arrays | Built-in | No |
| Parsing | `JSON.parse()` | DOM traversal |
| Reserved words | None | Yes |

### 7.3 Example Comparison

**JSON:**
```json
{
    "employees": [
        { "name": "John", "age": 30 },
        { "name": "Jane", "age": 25 }
    ]
}
```

**XML:**
```xml
<employees>
    <employee>
        <name>John</name>
        <age>30</age>
    </employee>
    <employee>
        <name>Jane</name>
        <age>25</age>
    </employee>
</employees>
```

---

## 8. Quick Reference

### 8.1 JSON Methods

```javascript
// Convert object to JSON string
JSON.stringify(object);

// Convert JSON string to object
JSON.parse(jsonString);
```

### 8.2 Common Patterns

```javascript
// Store object in localStorage
localStorage.setItem("key", JSON.stringify(obj));

// Retrieve object from localStorage
var obj = JSON.parse(localStorage.getItem("key"));

// Clone an object
var clone = JSON.parse(JSON.stringify(original));
```

### 8.3 Valid JSON Syntax

```javascript
// Keys must be quoted
{ "name": "John" }  // ✓ Valid
{ name: "John" }    // ✗ Invalid (key not quoted)

// Strings must use double quotes
{ "name": "John" }  // ✓ Valid
{ "name": 'John' }  // ✗ Invalid (single quotes)

// No trailing commas
{ "name": "John" }  // ✓ Valid
{ "name": "John", } // ✗ Invalid (trailing comma)
```

---

## 9. Interview Questions

### Q1: What is JSON?
**Answer**: JSON (JavaScript Object Notation) is a lightweight data-interchange format that's easy for humans to read and write. It's language-independent but uses conventions familiar to programmers.

### Q2: What is the difference between JSON.stringify() and JSON.parse()?
**Answer**:
- `JSON.stringify()`: Converts JavaScript object to JSON string
- `JSON.parse()`: Converts JSON string to JavaScript object

### Q3: Can JSON contain functions?
**Answer**: No. JSON can only contain strings, numbers, objects, arrays, booleans, and null. Functions, dates, and undefined are not valid JSON values.

### Q4: Why do JSON keys need double quotes?
**Answer**: JSON is a strict subset of JavaScript syntax. The specification requires all keys to be strings wrapped in double quotes for consistency and easier parsing.

### Q5: How do you deep clone an object using JSON?
**Answer**:
```javascript
var clone = JSON.parse(JSON.stringify(original));
```
Note: This doesn't work with functions, dates, undefined, or circular references.

### Q6: What happens when you JSON.parse() invalid JSON?
**Answer**: It throws a `SyntaxError` exception. Always wrap in try-catch for error handling:
```javascript
try {
    var obj = JSON.parse(invalidJSON);
} catch (e) {
    console.log("Invalid JSON");
}
```

---

## Navigation

← Previous: [22_Event_Object_and_All_Events.md](./22_Event_Object_and_All_Events.md) | Next: [24_LocalStorage_and_SessionStorage.md](./24_LocalStorage_and_SessionStorage.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 05*
