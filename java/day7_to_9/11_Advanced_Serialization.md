# Advanced Serialization in Java

## Externalizable Interface

**More control over serialization process**

```java
import java.io.Externalizable;
import java.io.ObjectInput;
import java.io.ObjectOutput;

class Employee implements Externalizable {
    private String name;
    private int salary;
    
    public Employee() { }  // Mandatory default constructor
    
    @Override
    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeObject(name);
        out.writeInt(salary);
    }
    
    @Override
    public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
        name = (String) in.readObject();
        salary = in.readInt();
    }
}
```

## Serializable vs Externalizable

| Aspect | Serializable | Externalizable |
|--------|--------------|----------------|
| **Methods** | None (marker) | writeExternal(), readExternal() |
| **Control** | Automatic | Manual |
| **Default constructor** | Not required | **Required** |
| **Performance** | Slower | Faster |
| **Use case** | Simple objects | Complex/large objects |

## Custom Serialization

**Override writeObject() and readObject() for Serializable**

```java
class Account implements Serializable {
    private String accountNumber;
    private transient String password;
    
    private void writeObject(ObjectOutputStream oos) throws IOException {
        oos.defaultWriteObject();  // Serialize normal fields
        // Custom logic: encrypt password before writing
        String encrypted = encrypt(password);
        oos.writeObject(encrypted);
    }
    
    private void readObject(ObjectInputStream ois) 
            throws IOException, ClassNotFoundException {
        ois.defaultReadObject();  // Deserialize normal fields
        // Custom logic: decrypt password after reading
        String encrypted = (String) ois.readObject();
        password = decrypt(encrypted);
    }
}
```

## serialVersionUID

**Handling Version Changes**

### Compatible Changes:
✅ Adding new fields  
✅ Adding methods  
✅ Changing field from transient to non-transient  

### Incompatible Changes:
❌ Deleting fields  
❌ Changing field type  
❌ Changing class hierarchy  

**If incompatible change:** `InvalidClassException` thrown during deserialization

## Enum Serialization

**Enums are special:**

```java
enum Season implements Serializable {  // Actually don't need to implement
    SPRING, SUMMER, FALL, WINTER
}
```

- Enums are **implicitly serializable**
- Only **enum name** is serialized (not ordinal)
- **Safe from attacks** (cannot create multiple instances)

## Object Graph Serialization

**When object references other objects, entire graph is serialized**

```java
class Department implements Serializable {
    String name;
    List<Employee> employees;  // All employees serialized too!
}
```

## Key Takeaways

1. **Externalizable** gives full control (must implement writeExternal/readExternal)
2. **Custom serialization** with writeObject/readObject for Serializable
3. **serialVersionUID** crucial for version compatibility
4. **Compatible changes** won't break deserialization
5. **Enum serialization** is automatic and safe

---

**End of Advanced Serialization**
