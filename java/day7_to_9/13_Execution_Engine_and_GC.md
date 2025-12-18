# Execution Engine and Garbage Collection

## Execution Engine Components

```
Execution Engine
├─ Interpreter
├─ JIT Compiler
└─ Garbage Collector
```

## Interpreter

**Purpose:** Executes bytecode line by line

**Process:**
1. Reads bytecode instruction
2. Converts to machine code
3. Executes

**Disadvantage:** Slow (interprets same code repeatedly)

## JIT Compiler (Just-In-Time)

**Purpose:** Compiles frequently executed bytecode (*hot code*) to native machine code

**Process:**
1. **Interpreter** executes initially
2. **JIT** identifies hot code (executed multiple times)
3. **Compiles** hot code to native code
4. **Caches** compiled code
5. **Reuses** compiled code (no reinterpretation needed)

**Advantage:** Much faster than interpretation

## javac vs JIT Compiler

| Aspect | javac | JIT |
|--------|-------|-----|
| **When** | Compile time | Runtime |
| **Input** | .java source | Bytecode |
| **Output** | Bytecode | Native machine code |
| **Purpose** | Platform independence | Performance optimization |

## Interpreter vs JIT

| Aspect | Interpreter | JIT Compiler |
|--------|-------------|--------------|
| **Speed** | Slow | Fast |
| **Memory** | Less | More (caches compiled code) |
| **Startup** | Fast | Slower (compilation overhead) |
| **Use case** | Code executed once | Code executed repeatedly |

## Garbage Collection

**Purpose:** Automatically reclaims memory from **unreachable objects**

### Object Lifecycle

```
new Object() → Referenced → Unreferenced → Garbage Collected
```

### Making Object Eligible for GC

1. **Nullify reference:** `obj = null;`
2. **Reassign reference:** `obj1 = obj2;`
3. **Anonymous object:** `new MyClass();`
4. **Island of Isolation:** Circular references with no external reference

### Requesting GC

```java
System.gc();  // Suggests JVM to run GC
Runtime.getRuntime().gc();  // Same
```

**Note:** Both just **suggest** GC; JVM decides when to actually run it

### finalize() Method

```java
protected void finalize() {
    // Cleanup before object is garbage collected
    // Called by GC thread
}
```

**Important:** 
- Called **at most once** per object
- Called by **Finalizer thread** (daemon thread)
- **Deprecated since Java 9** (use try-with-resources instead)

## Heap Memory Areas

```
Young Generation
├─ Eden Space
└─ Survivor Spaces (S0, S1)

Old Generation (Tenured)
```

### Minor GC
- **Runs on Young Generation**
- Fast and frequent
- Moves surviving objects to Old Generation

### Major GC (Full GC)
- **Runs on Old Generation**
- Slower, less frequent
- Cleans up long-lived objects

## GC Algorithm Types

1. **Serial GC** → Single thread
2. **Parallel GC** → Multiple threads (default)
3. **CMS (Concurrent Mark Sweep)** → Low pause time
4. **G1 (Garbage First)** → Balanced (default in Java 9+)
5. **ZGC** → Ultra-low pause time

## Native Method Interface

**Purpose:** Allows Java to call **native code** (C/C++)

```java
public class Native {
    public native void nativeMethod();  // Implemented in C/C++
    
    static {
        System.loadLibrary("nativeLib");  // Load native library
    }
}
```

## Key Points

1. **Interpreter** executes bytecode line by line
2. **JIT** compiles hot code to native for better performance
3. **GC** automatically reclaims memory from unreachable objects
4. **Minor GC** on Young Gen, **Major GC** on Old Gen
5. **finalize()** deprecated; use try-with-resources
6. **JNI** allows calling native C/C++ code

---

**End of Execution Engine and GC**
