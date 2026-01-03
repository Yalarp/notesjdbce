# 17_Arrays – MCQs

## EASY MCQs

### Q1. In C#, array indexing starts at:

A. 1  
B. 0  
C. -1  
D. User defined  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
C# arrays are zero-indexed, meaning the first element is at index 0.
</details>

### Q2. Which code correctly declares an integer array of size 5?

A. `int[5] arr;`  
B. `int arr = new int[5];`  
C. `int[] arr = new int[5];`  
D. `Array<int> arr = new Array(5);`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The correct syntax is `type[] name = new type[size];`.
</details>

### Q3. Are arrays in C# value types or reference types?

A. Value Types  
B. Reference Types  
C. Primitive Types  
D. Dynamic Types  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Arrays are Reference Types in C# (they inherit from `System.Array`), even if they hold value types like `int`. The array object itself is stored on the Heap.
</details>

### Q4. Which property is used to get the total number of elements in an array?

A. `Count`  
B. `Size`  
C. `Length`  
D. `Capacity`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The `Length` property returns the total number of elements in the array (across all dimensions for multi-dimensional arrays).
</details>

---

## MEDIUM MCQs

### Q5. What is the difference between a multi-dimensional array (`int[,]`) and a jagged array (`int[][]`)?

A. There is no difference.  
B. Multi-dimensional is a single block of memory (matrix); Jagged is an array of arrays (rows can differ in length).  
C. Multi-dimensional arrays are faster.  
D. Jagged arrays are dynamic.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`int[,]` represents a rectangular matrix stored contiguously. `int[][]` is an array where each element is itself an array reference, allowing "rows" to have different lengths.
</details>

### Q6. How do you find the size of the second dimension in a 2D array?

A. `arr.Length`  
B. `arr[1].Length`  
C. `arr.GetLength(1)`  
D. `arr.Size(1)`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
`GetLength(dimensionIndex)` returns the number of elements in that specific dimension. `GetLength(0)` is rows, `GetLength(1)` is columns.
</details>

### Q7. What happens if you try to access an index outside the bounds of an array?

A. It returns 0.  
B. It returns null.  
C. It expands the array.  
D. It throws an `IndexOutOfRangeException`.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** D

**Explanation:**  
Accessing an invalid index causes a runtime `IndexOutOfRangeException`.
</details>

### Q8. Which method copies elements from one array to another?

A. `Array.Move()`  
B. `Array.Copy()`  
C. `Array.Duplicate()`  
D. `Array.Transfer()`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`Array.Copy` is the static method used to copy a range of elements from one array to another. (Instance method `CopyTo` also exists).
</details>

---

## HARD MCQs

### Q9. What does `Array.Resize(ref arr, newSize)` actually do?

A. It resizes the memory block of the existing array in place.  
B. It allocates a new array of the new size, copies the elements, and updates the reference.  
C. It only updates the `Length` property.  
D. It deletes the array.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Since arrays are fixed-size, "resizing" is impossible in place. The method creates a *new* array, copies data, and reassigns the reference variable (hence the `ref` keyword). The original array becomes eligible for garbage collection.
</details>

### Q10. Consider `int[] a = {1}; int[] b = a; b[0] = 5;`. What is the value of `a[0]`?

A. 1  
B. 5  
C. 0  
D. Null  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Arrays are reference types. `b = a` copies the reference, so both point to the *same* array in memory. Changing `b[0]` modifies the shared object, so `a[0]` is also 5.
</details>

### Q11. Which interface does `System.Array` implement that allows iteration?

A. `IEnumerable`  
B. `IComparable`  
C. `IDisposable`  
D. `IQueryable`  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** A

**Explanation:**  
Array implements `IEnumerable` (and `IEnumerable<T>`), which allows it to be used in `foreach` loops.
</details>

### Q12. For a jagged array `int[][] arr`, how many objects are created on the Heap if it has 3 rows (and each row is initialized)?

A. 1 (The main array)  
B. 3 (The rows)  
C. 4 (The main array + 3 row arrays)  
D. It depends on the number of columns.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
One object is created for the outer array (holding references). Then, each of the 3 inner arrays is a separate object on the Heap. Total = 4 array objects.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
