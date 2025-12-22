# CDAC CCEE MCQ Practice Set 9

## 📝 MASTER LEVEL - Brain Teasers & Deep Conceptual Questions
**Total Questions: 50 | Time Limit: 60 minutes | No Negative Marking**

> **Difficulty: 🔥🔥 Master** - These questions are designed to test your deepest understanding of Java. They combine multiple concepts, require careful reasoning, and often have counter-intuitive answers.

---

### Question 1
What is the output?
```java
class A {
    int x = 1;
    A() {
        this.x = 2;
        x = 3;
        print();
    }
    void print() { System.out.println(x); }
}
class B extends A {
    int x = 4;
    void print() { System.out.println(x); }
}
new B().print();
```

A) 3 4  
B) 0 4  
C) 3 3  
D) 4 4

---

### Question 2
What is the output?
```java
class A {
    A() { m(); }
    void m() { System.out.print("A "); }
}
class B extends A {
    int x;
    B() { x = 10; }
    void m() { System.out.print(x + " "); }
}
B b = new B();
b.m();
```

A) A 10  
B) 0 10  
C) 10 10  
D) A A

---

### Question 3
What is the output?
```java
Integer i1 = new Integer(1);
Integer i2 = new Integer(1);
Integer i3 = Integer.valueOf(1);
Integer i4 = Integer.valueOf(1);
System.out.println((i1 == i2) + " " + (i3 == i4));
```

A) true true  
B) false true  
C) true false  
D) false false

---

### Question 4
What is the output?
```java
try {
    return 1;
} finally {
    return 2;
}
```

A) 1  
B) 2  
C) Compile error  
D) 1 then 2

---

### Question 5
What is the output?
```java
class A {
    static int x = m();
    static { System.out.print("static "); }
    static int m() { System.out.print("method "); return 10; }
}
System.out.println(A.x);
```

A) static method 10  
B) method static 10  
C) 10 method static  
D) method 10 static

---

### Question 6
What is the output?
```java
System.out.println(1.0 / 0.0);
System.out.println(0.0 / 0.0);
```

A) ArithmeticException  
B) Infinity, NaN  
C) Infinity, Infinity  
D) Error, Error

---

### Question 7
What is the output?
```java
String s = "Hello";
System.out.println(s.substring(5));
```

A) ""  
B) Error  
C) Hello  
D) null

---

### Question 8
What is the output?
```java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);
list.remove(1);
list.remove(Integer.valueOf(1));
System.out.println(list);
```

A) [3]  
B) [2, 3]  
C) [1, 3]  
D) []

---

### Question 9
What is the output?
```java
int[] a = {1, 2, 3};
int[] b = {1, 2, 3};
System.out.println(a.equals(b));
System.out.println(Arrays.equals(a, b));
```

A) true true  
B) false true  
C) true false  
D) false false

---

### Question 10
What is the output?
```java
class A {
    public void m() throws IOException { }
}
class B extends A {
    public void m() throws Exception { }
}
```

A) Compiles fine  
B) Compile error - B throws broader exception  
C) Runtime error  
D) Warning

---

### Question 11
What is the output?
```java
interface A {
    int x = 10;
}
class B implements A {
    public B() { x = 20; }
}
```

A) B.x = 20  
B) Compile error - cannot assign to final  
C) Works at runtime  
D) Warning

---

### Question 12
What is the output?
```java
String a = "abc";
String b = "abc";
String c = "ab" + "c";
String d = "ab";
d += "c";
System.out.println((a == b) + " " + (a == c) + " " + (a == d));
```

A) true true true  
B) true true false  
C) true false false  
D) false false false

---

### Question 13
What is the output?
```java
class A {
    private int x = getX();
    private int getX() { return 10; }
    public int getY() { return x; }
}
class B extends A {
    private int getX() { return 20; }
}
System.out.println(new B().getY());
```

A) 10  
B) 20  
C) 0  
D) Error

---

### Question 14
What is the output?
```java
synchronized(null) {
    System.out.println("Inside");
}
```

A) Inside  
B) NullPointerException  
C) Compile error  
D) Nothing

---

### Question 15
What is the output?
```java
enum E {
    A { void m() { System.out.println("A"); } },
    B { void m() { System.out.println("B"); } };
    abstract void m();
}
E.A.m();
```

