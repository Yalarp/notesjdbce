# Private and Protected Members in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Access Modifiers Convention](#2-access-modifiers-convention)
3. [Private Fields with # (ES2020)](#3-private-fields-with--es2020)
4. [Protected Members with _ Convention](#4-protected-members-with-_-convention)
5. [Private Methods](#5-private-methods)
6. [Private Getters and Setters](#6-private-getters-and-setters)
7. [Private Static Fields and Methods](#7-private-static-fields-and-methods)
8. [Complete Application Example](#8-complete-application-example)
9. [Quick Reference](#9-quick-reference)
10. [Interview Questions](#10-interview-questions)

---

## 1. Introduction

### 1.1 Definition
**Private members** are properties/methods accessible only within the class. **Protected members** are accessible within the class and its subclasses (in JavaScript, this is a naming convention).

### 1.2 Purpose
- **Encapsulation**: Hide internal implementation details
- **Data Integrity**: Prevent accidental modification
- **API Design**: Expose only necessary interfaces
- **Maintainability**: Change internal implementation without breaking external code

### 1.3 Evolution of Privacy in JavaScript

| Era | Method | Example |
|-----|--------|---------|
| Pre-ES6 | Closures | Variables inside IIFE |
| ES6 | _convention | `this._privateVar` |
| ES2020 | # prefix | `this.#privateField` |

---

## 2. Access Modifiers Convention

### 2.1 Public (Default)

All class members are public by default:

```javascript
class Account {
    name;       // Public instance field
    balance;    // Public instance field
    
    constructor(name, balance) {
        this.name = name;
        this.balance = balance;
    }
    
    deposit(amt) {  // Public method
        this.balance += amt;
    }
}

let acc = new Account("John", 1000);
acc.name = "Jane";       // Accessible
acc.balance = 999999;    // Accessible (problem!)
```

### 2.2 Protected (_underscore Convention)

The underscore prefix is a **naming convention** signaling "don't touch from outside":

```javascript
class Account {
    _name;      // Protected by convention
    _balance;   // Protected by convention
    
    constructor(name, balance) {
        this._name = name;
        this._balance = balance;
    }
}

let acc = new Account("John", 1000);
acc._balance = 999999;  // Still works! Just a convention warning
```

### 2.3 Private (#hash Prefix - ES2020)

True private fields that cannot be accessed from outside:

```javascript
class Account {
    #name;      // Truly private
    #balance;   // Truly private
    
    constructor(name, balance) {
        this.#name = name;
        this.#balance = balance;
    }
}

let acc = new Account("John", 1000);
acc.#balance = 999999;  // SyntaxError!
```

---

## 3. Private Fields with # (ES2020)

### 3.1 Basic Private Fields

```javascript
<script>
'use strict'
class Account {
    #name;
    #balance;
    
    constructor(name, amt) {
        this.#name = name;
        this.#balance = amt;
        alert(typeof this.constructor);
    }
    
    toString() {
        return `Name=${this.#name} Bal=${this.#balance}`;
    }
}

var obj1 = new Account("raj", 20000);
console.log(obj1);
document.write(obj1 instanceof Account);  // true
document.write(obj1 instanceof Object);   // true

// obj1.#name = "geeta";  // SyntaxError: Private field '#name' must be declared in an enclosing class
console.log(obj1);
document.write(obj1);     // Name=raj Bal=20000

var obj2 = new Account("Mona", 50000);
</script>
```

**Line-by-Line Explanation:**

| Line | Code | Explanation |
|------|------|-------------|
| 4-5 | `#name; #balance;` | Declare private fields |
| 7-8 | `this.#name = name` | Initialize private fields |
| 12-14 | `toString()` | Can access private fields inside class |
| 20 | `obj1.#name = "geeta"` | ERROR! Cannot access from outside |

**Key Points:**
- Private fields MUST be declared at class level
- Private fields can ONLY be accessed inside the class
- Accessing private fields outside throws SyntaxError
- Default value is `undefined` if not initialized

### 3.2 Memory Diagram

```
obj1:                                   obj2:
┌────────────────────────┐              ┌────────────────────────┐
│ #name: "raj"           │ (hidden)     │ #name: "Mona"          │ (hidden)
│ #balance: 20000        │ (hidden)     │ #balance: 50000        │ (hidden)
└────────────────────────┘              └────────────────────────┘
```

---

## 4. Protected Members with _ Convention

### 4.1 Basic Protected Pattern

```javascript
<script>
'use strict'
class Account {
    _name;
    _balance;
    
    constructor(name, amt) {
        this._name = name;
        this._balance = amt;
        alert(typeof this.constructor);
    }
    
    toString() {
        return `Name=${this._name} Bal=${this._balance}`;
    }
}

var obj1 = new Account("raj", 20000);
console.log(obj1);
document.write(obj1 instanceof Account);  // true
document.write(obj1 instanceof Object);   // true

obj1._name = "geeta";    // Works! (just convention, not enforced)
document.write(obj1);    // Name=geeta Bal=20000

var obj2 = new Account("Mona", 50000);
</script>
```

### 4.2 Protected with Inheritance

```javascript
class Account {
    _firstname;
    _lastname;
    _balance;
    
    constructor(fname, lname, amt) {
        this.firstname = fname;
        this.lastname = lname;
        this.balance = amt;
    }
    
    set firstname(value) { this._firstname = value; }
    get firstname() { return this._firstname; }
    
    set balance(value) { this._balance = value; }
    get balance() { return this._balance; }
    
    set lastname(value) { this._lastname = value; }
    get lastname() { return this._lastname; }
    
    deposit(amt) { this.balance += amt; }
    
    toString() { return this.firstname + "  " + this.lastname + " " + this.balance; }
}

class Savingaccount extends Account {
    type;
    
    constructor(acctype, fname, lname, amt) {
        super(fname, lname, amt);
        this.type = acctype;
    }
    
    withdraw(amt) {
        const minbal = 1000;
        if (amt > (this.balance - minbal))
            throw new TypeError("Insufficient balance");
        this.balance -= amt;
    }
}

var obj = new Savingaccount("sav", "Raj", "Mathur", 2000);
obj.deposit(2000);
document.write(obj);    // Raj  Mathur 4000
obj.withdraw(500);
document.write(obj);    // Raj  Mathur 3500
document.write(obj.balance);  // 3500
```

**Key Point:** `_` prefix signals "use only in class and subclasses" but doesn't enforce it.

---

## 5. Private Methods

### 5.1 Basic Private Method

```javascript
<script>
class ClassWithPrivateMethod {
    #privateMethod() {
        return 'hello world';
    }
    
    getPrivateMessage() {
        return this.#privateMethod();
    }
}

const instance = new ClassWithPrivateMethod();
console.log(instance.getPrivateMessage());  // "hello world"
// console.log(instance.#privateMethod());  // SyntaxError!
</script>
```

### 5.2 Private Methods for Internal Logic

```javascript
class Calculator {
    #validateNumber(n) {
        if (typeof n !== 'number' || isNaN(n)) {
            throw new Error("Invalid number");
        }
    }
    
    add(a, b) {
        this.#validateNumber(a);
        this.#validateNumber(b);
        return a + b;
    }
}

let calc = new Calculator();
console.log(calc.add(5, 3));  // 8
// calc.#validateNumber(5);   // SyntaxError!
```

---

## 6. Private Getters and Setters

### 6.1 Private Accessor Pattern

```javascript
class ClassWithPrivateAccessor {
    #message;
    
    get #decoratedMessage() {
        return `🎉 ${this.#message} 🎉`;
    }
    
    set #decoratedMessage(msg) {
        this.#message = msg;
    }
    
    constructor() {
        this.#decoratedMessage = 'hello world';
        console.log(this.#decoratedMessage);  // "🎉 hello world 🎉"
    }
}

let obj = new ClassWithPrivateAccessor();
// obj.#decoratedMessage;  // SyntaxError!
```

### 6.2 Public Getter for Private Field

```javascript
class Account {
    #balance;
    
    constructor(balance) {
        this.#balance = balance;
    }
    
    // Public getter for private field
    get balance() {
        return this.#balance;
    }
    
    // No setter - balance is read-only from outside
    
    deposit(amt) {
        if (amt > 0) {
            this.#balance += amt;
        }
    }
}

let acc = new Account(1000);
console.log(acc.balance);   // 1000 (getter works)
acc.balance = 999999;       // Does nothing (no setter)
acc.deposit(500);
console.log(acc.balance);   // 1500
```

---

## 7. Private Static Fields and Methods

### 7.1 Private Static Field

```javascript
class ClassWithPrivateStaticField {
    static #PRIVATE_STATIC_FIELD;
    
    static publicStaticMethod() {
        ClassWithPrivateStaticField.#PRIVATE_STATIC_FIELD = 42;
        return ClassWithPrivateStaticField.#PRIVATE_STATIC_FIELD;
    }
}

console.log(ClassWithPrivateStaticField.publicStaticMethod() === 42);  // true
// console.log(ClassWithPrivateStaticField.#PRIVATE_STATIC_FIELD);  // SyntaxError!
```

### 7.2 Private Static Method

```javascript
class ClassWithPrivateStaticMethod {
    static #privateStaticMethod() {
        return 42;
    }
    
    static publicStaticMethod1() {
        return ClassWithPrivateStaticMethod.#privateStaticMethod();
    }
    
    static publicStaticMethod2() {
        return this.#privateStaticMethod();  // Warning: inheritance issue
    }
}

console.log(ClassWithPrivateStaticMethod.publicStaticMethod1() === 42);  // true
console.log(ClassWithPrivateStaticMethod.publicStaticMethod2() === 42);  // true
```

### 7.3 Inheritance Caveat with Private Static

```javascript
class Base {
    static #privateStaticMethod() {
        return 42;
    }
    
    static publicStaticMethod1() {
        return Base.#privateStaticMethod();  // Uses class name - works
    }
    
    static publicStaticMethod2() {
        return this.#privateStaticMethod();  // Uses this - problematic
    }
}

class Derived extends Base {}

console.log(Derived.publicStaticMethod1());  // 42 (works)
// console.log(Derived.publicStaticMethod2());  // TypeError!
```

**Why?** When calling `Derived.publicStaticMethod2()`, `this` refers to `Derived`, not `Base`, and `Derived` doesn't have `#privateStaticMethod`.

---

## 8. Complete Application Example

### 8.1 Bank Account System

```javascript
<script>
'use strict'
class Account {
    #firstname;
    #lastname;
    #balance;
    #id;
    static #aid = 0;
    
    constructor(fname, lname, amt) {
        this.firstname = fname;
        this.lastname = lname;
        this._cbalance = amt;
        this.#id = ++Account.#aid;  // Auto-increment ID
    }
    
    set firstname(value) { this.#firstname = value; }
    get firstname() { return this.#firstname; }
    
    set _cbalance(value) { this.#balance = value; }
    get _cbalance() { return this.#balance; }
    
    set lastname(value) { this.#lastname = value; }
    get lastname() { return this.#lastname; }
    
    get gid() { return this.#id; }  // Only getter - ID is read-only
    
    deposit(amt) { this._cbalance += amt; }
    
    toString() {
        return this.gid + " " + this.firstname + "  " + this.lastname + " " + this._cbalance;
    }
}

class Savingaccount extends Account {
    type;
    
    constructor(acctype, fname, lname, amt) {
        super(fname, lname, amt);
        this.type = acctype;
    }
    
    withdraw(amt) {
        const minbal = 1000;
        if (amt > (this._cbalance - minbal))
            throw new TypeError("Insufficient balance");
        this._cbalance = this._cbalance - amt;
    }
}

var obj = new Savingaccount("sav", "Raj", "Mathur", 2000);
obj.deposit(2000);
document.write(obj);    // 1 Raj  Mathur 4000
obj.withdraw(500);
document.write(obj);    // 1 Raj  Mathur 3500

var obj2 = new Savingaccount("sav", "Mona", "Singh", 5000);
document.write(obj2);   // 2 Mona  Singh 5000
</script>
```

**Memory Diagram:**
```
Static Memory (Account class):
┌───────────────────────┐
│ #aid = 2              │ (private static counter)
└───────────────────────┘

obj (Instance 1):                       obj2 (Instance 2):
┌───────────────────────┐               ┌───────────────────────┐
│ #firstname: "Raj"     │ (private)     │ #firstname: "Mona"    │ (private)
│ #lastname: "Mathur"   │ (private)     │ #lastname: "Singh"    │ (private)
│ #balance: 3500        │ (private)     │ #balance: 5000        │ (private)
│ #id: 1                │ (private)     │ #id: 2                │ (private)
│ type: "sav"           │ (public)      │ type: "sav"           │ (public)
└───────────────────────┘               └───────────────────────┘
```

### 8.2 Design Decisions Explained

1. **`#firstname`, `#lastname`, `#balance`, `#id`** - Private fields for data protection
2. **`static #aid`** - Private static for account ID generation
3. **`get gid()`** - Only getter, no setter (ID cannot be changed)
4. **`_cbalance`** - Protected convention for child class access
5. **Validation in `withdraw()`** - Business logic enforcement

---

## 9. Quick Reference

### 9.1 Privacy Syntax

```javascript
class Example {
    // Public
    publicField = value;
    publicMethod() {}
    
    // Private (ES2020)
    #privateField = value;
    #privateMethod() {}
    
    // Protected (convention)
    _protectedField = value;
    _protectedMethod() {}
    
    // Private static
    static #privateStaticField = value;
    static #privateStaticMethod() {}
    
    // Private getters/setters
    get #privateGetter() {}
    set #privateSetter(value) {}
}
```

### 9.2 Access Comparison

| Type | Syntax | Class | Subclass | Outside |
|------|--------|-------|----------|---------|
| Public | `name` | ✅ | ✅ | ✅ |
| Protected | `_name` | ✅ | ✅ | ⚠️ (works but shouldn't) |
| Private | `#name` | ✅ | ❌ | ❌ |

### 9.3 Best Practices

| Scenario | Use |
|----------|-----|
| Internal implementation | Private `#field` |
| Subclass needs access | Protected `_field` with getter/setter |
| External needs read | Public getter only |
| External needs write | Public getter + setter with validation |

---

## 10. Interview Questions

### Q1: How do you create private variables in JavaScript classes?
**Answer**: Use the `#` prefix (ES2020):
```javascript
class Example {
    #privateField; // Truly private
    constructor(val) { this.#privateField = val; }
}
```

### Q2: What's the difference between # and _ for private fields?
**Answer**: 
- `#` (hash) - True privacy, enforced by the language
- `_` (underscore) - Convention only, not enforced

### Q3: Can private fields be accessed in subclasses?
**Answer**: No. Private fields are only accessible in the class that defines them. Subclasses cannot access parent's private fields directly.

### Q4: How do you make a read-only property?
**Answer**: Define only a getter, no setter:
```javascript
class Example {
    #field;
    get value() { return this.#field; }
    // No setter = read-only
}
```

### Q5: What happens if you try to access a private field outside the class?
**Answer**: You get a `SyntaxError: Private field '#fieldName' must be declared in an enclosing class`.

### Q6: Can static methods access private static fields?
**Answer**: Yes, but ONLY through the class name, not through `this` in inherited classes to avoid issues.

### Q7: Why use private fields instead of closures?
**Answer**: Private fields:
- Cleaner syntax
- Per-instance private data (closures are per-function)
- Work naturally with class syntax
- Better memory efficiency for multiple instances

---

## Navigation

← Previous: [09_ES6_Objects_and_Classes.md](./09_ES6_Objects_and_Classes.md) | Next: [11_Optional_Chaining.md](./11_Optional_Chaining.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 03*
