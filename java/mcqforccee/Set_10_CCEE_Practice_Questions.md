# CDAC CCEE MCQ Practice Set 10

## 📝 ULTIMATE LEVEL - The Final Challenge
**Total Questions: 50 | Time Limit: 60 minutes | No Negative Marking**

> **Difficulty: 🔥🔥🔥 Ultimate** - The most challenging questions combining all Java concepts. These will make you think deeply about language semantics, corner cases, and the interplay of multiple features. Only for those who have mastered Sets 1-9!

---

### Question 1
What is the output?
```java
class A {
    static int x = 10;
    A() { x += getIncrement(); }
    int getIncrement() { return 1; }
}
class B extends A {
    static int x = 20;
    int getIncrement() { return 2; }
}
System.out.println(A.x + " " + B.x);
```
After `new B();`

A) 12 20  
B) 10 22  
C) 11 20  
D) 10 20

---

### Question 2
What is the output?
```java
class A {
    { System.out.print("A1 "); }
    static { System.out.print("A2 "); }
    A() { System.out.print("A3 "); }
}
class B extends A {
    { System.out.print("B1 "); }
    static { System.out.print("B2 "); }
    B() { System.out.print("B3 "); }
}
new B();
new B();
```

A) A2 B2 A1 A3 B1 B3 A1 A3 B1 B3  
B) A2 B2 A1 A3 B1 B3 A2 B2 A1 A3 B1 B3  
C) A1 A2 A3 B1 B2 B3  
D) A2 A1 A3 B2 B1 B3

---

### Question 3
What is the output?
```java
try {
    try {
        throw new RuntimeException("A");
    } catch(RuntimeException e) {
        throw new RuntimeException("B");
    } finally {
        throw new RuntimeException("C");
    }
} catch(Exception e) {
    System.out.println(e.getMessage());
}
```

A) A  
B) B  
C) C  
D) A B C

---

### Question 4
What is the output?
```java
interface A { void m(); }
interface B { void m(); }
class C {
    public void m(A a) { System.out.print("A "); a.m(); }
    public void m(B b) { System.out.print("B "); b.m(); }
}
new C().m((A & B) () -> System.out.println("Lambda"));
```

A) A Lambda  
B) B Lambda  
C) Compile error - ambiguous  
D) Lambda

---

### Question 5
What is the output?
```java
String s1 = "Hello";
String s2 = new String("Hello");
String s3 = s2.intern();
System.out.println((s1 == s2) + " " + (s1 == s3) + " " + (s2 == s3));
```

A) false true false  
B) false false false  
C) true true true  
D) false true true

---

### Question 6
What is the output?
```java
class Holder {
    int x = getVal();
    int getVal() { return 10; }
}
class Child extends Holder {
    int y = 20;
    int getVal() { return y; }
}
System.out.println(new Child().x);
```

A) 10  
B) 20  
C) 0  
D) Error

---

### Question 7
What is the output?
```java
TreeSet<String> set = new TreeSet<>((a, b) -> {
    int cmp = a.length() - b.length();
    return cmp != 0 ? cmp : a.compareTo(b);
});
set.add("abc");
set.add("ab");
set.add("abcd");
set.add("ab");
System.out.println(set);
```

A) [ab, abc, abcd]  
B) [abcd, abc, ab]  
C) [ab, ab, abc, abcd]  
D) [abc, ab, abcd]

---

### Question 8
What is the output?
```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
list.stream()
    .peek(x -> System.out.print(x + " "))
    .filter(x -> x > 3)
    .peek(x -> System.out.print(x + " "))
    .findFirst();
```

A) 1 2 3 4 4  
B) 1 2 3 4 4 5 5  
C) 4 5  
D) 1 2 3 4 5 4 5

---

### Question 9
What is the output?
```java
class A {
    private static int x = 0;
    { x++; }
    public static int getX() { return x; }
}
new A();
new A();
new A();
System.out.println(A.getX());
```

A) 0  
B) 1  
C) 3  
D) Error

---

### Question 10
What is the output?
```java
interface A { int m(); }
class B {
    int x = 10;
    A getA() {
        return () -> x;
    }
}
B b = new B();
A a = b.getA();
b.x = 20;
System.out.println(a.m());
```

