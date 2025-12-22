# CDAC CCEE MCQ Practice Set 5

## 📝 HARD LEVEL - Collections, Generics & Threading Basics
**Total Questions: 50 | Time Limit: 60 minutes | No Negative Marking**

> **Difficulty: ⭐⭐⭐⭐ Hard** - These questions cover collections behavior, generics, basic threading, and require understanding of internal mechanisms. Demands deeper knowledge.

---

### Question 1
What is the output?
```java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
for(Integer i : list) {
    if(i == 1) list.remove(i);
}
```

A) [2]  
B) []  
C) ConcurrentModificationException  
D) [1, 2]

---

### Question 2
What is the output?
```java
Set<String> set = new HashSet<>();
set.add("A");
set.add("B");
set.add("A");
set.add("C");
System.out.println(set.size());
```

A) 4  
B) 3  
C) 2  
D) Error

---

### Question 3
What is the output?
```java
Map<Integer, String> map = new HashMap<>();
map.put(1, "One");
map.put(1, "First");
System.out.println(map.get(1));
```

A) One  
B) First  
C) null  
D) Error

---

### Question 4
What is the output?
```java
List<Integer> list = Arrays.asList(1, 2, 3);
list.add(4);
```

A) [1, 2, 3, 4]  
B) UnsupportedOperationException  
C) [1, 2, 3]  
D) Compile error

---

### Question 5
What is the output?
```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(3);
pq.add(1);
pq.add(2);
System.out.println(pq.poll());
```

A) 3  
B) 1  
C) 2  
D) Random

---

### Question 6
What is the output?
```java
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");
Iterator<String> it = list.iterator();
while(it.hasNext()) {
    String s = it.next();
    if(s.equals("A")) it.remove();
}
System.out.println(list);
```

A) [A, B]  
B) [B]  
C) ConcurrentModificationException  
D) []

---

### Question 7
What is the output?
```java
class Box<T> {
    T value;
    Box(T value) { this.value = value; }
}
Box<Integer> box = new Box<>(10);
System.out.println(box.value);
```

A) 10  
B) null  
C) Integer  
D) Compile error

---

### Question 8
What is the output?
```java
List<?> list = new ArrayList<String>();
list.add("Hello");
```

A) Adds Hello  
B) Compile error  
C) Runtime error  
D) Works fine

---

### Question 9
What is the output?
```java
List<? extends Number> list = new ArrayList<Integer>();
list.add(10);
```

A) Adds 10  
B) Compile error  
C) Runtime error  
D) Works fine

---

### Question 10
What is the output?
```java
Thread t = new Thread(() -> System.out.println("Hello"));
t.start();
t.start();
```

A) Hello Hello  
B) Hello  
C) IllegalThreadStateException  
D) Nothing

---

### Question 11
What is the output?
```java
Thread t = new Thread(() -> {
    for(int i = 0; i < 3; i++) {
        System.out.print(i + " ");
    }
});
t.run();
```

A) 0 1 2 (in new thread)  
B) 0 1 2 (in main thread)  
C) Nothing  
D) Error

---

### Question 12
What is the output?
```java
Map<String, Integer> map = new LinkedHashMap<>();
map.put("C", 3);
map.put("A", 1);
map.put("B", 2);
for(String key : map.keySet()) {
    System.out.print(key);
}
```

A) ABC  
B) CAB  
C) CBA  
D) Random

---

### Question 13
What is the output?
```java
TreeMap<String, Integer> map = new TreeMap<>();
map.put("C", 3);
map.put("A", 1);
map.put("B", 2);
System.out.println(map.firstKey());
```

A) C  
B) A  
C) B  
D) 1

---

### Question 14
What is the output?
```java
Deque<Integer> dq = new ArrayDeque<>();
dq.addFirst(1);
dq.addLast(2);
dq.addFirst(3);
System.out.println(dq);
```

A) [1, 2, 3]  
B) [3, 1, 2]  
C) [3, 2, 1]  
D) [2, 1, 3]

---

### Question 15
What is the output?
```java
Stack<Integer> stack = new Stack<>();
stack.push(1);
stack.push(2);
stack.push(3);
System.out.println(stack.pop());
System.out.println(stack.peek());
```

A) 3, 2  
B) 1, 1  
C) 3, 3  
D) 1, 2

---

