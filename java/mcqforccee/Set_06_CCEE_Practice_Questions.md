# CDAC CCEE MCQ Practice Set 6

## 📝 HARDER LEVEL - Advanced OOP, Reflection & JVM Concepts
**Total Questions: 50 | Time Limit: 60 minutes | No Negative Marking**

> **Difficulty: ⭐⭐⭐⭐⭐ Harder** - These questions cover advanced topics like reflection, cloning, serialization, JVM internals, and complex inheritance scenarios. Requires deep understanding.

---

### Question 1
What is the output?
```java
class A implements Cloneable {
    int[] arr = {1, 2, 3};
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
A a1 = new A();
A a2 = (A) a1.clone();
a2.arr[0] = 100;
System.out.println(a1.arr[0]);
```

A) 1  
B) 100  
C) CloneNotSupportedException  
D) Error

---

### Question 2
What is the output?
```java
class Person implements Serializable {
    String name = "John";
    transient int age = 25;
}
// After serialization and deserialization
System.out.println(person.age);
```

A) 25  
B) 0  
C) null  
D) Error

---

### Question 3
What is the output?
```java
Class<?> cls = String.class;
System.out.println(cls.getSuperclass().getSimpleName());
```

A) String  
B) Object  
C) Class  
D) null

---

### Question 4
What is the output?
```java
Method[] methods = String.class.getDeclaredMethods();
System.out.println(methods.length > 50);
```

A) true  
B) false  
C) Error  
D) 0

---

### Question 5
What is the output?
```java
class A {
    private int x = 10;
}
A a = new A();
Field f = A.class.getDeclaredField("x");
f.setAccessible(true);
System.out.println(f.get(a));
```

A) 10  
B) IllegalAccessException  
C) Error  
D) 0

---

### Question 6
What is the output?
```java
interface A { default void m() { System.out.print("A "); } }
interface B extends A { default void m() { System.out.print("B "); } }
class C implements A, B { }
new C().m();
```

A) A  
B) B  
C) A B  
D) Compile error

---

### Question 7
What is the output?
```java
class A {
    void m() throws IOException { }
}
class B extends A {
    void m() throws FileNotFoundException { }
}
class C extends A {
    void m() { }
}
```

A) All classes compile  
B) Only B compiles  
C) Only C compiles  
D) None compile

---

### Question 8
What is the output?
```java
class Singleton {
    private static Singleton instance = new Singleton();
    private Singleton() { System.out.print("Init "); }
    static Singleton getInstance() { return instance; }
}
Singleton s1 = Singleton.getInstance();
Singleton s2 = Singleton.getInstance();
System.out.println(s1 == s2);
```

A) Init Init true  
B) Init true  
C) Init Init false  
D) true

---

### Question 9
What is the output?
```java
String s = new String("Hello");
System.out.println(s.getClass().getInterfaces().length > 0);
```

A) true  
B) false  
C) 0  
D) Error

---

### Question 10
What is the output?
```java
class A {
    { throw new RuntimeException(); }
    A() { System.out.println("Constructor"); }
}
new A();
```

A) Constructor  
B) RuntimeException thrown  
C) Compile error  
D) Nothing

---

### Question 11
What is the output?
```java
class Parent implements Serializable {
    int x = 10;
}
class Child extends Parent {
    int y = 20;
}
// Child serialized and deserialized
System.out.println(child.x + " " + child.y);
```

A) 10 20  
B) 0 20  
C) 10 0  
D) 0 0

---

### Question 12
What is the output?
```java
class A {
    static { System.out.print("A "); }
}
class B extends A {
    static { System.out.print("B "); }
}
class C extends B {
    static { System.out.print("C "); }
}
new C();
```

A) C  
B) A B C  
C) C B A  
D) B C

---

### Question 13
What is the output?
```java
Class<?> cls = int.class;
System.out.println(cls.isPrimitive());
```

A) true  
B) false  
C) Error  
D) null

---

### Question 14
What is the output?
```java
interface A { void m(); }
class B {
    public void m() { System.out.println("B"); }
}
class C extends B implements A { }
new C().m();
```

A) B  
B) Compile error  
C) Nothing  
D) A

