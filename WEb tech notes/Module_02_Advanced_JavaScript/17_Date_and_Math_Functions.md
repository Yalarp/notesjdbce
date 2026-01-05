# Date and Math Functions in JavaScript

## Table of Contents
1. [Introduction](#1-introduction)
2. [Date Object](#2-date-object)
3. [Date Creation](#3-date-creation)
4. [Get Methods](#4-get-methods)
5. [Set Methods](#5-set-methods)
6. [Date Formatting and Parsing](#6-date-formatting-and-parsing)
7. [Math Object](#7-math-object)
8. [Math Methods](#8-math-methods)
9. [Random Numbers](#9-random-numbers)
10. [Quick Reference](#10-quick-reference)
11. [Interview Questions](#11-interview-questions)

---

## 1. Introduction

### 1.1 Date Object
The **Date** object in JavaScript is used to work with dates and times. It stores dates as the number of milliseconds since January 01, 1970, 00:00:00 UTC (Unix Epoch).

### 1.2 Math Object
The **Math** object is a built-in object with properties and methods for mathematical constants and functions. All Math methods are **static**.

---

## 2. Date Object

### 2.1 Default Output

```javascript
var d = new Date();
// Output: Mon Nov 30 2020 13:03:21 GMT+0530 (India Standard Time)
```

### 2.2 Key Points
- Uses browser's time zone by default
- Month is 0-indexed (0 = January, 11 = December)
- Day of week is 0-indexed (0 = Sunday, 6 = Saturday)

---

## 3. Date Creation

### 3.1 Four Ways to Create a Date

```javascript
// 1. Current date and time
new Date();

// 2. Specified date and time
new Date(year, month, day, hours, minutes, seconds, milliseconds);

// 3. Milliseconds since epoch
new Date(0);

// 4. Date string
new Date(date string);
```

### 3.2 Date Creation Examples

```javascript
// Current date and time
var d = new Date();
// Output: Mon Nov 30 2020 14:33:20 GMT+0530 (India Standard Time)

// Specific date with 7 parameters
var d = new Date(2018, 11, 24, 10, 33, 30, 0);
// Output: Mon Dec 24 2018 10:33:30 GMT+0530 (India Standard Time)

// 6 parameters (year, month, day, hour, minute, second)
var d = new Date(2018, 11, 24, 10, 33, 30);
// Output: Mon Dec 24 2018 10:33:30 GMT+0530 (India Standard Time)
```

### 3.3 Date Format Types

| Type | Example | Description |
|------|---------|-------------|
| ISO Date | "2015-03-25" | International Standard (preferred) |
| Short Date | "03/25/2015" | US format |
| Long Date | "Mar 25 2015" | String format |

---

## 4. Get Methods

### 4.1 Available Get Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `getFullYear()` | Get year | 4-digit year |
| `getMonth()` | Get month | 0-11 |
| `getDate()` | Get day of month | 1-31 |
| `getDay()` | Get day of week | 0-6 |
| `getHours()` | Get hour | 0-23 |
| `getMinutes()` | Get minutes | 0-59 |
| `getSeconds()` | Get seconds | 0-59 |
| `getMilliseconds()` | Get milliseconds | 0-999 |
| `getTime()` | Get milliseconds since epoch | Number |

### 4.2 Get Methods Example

```javascript
var a = new Date();

document.write("Date  " + a + "<br/>");
document.write("Date  " + a.getDate() + "<br/>");
document.write("Day  " + a.getDay() + "<br/>");
document.write("Hours  " + a.getHours() + "<br/>");
document.write("Minutes  " + a.getMinutes() + "<br/>");
document.write("Seconds " + a.getSeconds() + "<br/>");
document.write("Time  " + a.getTime() + "<br/>");
document.write("Month  " + a.getMonth() + "<br/>");
document.write("MillSec  " + a.getMilliseconds() + "<br/>");
document.write("FullYear  " + a.getFullYear() + "<br/>");
```

**Output:**
```
Date Mon Nov 30 2020 15:19:26 GMT+0530 (India Standard Time)
Date 30
Day 1
Hours 15
Minutes 19
Seconds 26
Time 1606729766545
Month 10
MillSec 545
FullYear 2020
```

**Note:** `getMonth()` returns 0-11, so November is 10, not 11!

---

## 5. Set Methods

### 5.1 Available Set Methods

| Method | Description |
|--------|-------------|
| `setDate()` | Set day of month (1-31) |
| `setFullYear()` | Set year (optionally month and day) |
| `setHours()` | Set hour (0-23) |
| `setMilliseconds()` | Set milliseconds (0-999) |
| `setMinutes()` | Set minutes (0-59) |
| `setMonth()` | Set month (0-11) |
| `setSeconds()` | Set seconds (0-59) |
| `setTime()` | Set time in milliseconds |

### 5.2 Set Methods Examples

```javascript
var d = new Date();
d.setFullYear(2020);

// Set year, month, and day together
var d = new Date();
d.setFullYear(2020, 11, 3);

// Set month only
var d = new Date();
d.setMonth(11);

// Set day only
var d = new Date();
d.setDate(15);
```

---

## 6. Date Formatting and Parsing

### 6.1 String to Date

```javascript
var s = "2015-03-25";
var d = new Date(s);
document.write(d);
```

### 6.2 Date.parse()

Converts a date string to milliseconds since epoch:

```javascript
var msec = Date.parse("March 21, 2012");
document.write(msec);  // 1332268200000

var d = new Date(msec);
document.write(d);  // Wed Mar 21 2012 00:00:00 GMT+0530
```

### 6.3 Digital Clock Example

```html
<html>
<head>
<script type="text/javascript">
function startTime() {
    var today = new Date();
    var h = today.getHours();
    var m = today.getMinutes();
    var s = today.getSeconds();
    
    // Add leading zero for numbers < 10
    m = checkTime(m);
    s = checkTime(s);
    h = checkTime(h);
    
    document.getElementById('txt').innerHTML = h + ":" + m + ":" + s;
    t = setTimeout('startTime()', 500);  // Update every 500ms
}

function checkTime(i) {
    if (i < 10) {
        i = "0" + i;
    }
    return i;
}
</script>
</head>
<body onload="startTime()">
<div id="txt"></div>
</body>
</html>
```

---

## 7. Math Object

### 7.1 Math Properties

| Property | Value | Description |
|----------|-------|-------------|
| `Math.PI` | 3.141592653589793 | Pi |
| `Math.E` | 2.718281828459045 | Euler's number |
| `Math.SQRT2` | 1.4142135623730951 | Square root of 2 |
| `Math.LN2` | 0.6931471805599453 | Natural log of 2 |
| `Math.LN10` | 2.302585092994046 | Natural log of 10 |

### 7.2 Key Point
All Math methods and properties are **static** - called directly on `Math`, not on an instance.

```javascript
// Correct
Math.random();
Math.floor(4.7);

// Wrong - no instances
var m = new Math();  // Error!
```

---

## 8. Math Methods

### 8.1 Common Math Methods

| Method | Description | Example |
|--------|-------------|---------|
| `Math.round(x)` | Round to nearest integer | `Math.round(4.7)` → 5 |
| `Math.floor(x)` | Round down | `Math.floor(4.7)` → 4 |
| `Math.ceil(x)` | Round up | `Math.ceil(4.4)` → 5 |
| `Math.pow(x, y)` | x to the power y | `Math.pow(8, 2)` → 64 |
| `Math.sqrt(x)` | Square root | `Math.sqrt(64)` → 8 |
| `Math.abs(x)` | Absolute value | `Math.abs(-5)` → 5 |
| `Math.min(...)` | Minimum value | `Math.min(0, 150, -8)` → -8 |
| `Math.max(...)` | Maximum value | `Math.max(0, 150, -8)` → 150 |

### 8.2 Examples

```javascript
Math.PI;                              // 3.141592653589793
Math.round(4.7);                      // 5
Math.pow(8, 2);                       // 64
Math.sqrt(64);                        // 8
Math.ceil(4.4);                       // 5
Math.floor(4.7);                      // 4
Math.min(0, 150, 30, 20, -8, -200);   // -200
Math.max(0, 150, 30, 20, -8, -200);   // 150
```

---

## 9. Random Numbers

### 9.1 Math.random()

Generates a random number between 0 (inclusive) and 1 (exclusive):

```javascript
document.write(Math.random());  // e.g., 0.025623787930399766
```

### 9.2 Random Integer in Range

```javascript
// Random number from 0 to n-1
var randomNum = Math.floor(n * Math.random());

// Example: Random from 0 to 3
a = (Math.random() * 4);
document.write(a);           // e.g., 0.5626264433314665

x = Math.floor(a);
document.write(x);           // e.g., 0
```

### 9.3 Random Background Color Example

```html
<html>
<head>
<script>
var tt;

function changebg() {
    var col = new Array("green", "blue", "red");
    var l = col.length;
    
    // Generate random number between [0 to 2]
    var rnd_no = Math.floor(l * Math.random());
    
    document.body.bgColor = col[rnd_no];
    
    tt = setTimeout('changebg()', 500);
}

function stopclock() {
    clearTimeout(tt);
}
</script>
</head>
<body onLoad="changebg()">
<input type="button" onclick="stopclock()" value="stop">
</body>
</html>
```

### 9.4 Random in Range Formula

```javascript
// Random integer between min (inclusive) and max (exclusive)
Math.floor(Math.random() * (max - min)) + min;

// Random integer between min and max (both inclusive)
Math.floor(Math.random() * (max - min + 1)) + min;
```

---

## 10. Quick Reference

### 10.1 Date Creation

```javascript
new Date();                          // Current date/time
new Date(2020, 11, 25);              // Dec 25, 2020
new Date("2020-12-25");              // From string
new Date(milliseconds);              // From epoch
```

### 10.2 Date Get Methods

```javascript
date.getFullYear();    // 4-digit year
date.getMonth();       // 0-11
date.getDate();        // 1-31
date.getDay();         // 0-6
date.getHours();       // 0-23
date.getMinutes();     // 0-59
date.getSeconds();     // 0-59
date.getTime();        // Milliseconds since epoch
```

### 10.3 Math Methods

```javascript
Math.round(x);         // Round to nearest
Math.floor(x);         // Round down
Math.ceil(x);          // Round up
Math.random();         // Random 0-1
Math.max(a, b, c);     // Maximum
Math.min(a, b, c);     // Minimum
Math.pow(base, exp);   // Power
Math.sqrt(x);          // Square root
Math.abs(x);           // Absolute value
```

---

## 11. Interview Questions

### Q1: Why is getMonth() 0-indexed?
**Answer**: JavaScript uses 0-based indexing for months (0 = January, 11 = December). This is a common convention in programming languages inherited from C. Always remember to add 1 when displaying months to users.

### Q2: How do you get the current timestamp?
**Answer**:
```javascript
Date.now();              // ES5+
new Date().getTime();    // Pre-ES5
+new Date();             // Unary + conversion
```

### Q3: What does Date.parse() return?
**Answer**: It returns the number of milliseconds since January 1, 1970, 00:00:00 UTC. Returns NaN if the string cannot be parsed.

### Q4: Why can't you use `new Math()`?
**Answer**: Math is not a constructor; it's a static object. All its methods and properties are called directly on Math itself (e.g., `Math.random()`, `Math.PI`).

### Q5: How do you generate a random integer between 1 and 10?
**Answer**:
```javascript
Math.floor(Math.random() * 10) + 1;
// random() gives 0-0.999...
// * 10 gives 0-9.999...
// floor() gives 0-9
// + 1 gives 1-10
```

### Q6: What's the difference between Math.floor() and Math.round()?
**Answer**:
- `Math.floor()` always rounds DOWN (toward negative infinity)
- `Math.round()` rounds to NEAREST integer (4.5 → 5, 4.4 → 4)

### Q7: How do you compare two dates?
**Answer**:
```javascript
var date1 = new Date("2020-01-01");
var date2 = new Date("2020-12-31");

if (date1.getTime() < date2.getTime()) {
    console.log("date1 is earlier");
}

// Or simply use comparison operators
if (date1 < date2) {
    console.log("date1 is earlier");
}
```

---

## Navigation

← Previous: [16_Strings_and_String_Methods.md](./16_Strings_and_String_Methods.md) | Next: [18_Form_Handling.md](./18_Form_Handling.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 04*
