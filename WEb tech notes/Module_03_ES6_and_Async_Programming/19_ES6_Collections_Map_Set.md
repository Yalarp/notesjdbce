# ES6 Collections: Map and Set

## Table of Contents
1. [Introduction](#1-introduction)
2. [Map](#2-map)
3. [Map Methods and Properties](#3-map-methods-and-properties)
4. [Set](#4-set)
5. [Set Methods and Properties](#5-set-methods-and-properties)
6. [WeakMap and WeakSet](#6-weakmap-and-weakset)
7. [Use Cases](#7-use-cases)
8. [Quick Reference](#8-quick-reference)
9. [Interview Questions](#9-interview-questions)

---

## 1. Introduction

### 1.1 Why ES6 Collections?
ES6 introduced `Map` and `Set` as new data structures that solve limitations of objects and arrays:

| Collection | Purpose | Key Feature |
|------------|---------|-------------|
| Map | Key-value pairs | Any type as key |
| Set | Unique values | No duplicates |
| WeakMap | Key-value pairs | Weak references |
| WeakSet | Unique objects | Auto garbage collection |

### 1.2 When to Use Map vs Object

Use **Map** when:
- Keys are unknown until runtime
- All values have the same type
- Keys aren't strings (objects, functions)
- Key-value pairs are frequently added/removed
- Collection is iterated

---

## 2. Map

### 2.1 Definition
A **Map** object holds key-value pairs where any value (objects and primitives) can be used as either a key or a value.

### 2.2 Creating a Map

```javascript
"use strict"
var myMap = new Map();
myMap.set(0, "zero");
myMap.set(1, "one");
```

**Memory Diagram:**
```
myMap (Map):
┌────────────┬───────────┐
│   Key      │   Value   │
├────────────┼───────────┤
│     0      │  "zero"   │
│     1      │  "one"    │
└────────────┴───────────┘
```

### 2.3 Iterating Over Map

```javascript
// Using for...of with destructuring
for (var [key, value] of myMap) {
    console.log(key + " = " + value);
}
// Output: "0 = zero", "1 = one"

// Keys only
for (var key of myMap.keys()) {
    console.log(key);
}
// Output: 0, 1

// Values only
for (var value of myMap.values()) {
    console.log(value);
}
// Output: "zero", "one"

// Entries
for (var [key, value] of myMap.entries()) {
    console.log(key + " = " + value);
}
// Output: "0 = zero", "1 = one"

// forEach
myMap.forEach(function(value, key) {
    console.log(key + " = " + value);
}, myMap);
```

---

## 3. Map Methods and Properties

### 3.1 Methods Table

| Method | Description |
|--------|-------------|
| `set(key, value)` | Add or update key-value pair |
| `get(key)` | Get value for key |
| `has(key)` | Check if key exists |
| `delete(key)` | Remove key-value pair |
| `clear()` | Remove all entries |
| `keys()` | Iterator for keys |
| `values()` | Iterator for values |
| `entries()` | Iterator for [key, value] pairs |
| `forEach(callback)` | Execute callback for each entry |

### 3.2 Properties

| Property | Description |
|----------|-------------|
| `size` | Number of entries |

---

## 4. Set

### 4.1 Definition
A **Set** object is a collection of unique values. A value in a Set may only occur once; it is unique in the Set's collection.

### 4.2 Creating a Set

```javascript
"use strict"
var mySet = new Set();

mySet.add(1);
mySet.add(5);
mySet.add("1");         // String "1" is different from number 1
mySet.add("some text");
var o = {a: 1, b: 2};
mySet.add(o);

mySet.size;  // 5
```

### 4.3 Checking Values

```javascript
mySet.has(1);                          // true
mySet.has(3);                          // false (not added)
mySet.has(5);                          // true
mySet.has(Math.sqrt(25));              // true (5)
mySet.has("Some Text".toLowerCase());  // true
mySet.has(o);                          // true
```

### 4.4 Deleting Values

```javascript
mySet.delete(5);   // removes 5 from the set
mySet.has(5);      // false, 5 has been removed
mySet.size;        // 4
```

### 4.5 Iterating Over Set

```javascript
// for...of
for (let item of mySet) {
    console.log(item);
}
// Output: 1, "1", "some text", {a: 1, b: 2}

// keys() - same as values() for Set
for (let item of mySet.keys()) {
    console.log(item);
}

// values()
for (let item of mySet.values()) {
    console.log(item);
}

// Convert to Array
var myarray = Array.from(mySet);
console.log(myarray);  // [1, "1", "some text", {a: 1, b: 2}]
```

---

## 5. Set Methods and Properties

### 5.1 Methods

| Method | Description |
|--------|-------------|
| `add(value)` | Add new value |
| `has(value)` | Check if value exists |
| `delete(value)` | Remove value |
| `clear()` | Remove all values |
| `keys()` | Iterator (same as values) |
| `values()` | Iterator for values |
| `entries()` | Iterator for [value, value] |
| `forEach(callback)` | Execute callback for each |

### 5.2 Properties

| Property | Description |
|----------|-------------|
| `size` | Number of values |

---

## 6. WeakMap and WeakSet

### 6.1 Why WeakMap?

**Problem with regular Map:**
```javascript
let john = { name: "John" };
let map = new Map();
map.set(john, "...");

john = null;  // overwrite the reference

// john is STILL stored inside the map!
// We can get it by using map.keys()
```

**Solution with WeakMap:**
```javascript
let john = { name: "John" };
let weakMap = new WeakMap();
weakMap.set(john, "...");

john = null;  // overwrite the reference

// john is REMOVED from memory!
```

### 6.2 WeakMap Rules

1. **Keys must be objects** (not primitives):
```javascript
let weakMap = new WeakMap();
let obj = {};

weakMap.set(obj, "ok");       // Works (object key)
weakMap.set("test", "Whoops"); // Error! String is not an object
```

2. **No iteration methods** - No `keys()`, `values()`, `entries()`
3. **No `size` property**

### 6.3 WeakMap Methods

| Method | Description |
|--------|-------------|
| `get(key)` | Get value |
| `set(key, value)` | Set value |
| `delete(key)` | Delete entry |
| `has(key)` | Check if exists |

### 6.4 WeakSet

Similar to Set, but:
- May only add **objects** (not primitives)
- Object exists in set while reachable from somewhere else
- Supports `add`, `has`, `delete`
- NO `size`, `keys()`, or iterations

```javascript
let visitedSet = new WeakSet();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

visitedSet.add(john);  // John visited us
visitedSet.add(pete);  // Then Pete
visitedSet.add(john);  // John again (ignored, already exists)

// visitedSet has 2 users now
alert(visitedSet.has(john));  // true
alert(visitedSet.has(mary));  // false

john = null;
// visitedSet will be cleaned automatically
```

---

## 7. Use Cases

### 7.1 Use Case: Additional Data Storage

```javascript
// Using WeakMap for private data
let visitsCountMap = new WeakMap();

function countUser(user) {
    let count = visitsCountMap.get(user) || 0;
    visitsCountMap.set(user, count + 1);
}

let john = { name: "John" };
countUser(john);  // count his visits

// later john leaves us
john = null;
// john is automatically removed from WeakMap!
```

### 7.2 Use Case: Caching

```javascript
// Without WeakMap - memory leak!
let cache = new Map();

function process(obj) {
    if (!cache.has(obj)) {
        let result = /* calculations */ obj;
        cache.set(obj, result);
    }
    return cache.get(obj);
}

let obj = {/* some object */};
let result1 = process(obj);
obj = null;
alert(cache.size);  // 1 - Still in cache! Memory leak!
```

```javascript
// With WeakMap - auto cleanup
let cache = new WeakMap();

function process(obj) {
    if (!cache.has(obj)) {
        let result = /* calculations */ obj;
        cache.set(obj, result);
    }
    return cache.get(obj);
}

let obj = {/* some object */};
let result1 = process(obj);
obj = null;
// cache auto-cleaned when obj is garbage collected
```

### 7.3 Use Case: Remove Duplicates

```javascript
let numbers = [1, 2, 2, 3, 4, 4, 5];
let unique = [...new Set(numbers)];
console.log(unique);  // [1, 2, 3, 4, 5]
```

---

## 8. Quick Reference

### 8.1 Map

```javascript
let map = new Map();
map.set(key, value);
map.get(key);
map.has(key);
map.delete(key);
map.clear();
map.size;
```

### 8.2 Set

```javascript
let set = new Set();
set.add(value);
set.has(value);
set.delete(value);
set.clear();
set.size;
```

### 8.3 WeakMap/WeakSet

```javascript
let weakMap = new WeakMap();
weakMap.set(objKey, value);  // Only objects as keys
weakMap.get(objKey);
weakMap.has(objKey);
weakMap.delete(objKey);
// No size, no iteration!

let weakSet = new WeakSet();
weakSet.add(obj);  // Only objects
weakSet.has(obj);
weakSet.delete(obj);
// No size, no iteration!
```

### 8.4 Comparison Table

| Feature | Map | Object | Set | Array |
|---------|-----|--------|-----|-------|
| Key types | Any | String/Symbol | N/A | N/A |
| Ordered | Yes | No (ES6: Yes) | Yes | Yes |
| Size | .size | Object.keys().length | .size | .length |
| Duplicates | Yes (different keys) | No | No | Yes |
| Iteration | Built-in | Manual | Built-in | Built-in |

---

## 9. Interview Questions

### Q1: What is the difference between Map and Object?
**Answer**:
- **Keys**: Map allows any type as key; Object only allows strings/symbols
- **Order**: Map maintains insertion order; Object doesn't guarantee order
- **Size**: Map has `size` property; Object requires `Object.keys().length`
- **Iteration**: Map is directly iterable; Object needs `Object.entries()`
- **Performance**: Map is better for frequent additions/removals

### Q2: What is the difference between Set and Array?
**Answer**:
- **Uniqueness**: Set only stores unique values; Array can have duplicates
- **Lookup**: Set.has() is O(1); Array.includes() is O(n)
- **Order**: Both maintain insertion order
- **Access**: Set has no index access; Array has index access

### Q3: Why use WeakMap instead of Map?
**Answer**: WeakMap allows keys to be garbage collected when there are no other references to them. This prevents memory leaks when storing metadata about objects that may be deleted.

### Q4: Can you iterate over a WeakMap?
**Answer**: No. WeakMap doesn't support iteration (`keys()`, `values()`, `entries()`) or `size` because the garbage collector may clean up entries at any time.

### Q5: How do you remove duplicates from an array using Set?
**Answer**:
```javascript
let arr = [1, 2, 2, 3, 3, 4];
let unique = [...new Set(arr)];  // [1, 2, 3, 4]
```

---

## Navigation

← Previous: [18_Form_Handling.md](../Module_02_Advanced_JavaScript/18_Form_Handling.md) | Next: [20_History_Navigator_Objects.md](./20_History_Navigator_Objects.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 05*