---

### Question 15
What is the output?
```java
class A {
    A() { print(); }
    void print() { System.out.println("A"); }
}
class B extends A {
    int x = 10;
    void print() { System.out.println(x); }
}
new B();
```

A) A  
B) 10  
C) 0  
D) Error

---

### Question 16
What is the output?
```java
abstract class A {
    abstract void m();
    A() { m(); }
}
class B extends A {
    int x = 10;
    void m() { System.out.println(x); }
}
new B();
```

A) 10  
B) 0  
C) Error  
D) Nothing

---

### Question 17
What is the output?
```java
class A {
    static void m() { System.out.println("A-static"); }
}
class B extends A {
    void m() { System.out.println("B-instance"); }
}
```

A) B-instance  
B) A-static  
C) Compile error  
D) Both at runtime

---

### Question 18
What is the output?
```java
interface A { void m(); }
A obj = () -> System.out.println("Lambda");
System.out.println(obj.getClass().getSuperclass().getSimpleName());
```

A) A  
B) Object  
C) Lambda  
D) Error

---

### Question 19
What is the output?
```java
Constructor<?> c = String.class.getConstructor(String.class);
String s = (String) c.newInstance("Hello");
System.out.println(s);
```

A) Hello  
B) Error  
C) NoSuchMethodException  
D) null

---

### Question 20
What is the output?
```java
enum Status {
    ACTIVE(1), INACTIVE(0);
    int code;
    Status(int code) { this.code = code; }
}
System.out.println(Status.ACTIVE.code);
```

A) ACTIVE  
B) 1  
C) 0  
D) Error

---

### Question 21
What is the output?
```java
class A {
    final void m() { System.out.println("A"); }
}
class B extends A {
    // void m() { System.out.println("B"); }
}
new B().m();
```

A) A  
B) B  
C) Compile error  
D) Nothing

---

### Question 22
What is the output?
```java
class ImmutableClass {
    private final String value;
    ImmutableClass(String value) { this.value = value; }
    String getValue() { return value; }
}
ImmutableClass obj = new ImmutableClass("Hello");
obj.getValue().concat(" World");
System.out.println(obj.getValue());
```

A) Hello World  
B) Hello  
C) Error  
D) null

---

### Question 23
What is the output?
```java
class A {
    private A() { System.out.println("Private"); }
    public static A create() { return new A(); }
}
A.create();
```

A) Private  
B) Error  
C) Nothing  
D) IllegalAccessException

---

### Question 24
What is the output?
```java
Object obj = new Object();
System.out.println(obj.hashCode() == obj.hashCode());
```

A) true  
B) false  
C) Random  
D) Error

---

### Question 25
What is the output?
```java
String s1 = "Hello";
String s2 = "Hello";
String s3 = new String("Hello").intern();
System.out.println((s1 == s2) + " " + (s1 == s3));
```

A) true true  
B) true false  
C) false true  
D) false false

---

### Question 26
What is the output?
```java
class A {
    static int x = 10;
}
class B extends A {
    static int x = 20;
}
A a = new B();
System.out.println(a.x);
```

A) 10  
B) 20  
C) Error  
D) 0

---

### Question 27
What is the output?
```java
try {
    throw new Error("Error");
} catch(Exception e) {
    System.out.println("Caught");
}
```

A) Caught  
B) Error thrown (not caught)  
C) Compile error  
D) Nothing

---

### Question 28
What is the output?
```java
class A {
    void m(int... args) { System.out.println("varargs"); }
    void m(Integer x) { System.out.println("Integer"); }
}
new A().m(10);
```

A) varargs  
B) Integer  
C) Compile error - ambiguous  
D) Both

---

### Question 29
What is the output?
```java
Object[] objs = new String[3];
objs[0] = "Hello";
objs[1] = 10;
```

A) Works fine  
B) ArrayStoreException  
C) Compile error  
D) null

---

### Question 30
What is the output?
```java
interface Marker { }
class A implements Marker { }
A a = new A();
System.out.println(a instanceof Marker);
```

A) true  
B) false  
C) Error  
D) Marker

---