A) A  
B) B  
C) Compile error  
D) E.A

---

### Question 16
What is the output?
```java
HashSet<ArrayList<Integer>> set = new HashSet<>();
ArrayList<Integer> list = new ArrayList<>();
set.add(list);
list.add(1);
System.out.println(set.contains(list));
```

A) true  
B) false  
C) Exception  
D) 1

---

### Question 17
What is the output?
```java
Short s1 = 1;
Short s2 = 1;
Short s3 = new Short((short) 1);
System.out.println((s1 == s2) + " " + s1.equals(s2) + " " + (s1 == s3));
```

A) true true true  
B) true true false  
C) false true false  
D) true false false

---

### Question 18
What is the output?
```java
try {
    throw null;
} catch(NullPointerException e) {
    System.out.println("NPE");
}
```

A) NPE  
B) Compile error - cannot throw null  
C) Nothing  
D) Different exception

---

### Question 19
What is the output?
```java
class A {
    void m(Integer i) { System.out.println("Integer"); }
    void m(int... i) { System.out.println("Varargs"); }
}
new A().m(1, 2);
```

A) Integer  
B) Varargs  
C) Compile error  
D) Integer Varargs

---

### Question 20
What is the output?
```java
List<String> list = null;
Optional.ofNullable(list)
    .ifPresentOrElse(
        l -> System.out.println(l.size()),
        () -> System.out.println("Empty")
    );
```

A) 0  
B) Empty  
C) NullPointerException  
D) Error

---

### Question 21
What is the output?
```java
Stream.of("a", "b", "c")
    .map(s -> { System.out.print(s); return s.toUpperCase(); })
    .filter(s -> s.equals("B"))
    .findFirst();
```

A) abc  
B) ab  
C) a  
D) AB

---

### Question 22
What is the output?
```java
class A {
    int x = 10;
}
class B extends A {
    int y = x + 5;
}
System.out.println(new B().y);
```

A) 15  
B) 5  
C) Error  
D) 0

---

### Question 23
What is the output?
```java
Long l1 = 127L;
Long l2 = 127L;
Long l3 = 128L;
Long l4 = 128L;
System.out.println((l1 == l2) + " " + (l3 == l4));
```

A) true true  
B) true false  
C) false true  
D) false false

---

### Question 24
What is the output?
```java
class A {
    static int x = B.y;
}
class B {
    static int y = A.x + 1;
}
System.out.println(A.x + " " + B.y);
```

A) 0 1  
B) 1 0  
C) 1 1  
D) Circular dependency error

---

### Question 25
What is the output?
```java
interface A { void m(); }
interface B { void m(); }
class C implements A, B {
    public void m() { System.out.println("C"); }
}
A a = new C();
B b = (B) a;
b.m();
```

A) C  
B) Compile error  
C) ClassCastException  
D) A

---

### Question 26
What is the output?
```java
Map<String, Integer> map = new TreeMap<>(String.CASE_INSENSITIVE_ORDER);
map.put("a", 1);
map.put("A", 2);
map.put("B", 3);
System.out.println(map.size() + " " + map.get("a"));
```

A) 3 1  
B) 2 2  
C) 2 1  
D) 3 2

---

### Question 27
What is the output?
```java
String s = "\u0048\u0065\u006C\u006C\u006F";
System.out.println(s);
```

A) \u0048\u0065\u006C\u006C\u006F  
B) Hello  
C) Error  
D) 5 characters

---

### Question 28
What is the output?
```java
class A {
    static class B { }
}
A.B b = new A.B();
System.out.println(b.getClass().getSimpleName());
```

A) B  
B) A.B  
C) A$B  
D) Error

---

### Question 29
What is the output?
```java
class A {
    void m() { System.out.println("A"); }
}
class B extends A {
    void m() { System.out.println("B"); }
}
class C extends B {
    void m() { super.super.m(); }
}
```

A) A  
B) B  
C) Compile error  
D) C

---

### Question 30
What is the output?
```java
Object o = true ? new Integer(1) : new Double(2.0);
System.out.println(o);
```

A) 1  
B) 1.0  
C) Integer  
D) Error

---

### Question 31
What is the output?
```java
int x = 1, y = 2;
x ^= y ^= x ^= y;
System.out.println(x + " " + y);
```

