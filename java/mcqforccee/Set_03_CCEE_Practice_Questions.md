# CDAC CCEE MCQ Practice Set 3

## 📝 MODERATE LEVEL - OOP Concepts & Method Behavior
**Total Questions: 50 | Time Limit: 60 minutes | No Negative Marking**

> **Difficulty: ⭐⭐⭐ Moderate** - These questions test OOP principles, constructor behavior, inheritance basics, and method interactions. Requires thinking about object relationships.

---

### Question 1
What is the output?
```java
class A {
    int x;
    A(int x) { this.x = x; }
}
A obj = new A();
```

A) Creates object with x = 0  
B) Compile error - no default constructor  
C) Runtime error  
D) Creates object with x = null

---

### Question 2
What is the output?
```java
class Parent {
    void show() { System.out.println("Parent"); }
}
class Child extends Parent {
    void show() { System.out.println("Child"); }
}
Parent p = new Child();
p.show();
```

A) Parent  
B) Child  
C) Compile error  
D) Parent Child

---

### Question 3
What is the output?
```java
class Test {
    static int count = 0;
    Test() { count++; }
}
new Test();
new Test();
new Test();
System.out.println(Test.count);
```

A) 0  
B) 1  
C) 3  
D) Error

---

### Question 4
What is the output?
```java
String s1 = new String("Hello");
String s2 = new String("Hello");
System.out.println(s1 == s2);
```

A) true  
B) false  
C) Hello  
D) Error

---

### Question 5
What is the output?
```java
class A { int x = 10; }
class B extends A { int x = 20; }
B obj = new B();
System.out.println(obj.x + " " + ((A)obj).x);
```

A) 20 20  
B) 10 10  
C) 20 10  
D) 10 20

---

### Question 6
What is the output?
```java
class Test {
    void m(int x) { System.out.print("int "); }
    void m(long x) { System.out.print("long "); }
}
new Test().m(5);
```

A) int  
B) long  
C) Compile error  
D) int long

---

### Question 7
What is the output?
```java
class A {
    A() { System.out.print("A "); }
}
class B extends A {
    B() { System.out.print("B "); }
}
new B();
```

A) B  
B) A  
C) A B  
D) B A

---