### Question 16
What is the output?
```java
List<Integer> list = new ArrayList<>();
list.add(10);
list.add(20);
list.remove(Integer.valueOf(10));
System.out.println(list);
```

A) [20]  
B) [10]  
C) IndexOutOfBoundsException  
D) Error

---

### Question 17
What is the output?
```java
class Counter {
    int count = 0;
    void increment() { count++; }
}
Counter c = new Counter();
Thread t1 = new Thread(() -> { for(int i=0; i<1000; i++) c.increment(); });
Thread t2 = new Thread(() -> { for(int i=0; i<1000; i++) c.increment(); });
t1.start(); t2.start();
t1.join(); t2.join();
System.out.println(c.count);
```

A) 2000  
B) Less than or equal to 2000  
C) Compile error  
D) 1000

---

### Question 18
What is the output?
```java
synchronized(this) {
    System.out.println("Hello");
}
```
In a static context?

A) Hello  
B) Compile error  
C) Runtime error  
D) Nothing

---

### Question 19
What is the output?
```java
Thread.currentThread().sleep(1000);
System.out.println("Done");
```

A) Done (after 1 second)  
B) Compile error - must handle InterruptedException  
C) Done (immediately)  
D) Nothing

---

### Question 20
What is the output?
```java
Thread t = new Thread();
System.out.println(t.getState());
```

A) RUNNABLE  
B) NEW  
C) RUNNING  
D) BLOCKED

---

### Question 21
What is the output?
```java
List<Integer> list = Collections.synchronizedList(new ArrayList<>());
list.add(1);
list.add(2);
System.out.println(list.size());
```

A) 2  
B) 0  
C) Exception  
D) Random

---

### Question 22
What is the output?
```java
Set<Integer> set1 = new HashSet<>(Arrays.asList(1, 2, 3));
Set<Integer> set2 = new HashSet<>(Arrays.asList(2, 3, 4));
set1.retainAll(set2);
System.out.println(set1);
```

A) [1, 2, 3]  
B) [2, 3]  
C) [1, 2, 3, 4]  
D) [4]

---

### Question 23
What is the output?
```java
EnumSet<Day> days = EnumSet.of(Day.MON, Day.TUE);
System.out.println(days.size());
```
Where Day is an enum with 7 days.

A) 7  
B) 2  
C) 0  
D) Compile error

---

### Question 24
What is the output?
```java
Comparator<String> comp = (a, b) -> b.compareTo(a);
List<String> list = Arrays.asList("A", "C", "B");
Collections.sort(list, comp);
System.out.println(list.get(0));
```

A) A  
B) B  
C) C  
D) Error

---

### Question 25
What is the output?
```java
class Person implements Comparable<Person> {
    int age;
    Person(int age) { this.age = age; }
    public int compareTo(Person p) { return this.age - p.age; }
}
TreeSet<Person> set = new TreeSet<>();
set.add(new Person(30));
set.add(new Person(20));
System.out.println(set.first().age);
```

A) 30  
B) 20  
C) ClassCastException  
D) Error

---

### Question 26
What is the output?
```java
Map<String, Integer> map = new HashMap<>();
map.put("A", 1);
map.put("B", 2);
map.put("C", 3);
map.remove("B");
System.out.println(map.containsKey("B"));
```

A) true  
B) false  
C) null  
D) Error

---

### Question 27
What is the output?
```java
List<String> list = new CopyOnWriteArrayList<>();
list.add("A");
list.add("B");
for(String s : list) {
    list.add("C");
}
System.out.println(list.size());
```

A) 2  
B) 4  
C) ConcurrentModificationException  
D) Infinite loop

---

### Question 28
What is the output?
```java
BlockingQueue<Integer> queue = new ArrayBlockingQueue<>(2);
queue.offer(1);
queue.offer(2);
System.out.println(queue.offer(3));
```

A) true  
B) false  
C) Exception  
D) Blocks forever

---

### Question 29
What is the output?
```java
AtomicInteger count = new AtomicInteger(0);
count.incrementAndGet();
count.incrementAndGet();
System.out.println(count.get());
```

A) 0  
B) 1  
C) 2  
D) Error

---

### Question 30
What is the output?
```java
Thread t = new Thread(() -> {
    try {
        Thread.sleep(5000);
    } catch(InterruptedException e) {
        System.out.println("Interrupted");
    }
});
t.start();
t.interrupt();
```

