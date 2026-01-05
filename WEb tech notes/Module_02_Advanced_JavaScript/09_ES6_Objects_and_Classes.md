# ES6 Objects and Classes in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [ES6 Class Syntax](#2-es6-class-syntax)
3. [Constructor Method](#3-constructor-method)
4. [Class Methods](#4-class-methods)
5. [Getters and Setters](#5-getters-and-setters)
6. [Static Methods and Properties](#6-static-methods-and-properties)
7. [Inheritance with extends](#7-inheritance-with-extends)
8. [The super Keyword](#8-the-super-keyword)
9. [The bind() Method](#9-the-bind-method)
10. [Quick Reference](#10-quick-reference)
11. [Interview Questions](#11-interview-questions)

---

## 1. Introduction

### 1.1 Definition
ES6 (ECMAScript 2015) introduced the `class` keyword, providing a cleaner, more intuitive syntax for creating objects and implementing inheritance in JavaScript. Under the hood, classes are still prototype-based.

### 1.2 Purpose
- Cleaner syntax for constructor functions
- Built-in support for inheritance (`extends`)
- More familiar OOP syntax for developers from other languages
- Better encapsulation with private fields (#)

### 1.3 Key Differences from Function Constructors

| Feature | Function Constructor | ES6 Class |
|---------|---------------------|-----------|
| Syntax | `function Person(){}` | `class Person {}` |
| Hoisting | ✅ Hoisted | ❌ Not hoisted |
| Strict mode | Optional | Always strict |
| Methods | Enumerable | Non-enumerable |
| Constructor call | Works without new* | Requires new |

*Without strict mode

---

## 2. ES6 Class Syntax

### 2.1 Basic Class Declaration

```javascript
<script>
'use strict'
class Account {
    constructor(name, amt) {
        this.name = name;
        this.balance = amt;
        alert(typeof this.constructor)  // "function"
    }
}

var obj1 = new Account("raj", 20000);
console.log(obj1);

document.write(obj1 instanceof Account);  // true
document.write(obj1 instanceof Object);   // true

obj1.name = "geeta";
console.log(obj1);
document.write(obj1);  // [object Object]

var obj2 = new Account("Mona", 50000);
document.write(obj2.name);  // Mona
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 2 | `'use strict'` | Classes always run in strict mode anyway |
| 3 | `class Account {` | Class declaration starts |
| 4 | `constructor(name, amt)` | Constructor method (runs when `new` is called) |
| 5-6 | `this.name = name` | Instance properties |
| 7 | `typeof this.constructor` | Returns "function" (class is a function) |
| 11 | `new Account("raj", 20000)` | Creates instance |
| 14 | `instanceof Account` | Checks if obj1 is instance |

**Memory Diagram:**
```
obj1:                      obj2:
┌─────────────────┐        ┌─────────────────┐
│ name: "geeta"   │        │ name: "Mona"    │
│ balance: 20000  │        │ balance: 50000  │
│ [[Prototype]]   │        │ [[Prototype]]   │
└───────┬─────────┘        └───────┬─────────┘
        │                          │
        └──────────┬───────────────┘
                   ↓
           Account.prototype
           ┌──────────────┐
           │ constructor  │
           └──────────────┘
                   ↓
           Object.prototype
```

### 2.2 Important Class Characteristics

1. **Classes are NOT hoisted** (unlike function declarations):
```javascript
const p = new Rectangle();  // ReferenceError!
class Rectangle {}
```

2. **Classes always use strict mode**:
```javascript
class Test {
    method() {
        // 'use strict' is automatic
        undeclaredVar = 5;  // Error!
    }
}
```

3. **Class methods are non-enumerable**:
```javascript
let person = function(nm, ag) {
    this.name = nm;
    this.age = ag;
    this.dojob = function() {
        document.write("doing job<br/>");
    }
}

let obj = new person("Raj", 25);

for (let prop in obj) {
    document.write(prop + " " + obj[prop]);  // Shows name, age, dojob
}

// With class - methods won't appear in for...in
```

### 2.3 Class Expression

```javascript
// Named class expression
let User = class MyClass {
    sayHi() {
        alert("Hello");
    }
};

new User().sayHi();  // "Hello"

// Anonymous class expression
let Person = class {
    constructor(name) {
        this.name = name;
    }
};
```

### 2.4 Dynamic Class Creation

```javascript
function makeClass(phrase) {
    return class {
        sayHi() {
            alert(phrase);
        }
    };
}

let User = makeClass("Hello");
new User().sayHi();  // "Hello"
```

---

## 3. Constructor Method

### 3.1 The constructor() Method

```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
}

let p = new Person("John", 30);
```

**Rules:**
- Only ONE constructor per class
- Called automatically when `new` is used
- Used to initialize instance properties
- If not defined, empty constructor is used

### 3.2 Constructor with Validation

```javascript
class Person {
    constructor(name, age) {
        if (!name) {
            throw new Error("Name is required");
        }
        if (age < 0) {
            throw new Error("Age cannot be negative");
        }
        this.name = name;
        this.age = age;
    }
}
```

---

## 4. Class Methods

### 4.1 Instance Methods

```javascript
class MyMath {
    constructor(number) {
        this.no = number;
    }
    
    sqr() {
        let s = this.no * this.no;
        return s;
    }
    
    cube() {
        let q = this.sqr() * this.no;  // Calling another method
        return q;
    }
}

obj = new MyMath(3);
console.log(obj.sqr());   // 9
console.log(obj.cube());  // 27
```

**Memory Diagram:**
```
obj:
┌────────────────┐
│ no: 3          │
│ [[Prototype]] ─┼────→ MyMath.prototype
└────────────────┘       ┌──────────────┐
                         │ sqr()        │
                         │ cube()       │
                         └──────────────┘
```

### 4.2 Calling Methods from Within Methods

```javascript
class Calculator {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
    
    add() {
        return this.x + this.y;
    }
    
    multiply() {
        return this.x * this.y;
    }
    
    // Calling other methods
    calculate() {
        return {
            sum: this.add(),
            product: this.multiply()
        };
    }
}

let calc = new Calculator(5, 3);
console.log(calc.calculate());  // { sum: 8, product: 15 }
```

---

## 5. Getters and Setters

### 5.1 Basic Getter and Setter

```javascript
class Account {
    _firstName;
    _lastName;
    _balance;
    
    constructor(fname, lname, amt) {
        this.firstname = fname;
        this.lastname = lname;
        this.balance = amt;
    }
    
    set firstname(value) { this._firstName = value; }
    get firstname() { return this._firstName; }
    
    set balance(value) { this._balance = value; }
    get balance() { return this._balance; }
    
    set lastname(value) { this._lastname = value; }
    get lastname() { return this._lastname; }

    deposit(amt) {
        this.balance += amt;
    }

    toString() {
        return this.firstname + "  " + this.lastname + " " + this.balance;
    }
}

var obj = new Account("Raj", "Mathur", 2000);
obj.deposit(500);
document.write(obj);  // Raj  Mathur 2500
```

### 5.2 Getter/Setter with Validation

```javascript
class Person {
    #age;  // Private field
    
    get age() {
        return this.#age;
    }
    
    set age(value) {
        if (value < 0 || value > 150) {
            throw new Error("Invalid age");
        }
        this.#age = value;
    }
}
```

### 5.3 Computed Properties

```javascript
class User {
    constructor(firstName, lastName) {
        this._firstName = firstName;
        this._lastName = lastName;
    }
    
    // Computed property (getter only)
    get fullName() {
        return `${this._firstName} ${this._lastName}`;
    }
    
    set fullName(value) {
        let parts = value.split(' ');
        this._firstName = parts[0];
        this._lastName = parts[1];
    }
}

let user = new User("John", "Doe");
console.log(user.fullName);  // "John Doe" - accessed like property!
user.fullName = "Jane Smith";
console.log(user._firstName);  // "Jane"
```

---

## 6. Static Methods and Properties

### 6.1 Static Methods

Static methods are called on the class itself, NOT on instances.

```javascript
<script>
'use strict'
class mymaths {
    static add(a, b) {
        return a + b;
    }
    
    static sqr(a) {
        return a * a;
    }
}

document.write(mymaths.add(3, 5));  // 8
document.write(mymaths.sqr(3));     // 9

// let obj = new mymaths();
// obj.add(3, 5);  // ERROR! Static methods not on instances
</script>
```

**Memory Diagram:**
```
mymaths (class/function):
┌───────────────────────┐
│ add: function()       │ ← Static (on class)
│ sqr: function()       │ ← Static (on class)
│ prototype ────────────┼──→ mymaths.prototype
└───────────────────────┘    ┌──────────────┐
                             │ constructor  │
                             └──────────────┘
```

### 6.2 Static Properties

```javascript
class Account {
    static bankName = "State Bank";
    static interestRate = 0.08;
    
    constructor(name, balance) {
        this.name = name;
        this.balance = balance;
    }
    
    static calculateInterest(principal, years) {
        return principal * Account.interestRate * years;
    }
}

console.log(Account.bankName);  // "State Bank"
console.log(Account.calculateInterest(10000, 2));  // 1600
```

### 6.3 Static for Auto-ID Generation

```javascript
class Account {
    static #aid = 0;  // Private static
    #id;
    
    constructor(name, balance) {
        this.name = name;
        this.balance = balance;
        this.#id = ++Account.#aid;
    }
    
    get id() {
        return this.#id;
    }
}

let acc1 = new Account("John", 1000);  // id = 1
let acc2 = new Account("Jane", 2000);  // id = 2
console.log(acc1.id, acc2.id);  // 1, 2
```

---

## 7. Inheritance with extends

### 7.1 Basic Inheritance

```javascript
class Account {
    constructor(name, balance) {
        this.name = name;
        this.balance = balance;
    }
    
    deposit(amt) {
        this.balance += amt;
    }
    
    toString() {
        return `${this.name}: $${this.balance}`;
    }
}

class SavingAccount extends Account {
    type;
    
    constructor(acctype, name, balance) {
        super(name, balance);  // MUST call parent constructor first
        this.type = acctype;
    }
    
    withdraw(amt) {
        const minbal = 1000;
        if (amt > (this.balance - minbal)) {
            throw new TypeError("Insufficient balance");
        }
        this.balance -= amt;
    }
}

var obj = new SavingAccount("sav", "Raj", 2000);
obj.deposit(2000);
document.write(obj);  // Raj: $4000
obj.withdraw(500);
document.write(obj);  // Raj: $3500
```

**Memory Diagram:**
```
obj (SavingAccount instance):
┌──────────────────┐
│ name: "Raj"      │
│ balance: 3500    │
│ type: "sav"      │
│ [[Prototype]] ───┼────→ SavingAccount.prototype
└──────────────────┘      ┌──────────────────┐
                          │ withdraw()       │
                          │ [[Prototype]] ───┼────→ Account.prototype
                          └──────────────────┘      ┌────────────────┐
                                                    │ deposit()      │
                                                    │ toString()     │
                                                    └────────────────┘
```

### 7.2 Method Overriding

```javascript
class Animal {
    speak() {
        return "Some sound";
    }
}

class Dog extends Animal {
    speak() {
        return "Woof!";  // Override parent method
    }
}

class Cat extends Animal {
    speak() {
        return "Meow!";  // Override parent method
    }
}

let dog = new Dog();
let cat = new Cat();
console.log(dog.speak());  // "Woof!"
console.log(cat.speak());  // "Meow!"
```

---

## 8. The super Keyword

### 8.1 super in Constructor

```javascript
class Parent {
    constructor(name) {
        this.name = name;
    }
}

class Child extends Parent {
    constructor(name, age) {
        super(name);  // Calls Parent constructor
        this.age = age;  // Then add own properties
    }
}
```

**Rules:**
- `super()` MUST be called before `this` in child constructor
- `super()` can only be used in derived class constructor

### 8.2 super to Call Parent Methods

```javascript
class Account {
    toString() {
        return `Name: ${this.name}`;
    }
}

class SavingAccount extends Account {
    toString() {
        return super.toString() + `, Type: ${this.type}`;
    }
}
```

---

## 9. The bind() Method

### 9.1 The Problem

```javascript
const module = {
    x: 42,
    getX: function() {
        return this.x;
    }
};

const unboundGetX = module.getX;
console.log(unboundGetX());  // undefined! (this = window)
```

### 9.2 Solution with bind()

```javascript
const module = {
    x: 42,
    getX: function() {
        return this.x;
    }
};

const unboundGetX = module.getX;
console.log(unboundGetX());  // undefined

const boundGetX = unboundGetX.bind(module);
console.log(boundGetX());  // 42

// Alternative: using call
console.log(module.getX.call(module));  // 42
```

### 9.3 bind() with Arguments

```javascript
function greet(greeting, punctuation) {
    return greeting + ' ' + this.name + punctuation;
}

const person = { name: 'John' };

const sayHello = greet.bind(person, 'Hello');
console.log(sayHello('!'));  // "Hello John!"
```

---

## 10. Quick Reference

### 10.1 Class Syntax

```javascript
class ClassName {
    // Static properties
    static staticProp = value;
    
    // Private fields (ES2020)
    #privateField;
    
    // Constructor
    constructor(param) {
        this.instanceProp = param;
        this.#privateField = value;
    }
    
    // Getter
    get propName() { return this.#privateField; }
    
    // Setter
    set propName(value) { this.#privateField = value; }
    
    // Instance method
    methodName() { }
    
    // Static method
    static staticMethod() { }
}

// Inheritance
class ChildClass extends ParentClass {
    constructor(param) {
        super(param);  // Call parent constructor
    }
    
    method() {
        super.method();  // Call parent method
    }
}
```

### 10.2 Access Modifiers

| Prefix | Meaning | Example |
|--------|---------|---------|
| None | Public | `this.name` |
| `_` | Protected (convention) | `this._balance` |
| `#` | Private (ES2020) | `this.#secret` |

### 10.3 Static vs Instance

| Feature | Static | Instance |
|---------|--------|----------|
| Access | `ClassName.method()` | `instance.method()` |
| `this` | The class | The instance |
| Use case | Utilities, factories | Object-specific behavior |

---

## 11. Interview Questions

### Q1: What is the difference between class and function constructor?
**Answer**: Classes are syntactic sugar over prototypes. Key differences:
- Classes are not hoisted
- Classes always run in strict mode
- Class methods are non-enumerable
- Classes require `new` to be called

### Q2: Can you have multiple constructors in a JavaScript class?
**Answer**: No, JavaScript classes can have only one constructor. For multiple initialization patterns, use default parameters, rest parameters, or factory methods.

### Q3: What is the purpose of the super keyword?
**Answer**: `super` is used to:
1. Call the parent class constructor: `super()`
2. Access parent class methods: `super.methodName()`
It must be called in child constructor before using `this`.

### Q4: What are static methods and when should you use them?
**Answer**: Static methods belong to the class, not instances. Use them for:
- Utility functions
- Factory methods
- Counting instances
- Shared functionality that doesn't need instance data

### Q5: How do you create private properties in ES6 classes?
**Answer**: Use the `#` prefix (ES2020):
```javascript
class Example {
    #privateField = 42;
    getPrivate() { return this.#privateField; }
}
```

### Q6: What is the difference between getter/setter and regular methods?
**Answer**: Getters and setters are accessed like properties (no parentheses) but execute code when accessed/assigned. They provide computed properties and validation.

### Q7: What does bind() do and when would you use it?
**Answer**: `bind()` creates a new function with `this` permanently set to a specified value. Use it when:
- Passing methods as callbacks
- Preserving context in event handlers
- Creating partially applied functions

---

## Navigation

← Previous: [08_Closures.md](./08_Closures.md) | Next: [10_Private_and_Protected_Members.md](./10_Private_and_Protected_Members.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 03*