A) 10  
B) 20  
C) 0  
D) Error

---

### Question 11
What is the output?
```java
Map<String, Integer> map = new HashMap<>();
map.put("a", 1);
map.put("b", 2);
map.put("c", 3);
map.computeIfPresent("a", (k, v) -> null);
map.computeIfAbsent("d", k -> 4);
System.out.println(map);
```

A) {a=null, b=2, c=3, d=4}  
B) {b=2, c=3, d=4}  
C) {a=1, b=2, c=3, d=4}  
D) {b=2, c=3}

---

### Question 12
What is the output?
```java
class A {
    void m() { System.out.println("A"); }
}
class B extends A {
    void m() { System.out.println("B"); }
}
class C extends A {
    void m() { System.out.println("C"); }
}
A[] arr = {new A(), new B(), new C()};
for(A a : arr) a.m();
```

A) A A A  
B) A B C  
C) Compile error  
D) B C A

---

### Question 13
What is the output?
```java
double d1 = 0.0 * Double.POSITIVE_INFINITY;
double d2 = Double.POSITIVE_INFINITY + Double.NEGATIVE_INFINITY;
System.out.println(d1 + " " + d2);
```

A) Infinity, 0.0  
B) NaN, NaN  
C) 0.0, NaN  
D) Error

---

### Question 14
What is the output?
```java
class A {
    int x = 10;
    void m(A a) { a.x = 20; }
}
A a1 = new A();
A a2 = a1;
a1.m(a1);
a1 = new A();
System.out.println(a2.x);
```

A) 10  
B) 20  
C) 0  
D) NullPointerException

---

### Question 15
What is the output?
```java
Boolean b = null;
if(b != null && b) {
    System.out.println("True");
} else if(b != null && !b) {
    System.out.println("False");
} else {
    System.out.println("Null");
}
```

A) True  
B) False  
C) Null  
D) NullPointerException

---

### Question 16
What is the output?
```java
class A {
    void m(CharSequence cs) { System.out.print("CS "); }
    void m(String s) { System.out.print("String "); }
}
CharSequence cs = "Hello";
new A().m(cs);
new A().m("Hello");
```

A) CS String  
B) String String  
C) CS CS  
D) String CS

---

### Question 17
What is the output?
```java
Set<List<Integer>> set = new HashSet<>();
List<Integer> list1 = new ArrayList<>();
list1.add(1);
set.add(list1);
List<Integer> list2 = new ArrayList<>();
list2.add(1);
set.add(list2);
System.out.println(set.size());
```

A) 1  
B) 2  
C) 0  
D) Error

---

### Question 18
What is the output?
```java
class Counter {
    private int count = 0;
    public synchronized void inc() { count++; }
    public int get() { return count; }
}
```
Is get() thread-safe?

A) Yes, reads are atomic  
B) No, may see stale value  
C) Yes, int is primitive  
D) Depends on JVM

---

### Question 19
What is the output?
```java
Optional.ofNullable(null)
    .map(s -> s.toString())
    .orElseGet(() -> "Default");
```

A) null  
B) Default  
C) NullPointerException  
D) ""

---

### Question 20
What is the output?
```java
List<String> list = List.of("a", "b", "c");
list.replaceAll(String::toUpperCase);
```

A) ["A", "B", "C"]  
B) UnsupportedOperationException  
C) ["a", "b", "c"]  
D) Compile error

---

### Question 21
What is the output?
```java
class A {
    static void m(Object... objs) {
        System.out.println(objs == null);
        System.out.println(objs.length);
    }
}
A.m(null);
A.m((Object) null);
```

A) true, NullPointerException; false, 1  
B) false, 1; true, NullPointerException  
C) true, 0; false, 1  
D) Error

---

### Question 22
What is the output?
```java
interface A { void m(); }
interface B { void m() throws IOException; }
class C implements A, B {
    public void m() { System.out.println("C"); }
}
B b = new C();
b.m();
```

A) C  
B) Compile error - must handle IOException  
C) IOException  
D) C (but must handle exception)

---

### Question 23
What is the output?
```java
Comparator<String> c = Comparator.comparingInt(String::length)
    .thenComparing(String::compareTo);
List<String> list = Arrays.asList("bc", "a", "abc");
list.sort(c);
System.out.println(list);
```