A) Interrupted  
B) Nothing  
C) InterruptedException  
D) Sleeps 5 seconds

---

### Question 31
What is the output?
```java
Optional<String> opt = Optional.of("Hello");
System.out.println(opt.orElse("World"));
```

A) Hello  
B) World  
C) Optional[Hello]  
D) null

---

### Question 32
What is the output?
```java
Optional<String> opt = Optional.empty();
System.out.println(opt.orElse("Default"));
```

A) null  
B) Default  
C) Optional.empty  
D) Exception

---

### Question 33
What is the output?
```java
Stream.of(1, 2, 3).filter(x -> x > 1).count();
```

A) 1  
B) 2  
C) 3  
D) Error

---

### Question 34
What is the output?
```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
int sum = list.stream().filter(x -> x % 2 == 0).mapToInt(x -> x).sum();
System.out.println(sum);
```

A) 15  
B) 6  
C) 9  
D) 2

---

### Question 35
What is the output?
```java
Thread t = new Thread();
t.setDaemon(true);
t.start();
System.out.println(t.isDaemon());
```

A) true  
B) false  
C) Exception  
D) Cannot set daemon

---

### Question 36
What is the output?
```java
ReentrantLock lock = new ReentrantLock();
lock.lock();
lock.lock();
System.out.println(lock.getHoldCount());
```

A) 1  
B) 2  
C) Exception  
D) Deadlock

---

### Question 37
What is the output?
```java
Map<String, Integer> map = new HashMap<>();
map.put("A", 1);
Integer val = map.getOrDefault("B", 0);
System.out.println(val);
```

A) null  
B) 0  
C) 1  
D) Exception

---

### Question 38
What is the output?
```java
Map<String, Integer> map = new HashMap<>();
map.put("A", 1);
map.compute("A", (k, v) -> v + 10);
System.out.println(map.get("A"));
```

A) 1  
B) 10  
C) 11  
D) null

---

### Question 39
What is the output?
```java
List<String> list = Arrays.asList("A", "B", "C");
String result = list.stream().reduce("", (a, b) -> a + b);
System.out.println(result);
```

A) ABC  
B) A  
C) CBA  
D) Error

---

### Question 40
What is the output?
```java
ExecutorService es = Executors.newFixedThreadPool(2);
es.submit(() -> System.out.println("Task 1"));
es.submit(() -> System.out.println("Task 2"));
es.shutdown();
```

A) Task 1 Task 2 (in order)  
B) May print in any order  
C) Nothing  
D) Exception

---

### Question 41
What is the output?
```java
Future<Integer> future = Executors.newSingleThreadExecutor().submit(() -> 10);
System.out.println(future.get());
```

A) 10  
B) null  
C) Future  
D) Exception

---

### Question 42
What is the output?
```java
List<Integer> list = new ArrayList<>(List.of(3, 1, 4, 1, 5));
Collections.sort(list);
System.out.println(list.get(0));
```

A) 3  
B) 1  
C) 5  
D) 4

---

### Question 43
What is the output?
```java
NavigableSet<Integer> set = new TreeSet<>();
set.add(1); set.add(2); set.add(3); set.add(4); set.add(5);
System.out.println(set.floor(3));
```

A) 2  
B) 3  
C) 4  
D) null

---

### Question 44
What is the output?
```java
WeakHashMap<String, Integer> map = new WeakHashMap<>();
String key = new String("key");
map.put(key, 1);
key = null;
System.gc();
System.out.println(map.size());
```

A) 1  
B) 0 (probably)  
C) null  
D) Exception

---

### Question 45
What is the output?
```java
ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
map.put("A", 1);
map.putIfAbsent("A", 2);
System.out.println(map.get("A"));
```

A) 1  
B) 2  
C) null  
D) Exception

---

### Question 46
What is the output?
```java
CountDownLatch latch = new CountDownLatch(2);
latch.countDown();
latch.countDown();
System.out.println(latch.getCount());
```

A) 2  
B) 1  
C) 0  
D) Exception

---

### Question 47
What is the output?
```java
Semaphore sem = new Semaphore(2);
sem.acquire();
sem.acquire();
System.out.println(sem.availablePermits());
```

A) 2  
B) 1  
C) 0  
D) Exception

---

### Question 48
What is the output?
```java
CompletableFuture<String> cf = CompletableFuture.supplyAsync(() -> "Hello");
System.out.println(cf.get());
```