### Question 31
What is the output?
```java
class A {
    protected A() { System.out.print("A "); }
}
class B extends A {
    B() { System.out.print("B"); }
}
new B();
```

A) B  
B) A  
C) A B  
D) Error

---

### Question 32
What is the output?
```java
final class A { }
class B extends A { }
```

A) Compiles fine  
B) Compile error - cannot extend final class  
C) Runtime error  
D) Warning only

---

### Question 33
What is the output?
```java
class A {
    void finalize() { System.out.println("Finalize"); }
}
A a = new A();
a = null;
System.gc();
```

A) Finalize (guaranteed)  
B) May or may not print Finalize  
C) Error  
D) Nothing

---

### Question 34
What is the output?
```java
StringBuilder sb1 = new StringBuilder("Hello");
StringBuilder sb2 = sb1;
sb1.append(" World");
System.out.println(sb2);
```

A) Hello  
B) Hello World  
C) null  
D) Error

---

### Question 35
What is the output?
```java
class A {
    int x;
    A(int x) { this.x = x; }
    public boolean equals(Object o) {
        if(o instanceof A) {
            return this.x == ((A)o).x;
        }
        return false;
    }
}
A a1 = new A(10);
A a2 = new A(10);
System.out.println(a1.equals(a2) + " " + (a1 == a2));
```

A) true true  
B) true false  
C) false true  
D) false false

---

### Question 36
What is the output?
```java
class Outer {
    int x = 10;
    void m() {
        int y = 20;
        class Local {
            void show() { System.out.println(x + " " + y); }
        }
        new Local().show();
    }
}
new Outer().m();
```

A) 10 20  
B) 10 0  
C) Error - y not effectively final  
D) 0 20

---

### Question 37
What is the output?
```java
class A {
    static class B {
        static void m() { System.out.println("Static nested"); }
    }
}
A.B.m();
```

A) Static nested  
B) Error  
C) Nothing  
D) A.B

---

### Question 38
What is the output?
```java
BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;
System.out.println(add.apply(3, 4));
```

A) 7  
B) 34  
C) Error  
D) null

---

### Question 39
What is the output?
```java
Predicate<String> isEmpty = String::isEmpty;
System.out.println(isEmpty.test(""));
```

A) true  
B) false  
C) Error  
D) null

---

### Question 40
What is the output?
```java
class A {
    { System.out.print("A-instance "); }
    static { System.out.print("A-static "); }
}
class B extends A {
    { System.out.print("B-instance "); }
    static { System.out.print("B-static "); }
}
new B();
new B();
```

A) A-static B-static A-instance B-instance A-instance B-instance  
B) A-static A-instance B-static B-instance  
C) A-static B-static A-instance B-instance  
D) A-static A-instance B-instance

---

### Question 41
What is the output?
```java
System.out.println(Runtime.getRuntime().availableProcessors() > 0);
```

A) true  
B) false  
C) Error  
D) Random

---

### Question 42
What is the output?
```java
class A {
    void m(Number n) { System.out.print("Number "); }
    void m(Integer i) { System.out.print("Integer "); }
}
Number n = 10;
new A().m(n);
```

A) Number  
B) Integer  
C) Compile error  
D) Both

---

### Question 43
What is the output?
```java
class A {
    int x = 10;
    static int y = 20;
}
A a = null;
System.out.println(a.y);
```

A) NullPointerException  
B) 20  
C) 10  
D) Error

---

### Question 44
What is the output?
```java
interface A { void m() throws Exception; }
interface B { void m() throws IOException; }
interface C extends A, B { }
```

A) C.m() throws Exception  
B) C.m() throws IOException  
C) Compile error  
D) C.m() throws nothing

---

### Question 45
What is the output?
```java
class A {
    void m(Object... objs) { System.out.println(objs.length); }
}
new A().m(null);
```

A) 0  
B) 1  
C) NullPointerException  
D) Error

---

### Question 46
What is the output?
```java
class A extends Thread {
    public void run() { System.out.println("Run"); }
    public static void main(String[] args) {
        A a = new A();
        a.start();
        a.run();
    }
}
```

A) Run  
B) Run Run  
C) Run (once, maybe twice depending on scheduling)  
D) Error

---