A) [a, bc, abc]  
B) [abc, bc, a]  
C) [a, abc, bc]  
D) [bc, a, abc]

---

### Question 24
What is the output?
```java
class A<T extends Number & Comparable<T>> {
    T max(T a, T b) {
        return a.compareTo(b) > 0 ? a : b;
    }
}
System.out.println(new A<Integer>().max(5, 10));
```

A) 5  
B) 10  
C) Compile error  
D) 0

---

### Question 25
What is the output?
```java
class A {
    String s = "Hello";
    void m() {
        class B {
            void print() { System.out.println(s); }
        }
        s = "World";
        new B().print();
    }
}
new A().m();
```

A) Hello  
B) World  
C) Compile error  
D) null

---

### Question 26
What is the output?
```java
interface Func<T, R> { R apply(T t); }
Func<Integer, Integer> f = x -> x * 2;
Func<Integer, Integer> g = x -> x + 1;
System.out.println(f.apply(g.apply(5)));
```

A) 11  
B) 12  
C) 10  
D) 6

---

### Question 27
What is the output?
```java
record Point(int x, int y) {
    public Point {
        System.out.print("Canonical ");
    }
    public Point(int x) {
        this(x, 0);
        System.out.print("Single ");
    }
}
new Point(1);
```

A) Canonical  
B) Single  
C) Canonical Single  
D) Single Canonical

---

### Question 28
What is the output?
```java
String[] arr = new String[]{"a", "b", "c"};
Stream.of(arr).forEach(s -> {
    if(s.equals("b")) return;
    System.out.print(s);
});
```

A) abc  
B) ac  
C) a  
D) Error

---

### Question 29
What is the output?
```java
class A {
    protected void m() { System.out.println("A"); }
}
class B extends A {
    public void m() { System.out.println("B"); }
}
A a = new B();
((A) a).m();
```

A) A  
B) B  
C) Compile error  
D) Both

---

### Question 30
What is the output?
```java
enum Status {
    ON(1) {
        void action() { System.out.println("Turning on"); }
    },
    OFF(0) {
        void action() { System.out.println("Turning off"); }
    };
    int code;
    Status(int code) { this.code = code; }
    abstract void action();
}
Status.ON.action();
System.out.println(Status.OFF.code);
```

A) Turning on, 0  
B) 1, Turning off  
C) Turning on, 1  
D) Error

---

### Question 31
What is the output?
```java
ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
map.put("a", 1);
map.forEach(1, (k, v) -> {
    if(k.equals("a")) map.put("b", 2);
});
System.out.println(map.size());
```

A) 1  
B) 2  
C) ConcurrentModificationException  
D) Depends

---

### Question 32
What is the output?
```java
IntStream.iterate(0, i -> i < 5, i -> i + 1)
    .forEach(System.out::print);
```

A) 01234  
B) 012345  
C) 0  
D) Infinite loop

---

### Question 33
What is the output?
```java
class A {
    static void m() { throw new RuntimeException("A"); }
    static { m(); }
}
try {
    Class.forName("A");
} catch(Throwable t) {
    System.out.println(t.getClass().getSimpleName());
}
```

A) RuntimeException  
B) ExceptionInInitializerError  
C) ClassNotFoundException  
D) Error

---

### Question 34
What is the output?
```java
class A {
    int[] arr = new int[]{1, 2, 3};
    A() { arr = new int[]{4, 5, 6}; }
}
A a = new A();
System.out.println(a.arr[0]);
```

A) 1  
B) 4  
C) 0  
D) Error

---

### Question 35
What is the output?
```java
String s = """
    Line 1
    Line 2
    """;
System.out.println(s.contains("\n"));
```

A) true  
B) false  
C) Error  
D) Depends on OS

---

### Question 36
What is the output?
```java
class Outer {
    private int x = 10;
    Runnable r = () -> {
        int x = 20;
        System.out.println(x + " " + this.x);
    };
}
new Outer().r.run();
```

A) 20 10  
B) 10 10  
C) 20 20  
D) Error

---

### Question 37
What is the output?
```java
List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
ListIterator<Integer> it = list.listIterator(list.size());
while(it.hasPrevious()) {
    System.out.print(it.previous() + " ");
}
```

