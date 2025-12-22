# CDAC CCEE MCQ Practice Set 2

## 📝 EASY-MODERATE LEVEL - Basic Code Understanding
**Total Questions: 50 | Time Limit: 60 minutes | No Negative Marking**

> **Difficulty: ⭐⭐ Easy-Moderate** - These questions require understanding simple code snippets and applying basic concepts. One step up from Set 1.

---

### Question 1
What is the output?
```java
int x = 5;
System.out.println(x++);
```

A) 5  
B) 6  
C) 4  
D) Error

---

### Question 2
What is the output?
```java
String s = "Hello";
System.out.println(s.length());
```

A) 4  
B) 5  
C) 6  
D) Hello

---

### Question 3
What is the output?
```java
int[] arr = {1, 2, 3};
System.out.println(arr[1]);
```

A) 1  
B) 2  
C) 3  
D) Error

---

### Question 4
What is the output?
```java
System.out.println(10 / 3);
```

A) 3  
B) 3.33  
C) 4  
D) 3.0

---

### Question 5
What is the output?
```java
boolean a = true;
boolean b = false;
System.out.println(a && b);
```

A) true  
B) false  
C) 1  
D) 0

---

### Question 6
What is the output?
```java
int x = 10;
if(x > 5) {
    System.out.println("Big");
} else {
    System.out.println("Small");
}
```

A) Big  
B) Small  
C) 10  
D) Error

---

### Question 7
What is the output?
```java
for(int i = 0; i < 3; i++) {
    System.out.print(i + " ");
}
```

A) 0 1 2  
B) 1 2 3  
C) 0 1 2 3  
D) 1 2

---

### Question 8
What is the output?
```java
String s1 = "Hello";
String s2 = "Hello";
System.out.println(s1 == s2);
```

A) true  
B) false  
C) Hello  
D) Error

---

### Question 9
What is the output?
```java
int x = 5;
x += 3;
System.out.println(x);
```

A) 5  
B) 3  
C) 8  
D) 15

---

### Question 10
What is the output?
```java
System.out.println("10" + 5);
```

A) 15  
B) 105  
C) 10 5  
D) Error

---

### Question 11
What is the output?
```java
int x = 10;
System.out.println(x > 5 && x < 15);
```

A) true  
B) false  
C) 10  
D) Error

---

### Question 12
What is the output?
```java
String s = "Java";
System.out.println(s.charAt(0));
```

A) J  
B) a  
C) 0  
D) Java

---

### Question 13
What is the output?
```java
int[] arr = new int[3];
System.out.println(arr[0]);
```

A) null  
B) 0  
C) undefined  
D) Error

---

### Question 14
What is the output?
```java
int x = 7;
System.out.println(x % 3);
```

A) 2  
B) 1  
C) 0  
D) 3

---

### Question 15
What is the output?
```java
class A {
    int x = 10;
}
A obj = new A();
System.out.println(obj.x);
```

A) 0  
B) 10  
C) null  
D) Error

---

### Question 16
What is the output?
```java
System.out.println("Hello".toUpperCase());
```

A) Hello  
B) HELLO  
C) hello  
D) Error

---

### Question 17
What is the output?
```java
int x = 10;
int y = 5;
System.out.println(x > y ? "A" : "B");
```

A) A  
B) B  
C) true  
D) 10

---

### Question 18
What is the output?
```java
int sum = 0;
for(int i = 1; i <= 3; i++) {
    sum += i;
}
System.out.println(sum);
```

A) 3  
B) 6  
C) 10  
D) 0

---

### Question 19
What is the output?
```java
String s = "Hello World";
System.out.println(s.indexOf("o"));
```

A) 3  
B) 4  
C) 5  
D) 7

---

### Question 20
What is the output?
```java
int x = 5;
System.out.println(++x);
```

A) 5  
B) 6  
C) 4  
D) Error

---

### Question 21
What is the output?
```java
System.out.println(5 + 3 + "Hello");
```

A) 53Hello  
B) 8Hello  
C) Hello53  
D) Hello8

---

### Question 22
What is the output?
```java
boolean result = !(5 > 3);
System.out.println(result);
```

A) true  
B) false  
C) 5  
D) Error

---

### Question 23
What is the output?
```java
String s = "Java";
System.out.println(s.substring(1, 3));
```

A) Ja  
B) av  
C) ava  
D) Java

---