A) 2 1  
B) 0 1  
C) 2 0  
D) Undefined

---

### Question 32
What is the output?
```java
class A {
    void m(int x) { System.out.println("int " + x); }
}
class B extends A {
    void m(Integer x) { System.out.println("Integer " + x); }
}
A a = new B();
a.m(10);
```

A) int 10  
B) Integer 10  
C) Compile error  
D) int 10 Integer 10

---

### Question 33
What is the output?
```java
class A {
    void m(Object o) { System.out.println("Object"); }
}
class B extends A {
    void m(String s) { System.out.println("String"); }
}
B b = new B();
b.m(null);
```

A) Object  
B) String  
C) Compile error - ambiguous  
D) NullPointer

---

### Question 34
What is the output?
```java
String s1 = "a";
String s2 = s1;
s1 += "b";
System.out.println(s1 == s2);
```

A) true  
B) false  
C) Error  
D) ab

---

### Question 35
What is the output?
```java
class Outer {
    int x = 10;
    void m() {
        int y = 20;
        y++;
        new Object() {
            void show() { System.out.println(y); }
        }.show();
    }
}
new Outer().m();
```

A) 21  
B) 20  
C) Compile error - y not effectively final  
D) 10

---

### Question 36
What is the output?
```java
Set<Integer> set = new LinkedHashSet<>();
set.add(3); set.add(1); set.add(2);
System.out.println(new TreeSet<>(set).first());
System.out.println(new ArrayList<>(set).get(0));
```

A) 1, 1  
B) 1, 3  
C) 3, 1  
D) 3, 3

---

### Question 37
What is the output?
```java
Pattern p = Pattern.compile("a+");
String[] result = p.split("aababaaa");
System.out.println(Arrays.toString(result));
```

A) [, b, b, ]  
B) [, b, b]  
C) [b, b]  
D) [a, a, a, a]

---

### Question 38
What is the output?
```java
class A {
    private void m() { System.out.println("A"); }
}
class B extends A {
    void m() { System.out.println("B"); }
}
A a = new B();
a.m();
```

A) A  
B) B  
C) Compile error  
D) Nothing

---

### Question 39
What is the output?
```java
class A {
    int x = 1;
    A() { x = 2; }
    { x = 3; }
}
System.out.println(new A().x);
```

A) 1  
B) 2  
C) 3  
D) 0

---

### Question 40
What is the output?
```java
interface A {
    default void m() { System.out.println("A"); }
}
interface B {
    default void m() { System.out.println("B"); }
}
interface C extends A, B {
    default void m() { B.super.m(); }
}
class D implements C { }
new D().m();
```

A) A  
B) B  
C) Compile error  
D) A B

---

### Question 41
What is the output?
```java
Map<String, String> map = Map.of("a", "1", "b", "2");
map.forEach((k, v) -> System.out.print(k + v));
```

A) a1b2  
B) b2a1  
C) Either a1b2 or b2a1  
D) Error

---

### Question 42
What is the output?
```java
abstract class A {
    abstract void m();
    static void n() { System.out.println("static"); }
}
A.n();
```

A) static  
B) Compile error  
C) AbstractMethodError  
D) Nothing

---

### Question 43
What is the output?
```java
int[] arr = {};
for(int i : arr) {
    System.out.println("Inside");
}
System.out.println("Done");
```

A) Inside Done  
B) Done  
C) Error - empty array  
D) Nothing

---

### Question 44
What is the output?
```java
System.out.println("java".toUpperCase(Locale.ENGLISH));
System.out.println("java".toUpperCase(new Locale("tr")));
```

A) JAVA, JAVA  
B) JAVA, JAVA (Turkish I without dot)  
C) Both same  
D) Error

---

### Question 45
What is the output?
```java
class MyException extends Exception { }
public void m() throws MyException {
    throw new MyException() { };
}
```
Is anonymous exception class valid?

A) Yes, compiles and runs  
B) No, compile error  
C) Runtime error  
D) MyException

---

### Question 46
What is the output?
```java
class A {
    static int x = 10;
    static { x++; }
    static { x++; }
}
System.out.println(A.x);
```

A) 10  
B) 11  
C) 12  
D) Error

---

