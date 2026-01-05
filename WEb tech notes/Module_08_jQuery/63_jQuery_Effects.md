# jQuery Effects

## Table of Contents
1. [Introduction](#1-introduction)
2. [Hide and Show](#2-hide-and-show)
3. [Fading](#3-fading)
4. [Sliding](#4-sliding)
5. [Animation](#5-animation)
6. [Chaining](#6-chaining)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

jQuery allows you to create effects on the page easily, such as showing/hiding elements, fading them in/out, or sliding them. Most effect methods allow a "callback" function to be executed after the animation completes.

---

## 2. Hide and Show

Simply toggles the `display` CSS property.

```javascript
// Syntax: $(selector).hide(speed, callback);

$("#hide").click(function(){
  $("p").hide(1000); // 1000ms = 1s
});

$("#show").click(function(){
  $("p").show("slow");
});

$("#toggle").click(function(){
  $("p").toggle();
});
```

---

## 3. Fading

Changes the opacity of elements.

| Method | Description |
|--------|-------------|
| `fadeIn()` | Fades in a hidden element |
| `fadeOut()` | Fades out a visible element |
| `fadeToggle()` | Toggles between fadeIn and fadeOut |
| `fadeTo()` | Fades to a specific opacity (0.0 to 1.0) |

```javascript
$("div").fadeIn();
$("div").fadeOut("slow");
$("div").fadeTo("slow", 0.5); // 50% opacity
```

---

## 4. Sliding

Slides elements up or down (modifies height).

| Method | Description |
|--------|-------------|
| `slideDown()` | Slides down (shows) |
| `slideUp()` | Slides up (hides) |
| `slideToggle()` | Toggles between slideDown and slideUp |

```javascript
$("#panel").slideDown();
```

---

## 5. Animation

The `animate()` method is used to create custom animations by changing CSS properties over time.

**Syntax:**
```javascript
$(selector).animate({params}, speed, callback);
```

**Constraints:**
- Colors cannot be animated without plugins.
- Only numeric values (height, width, opacity, margin) can be animated.
- Property names must be camel-cased (`paddingLeft` not `padding-left`).

**Example:**
```javascript
$("button").click(function(){
  $("div").animate({
    left: '250px',
    opacity: '0.5',
    height: '150px',
    width: '150px'
  });
});
```

### 5.1 Using Relative Values
You can define relative values (relative to current value).

```javascript
$("div").animate({
    left: '250px',
    height: '+=150px', // Increases height by 150px
    width: '+=150px'
});
```

### 5.2 Queue Functionality
jQuery comes with a queued functionality for animations. If you write multiple `animate()` calls one after another, jQuery creates an "internal" queue and runs them one by one.

```javascript
var div = $("div");
div.animate({height: '300px', opacity: '0.4'}, "slow");
div.animate({width: '300px', opacity: '0.8'}, "slow");
div.animate({height: '100px', opacity: '0.4'}, "slow");
div.animate({width: '100px', opacity: '0.8'}, "slow");
```

---

## 6. Chaining

Chaining allows us to run multiple jQuery commands, on the same element, one after the other.

**Example (from `27_chaining_element.html`):**

```javascript
$("#p1").css("color", "red").slideUp(2000).slideDown(2000);
```

**Explanation:**
1.  `$("#p1")` selects the element.
2.  Errors to red.
3.  Slides up (hides) over 2 seconds.
4.  Slides down (shows) over 2 seconds.
All happen sequentially because of the internal effect queue.

---

## 7. Quick Reference

| Effect | Methods |
|--------|---------|
| **Visibility** | `show()`, `hide()`, `toggle()` |
| **Fading** | `fadeIn()`, `fadeOut()`, `fadeToggle()`, `fadeTo()` |
| **Sliding** | `slideDown()`, `slideUp()`, `slideToggle()` |
| **Custom** | `animate({params}, speed)` |
| **Stop** | `stop()` stops current animation |

---

## 8. Interview Questions

### Q1: What is the "Callback" function in effects?
**Answer**: Javascript statements are executed line by line. However, effects take some time to finish. A callback function is executed **only after the effect is 100% finished**.
`$("p").hide("slow", function(){ alert("Hidden!"); });`

### Q2: Can you animate background color with standard jQuery?
**Answer**: No. The standard `animate()` function supports numeric CSS properties only. For colors, you need the jQuery UI library or a color animation plugin.

### Q3: How do you stop an animation midway?
**Answer**: By using the `stop()` method. `$(selector).stop()`.

### Q4: What is method chaining?
**Answer**: It is a technique where multiple methods are called on the same jQuery object in a single statement (e.g., `$("#d").hide().show()`). This works because most jQuery methods return the jQuery object itself.

---

## Navigation

← Previous: [62_jQuery_Loops.md](./62_jQuery_Loops.md) | Next: [64_jQuery_Forms.md](./64_jQuery_Forms.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 13*
