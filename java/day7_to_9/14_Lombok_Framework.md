# Lombok Framework in Java

## What is Lombok?

**Lombok** = Library that reduces boilerplate code using annotations

### Purpose:
- Eliminates need to write getters/setters
- Auto-generates constructors
- Reduces repetitive code

## Installation

### Maven Dependency

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.30</version>
    <scope>provided</scope>
</dependency>
```

### IDE Plugin
- **IntelliJ IDEA:** Install Lombok plugin
- **Eclipse:** Download lombok.jar, run installer

## Common Annotations

### @Getter and @Setter

```java
import lombok.Getter;
import lombok.Setter;

@Getter @Setter
public class User {
    private String name;
    private int age;
}

// Generates:
// public String getName() { return name; }
// public void setName(String name) { this.name = name; }
// public int getAge() { return age; }
// public void setAge(int age) { this.age = age; }
```

### @ToString

```java
import lombok.ToString;

@ToString
public class Person {
    private String name;
    private int age;
}

// Generates:
// public String toString() {
//     return "Person(name=" + name + ", age=" + age + ")";
// }
```

### @EqualsAndHashCode

```java
import lombok.EqualsAndHashCode;

@EqualsAndHashCode
public class Product {
    private String id;
    private String name;
}

// Generates equals() and hashCode() methods
```

### @NoArgsConstructor

```java
import lombok.NoArgsConstructor;

@NoArgsConstructor
public class Employee {
    private String name;
}

// Generates:
// public Employee() { }
```

### @AllArgsConstructor

```java
import lombok.AllArgsConstructor;

@AllArgsConstructor
public class Employee {
    private String name;
    private int salary;
}

// Generates:
// public Employee(String name, int salary) {
//     this.name = name;
//     this.salary = salary;
// }
```

### @RequiredArgsConstructor

```java
import lombok.RequiredArgsConstructor;

@RequiredArgsConstructor
public class Service {
    private final Repository repo;  // final or @NonNull
    private String temp;  // not included
}

// Generates:
// public Service(Repository repo) {
//     this.repo = repo;
// }
```

### @Data

**Combines: @Getter + @Setter + @ToString + @EqualsAndHashCode + @RequiredArgsConstructor**

```java
import lombok.Data;

@Data
public class Student {
    private String name;
    private int age;
    private String major;
}

// Generates ALL: getters, setters, toString, equals, hashCode
```

### @Builder

```java
import lombok.Builder;

@Builder
public class Car {
    private String brand;
    private String model;
    private int year;
}

// Usage:
Car car = Car.builder()
    .brand("Toyota")
    .model("Camry")
    .year(2023)
    .build();
```

### @Slf4j (Logging)

```java
import lombok.extern.slf4j.Slf4j;

@Slf4j
public class MyService {
    public void doSomething() {
        log.info("Doing something");
        log.error("Error occurred");
    }
}

// Generates:
// private static final org.slf4j.Logger log = 
//     org.slf4j.LoggerFactory.getLogger(MyService.class);
```

### @Value (Immutable)

```java
import lombok.Value;

@Value
public class Point {
    int x;
    int y;
}

// Generates:
// - final class
// - All fields are private final
// - Getters (no setters)
// - Constructor
// - toString, equals, hashCode
```

## Before vs After Lombok

### Before Lombok:

```java
public class Person {
    private String name;
    private int age;
    
    public Person() { }
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    public int getAge() {
        return age;
    }
    
    public void setAge(int age) {
        this.age = age;
    }
    
    @Override
    public String toString() {
        return "Person(name=" + name + ", age=" + age + ")";
    }
    
    @Override
    public boolean equals(Object o) {
        // ... 10+ lines of equals logic
    }
    
    @Override
    public int hashCode() {
        // ... hashCode logic
    }
}
```

### After Lombok:

```java
import lombok.Data;

@Data
public class Person {
    private String name;
    private int age;
}
```

**60+ lines reduced to 6 lines!**

## Key Points

1. **Reduces boilerplate** (getters, setters, constructors, etc.)
2. **@Data** most commonly used (all-in-one)
3. **@Builder** for builder pattern
4. **@Value** for immutable classes
5. **Requires IDE plugin** for proper support
6. **Compile-time annotation processing** (no runtime overhead)

## Advantages

✅ **Less code** to write and maintain  
✅ **Cleaner classes** focus on business logic  
✅ **Less error-prone** (no manual getters/setters)  
✅ **Faster development**  

## Disadvantages

❌ **IDE dependency** (needs plugin)  
❌ **Debugging harder** (generated code not visible)  
❌ **Team familiarity** required  

---

**End of Lombok Framework**