### Question 47
What is the output?
```java
interface A {
    static void m() { System.out.println("A"); }
}
class B implements A { }
B.m();
```

A) A  
B) Compile error  
C) Nothing  
D) Runtime error

---

### Question 48
What is the output?
```java
class A {
    int x;
    void m(int x) {
        x = x;
    }
}
A a = new A();
a.m(10);
System.out.println(a.x);
```

A) 10  
B) 0  
C) Error  
D) null

---

### Question 49
What is the output?
```java
class A {
    public A() { }
}
class B extends A {
    B() { super(); System.out.println("B"); }
}
new B();
```

A) B  
B) A B  
C) Error  
D) Nothing

---

### Question 50
What is the output?
```java
interface Printable {
    void print();
    default void display() { print(); }
}
class Document implements Printable {
    public void print() { System.out.println("Printing"); }
}
new Document().display();
```

A) Printing  
B) Nothing  
C) Error  
D) display

---

---

# 📝 Answer Key with Explanations

---

### Question 1
**Correct Answer: B) 100**

**Explanation:** Shallow clone shares array reference. a1.arr and a2.arr point to same array.

---

### Question 2
**Correct Answer: B) 0**

**Explanation:** transient fields are not serialized. After deserialization, age gets default value (0).

---

### Question 3
**Correct Answer: B) Object**

**Explanation:** String's superclass is Object. getSimpleName() returns "Object".

---

### Question 4
**Correct Answer: A) true**

**Explanation:** String class has many methods. getDeclaredMethods() returns more than 50.

---

### Question 5
**Correct Answer: A) 10**

**Explanation:** setAccessible(true) bypasses access control. Private field can be read.

---

### Question 6
**Correct Answer: B) B**

**Explanation:** B extends A and overrides m(). C implements B (not A directly for m()). B's m() is used.

---

### Question 7
**Correct Answer: A) All classes compile**

**Explanation:** Overriding can throw narrower exceptions or no exception. FileNotFoundException extends IOException.

---

### Question 8
**Correct Answer: B) Init true**

**Explanation:** Eager initialization - instance created once when class loads. Same instance for both calls.

---

### Question 9
**Correct Answer: A) true**

**Explanation:** String implements Serializable, Comparable, CharSequence. Has interfaces.

---

### Question 10
**Correct Answer: B) RuntimeException thrown**

**Explanation:** Instance block runs before constructor body. Exception thrown before constructor prints.

---

### Question 11
**Correct Answer: A) 10 20**

**Explanation:** Parent implements Serializable, so Child is also serializable. Both fields serialized correctly.

---

### Question 12
**Correct Answer: B) A B C**

**Explanation:** Static blocks run in class loading order: parent first, then children.

---

### Question 13
**Correct Answer: A) true**

**Explanation:** int.class is Class object for primitive int. isPrimitive() returns true.

---

### Question 14
**Correct Answer: A) B**

**Explanation:** B's public m() satisfies interface A's m() requirement. C inherits it.

---

### Question 15
**Correct Answer: C) 0**

**Explanation:** Parent constructor calls overridden print(). B's x not yet initialized (0).

---

### Question 16
**Correct Answer: B) 0**

**Explanation:** Abstract constructor calls abstract method implemented in subclass. B's x not initialized yet.

---

### Question 17
**Correct Answer: C) Compile error**

**Explanation:** Cannot override static method with instance method. Different signatures required.

---

### Question 18
**Correct Answer: B) Object**

**Explanation:** Lambda creates anonymous class. Its superclass is Object.

---

### Question 19
**Correct Answer: A) Hello**

**Explanation:** Reflection creates String object using constructor. Returns "Hello".

---

### Question 20
**Correct Answer: B) 1**

**Explanation:** Enum with field and constructor. ACTIVE has code 1.

---

### Question 21
**Correct Answer: A) A**

**Explanation:** B doesn't override m() (commented out). Inherits A's final method.

---

### Question 22
**Correct Answer: B) Hello**

**Explanation:** concat() returns new String but result not assigned. value unchanged.

---

### Question 23
**Correct Answer: A) Private**

**Explanation:** Private constructor can be called from within the class. Factory method works.

---

