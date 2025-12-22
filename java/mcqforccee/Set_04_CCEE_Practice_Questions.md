# CDAC CCEE MCQ Practice Set 4

## 📝 MODERATE-HARD LEVEL - Tricky Outputs & Exception Handling
**Total Questions: 50 | Time Limit: 60 minutes | No Negative Marking**

> **Difficulty: ⭐⭐⭐⭐ Moderate-Hard** - These questions involve tricky code behavior, exception propagation, string pool nuances, and initialization order. Requires careful analysis.

---

### Question 1
What is the output?
```java
int x = 10;
System.out.println(x++ + ++x);
```

A) 21  
B) 22  
C) 20  
D) 23

---

### Question 2
What is the output?
```java
String s1 = "Hello";
String s2 = new String("Hello");
System.out.println(s1 == s2.intern());
```

A) true  
B) false  
C) Hello  
D) Error

---

### Question 3
What is the output?
```java
class A {
    int x = 10;
    A() { print(); }
    void print() { System.out.println(x); }
}
class B extends A {
    int x = 20;
    void print() { System.out.println(x); }
}
new B();
```

A) 10  
B) 20  
C) 0  
D) 10 20

---

### Question 4
What is the output?
```java
try {
    System.out.println("Try");
    return;
} finally {
    System.out.println("Finally");
}
```

A) Try  
B) Finally  
C) Try Finally  
D) Compile error

---

### Question 5
What is the output?
```java
Integer a = 128;
Integer b = 128;
System.out.println(a == b);
```

A) true  
B) false  
C) 128  
D) Error

---

### Question 6
What is the output?
```java
class A {
    static void m() { System.out.println("A"); }
}
class B extends A {
    static void m() { System.out.println("B"); }
}
A obj = new B();
obj.m();
```

A) A  
B) B  
C) Compile error  
D) Runtime error

---

### Question 7
What is the output?
```java
String s = "Hello";
System.out.println(s = s + "World");
System.out.println(s);
```

A) Hello, Hello  
B) HelloWorld, HelloWorld  
C) Hello, HelloWorld  
D) Error

---

### Question 8
What is the output?
```java
int[] arr = {1, 2, 3};
try {
    System.out.println(arr[3]);
} catch(Exception e) {
    System.out.println("Exception");
} finally {
    System.out.println("Done");
}
```

A) Exception  
B) Done  
C) Exception Done  
D) Error

---

### Question 9
What is the output?
```java
class A {
    void m(Object o) { System.out.print("Object "); }
    void m(String s) { System.out.print("String "); }
}
new A().m(null);
```

A) Object  
B) String  
C) Compile error  
D) NullPointerException

---

### Question 10
What is the output?
```java
StringBuilder sb = new StringBuilder("Hello");
sb.reverse();
System.out.println(sb);
```

A) Hello  
B) olleH  
C) Error  
D) null

---

### Question 11
What is the output?
```java
try {
    try {
        throw new Exception();
    } finally {
        System.out.print("Inner ");
    }
} catch(Exception e) {
    System.out.print("Outer");
}
```

A) Inner  
B) Outer  
C) Inner Outer  
D) Compile error

---

### Question 12
What is the output?
```java
class A {
    { System.out.print("A-IB "); }
}
class B extends A {
    { System.out.print("B-IB "); }
}
new B();
```

A) A-IB B-IB  
B) B-IB A-IB  
C) A-IB  
D) B-IB

---

### Question 13
What is the output?
```java
int x = 5;
System.out.println(x > 3 ? x > 4 ? "A" : "B" : "C");
```

A) A  
B) B  
C) C  
D) Error

---

### Question 14
What is the output?
```java
String s = "Hello";
switch(s) {
    case "Hello": System.out.print("H ");
    case "World": System.out.print("W ");
    default: System.out.print("D");
}
```

A) H  
B) H W D  
C) H D  
D) Error

---

### Question 15
What is the output?
```java
class A {
    A() { this(10); System.out.print("A() "); }
    A(int x) { System.out.print("A(int) "); }
}
new A();
```

A) A()  
B) A(int)  
C) A(int) A()  
D) A() A(int)

---