A) 1 2 3 4 5  
B) 5 4 3 2 1  
C) 5  
D) Error

---

### Question 38
What is the output?
```java
Map<String, String> m1 = Map.of("a", "1", "b", "2");
Map<String, String> m2 = Map.of("a", "1", "b", "2");
System.out.println(m1.equals(m2));
System.out.println(m1 == m2);
```

A) true true  
B) true false  
C) false false  
D) false true

---

### Question 39
What is the output?
```java
Stream<String> s1 = Stream.of("a", "b");
Stream<String> s2 = Stream.of("c", "d");
Stream.concat(s1, s2)
    .peek(System.out::print)
    .filter(x -> x.equals("c"))
    .findFirst();
```

A) abcd  
B) abc  
C) c  
D) ab

---

### Question 40
What is the output?
```java
class A {
    void m(Number n) { System.out.println("Number"); }
}
class B extends A {
    void m(Object o) { System.out.println("Object"); }
}
B b = new B();
b.m(10);
```

A) Number  
B) Object  
C) Compile error  
D) Object Number

---

### Question 41
What is the output?
```java
ThreadLocal<Integer> tl = ThreadLocal.withInitial(() -> 0);
Thread t = new Thread(() -> {
    tl.set(10);
    System.out.println(tl.get());
});
t.start();
t.join();
System.out.println(tl.get());
```

A) 10, 10  
B) 10, 0  
C) 0, 0  
D) Error

---

### Question 42
What is the output?
```java
class A {
    static final int X;
    static {
        X = compute();
    }
    static int compute() {
        return X + 10;
    }
}
System.out.println(A.X);
```

A) 10  
B) 0  
C) Compile error  
D) 20

---

### Question 43
What is the output?
```java
int x = 5;
int y = ~x + 1;
System.out.println(y);
```

A) -5  
B) -6  
C) 5  
D) 4

---

### Question 44
What is the output?
```java
class A implements Serializable {
    private void writeObject(ObjectOutputStream oos) throws IOException {
        System.out.println("Writing");
        oos.defaultWriteObject();
    }
}
new ObjectOutputStream(new ByteArrayOutputStream()).writeObject(new A());
```

A) Writing  
B) Nothing  
C) Exception  
D) Error

---

### Question 45
What is the output?
```java
Supplier<Stream<Integer>> supplier = () -> Stream.of(1, 2, 3);
supplier.get().forEach(System.out::print);
System.out.println();
supplier.get().forEach(System.out::print);
```

A) 123, IllegalStateException  
B) 123, 123  
C) 123  
D) Error

---

### Question 46
What is the output?
```java
class A {
    int val;
    A(int val) { this.val = val; }
    public boolean equals(Object o) {
        return o instanceof A && ((A)o).val == this.val;
    }
    public int hashCode() { return val % 2; }
}
Set<A> set = new HashSet<>();
set.add(new A(1));
set.add(new A(3));
set.add(new A(5));
System.out.println(set.size());
```

A) 1  
B) 3  
C) 2  
D) Error

---

### Question 47
What is the output?
```java
Object o = (Predicate<String>) String::isEmpty;
System.out.println(o instanceof Serializable);
```

A) true  
B) false  
C) Compile error  
D) ClassCastException

---

### Question 48
What is the output?
```java
class A {
    void m(List<?> list) { System.out.println("Wildcard"); }
    void m(List<Object> list) { System.out.println("Object"); }
}
List<Object> list = new ArrayList<>();
new A().m(list);
```

A) Wildcard  
B) Object  
C) Compile error - ambiguous  
D) Both

---

### Question 49
What is the output?
```java
sealed class A permits B, C {}
non-sealed class B extends A {}
final class C extends A {}
class D extends B {}
System.out.println(new D() instanceof A);
```

A) true  
B) false  
C) Compile error  
D) Runtime error

---

### Question 50
What is the output?
```java
var list = new ArrayList<String>();
list.add("Hello");
var result = list.stream()
    .map(s -> {
        if(s.length() > 10) throw new RuntimeException();
        return s.toUpperCase();
    })
    .findFirst()
    .map(String::length)
    .orElse(-1);
System.out.println(result);
```

A) HELLO  
B) 5  
C) -1  
D) RuntimeException