### Question 24
What is the output?
```java
int x = 0;
while(x < 3) {
    System.out.print(x);
    x++;
}
```

A) 012  
B) 123  
C) 0123  
D) 0 1 2

---

### Question 25
What is the output?
```java
class Test {
    int x = 10;
    void display() {
        System.out.println(x);
    }
}
Test t = new Test();
t.display();
```

A) 0  
B) 10  
C) null  
D) Error

---

### Question 26
What is the output?
```java
System.out.println(Math.max(5, 10));
```

A) 5  
B) 10  
C) 15  
D) 0

---

### Question 27
What is the output?
```java
int x = 10;
switch(x) {
    case 10: System.out.println("Ten");
    default: System.out.println("Default");
}
```

A) Ten  
B) Default  
C) Ten Default  
D) Error

---

### Question 28
What is the output?
```java
String s = "hello";
System.out.println(s.equals("HELLO"));
```

A) true  
B) false  
C) hello  
D) Error

---

### Question 29
What is the output?
```java
int[] arr = {5, 10, 15};
System.out.println(arr.length);
```

A) 2  
B) 3  
C) 15  
D) 5

---

### Question 30
What is the output?
```java
class Parent {
    void show() { System.out.println("Parent"); }
}
class Child extends Parent {
}
Child c = new Child();
c.show();
```

A) Parent  
B) Child  
C) Error  
D) Nothing

---

### Question 31
What is the output?
```java
System.out.println("Java".concat(" Programming"));
```

A) Java  
B) Programming  
C) Java Programming  
D) JavaProgramming

---

### Question 32
What is the output?
```java
int x = 5;
if(x > 10)
    System.out.println("A");
System.out.println("B");
```

A) A  
B) B  
C) A B  
D) Nothing

---

### Question 33
What is the output?
```java
double d = 10.5;
int x = (int) d;
System.out.println(x);
```

A) 10.5  
B) 10  
C) 11  
D) Error

---

### Question 34
What is the output?
```java
String s = "Hello";
System.out.println(s.replace('l', 'x'));
```

A) Hello  
B) Hexxo  
C) Hexlo  
D) Error

---

### Question 35
What is the output?
```java
for(int i = 0; i < 5; i++) {
    if(i == 2) break;
    System.out.print(i);
}
```

A) 01  
B) 012  
C) 01234  
D) 0

---

### Question 36
What is the output?
```java
Integer x = 10;
Integer y = 10;
System.out.println(x.equals(y));
```

A) true  
B) false  
C) 10  
D) Error

---

### Question 37
What is the output?
```java
String s = "   Hello   ";
System.out.println(s.trim());
```

A) "   Hello   "  
B) "Hello"  
C) Hello  
D) Error

---

### Question 38
What is the output?
```java
int x = 5, y = 10;
int temp = x;
x = y;
y = temp;
System.out.println(x + " " + y);
```

A) 5 10  
B) 10 5  
C) 10 10  
D) 5 5

---

### Question 39
What is the output?
```java
System.out.println(Integer.parseInt("100"));
```

A) "100"  
B) 100  
C) Error  
D) 1

---

### Question 40
What is the output?
```java
class Test {
    static int x = 5;
}
Test.x = 10;
System.out.println(Test.x);
```

A) 5  
B) 10  
C) Error  
D) 0

---

### Question 41
What is the output?
```java
String[] arr = {"A", "B", "C"};
System.out.println(arr[arr.length - 1]);
```

A) A  
B) B  
C) C  
D) 2

---

### Question 42
What is the output?
```java
int x = 0;
do {
    System.out.print(x);
    x++;
} while(x < 2);
```

A) 0  
B) 01  
C) 012  
D) 12

---

### Question 43
What is the output?
```java
System.out.println("Hello".startsWith("He"));
```

A) true  
B) false  
C) He  
D) Error

---

### Question 44
What is the output?
```java
class Test {
    int x;
    Test(int x) {
        this.x = x;
    }
}
Test t = new Test(5);
System.out.println(t.x);
```

A) 0  
B) 5  
C) null  
D) Error

---

### Question 45
What is the output?
```java
int x = 10;
System.out.println(x == 10);
```

A) true  
B) false  
C) 10  
D) 1

---

### Question 46
What is the output?
```java
char c = 'A';
System.out.println((int) c);
```

A) A  
B) 65  
C) 1  
D) Error

---