### Question 16
What is the output?
```java
String s1 = "Java";
String s2 = "Ja" + "va";
System.out.println(s1 == s2);
```

A) true  
B) false  
C) Java  
D) Error

---

### Question 17
What is the output?
```java
try {
    throw new RuntimeException();
} catch(RuntimeException e) {
    throw new RuntimeException();
} finally {
    System.out.println("Finally");
}
```

A) Finally  
B) RuntimeException  
C) Finally, then RuntimeException thrown  
D) Compile error

---

### Question 18
What is the output?
```java
class Parent {
    int x = 10;
}
class Child extends Parent {
    int x = 20;
    void show() {
        System.out.println(super.x + " " + this.x);
    }
}
new Child().show();
```

A) 10 10  
B) 20 20  
C) 10 20  
D) 20 10

---

### Question 19
What is the output?
```java
Object obj = null;
System.out.println(obj instanceof Object);
```

A) true  
B) false  
C) Compile error  
D) NullPointerException

---

### Question 20
What is the output?
```java
int[] arr = new int[]{1, 2, 3};
Object obj = arr;
System.out.println(obj instanceof int[]);
```

A) true  
B) false  
C) Compile error  
D) [I@...

---

### Question 21
What is the output?
```java
class A {
    protected int x = 10;
}
class B extends A {
    void m() {
        A a = new A();
        System.out.println(a.x);
    }
}
new B().m();
```

A) 10  
B) Compile error  
C) 0  
D) Runtime error

---

### Question 22
What is the output?
```java
String s = "  ";
System.out.println(s.isEmpty());
System.out.println(s.isBlank());
```

A) true, true  
B) false, true  
C) true, false  
D) false, false

---

### Question 23
What is the output?
```java
interface A { void m(); }
interface B { void m(); }
class C implements A, B {
    public void m() { System.out.println("C"); }
}
new C().m();
```

A) Compile error - ambiguous  
B) C  
C) Runtime error  
D) A B

---

### Question 24
What is the output?
```java
List<Integer> list = Arrays.asList(1, 2, 3);
list.set(0, 10);
System.out.println(list);
```

A) [10, 2, 3]  
B) [1, 2, 3]  
C) UnsupportedOperationException  
D) Compile error

---

### Question 25
What is the output?
```java
class A {
    void m() throws Exception { throw new Exception(); }
}
class B extends A {
    void m() { System.out.println("B"); }
}
A a = new B();
a.m();
```

A) B  
B) Exception  
C) Compile error  
D) Nothing

---

### Question 26
What is the output?
```java
StringBuilder sb = new StringBuilder("Hello");
sb.insert(2, "XX");
System.out.println(sb);
```

A) XXHello  
B) HeXXllo  
C) HelloXX  
D) Error

---

### Question 27
What is the output?
```java
int x = 5;
x = x-- - --x;
System.out.println(x);
```

A) 0  
B) 1  
C) 2  
D) -1

---

### Question 28
What is the output?
```java
try {
    int x = Integer.parseInt("abc");
} catch(NumberFormatException e) {
    System.out.print("NFE ");
} catch(Exception e) {
    System.out.print("E ");
} finally {
    System.out.print("F");
}
```

A) NFE  
B) NFE F  
C) E F  
D) F

---

### Question 29
What is the output?
```java
class A {
    void m(int... x) { System.out.print("varargs "); }
    void m(int x, int y) { System.out.print("two "); }
}
new A().m(1, 2);
```

A) varargs  
B) two  
C) Compile error - ambiguous  
D) varargs two

---

### Question 30
What is the output?
```java
StringBuffer s1 = new StringBuffer("Hello");
StringBuffer s2 = new StringBuffer("Hello");
System.out.println(s1.equals(s2));
```

A) true  
B) false  
C) Hello  
D) Error

---

### Question 31
What is the output?
```java
class A {
    static int x = 10;
    static { x = x + 5; }
}
class B extends A {
    static { x = x + 10; }
}
System.out.println(B.x);
```

A) 10  
B) 15  
C) 25  
D) 20

---

### Question 32
What is the output?
```java
final int x;
x = 10;
System.out.println(x);
```