---

---

# 📝 Answer Key with Explanations

---

### Question 1
**Correct Answer: A) 12 20**

**Explanation:** Constructor calls overridden getIncrement() returning 2. A.x = 10 + 2 = 12. B.x unchanged at 20.

---

### Question 2
**Correct Answer: A) A2 B2 A1 A3 B1 B3 A1 A3 B1 B3**

**Explanation:** Static blocks only once. Instance/constructor blocks run for each new object.

---

### Question 3
**Correct Answer: C) C**

**Explanation:** Finally exception "C" suppresses catch exception "B". Only "C" propagates.

---

### Question 4
**Correct Answer: A) A Lambda**

**Explanation:** Cast to intersection type. First interface (A) is used for method resolution.

---

### Question 5
**Correct Answer: A) false true false**

**Explanation:** s1 != s2 (new object). s1 == s3 (intern returns pool). s2 != s3 (new vs pool).

---

### Question 6
**Correct Answer: C) 0**

**Explanation:** Parent's x = getVal() calls overridden method. Child's y not yet initialized (0).

---

### Question 7
**Correct Answer: A) [ab, abc, abcd]**

**Explanation:** Custom comparator: by length first, then alphabetically. Duplicate "ab" ignored.

---

### Question 8
**Correct Answer: A) 1 2 3 4 4**

**Explanation:** Short-circuit. Processes 1,2,3,4 until find first >3. Prints on both peeks.

---

### Question 9
**Correct Answer: C) 3**

**Explanation:** Instance block increments static x. Three objects = x incremented 3 times.

---

### Question 10
**Correct Answer: B) 20**

**Explanation:** Lambda captures reference to b, not value. When x changes, lambda sees new value.

---

### Question 11
**Correct Answer: B) {b=2, c=3, d=4}**

**Explanation:** computeIfPresent returning null removes entry. computeIfAbsent adds d.

---

### Question 12
**Correct Answer: B) A B C**

**Explanation:** Polymorphism. Each object's actual type's m() is called.

---

### Question 13
**Correct Answer: B) NaN, NaN**

**Explanation:** 0 × Infinity and Infinity - Infinity are both indeterminate = NaN.

---

### Question 14
**Correct Answer: B) 20**

**Explanation:** a2 references same object as original a1. x changed to 20. a1 reassigned but a2 still has modified object.

---

### Question 15
**Correct Answer: C) Null**

**Explanation:** Short-circuit prevents NPE. b != null is false, so else branch taken.

---

### Question 16
**Correct Answer: A) CS String**

**Explanation:** Method resolution uses compile-time type. cs is CharSequence, literal is String.

---

### Question 17
**Correct Answer: A) 1**

**Explanation:** ArrayList equals/hashCode based on contents. Both lists equal, so duplicate not added.

---

### Question 18
**Correct Answer: B) No, may see stale value**

**Explanation:** Without synchronization on get(), changes from inc() may not be visible.

---

### Question 19
**Correct Answer: B) Default**

**Explanation:** null mapped to Optional.empty(). map skipped. orElseGet returns "Default".

---

### Question 20
**Correct Answer: B) UnsupportedOperationException**

**Explanation:** List.of creates immutable list. replaceAll attempts modification.

---

### Question 21
**Correct Answer: A) true, NullPointerException; false, 1**

**Explanation:** m(null) treats null as the array itself. m((Object)null) treats null as one element.

---

### Question 22
**Correct Answer: D) C (but must handle exception)**

**Explanation:** Calling via B reference requires handling IOException (even though C doesn't throw).

---

### Question 23
**Correct Answer: A) [a, bc, abc]**

**Explanation:** Sort by length first: a(1), bc(2), abc(3). Then alphabetically within same length.

---

### Question 24
**Correct Answer: B) 10**

**Explanation:** Multiple bounds work. Integer satisfies both. max returns larger value.

---

### Question 25
**Correct Answer: B) World**

**Explanation:** s is instance variable (not local). Not final constraint. Sees "World".

---

### Question 26
**Correct Answer: B) 12**

**Explanation:** g.apply(5) = 6. f.apply(6) = 12.

---

### Question 27
**Correct Answer: C) Canonical Single**

**Explanation:** Single-arg constructor calls canonical. Canonical executes first.

