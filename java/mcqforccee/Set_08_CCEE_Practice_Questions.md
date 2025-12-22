# CDAC CCEE MCQ Practice Set 8

## 📝 EXPERT LEVEL - Complex Code Analysis & Edge Cases
**Total Questions: 50 | Time Limit: 60 minutes | No Negative Marking**

> **Difficulty: 🔥 Expert** - These questions involve complex scenarios, subtle bugs, edge cases, and require analyzing multiple interacting concepts. Think carefully!

---

### Question 1
What is the output?
```java
class A {
    int x = 10;
    int y = x + 5;
    { x = 20; }
    A() { y = x + 10; }
}
System.out.println(new A().x + " " + new A().y);
```

A) 20 30  
B) 10 15  
C) 20 15  
D) 10 30

---

### Question 2
What is the output?
```java
String s = "Hello";
try {
    s.charAt(10);
} catch(Exception e) {
    s = "Exception";
    throw e;
} finally {
    System.out.println(s);
}
```

A) Hello  
B) Exception  
C) Exception (then throws)  
D) Compile error

---

### Question 3
What is the output?
```java
interface A { default void m() { System.out.print("A "); } }
interface B extends A { default void m() { A.super.m(); System.out.print("B "); } }
class C implements B { }
new C().m();
```

A) A B  
B) B  
C) A  
D) B A

---

### Question 4
What is the output?
```java
List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
for(int i = 0; i < list.size(); i++) {
    if(list.get(i) % 2 == 0) {
        list.remove(i);
    }
}
System.out.println(list);
```

A) [1, 3, 5]  
B) [1, 3, 4, 5]  
C) ConcurrentModificationException  
D) [1, 2, 3, 4, 5]

---

### Question 5
What is the output?
```java
Map<List<Integer>, String> map = new HashMap<>();
List<Integer> key = new ArrayList<>();
key.add(1);
map.put(key, "One");
key.add(2);
System.out.println(map.get(key));
```

A) One  
B) null  
C) Exception  
D) [1, 2]

---

### Question 6
What is the output?
```java
class A {
    void m(int x, int y) { System.out.println(x - y); }
}
class B extends A {
    void m(int x, int y) { System.out.println(y - x); }
}
A a = new B();
a.m(10, 5);
```

A) 5  
B) -5  
C) 15  
D) Error

---

### Question 7
What is the output?
```java
class A {
    static final int X;
    static { X = getValue(); }
    static int getValue() { return 10; }
}
System.out.println(A.X);
```

A) 10  
B) 0  
C) Compile error - final not initialized  
D) Runtime error

---

### Question 8
What is the output?
```java
try {
    try {
        throw new RuntimeException("Inner");
    } finally {
        throw new RuntimeException("Finally");
    }
} catch(Exception e) {
    System.out.println(e.getMessage());
}
```

A) Inner  
B) Finally  
C) Inner Finally  
D) Both exceptions

---

### Question 9
What is the output?
```java
class A {
    void m(Object... objs) { System.out.print(objs.getClass().getSimpleName()); }
}
new A().m("a", "b");
```

A) String[]  
B) Object[]  
C) String  
D) Object

---

### Question 10
What is the output?
```java
Integer[] ints = {1, 2, 3};
Object[] objs = ints;
objs[0] = "Hello";
```

A) Works fine  
B) ArrayStoreException  
C) Compile error  
D) [Hello, 2, 3]

---

### Question 11
What is the output?
```java
enum Singleton {
    INSTANCE;
    private int value = 10;
    public int getValue() { return value; }
}
System.out.println(Singleton.INSTANCE.getValue());
```

A) 10  
B) 0  
C) Error  
D) INSTANCE

---

### Question 12
What is the output?
```java
class A {
    A m() { return this; }
}
class B extends A {
    B m() { return this; }
}
System.out.println(new B().m() instanceof B);
```

A) true  
B) false  
C) Compile error  
D) A

---

### Question 13
What is the output?
```java
interface A { void m(); }
interface B { String m(); }
class C implements A, B {
    // What should m() return?
}
```

A) void  
B) String  
C) Compile error - incompatible return types  
D) Either works

---

### Question 14
What is the output?
```java
class Outer {
    private int x = 10;
    class Inner {
        private int x = 20;
        void show() {
            int x = 30;
            System.out.println(x + " " + this.x + " " + Outer.this.x);
        }
    }
}
new Outer().new Inner().show();
```

A) 30 20 10  
B) 10 20 30  
C) 30 30 30  
D) Error

---