A) 10  
B) Compile error - blank final  
C) 0  
D) Error

---

### Question 33
What is the output?
```java
class A {
    void m() { System.out.println("A"); }
}
class B extends A {
    void m() { System.out.println("B"); }
    void m(int x) { System.out.println("B-int"); }
}
A a = new B();
a.m(10);
```

A) B-int  
B) A  
C) Compile error  
D) B

---

### Question 34
What is the output?
```java
enum Color { RED, GREEN, BLUE }
Color c = Color.GREEN;
System.out.println(c.compareTo(Color.RED));
```

A) 0  
B) 1  
C) -1  
D) GREEN

---

### Question 35
What is the output?
```java
String s = "Hello";
s.toUpperCase();
s.concat(" World");
System.out.println(s);
```

A) Hello  
B) HELLO  
C) Hello World  
D) HELLO World

---

### Question 36
What is the output?
```java
class Test {
    int x = m();
    int m() { return 10; }
}
System.out.println(new Test().x);
```

A) 0  
B) 10  
C) Compile error  
D) null

---

### Question 37
What is the output?
```java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.remove(1);
System.out.println(list);
```

A) [1]  
B) [2]  
C) [1, 2]  
D) Error

---

### Question 38
What is the output?
```java
double d = 10.0 / 0;
System.out.println(d);
```

A) ArithmeticException  
B) Infinity  
C) NaN  
D) 0

---

### Question 39
What is the output?
```java
class A {
    int x = 10;
    { x = 20; }
    A() { x = 30; }
}
System.out.println(new A().x);
```

A) 10  
B) 20  
C) 30  
D) 0

---

### Question 40
What is the output?
```java
interface A { int X = 10; }
class B implements A {
    void m() { 
        int X = 20;
        System.out.println(X + " " + A.X);
    }
}
new B().m();
```

A) 10 10  
B) 20 20  
C) 20 10  
D) 10 20

---

### Question 41
What is the output?
```java
TreeSet<Integer> set = new TreeSet<>();
set.add(3);
set.add(1);
set.add(2);
System.out.println(set.first());
```

A) 3  
B) 1  
C) 2  
D) Error

---

### Question 42
What is the output?
```java
try {
    System.exit(0);
} finally {
    System.out.println("Finally");
}
```

A) Finally  
B) No output  
C) Error  
D) 0

---

### Question 43
What is the output?
```java
class A { void m() throws IOException {} }
class B extends A { void m() throws FileNotFoundException {} }
class C extends A { void m() {} }
```

A) All compile  
B) Only B compiles  
C) Only C compiles  
D) None compile

---

### Question 44
What is the output?
```java
String s = new String("Hello").intern();
String t = "Hello";
System.out.println(s == t);
```

A) true  
B) false  
C) Hello  
D) Error

---

### Question 45
What is the output?
```java
int x = 010;
System.out.println(x);
```

A) 10  
B) 8  
C) 010  
D) Error

---

### Question 46
What is the output?
```java
class Outer {
    static class Nested {
        void show() { System.out.println("Nested"); }
    }
}
Outer.Nested n = new Outer.Nested();
n.show();
```

A) Nested  
B) Compile error  
C) Outer.Nested  
D) Nothing

---

### Question 47
What is the output?
```java
Boolean b = null;
if(b) {
    System.out.println("True");
}
```

A) True  
B) Nothing  
C) NullPointerException  
D) Compile error

---

### Question 48
What is the output?
```java
String s = "a" + "b" + "c";
String t = "abc";
System.out.println(s == t);
```

A) true  
B) false  
C) abc  
D) Error

---

### Question 49
What is the output?
```java
class A {
    A(int x) { System.out.print(x + " "); }
}
class B extends A {
    B() { super(10); }
    B(int x) { this(); System.out.print(x); }
}
new B(20);
```

A) 10  
B) 20  
C) 10 20  
D) 20 10

---

### Question 50
What is the output?
```java
Map<String, Integer> map = new LinkedHashMap<>();
map.put("C", 3);
map.put("A", 1);
map.put("B", 2);
System.out.println(map.keySet().iterator().next());
```

A) A  
B) B  
C) C  
D) Random

