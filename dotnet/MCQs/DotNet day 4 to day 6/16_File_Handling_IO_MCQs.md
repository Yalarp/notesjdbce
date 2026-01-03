# 16_File_Handling_IO – MCQs

## EASY MCQs

### Q1. Which namespace contains classes for file and stream I/O?
A. `System`  
B. `System.Data`  
C. `System.IO`  
D. `System.Files`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`System.IO` is the root namespace for classes like `File`, `Directory`, `Path`, `StreamReader`, etc.
</details>

### Q2. Which class facilitates reading characters from a byte stream?
A. `FileStream`  
B. `StreamReader`  
C. `BinaryReader`  
D. `StringReader`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`StreamReader` is designed for character-based input, handling encoding automatically when reading from an underlying byte stream like `FileStream`.
</details>

### Q3. Identify the static class that facilitates file creation, copying, deletion, moving, and opening.
A. `FileInfo`  
B. `File`  
C. `Directory`  
D. `Path`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `File` class provides static methods (`Create`, `Copy`, `Delete`, `Move`, `Open`) for typical file operations without holding onto a file handle object.
</details>

### Q4. Which mode should be used to append text to an existing file?
A. `FileMode.New`  
B. `FileMode.Append`  
C. `FileMode.Create`  
D. `FileMode.Truncate`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`FileMode.Append` opens the file if it exists and seeks to the end of the file, or creates a new file if it doesn't exist.
</details>

### Q5. What is the benefit of the `using` statement with file streams?
A. It compresses the file.  
B. It automatically disposes/closes the stream.  
C. It allows faster reading.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `using` block ensures that `Dispose()` is called on the IDisposable object (FileStream) immediately after the block exits, releasing the file handle back to the OS.
</details>

---

## MEDIUM MCQs

### Q6. Which method reads all lines of a text file into a string array?
A. `File.ReadAllText()`  
B. `File.ReadAllLines()`  
C. `StreamReader.ReadLine()`  
D. `File.ReadLines()`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`File.ReadAllLines(path)` opens a text file, reads all lines, and then closes the file, returning a `string[]`.
</details>

### Q7. The abstract base class for all streams is:
A. `System.IO.File`  
B. `System.IO.Stream`  
C. `System.Object`  
D. `System.IO.BinaryStream`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `Stream` class provides a generic view of a sequence of bytes and is the abstract parent for `FileStream`, `MemoryStream`, `NetworkStream`, etc.
</details>

### Q8. To manipulate directory structures (create, move, enumerate keys), use:
A. `Path`  
B. `Environment`  
C. `Directory`  
D. `Volume`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Directory` (static) and `DirectoryInfo` (instance) classes expose methods for creating, moving, and enumerating through directories and subdirectories.
</details>

### Q9. `Path.Combine("C:\Temp", "file.txt")` handles:
A. Creating the file.  
B. Validating if the file exists.  
C. Properly inserting platform-specific directory separators.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`Path.Combine` safely joins strings into a path, automatically handling missing or redundant slashes (`\` or `/` depending on OS).
</details>

### Q10. What exception is thrown if you try to open a non-existent file with `FileMode.Open`?
A. `IOException`  
B. `FileNotFoundException`  
C. `NullReferenceException`  
D. `ArgumentException`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`FileMode.Open` mandates that the file must exist; otherwise, it throws `System.IO.FileNotFoundException`.
</details>

---

## HARD MCQs

### Q11. Difference between `File` and `FileInfo` classes:
A. `File` is static; `FileInfo` is an instance wrapper.  
B. `File` is for binary; `FileInfo` is for text.  
C. `File` is faster for multiple operations on the same file.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
`File` provides static methods (good for one-off ops). `FileInfo` creates an object representing the file, which retains state (like attributes) and is more efficient if you need to perform multiple operations on the same file without re-checking the disk.
</details>

### Q12. `FileShare.Read` means:
A. Only I can read the file.  
B. I am opening the file, and I allow other processes to Read it simultaneously.  
C. I am blocking others from reading.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `FileShare` enum controls typical file locking. `FileShare.Read` designates that subsequent requests to open the file (by other processes) are allowed *only* if they request Read access.
</details>

### Q13. `FileStream` mainly deals with:
A. Text data.  
B. Structured data objects.  
C. Raw byte data.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`FileStream` provides access to the raw bytes of a file. It does not natively understand text encoding (UTF-8, etc.) without a helper like `StreamReader` or `TextWriter`.
</details>

### Q14. Which stream helper provides methods `ReadInt32`, `ReadDouble`, `ReadString`?
A. `StreamReader`  
B. `BinaryReader`  
C. `StringReader`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`BinaryReader` wraps a stream and allows reading primitives types directly from their binary representation.
</details>

### Q15. `Directory.GetFiles` vs `Directory.EnumerateFiles`:
A. `EnumerateFiles` is deprecated.  
B. `GetFiles` returns an array (waits for all); `EnumerateFiles` returns `IEnumerable` (lazy streaming).  
C. `GetFiles` is recursive; `EnumerateFiles` is not.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`EnumerateFiles` is more efficient for large directories because it yields filenames one by one as they are found, allowing you to start processing before the entire filesystem search completes.
</details>