### Question 15
What is the output?
```java
class A {
    int x = 10;
    class B {
        int x = 20;
        void m() {
            new Thread(() -> System.out.println(x + " " + A.this.x)).start();
        }
    }
}
new A().new B().m();
Thread.sleep(100);
```

A) 20 10  
B) 10 20  
C) 20 20  
D) 10 10

---

### Question 16
What is the output?
```java
class A implements Comparable<A> {
    int x;
    A(int x) { this.x = x; }
    public int compareTo(A a) { return this.x - a.x; }
    public boolean equals(Object o) {
        return o instanceof A && ((A)o).x == this.x;
    }
}
Set<A> set = new TreeSet<>();
set.add(new A(1));
set.add(new A(2));
set.add(new A(1));
System.out.println(set.size());
```

A) 3  
B) 2  
C) 1  
D) Error

---

### Question 17
What is the output?
```java
class A {
    static { System.out.print("A static "); }
    { System.out.print("A instance "); }
}
class B extends A {
    static { System.out.print("B static "); }
    { System.out.print("B instance "); }
}
A a = new B();
```

A) A static B static A instance B instance  
B) B static A static B instance A instance  
C) A static A instance B static B instance  
D) A static B static B instance A instance

---

### Question 18
What is the output?
```java
public static void main(String[] args) {
    try {
        main(null);
    } catch(StackOverflowError e) {
        System.out.println("Overflow");
    }
}
```

A) Overflow  
B) StackOverflowError (uncaught)  
C) Infinite loop  
D) Nothing

---

### Question 19
What is the output?
```java
Double d1 = 0.0;
Double d2 = -0.0;
System.out.println(d1.equals(d2) + " " + (d1.compareTo(d2) == 0));
```

A) true true  
B) false false  
C) false true  
D) true false

---

### Question 20
What is the output?
```java
Double d = Double.NaN;
System.out.println(d.equals(d) + " " + (d == d));
```

A) true true  
B) true false  
C) false false  
D) false true

---

### Question 21
What is the output?
```java
String s = "Hello";
System.out.println(s.replace("", "-"));
```

A) Hello  
B) -H-e-l-l-o-  
C) Error  
D) -Hello-

---

### Question 22
What is the output?
```java
class A {
    void m() { n(); }
    void n() { System.out.println("A.n"); }
}
class B extends A {
    void n() { System.out.println("B.n"); }
}
new B().m();
```

A) A.n  
B) B.n  
C) A.n B.n  
D) Error

---

### Question 23
What is the output?
```java
try(AutoCloseable a = () -> System.out.print("1 ");
    AutoCloseable b = () -> System.out.print("2 ")) {
    System.out.print("Try ");
}
```

A) Try 1 2  
B) Try 2 1  
C) 1 2 Try  
D) 2 1 Try

---

### Question 24
What is the output?
```java
class A {
    int[] arr;
    A() { arr = new int[]{1, 2, 3}; }
}
A a1 = new A();
A a2 = new A();
a2.arr = a1.arr;
a1.arr[0] = 100;
System.out.println(a2.arr[0]);
```

A) 1  
B) 100  
C) Error  
D) 0

---

### Question 25
What is the output?
```java
class A {
    String s;
    A(String s) { this.s = s; }
    public boolean equals(Object o) {
        return o != null && s.equals(((A)o).s);
    }
}
Set<A> set = new HashSet<>();
set.add(new A("Test"));
set.add(new A("Test"));
System.out.println(set.size());
```

A) 1  
B) 2  
C) 0  
D) Error

---

### Question 26
What is the output?
```java
Optional<Optional<String>> opt = Optional.of(Optional.of("Hello"));
System.out.println(opt.flatMap(o -> o).orElse("Default"));
```

A) Hello  
B) Default  
C) Optional[Hello]  
D) Error

---

### Question 27
What is the output?
```java
Stream.of("a", "b", "c")
    .peek(System.out::print)
    .findFirst();
```

A) abc  
B) a  
C) Nothing  
D) Error

---

### Question 28
What is the output?
```java
List<Integer> list = IntStream.range(1, 4)
    .boxed()
    .collect(Collectors.toUnmodifiableList());
list.set(0, 10);
```

A) [10, 2, 3]  
B) UnsupportedOperationException  
C) [1, 2, 3]  
D) Compile error

---

### Question 29
What is the output?
```java
Map<String, Integer> map = Stream.of("a", "b", "a")
    .collect(Collectors.toMap(s -> s, s -> 1, Integer::sum));
System.out.println(map.get("a"));
```

