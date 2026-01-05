# Arrays and Array Methods in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Array Declaration](#2-array-declaration)
3. [2D Arrays](#3-2d-arrays)
4. [Stack Operations (push/pop)](#4-stack-operations-pushpop)
5. [Queue Operations (shift/unshift)](#5-queue-operations-shiftunshift)
6. [Array Manipulation Methods](#6-array-manipulation-methods)
7. [Searching and Filtering](#7-searching-and-filtering)
8. [Transformation Methods](#8-transformation-methods)
9. [Sorting](#9-sorting)
10. [Quick Reference](#10-quick-reference)
11. [Interview Questions](#11-interview-questions)

---

## 1. Introduction

### 1.1 Definition
An **Array** in JavaScript is a collection of elements that can hold different data types. Arrays are objects in JavaScript, stored as key-value pairs where keys are numeric indices.

### 1.2 Key Characteristics
- Zero-based indexing
- Dynamic sizing (can grow/shrink)
- Can hold mixed data types
- Stored in heap memory (reference type)

### 1.3 Array Storage Model

```
Stack:           Heap:
┌─────────┐     ┌────────────────────────┐
│ arr ────┼────→│ 0: 1                   │
└─────────┘     │ 1: "vita"              │
                │ 2: 'g'                 │
                │ 3: 20.5                │
                │ length: 4              │
                └────────────────────────┘
```

---

## 2. Array Declaration

### 2.1 Using Array Constructor (Not Recommended)

```javascript
let arr = new Array();  // Don't use this
arr[0] = 1;
arr[1] = "vita";
arr[2] = 'g';
arr[3] = 20.5;
alert(arr.length);  // 4
```

**Warning with single numeric argument:**
```javascript
var aa = new Array(2);  // Creates array with length 2, NOT [2]
document.write(aa.length);  // 2
aa[0] = 7;
aa[1] = 3;
document.write(aa);  // 7,3
```

### 2.2 Using Array Literal (Recommended)

```javascript
let arr = [1, 2, "hi", "bye"];
document.write(arr);

// Empty array
let empty = [];
empty[0] = 5;
empty[4] = 4;
document.write(empty);  // 5,undefined,undefined,undefined,4
```

### 2.3 Iterating Arrays

```javascript
let arr = [1, "vita", 'g', 20.5];

// Traditional for loop
for (let i = 0; i < arr.length; i++) {
    document.write("<br>" + arr[i]);
}

// for...of (ES6+) - Recommended
for (let list of arr) {
    document.write("<br/>" + list);
}

// for...in (NOT recommended for arrays)
for (let x in arr) {
    document.write(arr[x]);
}

// toString() is overridden
document.write("<br/>" + arr);  // 1,vita,g,20.5
```

### 2.4 Handling Sparse Arrays

```javascript
let arr = [];
arr[0] = 5;
arr[4] = 4;
document.write(arr);  // 5,undefined,undefined,undefined,4

// Remove undefined values
for (let e of arr) {
    if (e) document.write(e);  // 5, 4
}
```

---

## 3. 2D Arrays

### 3.1 Creating 2D Arrays

```javascript
var a = new Array();
a[0] = new Array();
a[1] = new Array();

a[0][0] = "raj";
a[0][1] = 50;
a[0][2] = "A";

a[1][0] = "mona";
a[1][1] = 80;
a[1][2] = "B";

document.write(a[0][1] + "see");  // 50see
```

### 3.2 Iterating 2D Arrays

```javascript
for (i = 0; i < a.length; i++) {
    for (j = 0; j < a[i].length; j++) {
        document.write(" " + a[i][j]);
    }
    document.write("<hr/>");
}
```

### 3.3 Memory Diagram

```
a:
┌─────┐     ┌─────────────────────┐
│ 0 ──┼────→│ raj | 50 | A       │
├─────┤     ├─────────────────────┤
│ 1 ──┼────→│ mona | 80 | B      │
└─────┘     └─────────────────────┘
```

---

## 4. Stack Operations (push/pop)

### 4.1 push() - Add to End

```javascript
var arr = new Array(3);
arr[0] = "vita";
arr[1] = "dac";
arr[2] = "acts";

document.write(arr + "<br />");         // vita,dac,acts
document.write(arr.push("2020") + "<br />"); // 4 (new length)
document.write(arr);                     // vita,dac,acts,2020
```

**Key Point:** `push()` returns the NEW LENGTH of the array.

### 4.2 pop() - Remove from End

```javascript
var arr = new Array(3);
arr[0] = "D";
arr[1] = "A";
arr[2] = "C";

document.write(arr + "<br />");    // D,A,C
document.write(arr.pop() + "<br />"); // C (removed element)
document.write(arr);                // D,A
```

**Key Point:** `pop()` returns the REMOVED ELEMENT.

### 4.3 Stack Visualization

```
Before pop():           After pop():
┌─────┐                 ┌─────┐
│  C  │ ← TOP           │     │
├─────┤                 ├─────┤
│  A  │                 │  A  │ ← TOP
├─────┤                 ├─────┤
│  D  │                 │  D  │
└─────┘                 └─────┘
```

---

## 5. Queue Operations (shift/unshift)

### 5.1 shift() - Remove from Beginning

```javascript
var nar = [100, 200, 300];
document.write("after shift: " + nar.shift());  // 100 (removed)
document.write("</br>" + nar.length);           // 2
document.write("</br>" + nar);                  // 200,300
```

### 5.2 unshift() - Add to Beginning

```javascript
var arr = new Array();
arr[0] = "vita";
arr[1] = "dac";
arr[2] = "acts";

document.write(arr + "<br />");              // vita,dac,acts
document.write(arr.unshift("2020") + "<br />"); // 4 (new length)
document.write(arr);                          // 2020,vita,dac,acts
```

### 5.3 Queue Operations Summary

| Method | Action | Returns |
|--------|--------|---------|
| `push()` | Add to end | New length |
| `pop()` | Remove from end | Removed element |
| `unshift()` | Add to beginning | New length |
| `shift()` | Remove from beginning | Removed element |

---

## 6. Array Manipulation Methods

### 6.1 concat() - Join Arrays

```javascript
let nar = [10, 20, 30];
let ar = [5, 6, 7];
let result = ar.concat(nar);

document.write(result);    // 5,6,7,10,20,30
document.write("<br/>" + ar);   // 5,6,7 (unchanged)
document.write("<br/>" + nar);  // 10,20,30 (unchanged)
```

**Key Point:** Creates a NEW array, original arrays unchanged.

### 6.2 slice() - Extract Portion

```javascript
var cut = [100, 200, 300, 400];

var c = cut.slice(1);
document.write("</br>" + c);  // 200,300,400

document.write("<br>slice(1,3)=" + cut.slice(1, 3));  // 200,300
document.write("</br>" + cut);  // 100,200,300,400 (unchanged)
```

**Parameters:**
- `begin`: Starting index (inclusive)
- `end`: Ending index (exclusive, optional)

### 6.3 splice() - Add/Remove Elements

```javascript
array.splice(index, howmany, item1, ..., itemX)
```

**Remove elements:**
```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(1, 2);  // Remove 2 elements starting at index 1
document.write("</br>" + fruits);  // Banana,Mango
```

**Insert elements:**
```javascript
var fr = ["Banana", "Orange", "Apple", "Mango"];
fr.splice(2, 0, "Lemon", "Kiwi");  // Insert at index 2, remove 0
document.write("</br>" + fr);  // Banana,Orange,Lemon,Kiwi,Apple,Mango
```

### 6.4 join() - Array to String

```javascript
var ar = new Array(5, 3, 2);
let ans = ar.join("-");
document.write(ans);           // 5-3-2
document.write(typeof(ans));   // string

ans = ar.join();
document.write(ans);           // 5,3,2 (default comma)
```

### 6.5 reverse()

```javascript
var srt = new Array("anita", "zeena", "beena");
document.write("<br/>" + srt.reverse());  // beena,zeena,anita
document.write("<br/>affecting original: " + srt);  // beena,zeena,anita
```

**Warning:** `reverse()` MODIFIES the original array.

### 6.6 fill()

```javascript
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.fill("Kiwi", 2, 4);
// Output: Banana,Orange,Kiwi,Kiwi

const fruits2 = ["Banana", "Orange", "Apple", "Mango"];
fruits2.fill("Kiwi", 1);
// Output: Banana,Kiwi,Kiwi,Kiwi
```

---

## 7. Searching and Filtering

### 7.1 find() - First Matching Element

```javascript
const array1 = [5, 12, 8, 130, 44];
const found = array1.find(element => element > 10);
console.log(found);  // 12
```

**With objects:**
```javascript
const inventory = [
    {name: 'apples', quantity: 2},
    {name: 'bananas', quantity: 0},
    {name: 'cherries', quantity: 5}
];

function isCherries(fruit) {
    return fruit.name === 'cherries';
}

console.log(inventory.find(isCherries));
// { name: 'cherries', quantity: 5 }
```

### 7.2 filter() - All Matching Elements

```javascript
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];
const result = words.filter(word => word.length > 6);
console.log(result);  // ["exuberant", "destruction", "present"]

function isBigEnough(value) {
    return value >= 10;
}
let filtered = [12, 5, 8, 130, 44].filter(isBigEnough);
// filtered is [12, 130, 44]
```

### 7.3 includes() - Check Existence

```javascript
const array1 = [5, 12, 8, 130, 44];
const found = array1.includes(8);
console.log(found);  // true
```

### 7.4 at() - Access by Index

```javascript
const array1 = [5, 12, 8, 130, 44];

let index = 2;
console.log(`Using index ${index}: ${array1.at(index)}`);  // 8

index = -2;
console.log(`Using index ${index}: ${array1.at(index)}`);  // 130
```

---

## 8. Transformation Methods

### 8.1 map() - Transform Each Element

```javascript
const array1 = [1, 4, 9, 16];
const map1 = array1.map(x => x * 2);
console.log(map1);  // [2, 8, 18, 32]
```

**With HTML:**
```javascript
const array1 = [1, 4, 9, 16];
const map1 = array1.map(x => "<b>" + x + "</b>");
document.write(map1);
```

**Key Points:**
- Creates a NEW array
- Does NOT execute for empty elements
- Does NOT change original array

---

## 9. Sorting

### 9.1 Default Sort (Alphabetical)

```javascript
var srt = new Array("anita", "Zeena", "beena");
document.write("<br/>" + srt.sort());  // Zeena,anita,beena
```

**Warning - Numeric sort issues:**
```javascript
var srtno = [100, 350, 1, 2];
document.write("<br/>" + srtno.sort());  // 1,100,2,350 (WRONG!)
```

### 9.2 Numeric Sort with Comparator

```javascript
function sortnumber(a, b) {
    return a - b;
}

var srtno = [100, 350, 1, 2];
document.write("<br/>" + srtno.sort(sortnumber));  // 1,2,100,350

// Arrow function version
document.write("<br/>" + srtno.sort((a, b) => a - b));
```

**Descending order:**
```javascript
let nums = [3, 2, 6, 50, 10];
nums.sort((a, b) => b - a);  // [50, 10, 6, 3, 2]
```

### 9.3 Sorting Objects

```javascript
let users = [
    {name: 'Scotty', age: '18'},
    {name: 'Tommy', age: '21'},
    {name: 'Sally', age: '71'},
    {name: 'Billy', age: '18'},
    {name: 'Timmy', age: '21'}
];

users.sort((a, b) => {
    let keyA = a.age + a.name;
    let keyB = b.age + b.name;
    if (keyA < keyB) return -1;
    if (keyA > keyB) return 1;
    return 0;
});

// Result:
// [ { name: 'Billy', age: '18' },
//   { name: 'Scotty', age: '18' },
//   { name: 'Timmy', age: '21' },
//   { name: 'Tommy', age: '21' },
//   { name: 'Sally', age: '71' } ]
```

**Note:** `sort()` modifies the original array (in-place sorting).

---

## 10. Quick Reference

### 10.1 Mutating Methods (Change Original)

| Method | Description |
|--------|-------------|
| `push()` | Add to end |
| `pop()` | Remove from end |
| `shift()` | Remove from beginning |
| `unshift()` | Add to beginning |
| `splice()` | Add/remove elements |
| `reverse()` | Reverse order |
| `sort()` | Sort elements |
| `fill()` | Fill with value |

### 10.2 Non-Mutating Methods (Return New)

| Method | Description |
|--------|-------------|
| `concat()` | Join arrays |
| `slice()` | Extract portion |
| `map()` | Transform elements |
| `filter()` | Filter elements |
| `find()` | Find first match |
| `join()` | Convert to string |
| `includes()` | Check existence |
| `at()` | Access by index |

---

## 11. Interview Questions

### Q1: What's the difference between push() and unshift()?
**Answer**: `push()` adds elements to the END of an array, while `unshift()` adds elements to the BEGINNING. Both return the new length of the array.

### Q2: How do you remove duplicates from an array?
**Answer**:
```javascript
let arr = [1, 2, 2, 3, 3, 4];
let unique = [...new Set(arr)];  // [1, 2, 3, 4]
```

### Q3: What's the difference between slice() and splice()?
**Answer**:
- `slice()` returns a shallow copy of a portion, doesn't modify original
- `splice()` changes the array by adding/removing elements, modifies original

### Q4: Why does sort() not work correctly for numbers by default?
**Answer**: By default, `sort()` converts elements to strings and sorts alphabetically. For numbers, you need a comparator function: `arr.sort((a, b) => a - b)`.

### Q5: What's the difference between find() and filter()?
**Answer**:
- `find()` returns the FIRST element matching the condition (single value)
- `filter()` returns ALL elements matching the condition (array)

### Q6: What does map() return if no return statement is used?
**Answer**: It returns an array of `undefined` values, one for each element.

---

## Navigation

← Previous: [14_DOM_Manipulation.md](./14_DOM_Manipulation.md) | Next: [16_Strings_and_String_Methods.md](./16_Strings_and_String_Methods.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 04*
