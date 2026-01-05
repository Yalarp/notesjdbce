# Regular Expressions in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Creating Regular Expressions](#2-creating-regular-expressions)
3. [Basic Patterns](#3-basic-patterns)
4. [Special Characters](#4-special-characters)
5. [Quantifiers](#5-quantifiers)
6. [Character Sets and Ranges](#6-character-sets-and-ranges)
7. [Built-in Character Classes](#7-built-in-character-classes)
8. [Regex Flags](#8-regex-flags)
9. [String Methods with Regex](#9-string-methods-with-regex)
10. [Common Validation Patterns](#10-common-validation-patterns)
11. [Quick Reference](#11-quick-reference)
12. [Interview Questions](#12-interview-questions)

---

## 1. Introduction

### 1.1 Definition
A **Regular Expression** (regex) is a sequence of characters that forms a search pattern. It's used for text search, validation, and replace operations.

### 1.2 Why Use Regex?

**Without regex (verbose):**
```javascript
var str = "Neo| Trinity   |Morpheus    |  Smith|  Tank";
result = str.split("|");
// Still has spaces: ["Neo", " Trinity   ", "Morpheus    ", ...]
```

**With regex (clean):**
```javascript
var str = "Neo| Trinity   |Morpheus    |  Smith|  Tank";
var pattern = /\s*\|\s*/;
result = str.split(pattern);
// Clean: ["Neo", "Trinity", "Morpheus", "Smith", "Tank"]
```

---

## 2. Creating Regular Expressions

### 2.1 Regex Literal

```javascript
var pattern = /abc/;
var caseInsensitive = /abc/i;
```

### 2.2 RegExp Constructor

```javascript
var pattern = new RegExp("abc");
var caseInsensitive = new RegExp("abc", "i");
```

### 2.3 When to Use Each

| Method | Use Case |
|--------|----------|
| Literal `/pattern/` | Static patterns known at compile time |
| `new RegExp()` | Dynamic patterns built from variables |

---

## 3. Basic Patterns

### 3.1 Literal Matching

```javascript
/abc/.test("abc");     // true - exact match
/abc/.test("abcdef");  // true - contains "abc"
/abc/.test("defabc");  // true - contains "abc"
/abc/.test("ab c");    // false - space breaks match
/abc/.test("ABC");     // false - case sensitive
```

### 3.2 Anchors

| Symbol | Meaning | Example |
|--------|---------|---------|
| `^` | Start of line | `/^hello/` matches "hello world" |
| `$` | End of line | `/world$/` matches "hello world" |

```javascript
/^if$/.test("if");        // true - exact match
/^if$/.test("if else");   // false - has more text
```

---

## 4. Special Characters

### 4.1 Wildcards

| Symbol | Meaning | Example |
|--------|---------|---------|
| `.` | Any character (except `\n`) | `/.oo.y/` matches "Doocy", "goofy" |
| `\.` | Literal dot | `/\.com/` matches ".com" |

### 4.2 Escape Sequences

Characters that must be escaped: `/ \ $ . [ ] ( ) ^ * + ?`

```javascript
/http[s]?:\/\/w+\.com/   // Matches http or https URLs
```

### 4.3 OR and Grouping

| Symbol | Meaning | Example |
|--------|---------|---------|
| `\|` | OR | `/abc\|def/` matches "abc" or "def" |
| `()` | Grouping | `/(Homer\|Marge) Simpson/` |

```javascript
/abc|def|g/.test("hello go to school");  // true (matches "g")
```

---

## 5. Quantifiers

### 5.1 Basic Quantifiers

| Symbol | Meaning | Example |
|--------|---------|---------|
| `*` | 0 or more | `/abc*/` → "ab", "abc", "abcc" |
| `+` | 1 or more | `/abc+/` → "abc", "abcc" (not "ab") |
| `?` | 0 or 1 | `/colou?r/` → "color", "colour" |

### 5.2 Examples

```javascript
// * - zero or more
/a(bc)*/.test("a");      // true
/a(bc)*/.test("abcbc");  // true

// + - one or more
/Goo+gle/.test("Google");   // true
/Goo+gle/.test("Gooogle");  // true

// ? - zero or one
/Dan(iel)?/.test("Dan");      // true
/Dan(iel)?/.test("Daniel");   // true
```

### 5.3 Range Quantifiers

| Syntax | Meaning |
|--------|---------|
| `{n}` | Exactly n times |
| `{n,}` | n or more times |
| `{,n}` | Up to n times |
| `{n,m}` | Between n and m times |

```javascript
/a(bc){2,4}/   // Matches "abcbc", "abcbcbc", "abcbcbcbc"
```

---

## 6. Character Sets and Ranges

### 6.1 Character Sets

```javascript
/[bcd]art/   // Matches "bart", "cart", "dart"
/[.!*?]*/    // Matches ".", "!", "*", "?" (special chars are literal inside [])
```

### 6.2 Character Ranges

```javascript
/[a-z]/          // Any lowercase letter
/[A-Z]/          // Any uppercase letter
/[0-9]/          // Any digit
/[a-zA-Z0-9]/    // Any letter or digit
```

### 6.3 Negation

```javascript
/[^abcd]/   // Any character BUT a, b, c, d
/[^0-9]/    // Any non-digit
```

---

## 7. Built-in Character Classes

| Class | Meaning | Equivalent |
|-------|---------|------------|
| `\d` | Any digit | `[0-9]` |
| `\D` | Any non-digit | `[^0-9]` |
| `\w` | Any word character | `[A-Za-z0-9_]` |
| `\W` | Any non-word character | `[^A-Za-z0-9_]` |
| `\s` | Any whitespace | `[ \f\n\r\t\v]` |
| `\S` | Any non-whitespace | `[^ \f\n\r\t\v]` |
| `\b` | Word boundary | Space between words |
| `\B` | Non-word boundary | |

```javascript
/\w+\s+\w+/   // Two space-separated words
/\d{10}/      // 10 digits (phone number)
```

---

## 8. Regex Flags

| Flag | Meaning |
|------|---------|
| `g` | Global - match all occurrences |
| `i` | Case-insensitive |
| `m` | Multi-line mode |

```javascript
/abc/gi    // All occurrences, ignore case
/Marty/i   // Matches "marty", "MaRtY", etc.
```

---

## 9. String Methods with Regex

### 9.1 test()

```javascript
var pattern = /hello/;
pattern.test("hello world");  // true
pattern.test("goodbye");      // false
```

### 9.2 search()

```javascript
var str = "The Matrix";
str.search(/matrix/i);   // 4 (found at index 4)
str.search(/trinity/);   // -1 (not found)
```

### 9.3 match()

```javascript
"obama".match(/.a/g);      // ["ba", "ma"]
"hello".match(/[A-Z]/);    // null
"HELLO".match(/[A-Z]/g);   // ["H", "E", "L", "L", "O"]
```

### 9.4 replace()

```javascript
var state = "Mississippi";
state.replace(/s/, "x");     // "Mixsissippi" (first only)
state.replace(/s/g, "x");    // "Mixxixxippi" (all)
```

### 9.5 split()

```javascript
"a,b;c".split(/[,;]/);   // ["a", "b", "c"]
```

---

## 10. Common Validation Patterns

### 10.1 Password Validation

```javascript
function check_pass() {
    let cap = /[A-Z]{1,13}/;
    let small = /[a-z]{1,13}/;
    let num = /[0-9]{1,13}/;
    
    let str = document.getElementById("tt").value;
    
    if (!cap.test(str)) {
        alert("Capital letter is missing");
        return false;
    }
    if (!small.test(str)) {
        alert("Small letter is missing");
        return false;
    }
    if (!num.test(str)) {
        alert("Number is missing");
        return false;
    }
    return true;
}
```

### 10.2 Common Patterns

| Purpose | Pattern |
|---------|---------|
| Mobile (10 digit) | `/^[0-9]{10}$/` |
| Age (1-2 digit) | `/^[0-9]{1,2}$/` |
| Pincode (6 digit) | `/^\d{6}$/` |
| Username (3-15 chars) | `/^[A-Za-z0-9._-]{3,16}$/` |
| Password (8+ chars) | `/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d]{8,}$/` |
| Date (DD/MM/YYYY) | `/^(0[1-9]\|[12][0-9]\|3[01])[-\/](0[1-9]\|1[0-2])[-\/](19\|20)\d\d$/` |
| Time (12hr) | `/^(0[0-9]\|1[0-2]):([0-5][0-9])\s?(AM\|PM)$/i` |
| Email | `/^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,3}$/` |
| URL | `/^(https?:\/\/)?([\\da-z.-]+)\\.([a-z.]{2,6})([/\\w.-]*)*\\/?$/` |

### 10.3 Email Validation Breakdown

```javascript
/^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,3}$/
```

| Part | Meaning |
|------|---------|
| `^[a-zA-Z0-9._-]+` | Username: letters, numbers, dots, underscores, hyphens |
| `@` | Mandatory @ symbol |
| `[a-zA-Z0-9.-]+` | Domain name |
| `\.[a-zA-Z]{2,3}$` | TLD: 2-3 letters (.com, .net, .org) |

---

## 11. Quick Reference

### 11.1 Metacharacters

```
.     Any character (except newline)
^     Start of string
$     End of string
*     0 or more
+     1 or more
?     0 or 1
|     OR
()    Grouping
[]    Character set
[^]   Negated set
\     Escape
```

### 11.2 Character Classes

```
\d    Digit [0-9]
\D    Non-digit
\w    Word char [A-Za-z0-9_]
\W    Non-word
\s    Whitespace
\S    Non-whitespace
\b    Word boundary
```

### 11.3 Quantifiers

```
*       0 or more
+       1 or more
?       0 or 1
{n}     Exactly n
{n,}    n or more
{n,m}   Between n and m
```

### 11.4 Flags

```
g     Global
i     Case-insensitive
m     Multi-line
```

---

## 12. Interview Questions

### Q1: What is a regular expression?
**Answer**: A regular expression is a sequence of characters that defines a search pattern. It's used for pattern matching, validation, search, and replace operations in strings.

### Q2: What's the difference between `*` and `+` quantifiers?
**Answer**:
- `*` matches 0 or more occurrences
- `+` matches 1 or more occurrences
- `/ab*/` matches "a", "ab", "abb"
- `/ab+/` matches "ab", "abb" (not "a")

### Q3: How do you make a regex case-insensitive?
**Answer**: Add the `i` flag: `/pattern/i` or `new RegExp("pattern", "i")`

### Q4: What does `/^...$/.test(str)` ensure?
**Answer**: The anchors `^` and `$` ensure the entire string matches the pattern, not just a substring.

### Q5: How do you validate an email with regex?
**Answer**:
```javascript
var emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,3}$/;
emailPattern.test("user@example.com");  // true
```

### Q6: What is the difference between `match()` and `test()`?
**Answer**:
- `test()` returns boolean (true/false)
- `match()` returns the matched content (array or null)

---

## Navigation

← Previous: [20_History_Navigator_Objects.md](./20_History_Navigator_Objects.md) | Next: [22_Event_Object.md](./22_Event_Object.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 05*