### Question 8
What is the output?
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
System.out.println(sb);
```

A) Hello  
B) Hello World  
C) World  
D) Error

---

### Question 9
What is the output?
```java
String s = "Hello";
s.concat(" World");
System.out.println(s);
```

A) Hello  
B) Hello World  
C) World  
D) Error

---

### Question 10
What is the output?
```java
Integer a = 127;
Integer b = 127;
System.out.println(a == b);
```

A) true  
B) false  
C) 127  
D) Error

---

### Question 11
What is the output?
```java
class A {
    private void show() { System.out.println("A"); }
}
class B extends A {
    void show() { System.out.println("B"); }
}
B obj = new B();
obj.show();
```

A) A  
B) B  
C) A B  
D) Compile error

---

### Question 12
What is the output?
```java
final int x = 10;
x = 20;
System.out.println(x);
```

A) 10  
B) 20  
C) Compile error  
D) Runtime error

---

### Question 13
What is the output?
```java
class Test {
    int x = 10;
    void m() {
        int x = 20;
        System.out.println(x);
    }
}
new Test().m();
```

A) 10  
B) 20  
C) Compile error  
D) 0

---

### Question 14
What is the output?
```java
abstract class A {
    abstract void show();
}
class B extends A {
    void show() { System.out.println("B"); }
}
A obj = new B();
obj.show();
```

A) A  
B) B  
C) Compile error  
D) Nothing

---

### Question 15
What is the output?
```java
interface I {
    void m();
}
class A implements I {
    public void m() { System.out.println("A"); }
}
I obj = new A();
obj.m();
```

A) A  
B) Nothing  
C) Compile error  
D) I

---

### Question 16
What is the output?
```java
class A {
    void show() { System.out.println("A"); }
}
class B extends A {
}
class C extends B {
    void show() { System.out.println("C"); }
}
A obj = new C();
obj.show();
```

A) A  
B) C  
C) Compile error  
D) B

---

### Question 17
What is the output?
```java
try {
    System.out.println("Try");
} finally {
    System.out.println("Finally");
}
```

A) Try  
B) Finally  
C) Try Finally  
D) Compile error

---

### Question 18
What is the output?
```java
try {
    int x = 10 / 0;
    System.out.println("After");
} catch(ArithmeticException e) {
    System.out.println("Catch");
}
```

A) After  
B) Catch  
C) After Catch  
D) Error

---

### Question 19
What is the output?
```java
String[] arr = {"A", "B", "C"};
for(String s : arr) {
    System.out.print(s);
}
```

A) A B C  
B) ABC  
C) 0 1 2  
D) Error

---

### Question 20
What is the output?
```java
class Test {
    static void m() { System.out.println("Static"); }
}
Test t = null;
t.m();
```

A) Static  
B) NullPointerException  
C) Compile error  
D) Nothing

---

### Question 21
What is the output?
```java
interface A { int X = 10; }
class B implements A {
    void show() { System.out.println(X); }
}
new B().show();
```

A) 10  
B) 0  
C) Compile error  
D) null

---

### Question 22
What is the output?
```java
class A {
    int x = 10;
    A() { display(); }
    void display() { System.out.println(x); }
}
new A();
```

A) 0  
B) 10  
C) Compile error  
D) null

---

### Question 23
What is the output?
```java
String s = "Hello";
System.out.println(s instanceof String);
```

A) true  
B) false  
C) Hello  
D) Error

---

### Question 24
What is the output?
```java
Object obj = "Hello";
System.out.println(obj instanceof String);
```

A) true  
B) false  
C) Compile error  
D) Runtime error

---

### Question 25
What is the output?
```java
class A {
    void m(Object o) { System.out.print("Object "); }
    void m(String s) { System.out.print("String "); }
}
new A().m("Hello");
```

A) Object  
B) String  
C) Object String  
D) Compile error

---

### Question 26
What is the output?
```java
class A {
    static { System.out.print("Static "); }
    { System.out.print("Instance "); }
    A() { System.out.print("Constructor"); }
}
new A();
```

A) Constructor  
B) Static Instance Constructor  
C) Instance Static Constructor  
D) Static Constructor Instance

---

### Question 27
What is the output?
```java
int[] arr = {1, 2, 3};
int[] arr2 = arr;
arr2[0] = 10;
System.out.println(arr[0]);
```

A) 1  
B) 10  
C) Error  
D) 0

---

### Question 28
What is the output?
```java
String s = "Java";
s = s.toUpperCase();
System.out.println(s);
```

A) Java  
B) JAVA  
C) java  
D) Error

---

### Question 29
What is the output?
```java
class A {
    int x;
    A() { x = 5; }
    A(int x) { this.x = x; }
}
A a = new A();
System.out.println(a.x);
```

A) 0  
B) 5  
C) Compile error  
D) null

---

### Question 30
What is the output?
```java
class A {
    void show() { System.out.println("A"); }
}
class B extends A {
    void show() { 
        super.show();
        System.out.println("B"); 
    }
}
new B().show();
```

A) A  
B) B  
C) A B  
D) B A

---

### Question 31
What is the output?
```java
int x = 10;
int y = (x > 5) ? 100 : 200;
System.out.println(y);
```

A) 10  
B) 100  
C) 200  
D) true

---

### Question 32
What is the output?
```java
ArrayList<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);
System.out.println(list.get(1));
```

A) 1  
B) 2  
C) 3  
D) Error

---

### Question 33
What is the output?
```java
class Test {
    int x;
    Test m() {
        x = 10;
        return this;
    }
}
Test t = new Test().m();
System.out.println(t.x);
```

A) 0  
B) 10  
C) null  
D) Error

---

### Question 34
What is the output?
```java
interface A { 
    void m1(); 
}
interface B { 
    void m2(); 
}
class C implements A, B {
    public void m1() { System.out.print("1 "); }
    public void m2() { System.out.print("2"); }
}
C c = new C();
c.m1();
c.m2();
```

A) 1  
B) 2  
C) 1 2  
D) Compile error

---

### Question 35
What is the output?
```java
String s = null;
if(s != null && s.length() > 0) {
    System.out.println("Valid");
} else {
    System.out.println("Invalid");
}
```

A) Valid  
B) Invalid  
C) NullPointerException  
D) Error

---

### Question 36
What is the output?
```java
HashSet<Integer> set = new HashSet<>();
set.add(1);
set.add(2);
set.add(1);
System.out.println(set.size());
```

A) 1  
B) 2  
C) 3  
D) Error

---

### Question 37
What is the output?
```java
enum Day { MON, TUE, WED }
System.out.println(Day.MON.ordinal());
```

A) MON  
B) 0  
C) 1  
D) Monday

---

### Question 38
What is the output?
```java
class A {
    final void show() { System.out.println("A"); }
}
class B extends A {
    void show() { System.out.println("B"); }
}
```

A) A  
B) B  
C) Compile error  
D) Runtime error

---

### Question 39
What is the output?
```java
class Test {
    void m(int... x) {
        System.out.println(x.length);
    }
}
new Test().m(1, 2, 3, 4, 5);
```

A) 1  
B) 5  
C) Error  
D) 15

---

### Question 40
What is the output?
```java
String s = "Hello World";
String[] arr = s.split(" ");
System.out.println(arr.length);
```

A) 1  
B) 2  
C) 11  
D) Error

---

### Question 41
What is the output?
```java
class Outer {
    int x = 10;
    class Inner {
        void show() { System.out.println(x); }
    }
}
Outer.Inner in = new Outer().new Inner();
in.show();
```

A) 0  
B) 10  
C) Compile error  
D) null

---

### Question 42
What is the output?
```java
Double d = Double.parseDouble("10.5");
System.out.println(d + 5);
```

A) 10.55  
B) 15.5  
C) Error  
D) 10.5

---

### Question 43
What is the output?
```java
class A {
    void m(int x) { System.out.print("int "); }
    void m(double x) { System.out.print("double "); }
}
new A().m(10.0f);
```

A) int  
B) double  
C) Compile error  
D) Both

---

### Question 44
What is the output?
```java
HashMap<String, Integer> map = new HashMap<>();
map.put("A", 1);
map.put("B", 2);
map.put("A", 3);
System.out.println(map.get("A"));
```

A) 1  
B) 2  
C) 3  
D) Error

---

### Question 45
What is the output?
```java
class A {}
class B extends A {}
A obj = new B();
System.out.println(obj instanceof B);
```

A) true  
B) false  
C) Compile error  
D) Runtime error

---

### Question 46
What is the output?
```java
int x = 5;
System.out.println(x << 1);
```

A) 5  
B) 10  
C) 2  
D) 1

---

### Question 47
What is the output?
```java
String s = "  Hello  ";
System.out.println("[" + s.trim() + "]");
```

A) [  Hello  ]  
B) [Hello]  
C) Hello  
D) Error

---

### Question 48
What is the output?
```java
try {
    throw new RuntimeException();
} catch(Exception e) {
    System.out.println("Caught");
}
```

A) RuntimeException  
B) Caught  
C) Compile error  
D) Uncaught exception

---

### Question 49
What is the output?
```java
class A {
    int x = 10;
    void m() { System.out.println(this.x); }
}
new A().m();
```

A) 0  
B) 10  
C) this.x  
D) Error

---

### Question 50
What is the output?
```java
class Test implements Comparable<Test> {
    int x;
    Test(int x) { this.x = x; }
    public int compareTo(Test t) { return this.x - t.x; }
}
Test t1 = new Test(5);
Test t2 = new Test(3);
System.out.println(t1.compareTo(t2));
```

A) 0  
B) 2  
C) -2  
D) 5

---

---

# 📝 Answer Key with Explanations

---

### Question 1
**Correct Answer: B) Compile error - no default constructor**

**Explanation:** When you define a parameterized constructor, Java doesn't provide a default constructor. `new A()` requires a no-arg constructor which doesn't exist.

---

### Question 2
**Correct Answer: B) Child**

**Explanation:** Runtime polymorphism - the method called depends on the actual object type (Child), not reference type (Parent).

---

### Question 3
**Correct Answer: C) 3**

**Explanation:** Static variable is shared. Each constructor increments count. Three objects = count becomes 3.

---

### Question 4
**Correct Answer: B) false**

**Explanation:** `new String()` creates new objects on heap (not in String Pool). Different objects, so == returns false.

---

### Question 5
**Correct Answer: C) 20 10**

**Explanation:** Variables are not polymorphic. obj.x gets B's x (20). Casting to A and accessing x gets A's x (10).

---

### Question 6
**Correct Answer: A) int**

**Explanation:** Method overloading with 5 (int literal). Java chooses the most specific match (int) over long.

---

### Question 7
**Correct Answer: C) A B**

**Explanation:** Child constructor implicitly calls super() first. Parent's constructor runs, then Child's.

---

### Question 8
**Correct Answer: B) Hello World**

**Explanation:** StringBuilder is mutable. append() modifies the same object and adds " World".

---

### Question 9
**Correct Answer: A) Hello**

**Explanation:** String is immutable. concat() returns a new String but s still refers to the original "Hello".

---

### Question 10
**Correct Answer: A) true**

**Explanation:** Integer caching: values -128 to 127 are cached. Both a and b reference the same cached object.

---

### Question 11
**Correct Answer: B) B**

**Explanation:** Private methods are not inherited. B's show() is a new method, not an override. It prints "B".

---

### Question 12
**Correct Answer: C) Compile error**

**Explanation:** final variables cannot be reassigned. Attempting to change x causes compile error.

---

### Question 13
**Correct Answer: B) 20**

**Explanation:** Local variable x shadows instance variable x. Inside m(), x refers to local variable (20).

---

### Question 14
**Correct Answer: B) B**

**Explanation:** Abstract class reference can point to concrete subclass object. B's show() is called.

---

### Question 15
**Correct Answer: A) A**

**Explanation:** Interface reference can hold implementing class object. A's m() implementation is called.

---

### Question 16
**Correct Answer: B) C**

**Explanation:** C overrides A's show() (skipping B). Dynamic dispatch calls C's show().

---

### Question 17
**Correct Answer: C) Try Finally**

**Explanation:** try-finally without catch is valid. Both blocks execute normally.

---

### Question 18
**Correct Answer: B) Catch**

**Explanation:** Division by zero throws ArithmeticException. Catch block handles it. "After" is never reached.

---

### Question 19
**Correct Answer: B) ABC**

**Explanation:** Enhanced for-each loop iterates elements. print() without newline outputs ABC.

---

### Question 20
**Correct Answer: A) Static**

**Explanation:** Static methods belong to class, not instance. Can be called via null reference without exception.

---

### Question 21
**Correct Answer: A) 10**

**Explanation:** Interface variables are implicitly public static final. X is accessible to implementing class.

---

### Question 22
**Correct Answer: B) 10**

**Explanation:** Instance variable initialization happens before constructor body. x is 10 when display() is called from constructor.

---

### Question 23
**Correct Answer: A) true**

**Explanation:** s is a String object. instanceof confirms s is an instance of String class.

---

### Question 24
**Correct Answer: A) true**

**Explanation:** Object obj actually refers to a String. instanceof checks the actual object type, which is String.

---

### Question 25
**Correct Answer: B) String**

**Explanation:** Most specific method is chosen. String is more specific than Object, so m(String) is called.

---

### Question 26
**Correct Answer: B) Static Instance Constructor**

**Explanation:** Order: static block (once per class), instance block (each object), constructor.

---

### Question 27
**Correct Answer: B) 10**

**Explanation:** Arrays are reference types. arr and arr2 point to same array. Modifying through arr2 affects arr.

---

### Question 28
**Correct Answer: B) JAVA**

**Explanation:** toUpperCase() returns new String. Assigning back to s updates the reference.

---

### Question 29
**Correct Answer: B) 5**

**Explanation:** No-arg constructor A() is called, which sets x = 5.

---

### Question 30
**Correct Answer: C) A B**

**Explanation:** B's show() calls super.show() first (prints "A"), then prints "B".

---

### Question 31
**Correct Answer: B) 100**

**Explanation:** 10 > 5 is true, so y = 100.

---

### Question 32
**Correct Answer: B) 2**

**Explanation:** ArrayList is 0-indexed. get(1) returns element at index 1, which is 2.

---

### Question 33
**Correct Answer: B) 10**

**Explanation:** Method chaining - m() sets x=10 and returns this. t.x is 10.

---

### Question 34
**Correct Answer: C) 1 2**

**Explanation:** Class implements both interfaces and provides both methods. Both are called.

---

### Question 35
**Correct Answer: B) Invalid**

**Explanation:** Short-circuit evaluation: s != null is false, so s.length() is never called. No exception.

---

### Question 36
**Correct Answer: B) 2**

**Explanation:** HashSet doesn't allow duplicates. Adding 1 twice keeps only one. Size is 2.

---

### Question 37
**Correct Answer: B) 0**

**Explanation:** ordinal() returns the position of enum constant (0-indexed). MON is first, so 0.

---

### Question 38
**Correct Answer: C) Compile error**

**Explanation:** final methods cannot be overridden. B trying to override A's final show() causes error.

---

### Question 39
**Correct Answer: B) 5**

**Explanation:** Varargs receives 5 arguments as array. x.length is 5.

---

### Question 40
**Correct Answer: B) 2**

**Explanation:** split(" ") separates by space. "Hello World" becomes ["Hello", "World"], length 2.

---

### Question 41
**Correct Answer: B) 10**

**Explanation:** Inner class can access outer class members. x is accessed and prints 10.

---

### Question 42
**Correct Answer: B) 15.5**

**Explanation:** parseDouble returns 10.5. Adding 5 gives 15.5.

---

### Question 43
**Correct Answer: B) double**

**Explanation:** float literal 10.0f is widened to double (no float overload available). double version is called.

---

### Question 44
**Correct Answer: C) 3**

**Explanation:** HashMap replaces value for duplicate key. "A" was 1, updated to 3.

---

### Question 45
**Correct Answer: A) true**

**Explanation:** obj is actually a B object. instanceof checks actual type, not reference type.

---

### Question 46
**Correct Answer: B) 10**

**Explanation:** Left shift by 1 = multiply by 2. 5 << 1 = 10.

---

### Question 47
**Correct Answer: B) [Hello]**

**Explanation:** trim() removes leading/trailing spaces. Result is "Hello" within brackets.

---

### Question 48
**Correct Answer: B) Caught**

**Explanation:** RuntimeException extends Exception. catch(Exception) catches it.

---

### Question 49
**Correct Answer: B) 10**

**Explanation:** this.x refers to instance variable x, which is 10.

---

### Question 50
**Correct Answer: B) 2**

**Explanation:** compareTo returns this.x - t.x = 5 - 3 = 2. Positive means t1 > t2.

---

## 📊 Score Guide

| Score | Level | Next Step |
|-------|-------|-----------|
| 45-50 | Excellent! | Move to Set 4 |
| 35-44 | Good | Review OOP concepts, then Set 4 |
| 25-34 | Average | More practice on inheritance |
| 0-24 | Needs Work | Review Sets 1-2 first |

---

**Difficulty: ⭐⭐⭐ MODERATE** | **Next: Set 4 (⭐⭐⭐⭐ Moderate-Hard)**
