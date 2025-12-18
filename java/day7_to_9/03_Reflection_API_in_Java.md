# Reflection API in Java

## Table of Contents
1. [What is Reflection API?](#what-is-reflection-api)
2. [Understanding the Analogy](#understanding-the-analogy)
3. [Core Classes and Methods](#core-classes-and-methods)
4. [Getting Class Object](#getting-class-object)
5. [Creating Objects Dynamically](#creating-objects-dynamically)
6. [Accessing Constructors](#accessing-constructors)
7. [Accessing Fields](#accessing-fields)
8. [Accessing Methods](#accessing-methods)
9. [Complete Examples](#complete-examples)
10. [Use Cases](#use-cases)
11. [Disadvantages](#disadvantages)

---

## What is Reflection API?

**Reflection API** in Java allows a program to **inspect and manipulate** classes, methods, and fields at **runtime**, even if their names are unknown at compile time.

### Key Capabilities:
- ✅ Create objects dynamically (even without knowing class name at compile time)
- ✅ Access private methods and fields
- ✅ Invoke methods dynamically
- ✅ Analyze class structure (methods, fields, constructors)
- ✅ Modify field values (even private ones)
- ✅ Create proxy classes

### Official Definition:
> "The Reflection API in Java allows a program to inspect and manipulate classes, methods, and fields at runtime, even if their names are unknown at compile time. It helps in accessing private methods, creating objects dynamically, and analyzing class structure."

---

## Understanding the Analogy

### Human Being vs Execution Environment

**Analogy:** Think of how a human being interacts with an object vs how JVM (execution environment) does.

#### Human Being Perspective:
```java
Car c = new Car();  // I know the class name "Car" at compile time
c.start();          // I know the method name "start()"
```

- Human writes code with **known class names** and **known method names**
- Everything is determined at **compile time**

#### Execution Environment (JVM) Perspective:
- JVM doesn't "know" class names or method names like humans do
- JVM works with `.class` files containing **metadata** (class structure information)
- JVM uses this metadata to create objects, call methods, access fields
- This is exactly what **Reflection API** exposes to programmers!

**Key Insight:**
> Reflection API lets you do what JVM does internally - inspect and manipulate classes using metadata, without knowing names at compile time.

---

## Core Classes and Methods

### 1. `java.lang.Class`

Represents a class or interface. Every type in Java has a corresponding `Class` object.

**Key Methods:**
- `static Class forName(String className)` → Load class dynamically
- `Object newInstance()` → Create object using default constructor (Deprecated in Java 9+)
- `String getName()` → Get class name
- `Constructor[] getConstructors()` → Get public constructors
- `Field[] getFields()` → Get public fields
- `Method[] getMethods()` → Get public methods
- `Constructor getDeclaredConstructor(Class... parameterTypes)` → Get specific constructor

### 2. `java.lang.reflect.Constructor`

Represents a constructor of a class.

**Key Methods:**
- `Object newInstance(Object... args)` → Create object using this constructor
- `Class[] getParameterTypes()` → Get parameter types
- `void setAccessible(boolean flag)` → Access private constructors

### 3. `java.lang.reflect.Field`

Represents a field of a class.

**Key Methods:**
- `Object get(Object obj)` → Get field value
- `void set(Object obj, Object value)` → Set field value
- `void setAccessible(boolean flag)` → Access private fields
- `Class getType()` → Get field type

### 4. `java.lang.reflect.Method`

Represents a method of a class.

**Key Methods:**
- `Object invoke(Object obj, Object... args)` → Invoke method
- `Class[] getParameterTypes()` → Get parameter types
- `Class getReturnType()` → Get return type
- `void setAccessible(boolean flag)` → Access private methods

---

## Getting Class Object

There are **3 ways** to obtain a `Class` object:

### Method 1: Using `Class.forName()`

```java
Class c = Class.forName("java.lang.String");
System.out.println(c.getName());  // java.lang.String
```

**When to use:** When class name is unknown at compile time (e.g., from user input or config file).

### Method 2: Using `.class` Literal

```java
Class c = String.class;
System.out.println(c.getName());  // java.lang.String
```

**When to use:** When you know the class at compile time.

### Method 3: Using `getClass()` Method

```java
String s = "Hello";
Class c = s.getClass();
System.out.println(c.getName());  // java.lang.String
```

**When to use:** When you have an object instance.

---

## Creating Objects Dynamically

### Example 1: Basic Object Creation with Default Constructor

```java
public class ReflectionDemo1 {
    public static void main(String[] args) {
        Class c = null;
        try {
            // Load class at runtime
            c = Class.forName("java.lang.String");
            System.out.println("Class loaded: " + c.getName());
            
            // Create object using default constructor
            Object obj = c.newInstance();  // Deprecated in Java 9+
            
            System.out.println("Object created: " + obj);
            System.out.println("Object type: " + obj.getClass().getName());
            
        } catch (ClassNotFoundException e) {
            System.out.println("Class not found!");
            e.printStackTrace();
        } catch (InstantiationException e) {
            System.out.println("Cannot instantiate!");
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            System.out.println("Cannot access constructor!");
            e.printStackTrace();
        }
    }
}
```

**Output:**
```
Class loaded: java.lang.String
Object created: 
Object type: java.lang.String
```

**Line-by-Line Analysis:**

1. **Line 5:** `Class.forName("java.lang.String")` loads String class
   - JVM searches for `String.class` file
   - Creates `Class` object representing String class
   - Returns reference to this `Class` object

2. **Line 10:** `c.newInstance()` creates object
   - Calls default (no-argument) constructor of String class
   - Returns `Object` reference (must be cast to use specific methods)

3. **Exceptions:**
   - `ClassNotFoundException` → If class doesn't exist
   - `InstantiationException` → If class is abstract or interface
   - `IllegalAccessException` → If constructor is not accessible

---

### Example 2: Dynamic Object Creation Based on User Input

```java
class One {
    public One() {
        System.out.println("One's constructor");
    }
}

class Two {
    public Two() {
        System.out.println("Two's constructor");
    }
}

class Three {
    public Three() {
        System.out.println("Three's constructor");
    }
}

public class ReflectionDemo2 {
    // Factory method - creates object based on className
    static Object createObject(String className) {
        Object object = null;
        try {
            Class classDefinition = Class.forName(className);
            object = classDefinition.newInstance();
        } catch (ClassNotFoundException e) {
            System.out.println("Class not found: " + className);
        } catch (InstantiationException | IllegalAccessException e) {
            System.out.println("Cannot create object");
            e.printStackTrace();
        }
        return object;
    }
    
    public static void main(String[] args) {
        java.util.Scanner sc = new java.util.Scanner(System.in);
        
        System.out.println("Enter class name which you want to instantiate:");
        System.out.println("Options: One, Two, Three");
        String className = sc.next();
        
        Object obj = createObject(className);
        
        if (obj != null) {
            System.out.println("Object created successfully!");
            System.out.println("Object type: " + obj.getClass().getName());
        }
        
        sc.close();
    }
}
```

**Sample Execution:**
```
Enter class name which you want to instantiate:
Options: One, Two, Three
Two
Two's constructor
Object created successfully!
Object type: Two
```

**How It Works:**

1. **Line 24:** User provides class name as String
2. **Line 26:** `Class.forName(className)` loads the class dynamically
3. **Line 27:** `newInstance()` creates object of that class
4. **Result:** Object created without knowing class name at compile time!

**Real-World Use Case:** This pattern is used in:
- **Frameworks** (Spring, Hibernate) → Create beans dynamically
- **JDBC** → Load database drivers dynamically
- **Plugin systems** → Load plugins at runtime

---

## Accessing Constructors

### Example: Invoking Parameterized Constructor

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;

class MyClass {
    private String message;
    
    // Default constructor
    public MyClass() {
        super();
    }
    
    // Parameterized constructor
    public MyClass(String message) {
        super();
        this.message = message;
    }
    
    public String getMessage() {
        return message;
    }
    
    public void setMessage(String message) {
        this.message = message;
    }
    
    @Override
    public String toString() {
        return "MyClass [message=" + message + "]";
    }
}

public class Demo {
    public static void main(String[] args) {
        Class c = null;
        try {
            c = Class.forName("MyClass");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        
        // ===== Method 1: Using default constructor =====
        System.out.println("Instantiate MyClass using default constructor:");
        Object first = null;
        try {
            first = c.newInstance();  // Calls default constructor
        } catch (InstantiationException | IllegalAccessException e1) {
            e1.printStackTrace();
        }
        
        // Downcast and use
        MyClass ref = null;
        if (first instanceof MyClass) {
            ref = (MyClass) first;
        }
        ref.setMessage("hello world");
        System.out.println(ref.getMessage());
        
        // ===== Method 2: Using parameterized constructor =====
        System.out.println("Instantiate MyClass using parameterized constructor:");
        Constructor ctor = null;
        try {
            // Get constructor that takes String parameter
            ctor = c.getDeclaredConstructor(String.class);
        } catch (NoSuchMethodException e) {
            e.printStackTrace();
        } catch (SecurityException e) {
            e.printStackTrace();
        }
        
        Object second = null;
        try {
            // Create object by invoking constructor with argument
            second = ctor.newInstance("welcome");
        } catch (InstantiationException | IllegalAccessException 
                | InvocationTargetException e) {
            e.printStackTrace();
        }
        System.out.println(second);
    }
}
```

**Output:**
```
Instantiate MyClass using default constructor:
hello world
Instantiate MyClass using parameterized constructor:
MyClass [message=welcome]
```

**Line-by-Line Analysis:**

1. **Line 36:** Load `MyClass` using `forName()`
2. **Line 43:** Create object using default constructor
   - `newInstance()` calls no-argument constructor
3. **Line 50-53:** Downcast `Object` to `MyClass` to access specific methods
4. **Line 63:** `getDeclaredConstructor(String.class)` gets constructor taking String parameter
   - Parameter types specified as varargs: `String.class`
   - Returns `Constructor` object
5. **Line 73:** `ctor.newInstance("welcome")` invokes constructor
   - Pass actual arguments: `"welcome"`
   - Creates object with `message` field set to "welcome"

**Key Learning:** Use `getDeclaredConstructor()` to invoke constructors with parameters.

---

## Accessing Fields

### Example: Accessing and Modifying Private Fields

```java
import java.lang.reflect.Field;

class Sample {
    private int num;  // Private field
    private String message;  // Private field
    
    public Sample() {
        this.num = 10;
        this.message = "Hello";
    }
    
    @Override
    public String toString() {
        return "Sample [num=" + num + ", message=" + message + "]";
    }
}

public class ReflectionDemo3 {
    public static void main(String[] args) {
        Sample obj = new Sample();
        System.out.println("Before modification: " + obj);
        
        try {
            // Get Field object for 'num' field
            Field numField = Sample.class.getDeclaredField("num");
            
            // Make private field accessible
            numField.setAccessible(true);
            
            // Modify the field value
            numField.set(obj, 999);
            
            // Get Field object for 'message' field
            Field msgField = Sample.class.getDeclaredField("message");
            msgField.setAccessible(true);
            msgField.set(obj, "Modified!");
            
        } catch (NoSuchFieldException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        }
        
        System.out.println("After modification: " + obj);
    }
}
```

**Output:**
```
Before modification: Sample [num=10, message=Hello]
After modification: Sample [num=999, message=Modified!]
```

**Line-by-Line Analysis:**

1. **Line 25:** `getDeclaredField("num")` gets `Field` object for `num` field
   - Even though `num` is private
2. **Line 28:** `setAccessible(true)` makes private field accessible
   - Without this, you'd get `IllegalAccessException`
3. **Line 31:** `numField.set(obj, 999)` sets field value
   - First parameter: object instance
   - Second parameter: new value
4. **Lines 34-36:** Same process for `message` field

**Warning:** Accessing private fields breaks encapsulation. Use with caution!

---

## Accessing Methods

### Example: Invoking Private Methods

```java
import java.lang.reflect.Method;

class Sample {
    private String secret = "Secret Data";
    
    private void displaySecret() {
        System.out.println("Secret: " + secret);
    }
    
    private int add(int a, int b) {
        return a + b;
    }
}

public class ReflectionDemo4 {
    public static void main(String[] args) {
        Sample obj = new Sample();
        
        try {
            // Get private method with no parameters
            Method method1 = Sample.class.getDeclaredMethod("displaySecret");
            method1.setAccessible(true);  // Make accessible
            method1.invoke(obj);  // Invoke method
            
            // Get private method with parameters
            Method method2 = Sample.class.getDeclaredMethod("add", int.class, int.class);
            method2.setAccessible(true);
            Object result = method2.invoke(obj, 10, 20);  // Pass arguments
            System.out.println("Add result: " + result);
            
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**Output:**
```
Secret: Secret Data
Add result: 30
```

**Line-by-Line Analysis:**

1. **Line 21:** `getDeclaredMethod("displaySecret")` gets method with no parameters
2. **Line 22:** `setAccessible(true)` makes private method accessible
3. **Line 23:** `invoke(obj)` invokes method on `obj` instance
4. **Line 26:** `getDeclaredMethod("add", int.class, int.class)` gets method with 2 int parameters
5. **Line 28:** `invoke(obj, 10, 20)` invokes method with arguments
   - Returns `Object`, so cast if needed

---

## Complete Examples

### Example: Comprehensive Reflection Demo

```java
import java.lang.reflect.*;

class Person {
    private String name;
    private int age;
    
    public Person() {
        this.name = "Unknown";
        this.age = 0;
    }
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    private void greet() {
        System.out.println("Hello, I'm " + name);
    }
    
    @Override
    public String toString() {
        return "Person [name=" + name + ", age=" + age + "]";
    }
}

public class ReflectionDemo5 {
    public static void main(String[] args) {
        try {
            // 1. Get Class object
            Class c = Class.forName("Person");
            System.out.println("Class name: " + c.getName());
            
            // 2. Get all constructors
            Constructor[] constructors = c.getDeclaredConstructors();
            System.out.println("\nConstructors:");
            for (Constructor ctor : constructors) {
                System.out.println("  " + ctor);
            }
            
            // 3. Create object using parameterized constructor
            Constructor ctor = c.getDeclaredConstructor(String.class, int.class);
            Object obj = ctor.newInstance("Alice", 25);
            System.out.println("\nObject created: " + obj);
            
            // 4. Get all fields
            Field[] fields = c.getDeclaredFields();
            System.out.println("\nFields:");
            for (Field field : fields) {
                field.setAccessible(true);
                System.out.println("  " + field.getName() + " = " + field.get(obj));
            }
            
            // 5. Modify private field
            Field nameField = c.getDeclaredField("name");
            nameField.setAccessible(true);
            nameField.set(obj, "Bob");
            System.out.println("\nAfter modifying name: " + obj);
            
            // 6. Get all methods
            Method[] methods = c.getDeclaredMethods();
            System.out.println("\nMethods:");
            for (Method method : methods) {
                System.out.println("  " + method.getName());
            }
            
            // 7. Invoke private method
            Method greetMethod = c.getDeclaredMethod("greet");
            greetMethod.setAccessible(true);
            System.out.println("\nInvoking greet method:");
            greetMethod.invoke(obj);
            
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**Output:**
```
Class name: Person

Constructors:
  public Person(java.lang.String,int)
  public Person()

Object created: Person [name=Alice, age=25]

Fields:
  name = Alice
  age = 25

After modifying name: Person [name=Bob, age=25]

Methods:
  greet
  toString

Invoking greet method:
Hello, I'm Bob
```

**Complete Flow:**

1. **Load class** using `forName()`
2. **Analyze constructors** using `getDeclaredConstructors()`
3. **Create object** using specific constructor
4. **Inspect fields** using `getDeclaredFields()` and read their values
5. **Modify field** using `set()`
6. **Inspect methods** using `getDeclaredMethods()`
7. **Invoke method** using `invoke()`

---

## Use Cases

### 1. Frameworks and Libraries

**Spring Framework:**
```java
// Spring creates beans dynamically using reflection
@Component
public class UserService { }

// Spring uses reflection to:
// 1. Load UserService class
// 2. Create instance
// 3. Inject dependencies
```

### 2. JDBC Database Drivers

```java
// Loading driver at runtime
Class.forName("com.mysql.jdbc.Driver");

// Without reflection, you'd need:
// import com.mysql.jdbc.Driver;  // Hardcoded!
```

### 3. Testing Frameworks

**JUnit:**
```java
// JUnit uses reflection to:
// 1. Find all @Test annotated methods
// 2. Invoke them dynamically
@Test
public void testSomething() { }
```

### 4. Serialization

```java
// ObjectOutputStream uses reflection to:
// 1. Get all fields of object
// 2. Write field values to stream
ObjectOutputStream oos = new ObjectOutputStream(fos);
oos.writeObject(obj);
```

### 5. Dependency Injection

```java
@Autowired
private UserRepository userRepo;

// Framework uses reflection to:
// 1. Find fields with @Autowired
// 2. Create instances
// 3. Set field values
```

---

## Disadvantages

### 1. **Performance Overhead**

Reflection is **slower** than direct code:

```java
// Direct call - Fast
obj.method();

// Reflection call - Slower
Method m = obj.getClass().getMethod("method");
m.invoke(obj);
```

**Reason:** Reflection requires **runtime checking** and **type resolution**.

### 2. **Security Restrictions**

Security managers can prevent reflection:

```java
SecurityManager sm = System.getSecurityManager();
if (sm != null) {
    sm.checkPermission(new ReflectPermission("suppressAccessChecks"));
}
```

### 3. **Breaks Encapsulation**

Accessing private members violates OOP principles:

```java
field.setAccessible(true);  // Bypasses access modifiers!
field.set(obj, value);
```

### 4. **Compile-Time Safety Lost**

Errors detected at runtime, not compile time:

```java
// Typo in method name - no compile-time error!
Method m = c.getMethod("getMame");  // Should be "getName"
// Error only at runtime: NoSuchMethodException
```

### 5. **Code Complexity**

Reflection code is verbose and harder to read:

```java
// Direct code - clear and simple
person.setName("Alice");

// Reflection code - complex
Field nameField = Person.class.getDeclaredField("name");
nameField.setAccessible(true);
nameField.set(person, "Alice");
```

---

## Best Practices

### ✅ DO:

1. **Cache reflection results** (Class, Method, Field objects)
2. **Use for framework development** where flexibility is needed
3. **Handle exceptions properly** (`ClassNotFoundException`, `NoSuchMethodException`, etc.)
4. **Check security permissions** before using reflection

### ❌ DON'T:

1. **Don't use for regular application logic** - performance overhead
2. **Don't access private members unless necessary** - breaks encapsulation
3. **Don't ignore exceptions** - reflection throws many checked exceptions
4. **Don't use if direct code is possible** - use reflection only when necessary

---

## Summary Table

| Operation | Method | Returns |
|-----------|--------|---------|
| Load class | `Class.forName("ClassName")` | `Class` object |
| Create object | `class.newInstance()` | `Object` |
| Get constructor | `class.getDeclaredConstructor(Class...)` | `Constructor` |
| Invoke constructor | `constructor.newInstance(args...)` | `Object` |
| Get field | `class.getDeclaredField("fieldName")` | `Field` |
| Read field value | `field.get(obj)` | `Object` |
| Set field value | `field.set(obj, value)` | `void` |
| Get method | `class.getDeclaredMethod("name", Class...)` | `Method` |
| Invoke method | `method.invoke(obj, args...)` | `Object` |

---

## Key Takeaways

1. **Reflection = Runtime introspection and manipulation** of classes
2. **Use `Class.forName()`** to load classes dynamically
3. **Use `newInstance()`** to create objects (deprecated, use Constructor.newInstance())
4. **Use `setAccessible(true)`** to access private members
5. **Reflection is powerful but slow** - use judiciously
6. **Frameworks use reflection extensively** (Spring, Hibernate, JUnit)
7. **Breaks compile-time safety and encapsulation** - use with caution

---

## Interview Questions

### Q1: What is Reflection API in Java?
**A:** Reflection API allows inspecting and manipulating classes, methods, and fields at runtime, even if their names are unknown at compile time.

### Q2: What are the three ways to get a Class object?
**A:** 
1. `Class.forName("ClassName")`
2. `ClassName.class`
3. `object.getClass()`

### Q3: Why is reflection slow?
**A:** Reflection requires runtime type checking, method lookup, and security checks, which are slower than direct method calls resolved at compile time.

### Q4: What is `setAccessible(true)` used for?
**A:** It bypasses Java's access control checks, allowing access to private fields and methods.

### Q5: Where is Reflection API commonly used?
**A:** Frameworks (Spring, Hibernate), testing frameworks (JUnit), JDBC drivers, serialization, dependency injection, and plugin systems.

### Q6: What is the difference between `getMethod()` and `getDeclaredMethod()`?
**A:** 
- `getMethod()` returns only public methods (including inherited ones)
- `getDeclaredMethod()` returns all methods declared in the class (including private), but not inherited ones

---

**End of Reflection API Notes**
