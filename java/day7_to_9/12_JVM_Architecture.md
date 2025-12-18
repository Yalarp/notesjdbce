# JVM Architecture in Java

## Introduction

**JVM (Java Virtual Machine)** = Execution environment for Java programs

## How Java Achieves Platform Independence

```
Java Source Code (.java)
    ↓ javac (compiler)
Bytecode (.class)
    ↓
JVM (Windows/Linux/Mac)
    ↓
Machine Code (platform-specific)
```

**Key Point:** Bytecode is platform-independent; JVM is platform-specific

## JVM Architecture Components

```
┌─────────────────────────────────────┐
│     Class Loader Subsystem          │
├─────────────────────────────────────┤
│     Runtime Data Areas              │
│   - Method Area/Metaspace            │
│   - Heap                             │
│   - Stack (per thread)               │
│   - PC Register (per thread)         │
│   - Native Method Stack (per thread) │
├─────────────────────────────────────┤
│     Execution Engine                 │
│   - Interpreter                      │
│   - JIT Compiler                     │
│   - Garbage Collector                │
├─────────────────────────────────────┤
│   Native Method Interface (JNI)     │
└─────────────────────────────────────┘
```

## ClassLoader Subsystem

**Phases: Load → Link → Initialize**

### 1. Loading
- **Bootstrap ClassLoader** → Loads core Java classes (rt.jar)
- **Extension ClassLoader** → Loads extension classes (lib/ext)
- **Application ClassLoader** → Loads application classes (CLASSPATH)

### 2. Linking
- **Verification** → Verifies bytecode validity
- **Preparation** → Allocates memory for static variables
- **Resolution** → Resolves symbolic references

### 3. Initialization
- Executes static initializers and static blocks

## Delegation Hierarchy Principle

```
Application ClassLoader
    ↓ delegates to
Extension ClassLoader
    ↓ delegates to
Bootstrap ClassLoader
```

**Process:**
1. Application CL asks Extension CL
2. Extension CL asks Bootstrap CL
3. Bootstrap tries to load
4. If fails, Extension tries
5. If fails, Application tries

## Runtime Data Areas

### 1. Method Area / Metaspace
- Stores **class metadata** (structure, methods, fields)
- **Static variables**
- **Runtime constant pool**
- **Shared among all threads**

### 2. Heap
- Stores **objects**
- **Shared among all threads**
- **Garbage collected**

### 3. Stack (per thread)
- Stores **local variables** and **method calls**
- Each method call creates a **stack frame**
- **Thread-private**

### 4. PC Register (per thread)
- Stores **address of current instruction**
- **Thread-private**

### 5. Native Method Stack (per thread)
- For **native methods** (written in C/C++)
- **Thread-private**

## What Happens When You Execute Java Application?

1. **JVM starts**, creates main thread
2. **ClassLoader loads** Main class
3. **Linker verifies and prepares** class
4. **Initializer** runs static blocks
5. **Execution Engine** executes main() method

##  Magic Number

**Every .class file starts with: `0xCAFEBABE`**

**Purpose:** JVM uses this to verify it's a valid Java class file

## Major Version Numbers

| Java Version | Major Version |
|--------------|---------------|
| Java 8 | 52 |
| Java 11 | 55 |
| Java 17 | 61 |

## Key Points

1. **JVM is platform-specific**, bytecode is platform-independent
2. **Three class loaders**: Bootstrap, Extension, Application
3. **Delegation hierarchy**: Child delegates to parent first
4. **Method Area** for class metadata, **Heap** for objects
5. **Stack** is thread-private, **Heap** is shared
6. **Magic number** `0xCAFEBABE` identifies .class files

---

**End of JVM Architecture**