A) Hello  
B) CompletableFuture  
C) null  
D) Exception

---

### Question 49
What is the output?
```java
IdentityHashMap<String, Integer> map = new IdentityHashMap<>();
String s1 = new String("key");
String s2 = new String("key");
map.put(s1, 1);
map.put(s2, 2);
System.out.println(map.size());
```

A) 1  
B) 2  
C) 0  
D) Error

---

### Question 50
What is the output?
```java
List<Integer> list = Arrays.asList(1, 2, 3);
list.stream().parallel().forEach(System.out::print);
```

A) 123  
B) May print in any order  
C) Exception  
D) 321

---

---

# 📝 Answer Key with Explanations

---

### Question 1
**Correct Answer: C) ConcurrentModificationException**

**Explanation:** Modifying collection during for-each iteration causes ConcurrentModificationException.

---

### Question 2
**Correct Answer: B) 3**

**Explanation:** HashSet ignores duplicates. "A" appears twice but stored once. Set: {A, B, C}, size 3.

---

### Question 3
**Correct Answer: B) First**

**Explanation:** HashMap replaces value for existing key. Key 1 was "One", updated to "First".

---

### Question 4
**Correct Answer: B) UnsupportedOperationException**

**Explanation:** Arrays.asList returns fixed-size list. add() is not supported.

---

### Question 5
**Correct Answer: B) 1**

**Explanation:** PriorityQueue is min-heap by default. poll() returns smallest element (1).

---

### Question 6
**Correct Answer: B) [B]**

**Explanation:** Iterator.remove() is safe way to remove during iteration. No exception.

---

### Question 7
**Correct Answer: A) 10**

**Explanation:** Generic class stores and retrieves value correctly. Prints 10.

---

### Question 8
**Correct Answer: B) Compile error**

**Explanation:** Unbounded wildcard (?) means unknown type. Cannot add except null.

---

### Question 9
**Correct Answer: B) Compile error**

**Explanation:** Upper bounded wildcard (extends) is for reading. Cannot add because exact type unknown.

---

### Question 10
**Correct Answer: C) IllegalThreadStateException**

**Explanation:** Thread can only be started once. Second start() throws IllegalThreadStateException.

---

### Question 11
**Correct Answer: B) 0 1 2 (in main thread)**

**Explanation:** Calling run() directly doesn't create new thread. Runs in current thread.

---

### Question 12
**Correct Answer: B) CAB**

**Explanation:** LinkedHashMap maintains insertion order. Keys were inserted C, A, B.

---

### Question 13
**Correct Answer: B) A**

**Explanation:** TreeMap sorts by keys. First key alphabetically is "A".

---

### Question 14
**Correct Answer: B) [3, 1, 2]**

**Explanation:** addFirst(1)→[1], addLast(2)→[1,2], addFirst(3)→[3,1,2].

---

### Question 15
**Correct Answer: A) 3, 2**

**Explanation:** pop() removes and returns top (3). peek() returns top without removing (2).

---

### Question 16
**Correct Answer: A) [20]**

**Explanation:** Integer.valueOf(10) creates object. remove(Object) removes by value, not index.

---

### Question 17
**Correct Answer: B) Less than or equal to 2000**

**Explanation:** Race condition - increment is not atomic. count++ is read-modify-write, may lose updates.

---

### Question 18
**Correct Answer: B) Compile error**

**Explanation:** 'this' doesn't exist in static context. Cannot use synchronized(this).

---

### Question 19
**Correct Answer: B) Compile error - must handle InterruptedException**

**Explanation:** sleep() throws InterruptedException (checked). Must be caught or declared.

---

### Question 20
**Correct Answer: B) NEW**

**Explanation:** Thread created but not started is in NEW state.

---

### Question 21
**Correct Answer: A) 2**

**Explanation:** synchronizedList works correctly for single-threaded usage. Size is 2.

---

### Question 22
**Correct Answer: B) [2, 3]**

**Explanation:** retainAll keeps only elements in both sets (intersection). {1,2,3} ∩ {2,3,4} = {2,3}.

---

### Question 23
**Correct Answer: B) 2**

**Explanation:** EnumSet.of creates set with specified constants. Only MON and TUE, size 2.

---

### Question 24
**Correct Answer: C) C**

