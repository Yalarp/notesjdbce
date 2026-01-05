# Generators and Iterators in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [What are Iterators?](#2-what-are-iterators)
3. [What are Generators?](#3-what-are-generators)
4. [The yield Keyword](#4-the-yield-keyword)
5. [Generator Methods](#5-generator-methods)
6. [Generators in Classes](#6-generators-in-classes)
7. [Custom Iterators](#7-custom-iterators)
8. [Practical Examples](#8-practical-examples)
9. [Quick Reference](#9-quick-reference)
10. [Interview Questions](#10-interview-questions)

---

## 1. Introduction

### 1.1 Definitions
- **Iterator**: An object that provides a sequence of values, one at a time
- **Generator**: A special function that can pause and resume execution, producing a sequence of values

### 1.2 Purpose
- Lazy evaluation (compute values on demand)
- Memory-efficient iteration over large data
- Create custom iteration behavior
- Handle asynchronous operations (async generators)

### 1.3 Key Concepts

| Concept | Description |
|---------|-------------|
| `function*` | Generator function syntax |
| `yield` | Pauses execution and returns a value |
| `next()` | Resumes generator and gets next value |
| `done` | Boolean indicating if sequence is complete |

---

## 2. What are Iterators?

### 2.1 Iterator Protocol

An iterator is an object that implements the iterator protocol by having a `next()` method that returns:
- `value`: The next value in the sequence
- `done`: Boolean indicating if iteration is complete

### 2.2 Basic Iterator Structure

```javascript
const iterator = {
    current: 0,
    last: 3,
    next() {
        if (this.current <= this.last) {
            return { value: this.current++, done: false };
        }
        return { value: undefined, done: true };
    }
};

console.log(iterator.next()); // { value: 0, done: false }
console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
console.log(iterator.next()); // { value: 3, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

### 2.3 Iterable Protocol

An object is iterable if it implements `[Symbol.iterator]` method that returns an iterator:

```javascript
const range = {
    start: 1,
    end: 5,
    [Symbol.iterator]() {
        let current = this.start;
        const end = this.end;
        return {
            next() {
                if (current <= end) {
                    return { value: current++, done: false };
                }
                return { done: true };
            }
        };
    }
};

// Can now use for...of
for (let num of range) {
    console.log(num); // 1, 2, 3, 4, 5
}
```

---

## 3. What are Generators?

### 3.1 Generator Function Syntax

```javascript
function* generatorFunction() {
    yield value1;
    yield value2;
    yield value3;
}
```

**Key Points:**
- Use `function*` (asterisk after function)
- Use `yield` to produce values
- Calling the function returns a generator object
- Generator object is both iterable and iterator

### 3.2 Basic Generator Example

```javascript
<script>
function* generateSequence() {
    yield 1;
    yield 2;
    yield 3;
}

let sequence = [...generateSequence()];
alert(sequence); // 1, 2, 3
</script>
```

### 3.3 How Generators Work

```javascript
function* genFunc() {
    console.log("Start");
    yield 1;
    console.log("After first yield");
    yield 2;
    console.log("After second yield");
    return 3;
}

const generator = genFunc(); // Nothing executes yet!

console.log(generator.next()); 
// "Start"
// { value: 1, done: false }

console.log(generator.next()); 
// "After first yield"
// { value: 2, done: false }

console.log(generator.next()); 
// "After second yield"
// { value: 3, done: true }
```

**Execution Flow:**
```
┌──────────────────────────────────────────────────────────┐
│  generator = genFunc()    │ No execution, returns object │
└──────────────────────────────────────────────────────────┘
                ↓
┌──────────────────────────────────────────────────────────┐
│  generator.next()         │ Runs until first yield       │
│                           │ Returns { value: 1, done: false }
└──────────────────────────────────────────────────────────┘
                ↓
┌──────────────────────────────────────────────────────────┐
│  generator.next()         │ Runs until second yield      │
│                           │ Returns { value: 2, done: false }
└──────────────────────────────────────────────────────────┘
                ↓
┌──────────────────────────────────────────────────────────┐
│  generator.next()         │ Runs until return/end        │
│                           │ Returns { value: 3, done: true }
└──────────────────────────────────────────────────────────┘
```

---

## 4. The yield Keyword

### 4.1 Definition
The `yield` keyword pauses generator function execution and returns a value to the caller. When `next()` is called again, execution resumes from where it was paused.

### 4.2 yield vs return

| Feature | yield | return |
|---------|-------|--------|
| Pauses function | Yes | No (ends) |
| Can be used multiple times | Yes | No |
| Allows resumption | Yes | No |
| Sets `done` | false | true |

### 4.3 yield with Expressions

```javascript
function* counter() {
    let count = 0;
    while (true) {
        yield count++;
    }
}

const gen = counter();
console.log(gen.next().value); // 0
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
```

### 4.4 yield* (Delegation)

Use `yield*` to delegate to another generator or iterable:

```javascript
function* gen1() {
    yield 1;
    yield 2;
}

function* gen2() {
    yield* gen1(); // Delegates to gen1
    yield 3;
}

console.log([...gen2()]); // [1, 2, 3]
```

---

## 5. Generator Methods

### 5.1 next()

Resumes generator and returns next value:

```javascript
function* gen() {
    yield 1;
    yield 2;
}

const g = gen();
g.next(); // { value: 1, done: false }
g.next(); // { value: 2, done: false }
g.next(); // { value: undefined, done: true }
```

### 5.2 return()

Terminates generator early:

```javascript
function* gen() {
    yield 1;
    yield 2;
    yield 3;
}

const g = gen();
g.next();     // { value: 1, done: false }
g.return(10); // { value: 10, done: true }
g.next();     // { value: undefined, done: true }
```

### 5.3 throw()

Throws an error inside the generator:

```javascript
function* gen() {
    try {
        yield 1;
        yield 2;
    } catch (e) {
        console.log("Caught:", e);
    }
}

const g = gen();
g.next();           // { value: 1, done: false }
g.throw("Error!");  // "Caught: Error!", { value: undefined, done: true }
```

---

## 6. Generators in Classes

### 6.1 Generator Method in Class

```javascript
<script>
class MyClass {
    *createIterator() {
        yield 1;
        yield 2;
        yield 3;
    }
}

let instance = new MyClass();
let iterator = instance.createIterator();

console.log(iterator);
let one = iterator.next();
alert(JSON.stringify(one));   // {"value":1,"done":false}

let two = iterator.next();
alert(JSON.stringify(two));   // {"value":2,"done":false}

let three = iterator.next();
alert(JSON.stringify(three)); // {"value":3,"done":false}

let four = iterator.next();
alert(JSON.stringify(four));  // {"done":true}
</script>
```

**Memory Diagram:**
```
instance (MyClass):
┌────────────────────────────┐
│ [[Prototype]] → MyClass    │
└────────────────────────────┘

iterator (Generator):
┌────────────────────────────┐
│ next()                     │
│ return()                   │
│ throw()                    │
│ Internal state: paused     │
└────────────────────────────┘
```

### 6.2 Class with Polygon Example

```javascript
class Polygon {
    constructor(...sides) {
        this.sides = sides;
    }
    
    // Generator Method
    *getSides() {
        for (const side of this.sides) {
            yield side;
        }
    }
}

const pentagon = new Polygon(1, 2, 3, 4, 5);
console.log([...pentagon.getSides()]); // [1, 2, 3, 4, 5]
```

### 6.3 yield* with Arrays in Classes

```javascript
class Company {
    constructor() {
        this.x = new Array();
        this.x[0] = new Employee("Raj", 1);
        this.x[1] = new Employee("Mona", 2);
        this.x[2] = new Employee("Geeta", 3);
    }
    
    *crIterator() {
        yield* this.x;  // Delegates to array
    }
}

class Employee {
    constructor(nm, id) {
        this.name = nm;
        this.id = id;
    }
    
    toString() {
        return this.name + " " + this.id;
    }
}

var cc = new Company();
var i = cc.crIterator();

for (let x of i) {
    document.write(x);  // Raj 1, Mona 2, Geeta 3
}
```

---

## 7. Custom Iterators

### 7.1 Manual Iterator with Symbol.iterator

```javascript
<script>
class MyIterator {
    constructor() {
        this.i = 0;
        this.step = new Array(1, 2);
    }
    
    [Symbol.iterator]() {
        return this;
    }
    
    next() {
        if (this.i < this.step.length) {
            return { value: this.step[this.i++], done: false };
        }
        return { done: true };
    }
}

let iter = new MyIterator();
console.log(iter.next()); // { value: 1, done: false }
console.log(iter.next()); // { value: 2, done: false }
console.log(iter.next()); // { done: true }
</script>
```

### 7.2 Making a Class Iterable

```javascript
class Range {
    constructor(start, end) {
        this.start = start;
        this.end = end;
    }
    
    *[Symbol.iterator]() {
        for (let i = this.start; i <= this.end; i++) {
            yield i;
        }
    }
}

const range = new Range(1, 5);

// Now we can use for...of
for (let num of range) {
    console.log(num); // 1, 2, 3, 4, 5
}

// And spread operator
console.log([...range]); // [1, 2, 3, 4, 5]
```

---

## 8. Practical Examples

### 8.1 Infinite Sequence

```javascript
function* fibonacci() {
    let [prev, curr] = [0, 1];
    while (true) {
        yield curr;
        [prev, curr] = [curr, prev + curr];
    }
}

const fib = fibonacci();
console.log(fib.next().value); // 1
console.log(fib.next().value); // 1
console.log(fib.next().value); // 2
console.log(fib.next().value); // 3
console.log(fib.next().value); // 5
```

### 8.2 ID Generator

```javascript
function* idGenerator(prefix = "ID") {
    let id = 1;
    while (true) {
        yield `${prefix}-${id++}`;
    }
}

const userIds = idGenerator("USER");
console.log(userIds.next().value); // USER-1
console.log(userIds.next().value); // USER-2
console.log(userIds.next().value); // USER-3
```

### 8.3 Paginated Data

```javascript
function* paginate(data, pageSize) {
    for (let i = 0; i < data.length; i += pageSize) {
        yield data.slice(i, i + pageSize);
    }
}

const items = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const pages = paginate(items, 3);

console.log(pages.next().value); // [1, 2, 3]
console.log(pages.next().value); // [4, 5, 6]
console.log(pages.next().value); // [7, 8, 9]
console.log(pages.next().value); // [10]
```

---

## 9. Quick Reference

### 9.1 Generator Syntax

```javascript
// Generator function
function* genFunc() {
    yield value;
}

// Generator method in class
class MyClass {
    *genMethod() {
        yield value;
    }
}

// Using the generator
const gen = genFunc();
gen.next();    // { value: ..., done: false }
gen.return();  // { value: ..., done: true }
gen.throw();   // throws error in generator
```

### 9.2 Iterator Protocol

```javascript
const iterator = {
    next() {
        return { value: ..., done: boolean };
    }
};
```

### 9.3 Iterable Protocol

```javascript
const iterable = {
    [Symbol.iterator]() {
        return iterator;  // Return an iterator
    }
};
```

### 9.4 Common Patterns

| Pattern | Use |
|---------|-----|
| `yield value` | Return a single value |
| `yield* iterable` | Delegate to another iterable |
| `for...of gen()` | Iterate over generator values |
| `[...gen()]` | Spread generator into array |

---

## 10. Interview Questions

### Q1: What is the difference between a generator and a regular function?
**Answer**: A generator can pause execution with `yield` and resume later with `next()`. Regular functions run to completion. Generators use `function*` syntax and return a generator object.

### Q2: What does the yield keyword do?
**Answer**: `yield` pauses the generator function and returns a value to the caller. When `next()` is called, execution resumes from where it was paused.

### Q3: How do you make a class iterable?
**Answer**: Implement the `[Symbol.iterator]` method that returns an iterator:
```javascript
class MyClass {
    *[Symbol.iterator]() {
        yield* this.data;
    }
}
```

### Q4: What is yield* used for?
**Answer**: `yield*` delegates iteration to another iterable or generator. It yields all values from the delegated generator/iterable.

### Q5: What are the three methods available on a generator object?
**Answer**:
1. `next(value)` - Resumes execution, optionally passing a value
2. `return(value)` - Terminates the generator
3. `throw(error)` - Throws an error inside the generator

### Q6: What is the difference between an iterator and an iterable?
**Answer**:
- **Iterator**: Object with a `next()` method that returns `{ value, done }`
- **Iterable**: Object with `[Symbol.iterator]` method that returns an iterator
An object can be both (like generators).

---

## Navigation

← Previous: [12_Optional_Chaining_and_Nullish_Coalescing.md](./12_Optional_Chaining_and_Nullish_Coalescing.md) | Next: Module 3 →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 03*
