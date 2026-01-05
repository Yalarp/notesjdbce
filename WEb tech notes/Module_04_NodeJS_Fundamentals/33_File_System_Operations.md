# File System Operations in Node.js

## Table of Contents
1. [Introduction](#1-introduction)
2. [Reading Files](#2-reading-files)
3. [Writing Files](#3-writing-files)
4. [File Operations](#4-file-operations)
5. [Directory Operations](#5-directory-operations)
6. [Streams](#6-streams)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 The fs Module
The `fs` (File System) module provides an API for interacting with the file system. It's a core module that doesn't need installation.

```javascript
const fs = require('fs');
```

### 1.2 Sync vs Async
Every fs method has two versions:

| Type | Description | Example |
|------|-------------|---------|
| Synchronous | Blocks execution | `readFileSync()` |
| Asynchronous | Non-blocking | `readFile()` |

**Rule**: Use async methods in production to avoid blocking.

---

## 2. Reading Files

### 2.1 Asynchronous Read

```javascript
const fs = require('fs');

fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Error reading file:', err);
        return;
    }
    console.log(data);
});

console.log('This runs before file is read!');
```

### 2.2 Synchronous Read

```javascript
const fs = require('fs');

try {
    const data = fs.readFileSync('example.txt', 'utf8');
    console.log(data);
} catch (err) {
    console.error('Error reading file:', err);
}

console.log('This runs after file is read');
```

### 2.3 Reading JSON Files

```javascript
const fs = require('fs');

// Async
fs.readFile('config.json', 'utf8', (err, data) => {
    if (err) throw err;
    const config = JSON.parse(data);
    console.log(config);
});

// Sync
const data = fs.readFileSync('config.json', 'utf8');
const config = JSON.parse(data);
```

---

## 3. Writing Files

### 3.1 Asynchronous Write

```javascript
const fs = require('fs');

const content = 'Hello, World!';

fs.writeFile('output.txt', content, 'utf8', (err) => {
    if (err) {
        console.error('Error writing file:', err);
        return;
    }
    console.log('File written successfully!');
});
```

### 3.2 Synchronous Write

```javascript
const fs = require('fs');

try {
    fs.writeFileSync('output.txt', 'Hello, World!', 'utf8');
    console.log('File written successfully!');
} catch (err) {
    console.error('Error writing file:', err);
}
```

### 3.3 Appending to Files

```javascript
// Async
fs.appendFile('log.txt', 'New log entry\n', (err) => {
    if (err) throw err;
    console.log('Data appended');
});

// Sync
fs.appendFileSync('log.txt', 'New log entry\n');
```

### 3.4 Writing JSON

```javascript
const data = { name: 'John', age: 30 };

fs.writeFile('user.json', JSON.stringify(data, null, 2), (err) => {
    if (err) throw err;
    console.log('JSON saved');
});
```

---

## 4. File Operations

### 4.1 Check If File Exists

```javascript
// Modern approach (Node 10+)
fs.access('file.txt', fs.constants.F_OK, (err) => {
    if (err) {
        console.log('File does not exist');
    } else {
        console.log('File exists');
    }
});

// Synchronous
if (fs.existsSync('file.txt')) {
    console.log('File exists');
}
```

### 4.2 Get File Statistics

```javascript
fs.stat('file.txt', (err, stats) => {
    if (err) throw err;
    
    console.log('Is file:', stats.isFile());
    console.log('Is directory:', stats.isDirectory());
    console.log('Size:', stats.size, 'bytes');
    console.log('Created:', stats.birthtime);
    console.log('Modified:', stats.mtime);
});
```

### 4.3 Rename File

```javascript
fs.rename('old.txt', 'new.txt', (err) => {
    if (err) throw err;
    console.log('File renamed');
});
```

### 4.4 Delete File

```javascript
fs.unlink('file.txt', (err) => {
    if (err) throw err;
    console.log('File deleted');
});
```

### 4.5 Copy File

```javascript
fs.copyFile('source.txt', 'destination.txt', (err) => {
    if (err) throw err;
    console.log('File copied');
});
```

---

## 5. Directory Operations

### 5.1 Create Directory

```javascript
// Single directory
fs.mkdir('newfolder', (err) => {
    if (err) throw err;
    console.log('Directory created');
});

// Nested directories
fs.mkdir('path/to/newfolder', { recursive: true }, (err) => {
    if (err) throw err;
    console.log('Directories created');
});
```

### 5.2 Read Directory Contents

```javascript
fs.readdir('./', (err, files) => {
    if (err) throw err;
    
    files.forEach(file => {
        console.log(file);
    });
});

// With file type info
fs.readdir('./', { withFileTypes: true }, (err, files) => {
    files.forEach(file => {
        if (file.isDirectory()) {
            console.log('Directory:', file.name);
        } else {
            console.log('File:', file.name);
        }
    });
});
```

### 5.3 Remove Directory

```javascript
// Empty directory
fs.rmdir('folder', (err) => {
    if (err) throw err;
    console.log('Directory removed');
});

// Directory with contents (Node 14+)
fs.rm('folder', { recursive: true }, (err) => {
    if (err) throw err;
    console.log('Directory removed');
});
```

---

## 6. Streams

### 6.1 What are Streams?
Streams allow reading/writing data in chunks instead of loading entire files into memory.

### 6.2 Stream Types

| Type | Description |
|------|-------------|
| Readable | For reading (fs.createReadStream) |
| Writable | For writing (fs.createWriteStream) |
| Duplex | Both read and write |
| Transform | Modify data as it passes |

### 6.3 Reading with Streams

```javascript
const fs = require('fs');

const readStream = fs.createReadStream('large-file.txt', 'utf8');

readStream.on('data', (chunk) => {
    console.log('Received chunk:', chunk.length, 'bytes');
});

readStream.on('end', () => {
    console.log('Finished reading');
});

readStream.on('error', (err) => {
    console.error('Error:', err);
});
```

### 6.4 Writing with Streams

```javascript
const writeStream = fs.createWriteStream('output.txt');

writeStream.write('First line\n');
writeStream.write('Second line\n');
writeStream.end('Final line');

writeStream.on('finish', () => {
    console.log('Write completed');
});
```

### 6.5 Piping Streams

```javascript
// Copy file using streams
const readStream = fs.createReadStream('source.txt');
const writeStream = fs.createWriteStream('destination.txt');

readStream.pipe(writeStream);

writeStream.on('finish', () => {
    console.log('File copied');
});
```

---

## 7. Quick Reference

### 7.1 Reading

```javascript
// Async
fs.readFile('file', 'utf8', callback);

// Sync
fs.readFileSync('file', 'utf8');

// Stream
fs.createReadStream('file');
```

### 7.2 Writing

```javascript
// Async
fs.writeFile('file', data, callback);

// Sync
fs.writeFileSync('file', data);

// Append
fs.appendFile('file', data, callback);

// Stream
fs.createWriteStream('file');
```

### 7.3 File Operations

```javascript
fs.unlink('file', cb);      // Delete
fs.rename('old', 'new', cb); // Rename
fs.copyFile('src', 'dest', cb); // Copy
fs.stat('file', cb);        // Info
fs.access('file', cb);      // Check exists
```

### 7.4 Directory Operations

```javascript
fs.mkdir('dir', cb);        // Create
fs.readdir('dir', cb);      // List
fs.rmdir('dir', cb);        // Remove
```

---

## 8. Interview Questions

### Q1: What is the fs module?
**Answer**: The fs (File System) module is a core Node.js module that provides an API for interacting with the file system. It allows reading, writing, updating, and deleting files and directories.

### Q2: What is the difference between sync and async methods in fs?
**Answer**:
- **Async**: Non-blocking, uses callbacks, continues execution
- **Sync**: Blocking, waits until operation completes, simpler but slower

### Q3: What are streams in Node.js?
**Answer**: Streams are objects for handling data in chunks rather than loading entire files into memory. They're useful for large files and real-time data. Types: Readable, Writable, Duplex, Transform.

### Q4: What is the difference between readFile and createReadStream?
**Answer**:
- `readFile`: Loads entire file into memory, good for small files
- `createReadStream`: Reads in chunks, memory efficient for large files

### Q5: How do you handle errors in file operations?
**Answer**: 
- **Async**: Check error in callback first parameter
- **Sync**: Use try-catch blocks
- **Streams**: Listen to 'error' event

### Q6: What does pipe() do?
**Answer**: `pipe()` connects a readable stream to a writable stream, automatically handling data flow and back-pressure. It's commonly used for copying files or sending data.

---

## Navigation

← Previous: [32_Modules_and_Exports.md](./32_Modules_and_Exports.md) | Next: [34_HTTP_Server_Basics.md](./34_HTTP_Server_Basics.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 07*