A) 1  
B) 2  
C) Exception - duplicate key  
D) null

---

### Question 30
What is the output?
```java
String result = Stream.of("a", "b", "c")
    .collect(Collectors.joining(", ", "[", "]"));
System.out.println(result);
```

A) a, b, c  
B) [a, b, c]  
C) [a, b, c,]  
D) Error

---

### Question 31
What is the output?
```java
class A<T extends Comparable<T>> {
    T max(T a, T b) {
        return a.compareTo(b) > 0 ? a : b;
    }
}
A<Integer> obj = new A<>();
System.out.println(obj.max(5, 10));
```

A) 5  
B) 10  
C) Error  
D) 0

---

### Question 32
What is the output?
```java
class Box<T> {
    T value;
    void set(T value) { this.value = value; }
    T get() { return value; }
}
Box<?> box = new Box<String>();
box.set("Hello");
```

A) Sets Hello  
B) Compile error  
C) Works fine  
D) Runtime error

---

### Question 33
What is the output?
```java
List<? super Integer> list = new ArrayList<Number>();
list.add(10);
list.add(20);
Object obj = list.get(0);
System.out.println(obj);
```

A) 10  
B) Error  
C) null  
D) Compile error

---

### Question 34
What is the output?
```java
class A {
    static void m(List<Integer> list) { System.out.println("Integer"); }
    static void m(List<String> list) { System.out.println("String"); }
}
```

A) Integer  
B) String  
C) Compile error - same erasure  
D) Works fine

---

### Question 35
What is the output?
```java
@SuppressWarnings("unchecked")
public static <T> T[] createArray(int size) {
    return (T[]) new Object[size];
}
String[] arr = createArray(5);
arr[0] = "Hello";
```

A) Works fine  
B) ClassCastException  
C) Compile error  
D) ArrayStoreException

---

### Question 36
What is the output?
```java
class Parent<T> {
    T value;
}
class Child extends Parent<String> {
    void m() { System.out.println(value.length()); }
}
Child c = new Child();
c.value = "Hello";
c.m();
```

A) 5  
B) Error  
C) null  
D) 0

---

### Question 37
What is the output?
```java
interface Processor<T, R> {
    R process(T input);
}
Processor<String, Integer> p = String::length;
System.out.println(p.process("Hello"));
```

A) 5  
B) Hello  
C) Error  
D) null

---

### Question 38
What is the output?
```java
class A {
    void m(List<? extends Number> list) {
        list.add(null);
        // list.add(1); // Would this compile?
    }
}
```
Would `list.add(1)` compile?

A) Yes  
B) No - can only add null  
C) Yes, if list is List<Integer>  
D) Depends on runtime type

---

### Question 39
What is the output?
```java
BiConsumer<StringBuilder, String> appender = StringBuilder::append;
StringBuilder sb = new StringBuilder();
appender.accept(sb, "Hello");
appender.accept(sb, " World");
System.out.println(sb);
```

A) Hello World  
B) World  
C) Hello  
D) Error

---

### Question 40
What is the output?
```java
Function<String, String> f1 = s -> s.toUpperCase();
Function<String, Integer> f2 = s -> s.length();
System.out.println(f1.andThen(f2).apply("hello"));
```

A) hello  
B) HELLO  
C) 5  
D) Error

---

### Question 41
What is the output?
```java
class A {
    private final int x;
    A() {
        new Thread(() -> System.out.println(x)).start();
        x = 10;
    }
}
new A();
Thread.sleep(100);
```

A) 10  
B) 0  
C) Either 0 or 10  
D) Compile error

---

### Question 42
What is the output?
```java
String s1 = "a" + "b" + "c";
String s2 = "abc";
String s3 = new String("abc").intern();
System.out.println((s1 == s2) + " " + (s1 == s3));
```

A) true true  
B) false false  
C) true false  
D) false true

---

### Question 43
What is the output?
```java
class A {
    void m(long x) { System.out.println("long"); }
    void m(Integer x) { System.out.println("Integer"); }
}
new A().m(10);
```

A) long  
B) Integer  
C) Compile error - ambiguous  
D) Both

---

### Question 44
What is the output?
```java
switch("Hello".hashCode()) {
    case "Hello".hashCode(): System.out.println("Match");
}
```

A) Match  
B) Compile error - case must be constant  
C) Runtime error  
D) Nothing

---

### Question 45
What is the output?
```java
class A {
    static int x = 10;
}
class B extends A {
    static { x = 20; }
}
System.out.println(A.x);
System.out.println(B.x);
```

