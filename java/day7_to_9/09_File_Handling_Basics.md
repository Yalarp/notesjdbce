# File Handling Basics in Java

## Introduction

**File Handling** in Java allows reading from and writing to files using streams.

## Stream Concept

**Stream** = Communication path between source and destination

### Types:
- **Input Stream** → For reading (from file, network, etc.)
- **Output Stream** → For writing (to file, network, etc.)

## Java Stream Categories

### 1. Byte Streams
- Handle raw binary data (images, videos, audio)
- Read/write data **byte by byte**
- Classes: `InputStream`, `OutputStream`

### 2. Character Streams  
- Handle text data with proper encoding (UTF-8, UTF-16)
- Read/write data **character by character**
- Classes: `Reader`, `Writer`

## File Class

**Purpose:** Get file/folder metadata (exists, length, last modified, etc.)

```java
import java.io.File;

File file = new File("test.txt");
System.out.println("Exists: " + file.exists());
System.out.println("Length: " + file.length());
System.out.println("Can Read: " + file.canRead());
System.out.println("Can Write: " + file.canWrite());
System.out.println("Is Directory: " + file.isDirectory());
System.out.println("Last Modified: " + file.lastModified());
```

## FileInputStream and FileOutputStream

**For byte-level operations**

```java
// Write bytes
FileOutputStream fos = new FileOutputStream("data.txt");
fos.write(65);  // Writes 'A'
fos.close();

// Read bytes
FileInputStream fis = new FileInputStream("data.txt");
int data = fis.read();  // Reads 65
System.out.println((char) data);  // Prints 'A'
fis.close();
```

## FileReader and FileWriter

**For character-level operations**

```java
// Write characters
FileWriter fw = new FileWriter("text.txt");
fw.write("Hello World");
fw.close();

// Read characters
FileReader fr = new FileReader("text.txt");
int ch;
while ((ch = fr.read()) != -1) {
    System.out.print((char) ch);
}
fr.close();
```

## BufferedReader and BufferedWriter

**For efficient reading/writing with buffering**

```java
// Buffered writing
BufferedWriter bw = new BufferedWriter(new FileWriter("file.txt"));
bw.write("Line 1");
bw.newLine();
bw.write("Line 2");
bw.close();

// Buffered reading
BufferedReader br = new BufferedReader(new FileReader("file.txt"));
String line;
while ((line = br.readLine()) != null) {
    System.out.println(line);
}
br.close();
```

## Key Points

1. **Always close streams** (use try-with-resources)
2. **Byte streams for binary**, character streams for text
3. **BufferedReader/Writer** for better performance
4. **File class** for metadata, not actual I/O
5. Package: `java.io`

---

**End of File Handling Basics**
