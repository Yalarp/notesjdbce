# Strings and String Methods in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [String Creation](#2-string-creation)
3. [String Equality](#3-string-equality)
4. [Character Access](#4-character-access)
5. [Substring Methods](#5-substring-methods)
6. [Search Methods](#6-search-methods)
7. [String Manipulation](#7-string-manipulation)
8. [Case and Whitespace](#8-case-and-whitespace)
9. [ES6 String Methods](#9-es6-string-methods)
10. [Quick Reference](#10-quick-reference)
11. [Interview Questions](#11-interview-questions)

---

## 1. Introduction

### 1.1 Definition
A **String** in JavaScript is a sequence of characters used to represent text. Strings are **immutable** - once created, they cannot be changed (any operation creates a new string).

### 1.2 Key Characteristics
- Immutable (cannot be modified in place)
- Zero-based indexing
- Has a `length` property
- Can be created as primitive or object

### 1.3 Memory Diagram

```
Primitive string:           Object string:
┌─────────────┐             ┌─────────────────┐
│ a = "hello" │             │ str (reference) │──→ String Object
└─────────────┘             └─────────────────┘    ┌───────────────┐
(Stack)                     (Stack)                │ value: "hello"│
                                                   │ length: 5     │
                                                   └───────────────┘
                                                   (Heap)
```

---

## 2. String Creation

### 2.1 Primitive String (Recommended)

```javascript
var a = "VIDYANIDHI";
document.write(a);              // VIDYANIDHI
document.write(typeof(a));      // string
document.write(a.length);       // 10
```

### 2.2 String Object (Not Recommended)

```javascript
var str = new String("hello");
document.write(typeof(str));    // object
document.write(str);            // hello
```

**Warning:** Do NOT use:
- `new String()`
- `new Number()`
- `new Boolean()`
- `new Array()`

### 2.3 String Concatenation

```javascript
var a = "VIDYANIDHI";
m = a + "raj";
document.write(m);          // VIDYANIDHIraj
document.write(a);          // VIDYANIDHI (unchanged - immutable!)
document.write(a.length);   // 10 (still 10)
```

**Immutability Visualization:**
```
a → "VIDYANIDHI"
m → "VIDYANIDHIraj"  (new string created)
a is unchanged!
```

---

## 3. String Equality

### 3.1 Comparing String Objects

```javascript
var a = new String("abc");
var b = new String("abc");

document.write(a == b);       // false (different references)
document.write(a === b);      // false (different references)

var c = b;
document.write(c == b);       // true (same reference)

document.write(a.valueOf() == b.valueOf());  // true (compare values)
```

### 3.2 Comparing Primitive Strings

```javascript
var x = "abc";
var y = "abc";

document.write(x == y);       // true
document.write(x === y);      // true
document.write(x.valueOf() == y.valueOf());  // true
```

### 3.3 Mixed Comparison

```javascript
var a = new String("abc");
var x = "abc";

document.write(a == x);       // true (type coercion)
document.write(a === x);      // false (different types)
```

### 3.4 Warning: String Concatenation in Loops

```javascript
// AVOID THIS - Very slow!
str = "";
for (i = 0; i < 1000000; i++) {
    str = str + i;  // Creates new string each iteration
}
document.write(str);
```

---

## 4. Character Access

### 4.1 charAt()

```javascript
var a = "VIDYANIDHI";
document.write(a.charAt(1));  // I
```

**Index table:**
```
Index: 0  1  2  3  4  5  6  7  8  9
Char:  V  I  D  Y  A  N  I  D  H  I
```

**Get first and last character:**
```javascript
var str = "VIDYANIDHI";
var first = str.charAt(0);           // V
var last = str.charAt(str.length-1); // I
```

### 4.2 charCodeAt() / fromCharCode()

```javascript
var str = "HELLO WORLD";
var n = str.charCodeAt(0);  // 72 (Unicode for 'H')
document.write(n);

var res = String.fromCharCode(n);  // H
document.write(res);
```

**Note:** `fromCharCode()` is a static method called on `String`, not on an instance.

---

## 5. Substring Methods

### 5.1 substring(start, end)

Extracts characters between two indices (end is exclusive).

```javascript
var str = "Hello world";
document.write(str.substring(3, 7));  // "lo w"
document.write(str.substring(2));     // "llo world"
```

**Key Points:**
- If start > end, they are swapped
- Negative values treated as 0
- Does NOT change original string

### 5.2 substr(start, length)

Extracts a portion starting from a position for a specified length.

```javascript
var str = "Hello world!";
var res = str.substr(6);     // "world!"
var res2 = str.substr(1, 3); // "ell"
```

### 5.3 Difference: substr() vs substring()

| Feature | substr() | substring() |
|---------|----------|-------------|
| Syntax | `str.substr(start, length)` | `str.substring(start, end)` |
| Second param | Number of characters | End index (exclusive) |
| Negative start | Counts from end | Treated as 0 |

**Example:**
```javascript
var str = "Hello";
str.substr(1, 3);     // "ell" (3 characters from index 1)
str.substring(1, 3);  // "el" (from index 1 to 3, exclusive)
```

---

## 6. Search Methods

### 6.1 indexOf(searchValue, startIndex)

Returns position of FIRST occurrence, or -1 if not found.

```javascript
var txt = "PGDAC CDAC";
document.write(txt.indexOf("D"));      // 2
document.write(txt.indexOf("C", 5));   // 6 (start from index 5)

var a = txt.indexOf("D");
document.write(txt.indexOf("D", a+1)); // 7 (find next D)

document.write(txt.indexOf("X"));      // -1 (not found)
document.write(txt.indexOf("d"));      // -1 (case sensitive!)
```

**Index table:**
```
Index: 0  1  2  3  4  5  6  7  8  9
Char:  P  G  D  A  C     C  D  A  C
```

### 6.2 lastIndexOf(searchValue, endIndex)

Returns position of LAST occurrence (searched from end).

```javascript
var txt = "PGDAC CDAC";
document.write(txt.lastIndexOf("D"));      // 7
document.write(txt.lastIndexOf("D", 6));   // 2 (search before index 6)
document.write(txt.lastIndexOf("X"));      // -1
document.write(txt.lastIndexOf("d"));      // -1 (case sensitive)
```

### 6.3 match() with Regular Expressions

```javascript
var str = "Center Vita Center";
document.write(str.match("Center"));       // Center (first match only)

var str = "Center Vita center";
let s = str.match(/center/ig);  // i=ignore case, g=global
for (i = 0; i < s.length; i++) {
    document.write(s[i]);       // Center, center
}

document.write(str.match("dac"));  // null
```

---

## 7. String Manipulation

### 7.1 concat()

```javascript
var str1 = "Hello ";
var str2 = "world!";
var str3 = str1.concat(str2);
document.write(str3);    // "Hello world!"
document.write(str1);    // "Hello " (unchanged)
document.write(str2);    // "world!" (unchanged)
```

### 7.2 split() - String to Array

```javascript
var str = "wel-come";
var s = str.split("-");
document.write(s);       // wel,come
document.write(s[0]);    // wel
document.write(s[1]);    // come

// Split each character
var s2 = str.split("");
document.write(s2);      // w,e,l,-,c,o,m,e
```

### 7.3 replace()

```javascript
var str = "Visit CDAC cdac is good center!";
document.write(str.replace(/cdac/ig, "VITA"));
// Output: Visit VITA VITA is good center!
```

**Modifiers:**
- `i` = ignore case
- `g` = global (all occurrences)

**Without global modifier:**
```javascript
var str = "Visit CDAC cdac is good!";
document.write(str.replace("CDAC", "VITA"));
// Only replaces first occurrence
```

---

## 8. Case and Whitespace

### 8.1 toUpperCase() / toLowerCase()

```javascript
var str = "Hello World!";
var res = str.toLowerCase();   // "hello world!"
var result = str.toUpperCase(); // "HELLO WORLD!"
```

**Note:** Does NOT change original string.

### 8.2 trim()

```javascript
var str = "  Hello World!  ";
alert(str.trim());  // "Hello World!" (whitespace removed)
```

---

## 9. ES6 String Methods

### 9.1 repeat()

```javascript
var str = "Hello World! ";
document.write(str.repeat(2));  // "Hello World! Hello World! "
```

### 9.2 startsWith() / endsWith()

```javascript
var str = "Hello World!";
var n = str.startsWith("Hello");  // true
var en = str.endsWith("!");       // true
```

**Note:** Case sensitive!

### 9.3 includes()

```javascript
var str = "Hello World!";
var rr = str.includes("World", 5);  // true (search from index 5)
```

**Syntax:** `string.includes(searchvalue, start)`

---

## 10. Quick Reference

### 10.1 Character Access

| Method | Description |
|--------|-------------|
| `charAt(index)` | Character at position |
| `charCodeAt(index)` | Unicode of character |
| `String.fromCharCode(code)` | Character from Unicode |

### 10.2 Search Methods

| Method | Description |
|--------|-------------|
| `indexOf(str, start)` | First occurrence position |
| `lastIndexOf(str, end)` | Last occurrence position |
| `match(regex)` | Match against regex |
| `includes(str)` | Check if contains (ES6) |

### 10.3 Extraction Methods

| Method | Description |
|--------|-------------|
| `substring(start, end)` | Extract by index range |
| `substr(start, length)` | Extract by length |
| `slice(start, end)` | Extract portion |

### 10.4 Transformation

| Method | Description |
|--------|-------------|
| `toUpperCase()` | Convert to uppercase |
| `toLowerCase()` | Convert to lowercase |
| `trim()` | Remove whitespace |
| `replace(old, new)` | Replace substring |
| `split(separator)` | Split to array |
| `concat(str)` | Concatenate strings |
| `repeat(n)` | Repeat n times |

---

## 11. Interview Questions

### Q1: Why are strings immutable in JavaScript?
**Answer**: Strings are immutable for thread safety, security, and memory efficiency. When you "modify" a string, a new string is created in memory. This prevents unexpected changes and enables string interning (reusing identical strings).

### Q2: What's the difference between indexOf() and includes()?
**Answer**:
- `indexOf()` returns the position (number) or -1 if not found
- `includes()` returns `true` or `false`
- `includes()` is more readable for boolean checks

### Q3: What's the difference between substr() and substring()?
**Answer**:
- `substr(start, length)` - second param is number of characters
- `substring(start, end)` - second param is ending index (exclusive)
- `substr()` accepts negative start (counts from end)

### Q4: How do you check if a string contains a specific substring?
**Answer**:
```javascript
// ES6
str.includes("substring")

// Pre-ES6
str.indexOf("substring") !== -1
```

### Q5: How do you split a string by multiple delimiters?
**Answer**: Use a regular expression:
```javascript
var str = "apple,banana;cherry";
var arr = str.split(/[,;]/);  // ["apple", "banana", "cherry"]
```

### Q6: How do you reverse a string?
**Answer**:
```javascript
var str = "Hello";
var reversed = str.split("").reverse().join("");
// "olleH"
```

### Q7: What is the output of `"abc" === new String("abc")`?
**Answer**: `false`, because `===` checks type and the left is a primitive string while the right is a String object.

---

## Navigation

← Previous: [15_Arrays_and_Array_Methods.md](./15_Arrays_and_Array_Methods.md) | Next: [17_Date_and_Math_Functions.md](./17_Date_and_Math_Functions.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 04*