A) 10, 20  
B) 10, 10  
C) 20, 20  
D) 10 then 20

---

### Question 46
What is the output?
```java
record Person(String name, int age) { }
Person p1 = new Person("John", 25);
Person p2 = new Person("John", 25);
System.out.println(p1.equals(p2) + " " + (p1 == p2));
```

A) true true  
B) true false  
C) false true  
D) false false

---

### Question 47
What is the output?
```java
var list = List.of(1, 2, 3);
System.out.println(list.getClass().getSimpleName());
```

A) ArrayList  
B) ImmutableCollections$ListN  
C) Something with "Immutable"  
D) LinkedList

---

### Question 48
What is the output?
```java
sealed interface Shape permits Circle, Square { }
final class Circle implements Shape { }
final class Square implements Shape { }
class Rectangle implements Shape { }
```

A) Compiles fine  
B) Compile error - Rectangle not permitted  
C) Runtime error  
D) Warning only

---

### Question 49
What is the output?
```java
Object obj = switch(1) {
    case 1 -> "One";
    case 2 -> 2;
    default -> null;
};
System.out.println(obj.getClass().getSimpleName());
```

A) String  
B) Object  
C) Integer  
D) Error

---

### Question 50
What is the output?
```java
String text = """
    Hello
    World
    """;
System.out.println(text.lines().count());
```

A) 2  
B) 3  
C) 1  
D) Error

---

---

# 📝 Answer Key with Explanations

---

### Question 1
**Correct Answer: A) 20 30**

**Explanation:** Order: x=10, y=15 (field init), x=20 (instance block), y=30 (constructor). Each new A() follows this.

---

### Question 2
**Correct Answer: C) Exception (then throws)**

**Explanation:** Catch modifies s and re-throws. Finally executes before propagation, prints "Exception".

---

### Question 3
**Correct Answer: A) A B**

**Explanation:** B's default method calls A.super.m() first, then prints B.

---

### Question 4
**Correct Answer: B) [1, 3, 4, 5]**

**Explanation:** When 2 removed at i=1, 4 shifts to i=1. i++ skips it. 4 remains. Not CME because using index-based removal.

---

### Question 5
**Correct Answer: B) null**

**Explanation:** Mutable key's hashCode changes after modification. Key lookup fails.

---

### Question 6
**Correct Answer: B) -5**

**Explanation:** Dynamic dispatch calls B's m(). 5 - 10 = -5.

---

### Question 7
**Correct Answer: A) 10**

**Explanation:** Static final can be initialized in static block. getValue() returns 10.

---

### Question 8
**Correct Answer: B) Finally**

**Explanation:** Finally exception suppresses inner exception. Only "Finally" exception propagates.

---

### Question 9
**Correct Answer: B) Object[]**

**Explanation:** Varargs creates Object[] at runtime (compile-time component type).

---

### Question 10
**Correct Answer: B) ArrayStoreException**

**Explanation:** Integer[] only accepts Integer. Storing String throws ArrayStoreException.

---

### Question 11
**Correct Answer: A) 10**

**Explanation:** Enum singleton pattern. Instance has value 10.

---

### Question 12
**Correct Answer: A) true**

**Explanation:** Covariant return type allows B to return B. instanceof B is true.

---

### Question 13
**Correct Answer: C) Compile error - incompatible return types**

**Explanation:** void and String cannot be reconciled. No single method can satisfy both.

---

### Question 14
**Correct Answer: A) 30 20 10**

**Explanation:** x=30 (local), this.x=20 (Inner's), Outer.this.x=10 (Outer's).

---

### Question 15
**Correct Answer: A) 20 10**

**Explanation:** Lambda captures x from B (20) and A.this.x (10).

---

### Question 16
**Correct Answer: B) 2**

**Explanation:** TreeSet uses compareTo for equality. Two distinct x values (1, 2).

---

### Question 17
**Correct Answer: A) A static B static A instance B instance**

**Explanation:** Static blocks first (parent then child), then instance blocks (parent then child).

---

### Question 18
**Correct Answer: A) Overflow**

**Explanation:** StackOverflowError is caught. Error is Throwable, can be caught.

---

### Question 19
**Correct Answer: C) false true**

**Explanation:** equals distinguishes 0.0 and -0.0 (false). compareTo treats them equal (true).

---

### Question 20
**Correct Answer: B) true false**

**Explanation:** NaN.equals(NaN) is true. NaN == NaN is false (IEEE 754).

---

### Question 21
**Correct Answer: B) -H-e-l-l-o-**