### Question 47
What is the output?
```java
String s = null;
System.out.println(s);
```

A) ""  
B) null  
C) Error  
D) NullPointerException

---

### Question 48
What is the output?
```java
for(int i = 0; i < 5; i++) {
    if(i == 2) continue;
    System.out.print(i);
}
```

A) 01234  
B) 0134  
C) 012  
D) 34

---

### Question 49
What is the output?
```java
System.out.println(10 > 5 || 3 > 5);
```

A) true  
B) false  
C) 10  
D) Error

---

### Question 50
What is the output?
```java
class A {
    int x = 5;
}
A a1 = new A();
A a2 = a1;
a2.x = 10;
System.out.println(a1.x);
```

A) 5  
B) 10  
C) Error  
D) 0

---

---

# 📝 Answer Key with Explanations

---

### Question 1
**Correct Answer: A) 5**

**Explanation:** Post-increment (x++) returns the original value first, then increments. So 5 is printed, then x becomes 6.

---

### Question 2
**Correct Answer: B) 5**

**Explanation:** The `length()` method returns the number of characters. "Hello" has 5 characters.

---

### Question 3
**Correct Answer: B) 2**

**Explanation:** Arrays are 0-indexed. arr[0]=1, arr[1]=2, arr[2]=3. So arr[1] is 2.

---

### Question 4
**Correct Answer: A) 3**

**Explanation:** Integer division truncates the decimal. 10/3 = 3.33, but as integers it's 3.

---

### Question 5
**Correct Answer: B) false**

**Explanation:** The AND operator (&&) returns true only if both operands are true. true && false = false.

---

### Question 6
**Correct Answer: A) Big**

**Explanation:** 10 > 5 is true, so the if block executes, printing "Big".

---

### Question 7
**Correct Answer: A) 0 1 2**

**Explanation:** Loop runs for i=0,1,2 (while i<3). Each iteration prints i and a space.

---

### Question 8
**Correct Answer: A) true**

**Explanation:** String literals are stored in String Pool. Both reference the same object, so == returns true.

---

### Question 9
**Correct Answer: C) 8**

**Explanation:** x += 3 is equivalent to x = x + 3. 5 + 3 = 8.

---

### Question 10
**Correct Answer: B) 105**

**Explanation:** When + involves a String, it concatenates. "10" + 5 = "105" (String concatenation).

---

### Question 11
**Correct Answer: A) true**

**Explanation:** 10 > 5 is true AND 10 < 15 is true. true && true = true.

---

### Question 12
**Correct Answer: A) J**

**Explanation:** charAt(0) returns the character at index 0, which is 'J'.

---

### Question 13
**Correct Answer: B) 0**

**Explanation:** Arrays of primitives are initialized to default values. For int, that's 0.

---

### Question 14
**Correct Answer: B) 1**

**Explanation:** Modulo operator gives remainder. 7 ÷ 3 = 2 remainder 1.

---

### Question 15
**Correct Answer: B) 10**

**Explanation:** Instance variable x is initialized to 10. Accessing obj.x gives 10.

---

### Question 16
**Correct Answer: B) HELLO**

**Explanation:** toUpperCase() returns a new string with all characters in uppercase.

---

### Question 17
**Correct Answer: A) A**

**Explanation:** Ternary operator: condition ? valueIfTrue : valueIfFalse. 10 > 5 is true, so "A".

---

### Question 18
**Correct Answer: B) 6**

**Explanation:** sum = 0 + 1 + 2 + 3 = 6. Loop adds 1, 2, 3 to sum.

---

### Question 19
**Correct Answer: B) 4**

**Explanation:** indexOf returns the first occurrence index. 'o' first appears at index 4 in "Hello World".

---

### Question 20
**Correct Answer: B) 6**

**Explanation:** Pre-increment (++x) increments first, then returns value. x becomes 6, then 6 is printed.

---

### Question 21
**Correct Answer: B) 8Hello**

**Explanation:** Left to right: 5+3=8 (arithmetic), then 8+"Hello"="8Hello" (concatenation).

---

### Question 22
**Correct Answer: B) false**

**Explanation:** 5 > 3 is true, !(true) = false.

---

### Question 23
**Correct Answer: B) av**

**Explanation:** substring(1, 3) extracts from index 1 to 2 (end exclusive). "Java"[1:3] = "av".

---

### Question 24
**Correct Answer: A) 012**

