# Serialization in Java

## What is Serialization?

**Serialization** = Converting an object into a byte stream for storage or transmission

**Deserialization** = Converting byte stream back into object

### Use Cases:
- Save object to file (persistence)
- Send object over network
- Store object in database
- Caching

## Serializable Interface

**Marker interface** (no methods) that signals JVM to allow serialization

```java
import java.io.Serializable;

class Person implements Serializable {
    private String name;
    private int age;
    
    // Constructor, getters, setters...
}
```

## Serialization Process

```java
// Create object
Person person = new Person("Alice", 25);

// Serialize
FileOutputStream fos = new FileOutputStream("person.ser");
ObjectOutputStream oos = new ObjectOutputStream(fos);
oos.writeObject(person);
oos.close();
```

## Deserialization Process

```java
// Deserialize
FileInputStream fis = new FileInputStream("person.ser");
ObjectInputStream ois = new ObjectInputStream(fis);
Person person = (Person) ois.readObject();
ois.close

();

System.out.println(person.getName());  // Alice
```

## What Gets Serialized?

✅ **Serialized:**
- Class name
- serialVersionUID
- Non-static, non-transient fields

❌ **NOT Serialized:**
- Static fields
- Transient fields
- Methods

## transient Keyword

**Prevents field from being serialized**

```java
class User implements Serializable {
    private String username;
    private transient String password;  // NOT serialized
}
```

## serialVersionUID

**Version number for class compatibility**

```java
private static final long serialVersionUID = 1L;
```

**Purpose:** Ensures sender and receiver have compatible class versions

## Key Points

1. Class must implement `Serializable`
2. All fields are serialized except `static` and `transient`
3. Use `transient` for sensitive data
4. `serialVersionUID` for version control
5. Inheritance: Parent class fields serialized if parent implements `Serializable`

---

**End of Serialization in Java**