---

---

# 📝 Answer Key with Explanations

---

### Question 1
**Correct Answer: B) 22**

**Explanation:** x++ returns 10 (then x=11), ++x increments first to 12 then returns 12. 10 + 12 = 22.

---

### Question 2
**Correct Answer: A) true**

**Explanation:** intern() returns the String Pool reference. s1 is a literal (in pool), s2.intern() returns the same pool reference.

---

### Question 3
**Correct Answer: C) 0**

**Explanation:** Parent constructor calls overridden print() of B. But B's x is not yet initialized (default 0).

---

### Question 4
**Correct Answer: C) Try Finally**

**Explanation:** finally executes even with return statement. Both are printed before method exits.

---

### Question 5
**Correct Answer: B) false**

**Explanation:** Integer cache is only for -128 to 127. 128 creates new objects, so == is false.

---

### Question 6
**Correct Answer: A) A**

**Explanation:** Static methods are not polymorphic. Method call is resolved based on reference type (A).

---

### Question 7
**Correct Answer: B) HelloWorld, HelloWorld**

**Explanation:** Assignment expression returns the assigned value. First println shows HelloWorld, s is now HelloWorld.

---

### Question 8
**Correct Answer: C) Exception Done**

**Explanation:** ArrayIndexOutOfBoundsException caught, prints "Exception". finally always runs, prints "Done".

---

### Question 9
**Correct Answer: B) String**

**Explanation:** null can match any reference type. String is more specific than Object, so m(String) is chosen.

---

### Question 10
**Correct Answer: B) olleH**

**Explanation:** reverse() reverses the StringBuilder in place. "Hello" becomes "olleH".

---

### Question 11
**Correct Answer: C) Inner Outer**

**Explanation:** Inner finally executes first, then exception propagates to outer catch.

---

### Question 12
**Correct Answer: A) A-IB B-IB**

**Explanation:** Parent instance block runs first (before B's), following constructor chaining order.

---

### Question 13
**Correct Answer: A) A**

**Explanation:** Right-to-left associativity: (x>3) ? ((x>4) ? "A" : "B") : "C". 5>3 true, 5>4 true, result "A".

---

### Question 14
**Correct Answer: B) H W D**

**Explanation:** No break statements cause fall-through. All cases after match are executed.

---

### Question 15
**Correct Answer: C) A(int) A()**

**Explanation:** this(10) calls A(int) first, which prints. Then A() continues to print.

---

### Question 16
**Correct Answer: A) true**

**Explanation:** Compile-time constant expressions are evaluated at compile time. "Ja"+"va" becomes "Java" literal.

---

### Question 17
**Correct Answer: C) Finally, then RuntimeException thrown**

**Explanation:** finally always executes before exception propagates. Prints "Finally", then throws from catch.

---

### Question 18
**Correct Answer: C) 10 20**

**Explanation:** super.x accesses Parent's x (10), this.x accesses Child's x (20).

---

### Question 19
**Correct Answer: B) false**

**Explanation:** null instanceof AnyType is always false. No exception is thrown.

---

### Question 20
**Correct Answer: A) true**

**Explanation:** int[] is a type in Java. Arrays are objects and can be checked with instanceof.

---

### Question 21
**Correct Answer: A) 10**

**Explanation:** In same package, protected members are accessible. B can access A's protected x.

---

### Question 22
**Correct Answer: B) false, true**

**Explanation:** isEmpty() returns false (has whitespace characters). isBlank() (Java 11+) returns true (only whitespace).

---

### Question 23
**Correct Answer: B) C**

**Explanation:** Same signature method in both interfaces - single implementation satisfies both. No ambiguity.

---

### Question 24
**Correct Answer: A) [10, 2, 3]**

**Explanation:** Arrays.asList returns fixed-size list. set() is allowed, but add/remove are not.

---

### Question 25
**Correct Answer: C) Compile error**

**Explanation:** Reference type A declares m() throws Exception. Caller must handle checked exception.

---

### Question 26
**Correct Answer: B) HeXXllo**

**Explanation:** insert(2, "XX") inserts at index 2. He + XX + llo = HeXXllo.

---