**Explanation:** Replace empty string inserts between every character and at edges.

---

### Question 22
**Correct Answer: B) B.n**

**Explanation:** m() calls n(). n() is overridden in B. Dynamic dispatch calls B's n().

---

### Question 23
**Correct Answer: B) Try 2 1**

**Explanation:** Resources closed in reverse order of declaration. b closes, then a.

---

### Question 24
**Correct Answer: B) 100**

**Explanation:** a2.arr = a1.arr shares array reference. Modifying a1.arr affects a2.arr.

---

### Question 25
**Correct Answer: B) 2**

**Explanation:** equals without hashCode override. Different hashCodes, both added.

---

### Question 26
**Correct Answer: A) Hello**

**Explanation:** flatMap unwraps nested optional. Inner optional has "Hello".

---

### Question 27
**Correct Answer: B) a**

**Explanation:** Short-circuit. findFirst() only needs first element. peek prints "a" only.

---

### Question 28
**Correct Answer: B) UnsupportedOperationException**

**Explanation:** toUnmodifiableList creates immutable list. set() throws exception.

---

### Question 29
**Correct Answer: B) 2**

**Explanation:** Merge function (Integer::sum) handles duplicate key "a". 1 + 1 = 2.

---

### Question 30
**Correct Answer: B) [a, b, c]**

**Explanation:** joining with delimiter, prefix, suffix creates "[a, b, c]".

---

### Question 31
**Correct Answer: B) 10**

**Explanation:** max(5, 10) compares and returns larger (10).

---

### Question 32
**Correct Answer: B) Compile error**

**Explanation:** Wildcard (?) means unknown type. Cannot add anything except null.

---

### Question 33
**Correct Answer: A) 10**

**Explanation:** Lower bound (super Integer) allows adding Integer. get() returns Object.

---

### Question 34
**Correct Answer: C) Compile error - same erasure**

**Explanation:** Type erasure: both become m(List). Same signature, can't overload.

---

### Question 35
**Correct Answer: B) ClassCastException**

**Explanation:** Generic array creation creates Object[]. Cannot assign to String[].

---

### Question 36
**Correct Answer: A) 5**

**Explanation:** Child specifies String type. value.length() works.

---

### Question 37
**Correct Answer: A) 5**

**Explanation:** Method reference works as Processor. "Hello".length() = 5.

---

### Question 38
**Correct Answer: B) No - can only add null**

**Explanation:** Upper bound (extends) is producer (read-only). Cannot add except null.

---

### Question 39
**Correct Answer: A) Hello World**

**Explanation:** BiConsumer appends to StringBuilder. "Hello" + " World".

---

### Question 40
**Correct Answer: C) 5**

**Explanation:** f1 uppercase "hello"→"HELLO", f2 gets length→5.

---

### Question 41
**Correct Answer: D) Compile error**

**Explanation:** Cannot use x before final assignment. Lambda captures uninitialized field.

---

### Question 42
**Correct Answer: A) true true**

**Explanation:** Compile-time constant + intern = same pool reference.

---

### Question 43
**Correct Answer: A) long**

**Explanation:** Widening (int→long) preferred over boxing (int→Integer).

---

### Question 44
**Correct Answer: B) Compile error - case must be constant**

**Explanation:** Method call in case expression. Not a compile-time constant.

---

### Question 45
**Correct Answer: A) 10, 20**

**Explanation:** First prints 10 (before B loads). Loading B changes x to 20.

---

### Question 46
**Correct Answer: B) true false**

**Explanation:** Records auto-generate equals based on components. Different objects, same values.

---

### Question 47
**Correct Answer: C) Something with "Immutable"**

**Explanation:** List.of returns ImmutableCollections internal class.

---

### Question 48
**Correct Answer: B) Compile error - Rectangle not permitted**

**Explanation:** Sealed interface only permits listed classes.

---

### Question 49
**Correct Answer: A) String**

**Explanation:** Switch returns "One" (String) for case 1.

---

### Question 50
**Correct Answer: B) 3**

**Explanation:** Text block: "Hello\nWorld\n" has 3 lines (including empty final).

---

## 📊 Score Guide

| Score | Level | Next Step |
|-------|-------|-----------|
| 45-50 | Outstanding! | Move to Set 9 |
| 35-44 | Excellent | Review complex areas |
| 25-34 | Good | Needs more practice |
| 0-24 | Keep trying | Review Sets 6-7 |

---

**Difficulty: 🔥 EXPERT** | **Next: Set 9 (🔥🔥 Master)**