### Question 47
What is the output?
```java
class A<T> {
    T value;
    A(T value) { this.value = value; }
    T get() { return value; }
}
A<String> a = new A<>("Hello");
Object o = a;
A<Integer> b = (A<Integer>) o;
System.out.println(b.get());
```

A) Hello  
B) ClassCastException  
C) Compile error  
D) null

---

### Question 48
What is the output?
```java
String s = switch(2) {
    case 1: yield "One";
    case 2: yield "Two";
    default: yield "Other";
};
System.out.println(s);
```

A) Two  
B) Compile error  
C) Other  
D) 2

---

### Question 49
What is the output?
```java
record Point(int x, int y) {
    public Point {
        if(x < 0) x = 0;
        if(y < 0) y = 0;
    }
}
Point p = new Point(-1, -2);
System.out.println(p.x() + " " + p.y());
```

A) -1 -2  
B) 0 0  
C) Compile error  
D) Error

---

### Question 50
What is the output?
```java
var x = new Object() {
    int value = 42;
}.value;
System.out.println(x);
```

A) 42  
B) Compile error  
C) null  
D) Object

---

---

# 📝 Answer Key with Explanations

---

### Question 1
**Correct Answer: B) 0 4**

**Explanation:** A's constructor calls overridden print(). B's x not initialized (0). After construction, B's x = 4.

---

### Question 2
**Correct Answer: B) 0 10**

**Explanation:** A() calls overridden m(). B's x = 0 (not yet 10). After super(), x=10, m() prints 10.

---

### Question 3
**Correct Answer: B) false true**

**Explanation:** new Integer creates new objects (false). valueOf uses cache for -128 to 127 (true).

---

### Question 4
**Correct Answer: B) 2**

**Explanation:** Finally's return overrides try's return. Returns 2.

---

### Question 5
**Correct Answer: B) method static 10**

**Explanation:** Static field init before static block. m() called first, then static block.

---

### Question 6
**Correct Answer: B) Infinity, NaN**

**Explanation:** Float division by zero = Infinity. 0.0/0.0 = NaN (indeterminate).

---

### Question 7
**Correct Answer: A) ""**

**Explanation:** substring(5) from length-5 string returns empty string "".

---

### Question 8
**Correct Answer: A) [3]**

**Explanation:** remove(1) removes index 1→[1,3]. remove(Integer.valueOf(1)) removes value 1→[3].

---

### Question 9
**Correct Answer: B) false true**

**Explanation:** Array equals uses Object.equals (reference). Arrays.equals compares content.

---

### Question 10
**Correct Answer: B) Compile error - B throws broader exception**

**Explanation:** Override cannot throw broader checked exception.

---

### Question 11
**Correct Answer: B) Compile error - cannot assign to final**

**Explanation:** Interface variables are implicitly final.

---

### Question 12
**Correct Answer: B) true true false**

**Explanation:** a, b, c are compile-time constants (same pool). d is runtime concat (new object).

---

### Question 13
**Correct Answer: A) 10**

**Explanation:** Private methods are not overridden. A.getX() (10) is called.

---

### Question 14
**Correct Answer: B) NullPointerException**

**Explanation:** Cannot synchronize on null object.

---

### Question 15
**Correct Answer: A) A**

**Explanation:** Enum constants can have method implementations. A.m() prints "A".

---

### Question 16
**Correct Answer: B) false**

**Explanation:** Modifying list changes hashCode. Lookup fails with new hash.

---

### Question 17
**Correct Answer: B) true true false**

**Explanation:** Short also has cache. s3 is new object (not cached).

---

### Question 18
**Correct Answer: A) NPE**

**Explanation:** throw null throws NullPointerException.

---

### Question 19
**Correct Answer: B) Varargs**

**Explanation:** Two ints can only match varargs. Integer can't accept two arguments.

---

### Question 20
**Correct Answer: B) Empty**

**Explanation:** list is null. Optional empty. ifPresentOrElse calls else action.

---

### Question 21
**Correct Answer: B) ab**

**Explanation:** Lazy evaluation. Processes until findFirst gets match. "a", "b" printed.

---

### Question 22
**Correct Answer: A) 15**

**Explanation:** B's y initialized using inherited x (10). y = 10 + 5 = 15.

---

### Question 23
**Correct Answer: B) true false**