### Question 24
**Correct Answer: A) true**

**Explanation:** Same object returns same hashCode. Consistent within JVM session.

---

### Question 25
**Correct Answer: A) true true**

**Explanation:** All three reference same String Pool object after intern().

---

### Question 26
**Correct Answer: A) 10**

**Explanation:** Static variables are not polymorphic. Reference type A determines which x.

---

### Question 27
**Correct Answer: B) Error thrown (not caught)**

**Explanation:** Error is not Exception. catch(Exception) doesn't catch Error.

---

### Question 28
**Correct Answer: B) Integer**

**Explanation:** Specific method (Integer) preferred over varargs. Boxing 10 to Integer.

---

### Question 29
**Correct Answer: B) ArrayStoreException**

**Explanation:** Runtime type is String[]. Cannot store Integer in String array.

---

### Question 30
**Correct Answer: A) true**

**Explanation:** A implements Marker. instanceof returns true for implemented interfaces.

---

### Question 31
**Correct Answer: C) A B**

**Explanation:** Protected constructor accessible in subclass. super() called implicitly first.

---

### Question 32
**Correct Answer: B) Compile error - cannot extend final class**

**Explanation:** final classes cannot be extended. This is by design.

---

### Question 33
**Correct Answer: B) May or may not print Finalize**

**Explanation:** gc() is only a suggestion. Finalization timing is not guaranteed.

---

### Question 34
**Correct Answer: B) Hello World**

**Explanation:** sb1 and sb2 reference same object. append() modifies the object.

---

### Question 35
**Correct Answer: B) true false**

**Explanation:** equals() overridden to compare x (true). == compares references (false).

---

### Question 36
**Correct Answer: A) 10 20**

**Explanation:** y is effectively final (not modified). Local class can access it.

---

### Question 37
**Correct Answer: A) Static nested**

**Explanation:** Static nested class method called directly without outer instance.

---

### Question 38
**Correct Answer: A) 7**

**Explanation:** BiFunction takes two inputs, returns one output. 3 + 4 = 7.

---

### Question 39
**Correct Answer: A) true**

**Explanation:** Method reference creates Predicate. Empty string returns true for isEmpty().

---

### Question 40
**Correct Answer: A) A-static B-static A-instance B-instance A-instance B-instance**

**Explanation:** Static blocks once. Instance blocks for each object creation.

---

### Question 41
**Correct Answer: A) true**

**Explanation:** Every system has at least one processor. Returns positive number.

---

### Question 42
**Correct Answer: A) Number**

**Explanation:** Method resolution uses compile-time type. n declared as Number.

---

### Question 43
**Correct Answer: B) 20**

**Explanation:** Static members accessed via null reference don't throw NPE.

---

### Question 44
**Correct Answer: B) C.m() throws IOException**

**Explanation:** Intersection of exceptions. IOException is subset of Exception.

---

### Question 45
**Correct Answer: C) NullPointerException**

**Explanation:** null passed to varargs is null array, not array with null. Accessing length throws NPE.

---

### Question 46
**Correct Answer: B) Run Run**

**Explanation:** start() creates new thread (runs run()). run() called directly runs in main thread.

---

### Question 47
**Correct Answer: B) Compile error**

**Explanation:** Static interface methods cannot be inherited or called via implementing class.

---

### Question 48
**Correct Answer: B) 0**

**Explanation:** x = x assigns parameter to itself. Instance variable unchanged (default 0).

---

### Question 49
**Correct Answer: A) B**

**Explanation:** super() calls parent constructor (no output). Then prints "B".

---

### Question 50
**Correct Answer: A) Printing**

**Explanation:** Default method display() calls abstract method print(), which is implemented.

---

## 📊 Score Guide

| Score | Level | Next Step |
|-------|-------|-----------|
| 45-50 | Excellent! | Move to Set 7 |
| 35-44 | Good | Review advanced topics |
| 25-34 | Average | More OOP practice needed |
| 0-24 | Needs Work | Review Sets 4-5 |

---

**Difficulty: ⭐⭐⭐⭐⭐ HARDER** | **Next: Set 7 (⭐⭐⭐⭐⭐ Advanced)**