**Explanation:** Comparator reverses order (b.compareTo(a)). Sorted descending: [C, B, A]. First is C.

---

### Question 25
**Correct Answer: B) 20**

**Explanation:** TreeSet sorts by natural order (compareTo). Smaller age first. first() returns age 20.

---

### Question 26
**Correct Answer: B) false**

**Explanation:** Key "B" was removed. containsKey("B") returns false.

---

### Question 27
**Correct Answer: B) 4**

**Explanation:** CopyOnWriteArrayList is thread-safe. Iterator uses snapshot. Two original + two added = 4.

---

### Question 28
**Correct Answer: B) false**

**Explanation:** ArrayBlockingQueue capacity is 2. offer() returns false when full (doesn't block).

---

### Question 29
**Correct Answer: C) 2**

**Explanation:** AtomicInteger provides thread-safe operations. Two increments = 2.

---

### Question 30
**Correct Answer: A) Interrupted**

**Explanation:** interrupt() sets interrupt flag. Thread catches InterruptedException when sleeping.

---

### Question 31
**Correct Answer: A) Hello**

**Explanation:** Optional contains value. orElse returns contained value, not the default.

---

### Question 32
**Correct Answer: B) Default**

**Explanation:** Empty Optional has no value. orElse returns the default "Default".

---

### Question 33
**Correct Answer: B) 2**

**Explanation:** filter(x > 1) keeps [2, 3]. count() returns 2.

---

### Question 34
**Correct Answer: B) 6**

**Explanation:** filter keeps even numbers [2, 4]. sum = 2 + 4 = 6.

---

### Question 35
**Correct Answer: A) true**

**Explanation:** setDaemon(true) before start() makes it daemon. isDaemon() returns true.

---

### Question 36
**Correct Answer: B) 2**

**Explanation:** ReentrantLock is reentrant - same thread can lock multiple times. Hold count is 2.

---

### Question 37
**Correct Answer: B) 0**

**Explanation:** getOrDefault returns default if key absent. "B" not in map, returns 0.

---

### Question 38
**Correct Answer: C) 11**

**Explanation:** compute applies function to existing value. 1 + 10 = 11.

---

### Question 39
**Correct Answer: A) ABC**

**Explanation:** reduce concatenates with identity "". "" + "A" + "B" + "C" = "ABC".

---

### Question 40
**Correct Answer: B) May print in any order**

**Explanation:** Thread pool with 2 threads. Tasks may execute in any order.

---

### Question 41
**Correct Answer: A) 10**

**Explanation:** Callable returns value. future.get() blocks and returns result (10).

---

### Question 42
**Correct Answer: B) 1**

**Explanation:** After sorting: [1, 1, 3, 4, 5]. First element is 1.

---

### Question 43
**Correct Answer: B) 3**

**Explanation:** floor(3) returns greatest element <= 3. That's 3 itself.

---

### Question 44
**Correct Answer: B) 0 (probably)**

**Explanation:** WeakHashMap uses weak keys. After key=null and GC, entry may be removed.

---

### Question 45
**Correct Answer: A) 1**

**Explanation:** putIfAbsent doesn't replace existing value. "A" already has 1, stays 1.

---

### Question 46
**Correct Answer: C) 0**

**Explanation:** Two countDowns bring count to 0. getCount() returns 0.

---

### Question 47
**Correct Answer: C) 0**

**Explanation:** Two permits acquired from Semaphore(2). availablePermits() returns 0.

---

### Question 48
**Correct Answer: A) Hello**

**Explanation:** supplyAsync runs asynchronously, returns "Hello". get() retrieves it.

---

### Question 49
**Correct Answer: B) 2**

**Explanation:** IdentityHashMap uses == not equals(). s1 and s2 are different objects, both stored.

---

### Question 50
**Correct Answer: B) May print in any order**

**Explanation:** parallel() creates parallel stream. forEach doesn't guarantee order.

---

## 📊 Score Guide

| Score | Level | Next Step |
|-------|-------|-----------|
| 45-50 | Excellent! | Move to Set 6 |
| 35-44 | Good | Review weak areas, then Set 6 |
| 25-34 | Average | More practice on collections |
| 0-24 | Needs Work | Review Sets 3-4 |

---

**Difficulty: ⭐⭐⭐⭐ HARD** | **Next: Set 6 (⭐⭐⭐⭐⭐ Harder)**