---

### Question 28
**Correct Answer: B) ac**

**Explanation:** return in forEach lambda only exits that iteration. Prints a and c.

---

### Question 29
**Correct Answer: B) B**

**Explanation:** Dynamic dispatch. Cast doesn't change actual object type. B's m() called.

---

### Question 30
**Correct Answer: A) Turning on, 0**

**Explanation:** Enum with abstract methods. ON.action() prints message. OFF.code is 0.

---

### Question 31
**Correct Answer: B) 2**

**Explanation:** ConcurrentHashMap allows modification during iteration. "b" added.

---

### Question 32
**Correct Answer: A) 01234**

**Explanation:** iterate with predicate (Java 9+). Runs while i < 5.

---

### Question 33
**Correct Answer: B) ExceptionInInitializerError**

**Explanation:** Static initializer exception wrapped in ExceptionInInitializerError.

---

### Question 34
**Correct Answer: B) 4**

**Explanation:** Field init then constructor. Constructor overwrites arr with {4,5,6}.

---

### Question 35
**Correct Answer: A) true**

**Explanation:** Text block with newlines. Contains \n between lines.

---

### Question 36
**Correct Answer: A) 20 10**

**Explanation:** Local x = 20. this.x is Outer's x = 10.

---

### Question 37
**Correct Answer: B) 5 4 3 2 1**

**Explanation:** ListIterator starting at end, iterating backwards.

---

### Question 38
**Correct Answer: B) true false**

**Explanation:** Map.of equality based on contents (true). Different instances (false).

---

### Question 39
**Correct Answer: B) abc**

**Explanation:** Short-circuit. Processes until first match "c".

---

### Question 40
**Correct Answer: A) Number**

**Explanation:** Overloading in B. Number more specific than Object for Integer.

---

### Question 41
**Correct Answer: B) 10, 0**

**Explanation:** ThreadLocal per-thread. Child thread has 10, main thread has initial value 0.

---

### Question 42
**Correct Answer: A) 10**

**Explanation:** compute() uses X (0 before assignment) + 10 = 10. X assigned 10.

---

### Question 43
**Correct Answer: A) -5**

**Explanation:** Two's complement negation: ~x + 1 = -x. ~5 + 1 = -5.

---

### Question 44
**Correct Answer: A) Writing**

**Explanation:** Custom writeObject called during serialization.

---

### Question 45
**Correct Answer: B) 123, 123**

**Explanation:** Supplier creates new stream each time. Both usable.

---

### Question 46
**Correct Answer: B) 3**

**Explanation:** Same hashCode (1%2=1, 3%2=1, 5%2=1) but different equals (different vals). All added.

---

### Question 47
**Correct Answer: B) false**

**Explanation:** Lambda not cast to Serializable. Not serializable by default.

---

### Question 48
**Correct Answer: B) Object**

**Explanation:** List<Object> more specific than List<?>. Object version called.

---

### Question 49
**Correct Answer: A) true**

**Explanation:** B is non-sealed, allowing D. D extends A through B.

---

### Question 50
**Correct Answer: B) 5**

**Explanation:** "Hello" length <= 10, no exception. map to uppercase, map to length = 5.

---

## 🎉 Congratulations!

You've completed all 10 MCQ practice sets - **500 comprehensive questions** progressing from basic to ultimate difficulty!

### Your Journey:
| Set | Difficulty | Focus |
|-----|------------|-------|
| 1 | ⭐ Basic | Definitions |
| 2 | ⭐⭐ Easy-Moderate | Code output |
| 3 | ⭐⭐⭐ Moderate | OOP concepts |
| 4 | ⭐⭐⭐⭐ Moderate-Hard | Tricky scenarios |
| 5 | ⭐⭐⭐⭐ Hard | Collections/Generics |
| 6 | ⭐⭐⭐⭐⭐ Harder | Reflection/JVM |
| 7 | ⭐⭐⭐⭐⭐ Advanced | Threading |
| 8 | 🔥 Expert | Edge cases |
| 9 | 🔥🔥 Master | Brain teasers |
| 10 | 🔥🔥🔥 Ultimate | Everything combined |

---

*You're ready for the CDAC CCEE exam! Good luck!* 🚀🎯