**Explanation:** Long cache is -128 to 127. 127 cached (true), 128 not (false).

---

### Question 24
**Correct Answer: A) 0 1**

**Explanation:** A.x = B.y triggers B load. B.y = A.x(0) + 1 = 1. A.x = 0 (default before B.y evaluated).

---

### Question 25
**Correct Answer: A) C**

**Explanation:** C implements both A and B. Cast succeeds. m() prints "C".

---

### Question 26
**Correct Answer: B) 2 2**

**Explanation:** Case-insensitive comparator. "a" and "A" same key. 2 entries. "a" gets value 2.

---

### Question 27
**Correct Answer: B) Hello**

**Explanation:** Unicode escapes processed at compile time. \u0048 = 'H', etc.

---

### Question 28
**Correct Answer: A) B**

**Explanation:** getSimpleName() returns just "B", not full path.

---

### Question 29
**Correct Answer: C) Compile error**

**Explanation:** super.super is not valid Java syntax.

---

### Question 30
**Correct Answer: B) 1.0**

**Explanation:** Ternary types unified to Double. Integer 1 widened to 1.0.

---

### Question 31
**Correct Answer: B) 0 1**

**Explanation:** Compound assignment evaluates left to right. x becomes 0 due to order.

---

### Question 32
**Correct Answer: A) int 10**

**Explanation:** Reference type A determines which method. A.m(int) is called.

---

### Question 33
**Correct Answer: B) String**

**Explanation:** null matches most specific type. String is more specific.

---

### Question 34
**Correct Answer: B) false**

**Explanation:** s1 += creates new object. s2 still references "a".

---

### Question 35
**Correct Answer: C) Compile error - y not effectively final**

**Explanation:** y++ modifies y. Not effectively final for local class.

---

### Question 36
**Correct Answer: B) 1, 3**

**Explanation:** TreeSet sorts (first = 1). LinkedHashSet keeps insertion order (first = 3).

---

### Question 37
**Correct Answer: B) [, b, b]**

**Explanation:** Split on a+. Empty string before first match, then "b"s between.

---

### Question 38
**Correct Answer: C) Compile error**

**Explanation:** A.m() is private. Not accessible via A reference even with B object.

---

### Question 39
**Correct Answer: B) 2**

**Explanation:** Order: x=1 (field), x=3 (instance block), x=2 (constructor).

---

### Question 40
**Correct Answer: B) B**

**Explanation:** C's default method resolves conflict by calling B.super.m().

---

### Question 41
**Correct Answer: C) Either a1b2 or b2a1**

**Explanation:** Map.of doesn't guarantee order. HashMap used internally.

---

### Question 42
**Correct Answer: A) static**

**Explanation:** Can call static method on abstract class. No instance needed.

---

### Question 43
**Correct Answer: B) Done**

**Explanation:** Empty array, loop body never executes. Prints "Done".

---

### Question 44
**Correct Answer: B) JAVA, JAVA (Turkish I without dot)**

**Explanation:** Turkish locale has dotless I. May differ visually.

---

### Question 45
**Correct Answer: A) Yes, compiles and runs**

**Explanation:** Anonymous class can extend exception. Valid Java.

---

### Question 46
**Correct Answer: C) 12**

**Explanation:** x=10, first block x=11, second block x=12.

---

### Question 47
**Correct Answer: A) Hello**

**Explanation:** Type erasure. Runtime sees Object. get() returns "Hello". No ClassCastException until specific type operation.

---

### Question 48
**Correct Answer: A) Two**

**Explanation:** Switch expression with yield returns "Two" for case 2.

---

### Question 49
**Correct Answer: B) 0 0**

**Explanation:** Compact constructor can modify parameters before final assignment.

---

### Question 50
**Correct Answer: A) 42**

**Explanation:** var infers anonymous type. Can access value field directly.

---

## 📊 Score Guide

| Score | Level | Next Step |
|-------|-------|-----------|
| 45-50 | Exceptional! | Move to Set 10 |
| 35-44 | Outstanding | Minor review |
| 25-34 | Very Good | More practice |
| 0-24 | Good effort | Review Sets 7-8 |

---

**Difficulty: 🔥🔥 MASTER** | **Next: Set 10 (🔥🔥🔥 Ultimate)**