**Explanation:** Loop prints 0, 1, 2 without spaces. System.out.print doesn't add newline.

---

### Question 25
**Correct Answer: B) 10**

**Explanation:** display() method prints instance variable x, which is 10.

---

### Question 26
**Correct Answer: B) 10**

**Explanation:** Math.max() returns the larger of two numbers. 10 > 5.

---

### Question 27
**Correct Answer: C) Ten Default**

**Explanation:** Without break, switch "falls through" to subsequent cases. Both "Ten" and "Default" are printed.

---

### Question 28
**Correct Answer: B) false**

**Explanation:** equals() is case-sensitive. "hello" ≠ "HELLO". Use equalsIgnoreCase() for case-insensitive comparison.

---

### Question 29
**Correct Answer: B) 3**

**Explanation:** Array length property returns number of elements. Array has 3 elements.

---

### Question 30
**Correct Answer: A) Parent**

**Explanation:** Child inherits show() from Parent. Since Child doesn't override it, Parent's version is called.

---

### Question 31
**Correct Answer: C) Java Programming**

**Explanation:** concat() appends the argument to the string. "Java" + " Programming" = "Java Programming".

---

### Question 32
**Correct Answer: B) B**

**Explanation:** 5 > 10 is false, so the if block is skipped. Only "B" (outside if) is printed.

---

### Question 33
**Correct Answer: B) 10**

**Explanation:** Casting double to int truncates the decimal part. 10.5 becomes 10.

---

### Question 34
**Correct Answer: B) Hexxo**

**Explanation:** replace('l', 'x') replaces ALL occurrences of 'l' with 'x'. "Hello" → "Hexxo".

---

### Question 35
**Correct Answer: A) 01**

**Explanation:** Loop prints 0, 1. When i=2, break exits the loop before printing 2.

---

### Question 36
**Correct Answer: A) true**

**Explanation:** Integer.equals() compares values. Both have value 10, so they're equal.

---

### Question 37
**Correct Answer: C) Hello**

**Explanation:** trim() removes leading and trailing whitespace. Result is "Hello" (printed without quotes).

---

### Question 38
**Correct Answer: B) 10 5**

**Explanation:** Classic swap algorithm using temp variable. Values of x and y are swapped.

---

### Question 39
**Correct Answer: B) 100**

**Explanation:** parseInt converts String to int. "100" becomes integer 100.

---

### Question 40
**Correct Answer: B) 10**

**Explanation:** Static variable x is changed to 10. When accessed, it shows 10.

---

### Question 41
**Correct Answer: C) C**

**Explanation:** arr.length is 3, so arr[3-1] = arr[2] = "C" (last element).

---

### Question 42
**Correct Answer: B) 01**

**Explanation:** do-while executes body first. Prints 0, x=1, prints 1, x=2, condition 2<2 is false, exits.

---

### Question 43
**Correct Answer: A) true**

**Explanation:** startsWith() checks if string begins with specified prefix. "Hello" starts with "He".

---

### Question 44
**Correct Answer: B) 5**

**Explanation:** Constructor sets this.x = 5. The instance variable x is 5.

---

### Question 45
**Correct Answer: A) true**

**Explanation:** == compares values for primitives. 10 == 10 is true.

---

### Question 46
**Correct Answer: B) 65**

**Explanation:** Casting char to int gives ASCII/Unicode value. 'A' = 65.

---

### Question 47
**Correct Answer: B) null**

**Explanation:** println() can print null without throwing exception. It just prints "null".

---

### Question 48
**Correct Answer: B) 0134**

**Explanation:** continue skips the current iteration. When i=2, print is skipped, but loop continues.

---

### Question 49
**Correct Answer: A) true**

**Explanation:** OR (||) returns true if at least one is true. 10 > 5 is true, so result is true.

---

### Question 50
**Correct Answer: B) 10**

**Explanation:** a1 and a2 reference the same object. Changing a2.x also changes a1.x (same memory).

---

## 📊 Score Guide

| Score | Level | Next Step |
|-------|-------|-----------|
| 45-50 | Excellent! | Move to Set 3 |
| 35-44 | Good | Review mistakes, then Set 3 |
| 25-34 | Average | Practice more basic code |
| 0-24 | Needs Work | Review Set 1 concepts |

---

**Difficulty: ⭐⭐ EASY-MODERATE** | **Next: Set 3 (⭐⭐⭐ Moderate)**