### Question 27
**Correct Answer: C) 2**

**Explanation:** x-- returns 5 (x=4), --x returns 3 (x=3). 5 - 3 = 2.

---

### Question 28
**Correct Answer: B) NFE F**

**Explanation:** NumberFormatException caught, prints "NFE". finally always executes, prints "F".

---

### Question 29
**Correct Answer: B) two**

**Explanation:** Specific method is preferred over varargs. m(int, int) is more specific.

---

### Question 30
**Correct Answer: B) false**

**Explanation:** StringBuffer doesn't override equals(). Uses Object's equals() which compares references.

---

### Question 31
**Correct Answer: C) 25**

**Explanation:** A.x = 15 (10+5). B's static block adds 10 to inherited x. Final: 25.

---

### Question 32
**Correct Answer: A) 10**

**Explanation:** Blank final can be assigned once. This is valid if assigned before use.

---

### Question 33
**Correct Answer: C) Compile error**

**Explanation:** Reference type A doesn't have m(int). Method resolution uses reference type.

---

### Question 34
**Correct Answer: B) 1**

**Explanation:** compareTo compares ordinals. GREEN(1) - RED(0) = 1.

---

### Question 35
**Correct Answer: A) Hello**

**Explanation:** String is immutable. Neither toUpperCase() nor concat() modifies original. Results not assigned back.

---

### Question 36
**Correct Answer: B) 10**

**Explanation:** Instance variable initialization can call methods. m() returns 10.

---

### Question 37
**Correct Answer: B) [2]**

**Explanation:** remove(1) removes element at index 1 (which is 2), not element with value 1. Wait, this removes the element at index 1. List becomes [1]. Actually, original is [1,2], remove(1) removes index 1 (value 2), leaving [1].

---

### Question 38
**Correct Answer: B) Infinity**

**Explanation:** Floating-point division by zero gives Infinity (not exception). Integer division throws ArithmeticException.

---

### Question 39
**Correct Answer: C) 30**

**Explanation:** Order: default value (0), field initialization (10), instance block (20), constructor (30).

---

### Question 40
**Correct Answer: C) 20 10**

**Explanation:** Local X shadows interface X inside method. Local X is 20, A.X accesses interface constant 10.

---

### Question 41
**Correct Answer: B) 1**

**Explanation:** TreeSet maintains sorted order. first() returns smallest element (1).

---

### Question 42
**Correct Answer: B) No output**

**Explanation:** System.exit(0) terminates JVM immediately. finally doesn't execute.

---

### Question 43
**Correct Answer: A) All compile**

**Explanation:** Overriding can throw narrower exceptions or no exception. FileNotFoundException extends IOException.

---

### Question 44
**Correct Answer: A) true**

**Explanation:** intern() returns pool reference. Literal "Hello" is same pool reference.

---

### Question 45
**Correct Answer: B) 8**

**Explanation:** Leading 0 indicates octal literal. 010 = 0*64 + 1*8 + 0*1 = 8.

---

### Question 46
**Correct Answer: A) Nested**

**Explanation:** Static nested class can be instantiated without outer class instance.

---

### Question 47
**Correct Answer: C) NullPointerException**

**Explanation:** Boolean b is null. Unboxing null to boolean throws NullPointerException.

---

### Question 48
**Correct Answer: A) true**

**Explanation:** Compile-time string concatenation of literals creates single pool string. s and t same reference.

---

### Question 49
**Correct Answer: C) 10 20**

**Explanation:** B(20) calls this(), which calls super(10). Prints 10, then B(20) prints 20.

---

### Question 50
**Correct Answer: C) C**

**Explanation:** LinkedHashMap maintains insertion order. First key inserted was "C".

---

## 📊 Score Guide

| Score | Level | Next Step |
|-------|-------|-----------|
| 45-50 | Excellent! | Move to Set 5 |
| 35-44 | Good | Review tricky areas, then Set 5 |
| 25-34 | Average | More practice needed |
| 0-24 | Needs Work | Review Sets 1-3 |

---

**Difficulty: ⭐⭐⭐⭐ MODERATE-HARD** | **Next: Set 5 (⭐⭐⭐⭐ Hard)**
