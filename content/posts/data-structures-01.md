+++
date = '2025-05-17T07:27:31+09:00'
title = '[Data Structures] [01] Array ADT and Implementation'
description = "Understanding the Array Abstract Data Type in Data Structures and implement in C"
categories = ["Computer Science/Algorithms & Data Structures"]
tags = ["Data Structures"]
slug = "array-adt"
math = true
draft = false
+++

# Chapter 01. Array ADT and Implementation

> **Outline:**  
> This chapter introduces the **Array Abstract Data Type (ADT)** as a foundational structure in data organization.  
> It explores both the abstract model (ADT) and its concrete implementations in C, including static and dynamic arrays.  
> Through this chapter, you will gain a clear understanding of array operations, memory layout, pointer behaviors, and their practical use cases and limitations.  
> This chapter also highlights the motivation for more flexible structures like linked lists and addresses typical interview questions related to arrays.

---

## Contents

- [1.1. Array Abstract Data Type (ADT)](#section-11-array-abstract-data-type-adt)
- [1.2. What Is an Array in C?](#section-12-what-is-an-array-in-c)
- [1.3. Implementing Static Arrays in C](#section-13-implementing-static-arrays-in-c)
- [1.4. Memory Model and Pointer Behavior in Arrays](#section-14-memory-model-and-pointer-behavior-in-arrays)
- [1.5. Multidimensional Arrays](#section-15-multidimensional-arrays)
- [1.6. Dynamic (Resizable) Arrays in C](#section-16-dynamic-resizable-arrays-in-c)
- [1.7. Limitations of Arrays and Why Linked Lists Are Needed](#section-17-limitations-of-arrays-and-why-linked-lists-are-needed)
- [1.8. Arrays vs Pointers in C (optional)](#section-18-arrays-vs-pointers-in-c)

---

## Section 1.1. Array Abstract Data Type (ADT)

### 1.1.1. What Is the Array ADT?

- The **Array Abstract Data Type (ADT)** is a logical model that represents a **fixed-size**, **index-based**, and **homogeneous** (동종의) collection of elements. Each element is identified by an integer index and stored in a specific position.

> An array ADT can also be formally described as a collection of ordered pairs **⟨index, value⟩**, where each valid index maps uniquely to a corresponding value:
> ⟨0, A[0]⟩, ⟨1, A[1]⟩, …, ⟨n−1, A[n−1]⟩
> Indices(the plural form of index) are typically zero-based, and valid indices range from `0` to `size - 1`.

- This abstraction allows for **constant-time access** to any element using its index and forms the basis of many efficient algorithms and data structures.

> For a detailed explanation of what an Abstract Data Type (ADT) is, refer to **Chapter 00, Section 0.3**.

---

**Essential Properties of the Array ADT:**

| Property           | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| **Fixed Size**     | The number of elements is determined at creation and does not change        |
| **Indexed Access** | Each element is accessible via a unique integer index (0-based indexing)    |
| **Homogeneous**    | All elements belong to the same data type                                   |

---

### 1.1.2. Array ADT Specification

- **Objects:**  
    A **fixed-size**, **indexed** sequence of elements of the **same type**.

- **Operations:**
    - `create(size)`  
      ::= Creates an array that can hold `size` number of elements.

    - `get(A, i)`  
      ::= Returns the element at index `i` from array `A`.

    - `set(A, i, v)`  
      ::= Stores value `v` at index `i` in array `A`.

    - `length(A)`  
      ::= Returns the number of elements in array `A`.

    - `traverse(A)`  
      ::= Visits each element of array `A` in order.

    - `search(A, x)`  
      ::= Returns the index of value `x` in array `A`, if present.

    - `insert(A, i, x)`  
      ::= Inserts `x` at index `i` in array `A`; elements may shift.

    - `delete(A, i)`  
      ::= Deletes the element at index `i`; elements may shift to fill the gap.

---

**Summary of Operations**

| Operation           | Time Complexity  | Remarks (촌평)                                            |
|---------------------|------------------|----------------------------------------------------------|
| `create(size)`      | O(1)             | Initializes a fixed-size array                           |
| `get(A, i)`         | O(1)             | Returns value at index `i`; constant-time random access  |
| `set(A, i, v)`      | O(1)             | Updates value at index `i`                               |
| `length(A)`         | O(1)             | Returns current number of elements                       |
| `traverse(A)`       | O(n)             | Iterates over all elements                               |
| `search(A, x)`      | O(n)             | Linear search; may return first matching index           |
| `insert(A, i, x)`   | O(n)             | Requires shifting elements to make space                 |
| `delete(A, i)`      | O(n)             | Requires shifting elements to fill the gap               |

---

> Note:  
> Operations such as `insert` and `delete` are inefficient in fixed-size arrays because they often require shifting multiple elements, which leads to a higher time complexity.
> This limitation is one of the primary reasons for introducing linked lists, which support more efficient insertions and deletions.

---

### 1.1.3. Example Usage Scenario

- A leaderboard holding the top 100 player scores → indexed access is efficient
- A monthly calendar with 31 days → fixed-size, one-to-one mapping with indices
- A timetable grid (e.g., 7 days × 24 hours) → 2D array (to be discussed later)

---

> **Summary**  
> The Array ADT is the simplest and most efficient structure for **fixed-size, index-based, homogeneous data**.  
> However, due to its rigid(고정된, 굳은) size and costly insertion/deletion, it is best suited for **static datasets**.

---

## Section 1.2. What Is an Array in C?

### 1.2.1. Definition

In the C programming language, an **array** is a fixed-size collection of elements of the same type stored in **contiguous memory locations**. Each element is accessed using an index, with indexing starting at zero.

> Arrays in C are **not dynamic by default**. Once declared, the size of an array cannot be changed.

**Characteristics**

| Feature              | Description                            |
|----------------------|----------------------------------------|
| Fixed size           | Must be declared with a known size     |
| Static allocation    | Memory allocated at compile time       |
| Same-type elements   | All elements must be of one data type  |
| Index-based access   | Direct access via zero-based indexing  |

---

### 1.2.2. Basic Syntax

**Declaration Example:**

```c
int scores[5];       // Declares an array of 5 integers
char name[20];       // Declares an array of 20 characters
float prices[10];    // Declares an array of 10 floats
```

> The above declarations allocate memory for a fixed number of elements.
> The size must be a **constant** at compile time.

---

**Initialization Example:**

```c
int A[5] = {1, 2, 3, 4, 5};        // full initialization
int B[5] = {1, 2};                 // partial, rest are zero
int C[]  = {10, 20, 30};           // size inferred from initializer
```

> Arrays can be initialized at the time of declaration.
> If fewer initializers are provided, the remaining elements are zero-initialized. (i.e. Uninitialized elements are filled with `0` only if((충족)한다면) at least one initializer is provided.)
> If the size is omitted, it is inferred from the number of initializers.

---

**Access and Modification Example:**

```c
scores[1] = 85;                     // update value
printf("%d", scores[1]);           // access value
```

> C allows **indexed access** to each element of array using square brackets `[]`.
> Indexing starts at `0` (i.e., the first element is `arr[0]`, the last is `arr[size - 1]`).
> Accessing an out-of-bounds index leads to **undefined behavior**, due to the lack of built-in bounds checking in C.

---

### 1.2.3. Memory Layout and Indexing
Arrays are stored in contiguous memory, meaning each element is placed next to the previous one. This allows for efficient computation of any element’s address using the base address and offset.

- The array name (scores, name, etc.) acts as a pointer to the first element.
- A contiguous block of memory allows for efficient random(임의) access to array elements using index arithmetic.
    - (\text{Address of } arr[i] = \text{base\_address} + (i \times \text{element\_size}))
    - (\text{Address of } arr[i] = \text{base\_address} + (i \times \text{sizeof(data\_type)}))
- This property makes array element access **O(1)** in time complexity.

---

**Example:**

```c
int A[4] = {10, 20, 30, 40};
// Memory layout:
A[0] → 10
A[1] → 20
A[2] → 30
A[3] → 40
```

---

### 1.2.4. Abstract View vs Concrete View (Array ADT vs Array in C)

| Feature                   | Array ADT (Abstract)                               | Static Array in C (Implementation)              |
|---------------------------|----------------------------------------------------|------------------------------- -----------------|
| **Definition Level**      | Logical model                                      | Language-level memory construct                 |
| **Size**                  | Fixed at creation (`create(size)`)                 | Fixed at declaration (compile-time constant)    |
| **Element Type**          | Homogeneous (same data type)                       | Must be same type (enforced by compiler)        |
| **Indexing**              | Must support indexed access (e.g., `get(i)`)       | Zero-based indexing with `arr[i]`               |
| **Memory Layout**         | Abstract – does not specify how memory is arranged | Contiguous memory layout                        |
| **Bounds Checking**       | Not defined (depends on implementation)            | No built-in bounds checking                     |
| **Mutability**            | Allows `set(i, value)` operation                   | Allows mutation via `arr[i] = value`            |
| **Language Independence** | Yes                                                | No (specific to C)                              |

> Arrays in C provide efficient random access due to their contiguous memory layout,  
> but they have limitations such as a **fixed size** and **the lack of built-in bounds checking**.

---

## Section 1.3. Implementing Static Arrays in C

### 1.3.1. What Is a Static Array?

A **static array** in C is an array whose size is known and fixed at **compile time**. Its memory is allocated either on the **stack** (for local variables) or in the **data segment** (for global/static variables).

> Static here(여기에서, 이 문장에서) refers to **fixed-size** allocation, not necessarily the use of the `static` keyword.

---

### 1.3.2. Declaring and Using Static Arrays

Declaration:
```c
int A[5];              // Declares an array of 5 integers
```
Initialization:
```c
for (int i = 0; i < 5; i++) {
    A[i] = i * 10;
}
```
Traversal:
```c
for (int i = 0; i < 5; i++) {
    printf("A[%d] = %d\n", i, A[i]);
}
```
Output:
```c
A[0] = 0  
A[1] = 10  
A[2] = 20  
A[3] = 30  
A[4] = 40
```

---

### 1.3.3. Common Operations on Static Arrays

| Operation    | Code Example              | Time Complexity |
|--------------|---------------------------|-----------------|
| Access       | `x = A[3];`               | O(1)            |
| Update       | `A[2] = 99;`              | O(1)            |
| Traverse     | for loop with indexing    | O(n)            |
| Search       | Linear search via loop    | O(n)            |
| Insert/Shift | Manual shifting needed    | O(n)            |
| Delete       | Simulate or shift         | O(n)            |

---

### 1.3.4. Example: Linear Search in Static Array

```c
int search(int A[], int n, int key) {
    for (int i = 0; i < n; i++) {
        if (A[i] == key)
            return i;
    }
    return -1;  // not found
}
```

---

### 1.3.5. Limitations of Static Arrays

| Limitation               | Explanation                                                  |
|--------------------------|--------------------------------------------------------------|
| Fixed size               | Cannot grow/shrink at runtime                                |
| No insert/delete         | Requires manual element shifting                             |
| Memory waste or overflow | Over-allocation wastes memory; under-allocation causes limits |
| No boundary check        | Accessing invalid index causes undefined behavior            |

---

**Summary**  
Static arrays in C are efficient for fixed-size data with known limits.  
They provide fast access but lack dynamic features like resizing or safe insert/delete.

---

## Section 1.4. Memory Model and Pointer Behavior in Arrays

### 1.4.1. Memory Model of Arrays

In C, arrays are stored in **contiguous memory locations**, which means that all elements are laid out one after another in memory without any gaps.

**Example:**
Given:
```c    
int A[4] = {10, 20, 30, 40};
```

The memory layout might look like:
| Address   | Content | Index  |
|:---------:|:-------:|:------:|
| `0x1000`  |   `10`  | `A[0]` |
| `0x1004`  |   `20`  | `A[1]` |
| `0x1008`  |   `30`  | `A[2]` |
| `0x100C`  |   `40`  | `A[3]` |


If `int` is 4 bytes, then the address of `A[i]` is computed as:
    base_address + (i × sizeof(int))

This direct computation allows constant-time access: **O(1)**.

---

### 1.4.2. Array Name as a Pointer

In most contexts, the name of an array behaves like a pointer to its first element.

**Example:**
```c
int A[3] = {1, 2, 3};
int *p = A;
```

Here:
- `A` is automatically converted to `&A[0]`
- `p` now points to the first element of array `A`
- `p[1]` is equivalent to `*(p + 1)` and to `A[1]`

> However, **`A` is not a pointer variable**; it's a symbolic name for the array and cannot be reassigned like a pointer.

---

### 1.4.3. Pointer Arithmetic on Arrays

You can perform pointer arithmetic using array names or pointer variables:

**Examples:**
```c
*(A + 2)      // same as A[2]
*(p + 2)      // same as p[2]
*(A + i)      // equivalent to A[i]
```

You can also iterate over an array using a pointer:
```c
int *ptr = A;
for (int i = 0; i < 3; i++) {
    printf("%d\n", *(ptr + i));
}
```

---

### 1.4.4. Differences Between Arrays and Pointers

| Aspect             | Array                        | Pointer                          |
|--------------------|------------------------------|-----------------------------------|
| Modifiability      | Cannot be reassigned         | Can be reassigned                |
| sizeof operator    | Size of entire array         | Size of pointer (e.g., 8 bytes)  |
| Memory allocation  | Contiguous block             | Points to any address            |
| Storage duration   | Stack or data segment        | Stack, heap, or data segment     |

**Example:**
```c
int A[5];
int *p = A;

sizeof(A) → 20 (if int is 4 bytes)  
sizeof(p) → 8 (on 64-bit machine)
```

---

**Summary**  
- Arrays are stored in contiguous memory and support fast indexed access.
- In most contexts, an array name acts like a pointer to the first element.
- However, arrays and pointers are **not the same**, and knowing the differences is essential to avoid memory errors.

> [More about pointer and array](#section-19-arrays-vs-pointers-in-c)

---

## Section 1.5. Multidimensional Arrays

### 1.5.1. What Is a Multidimensional Array?

A **multidimensional array** is an array of arrays. In C, the most common type is the **two-dimensional array** (2D array), which can be visualized as a **table** or **matrix** with rows and columns.

Declaration syntax:
```c
type array_name[rows][columns];
```

Example:
```c
int matrix[3][4];   // 3 rows, 4 columns
// This creates a contiguous memory block to store 12 integers (3 × 4 = 12).
```

---

### 1.5.2. Memory Layout

Even though a 2D array is written as a table, it is stored **linearly in row-major order** in memory.

Example:
```c
int A[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};
```

Memory layout:

| Address   | Value | Index     |
|:---------:|:-----:|:---------:|
| `0x1000`  |  `1`  | `A[0][0]` |
| `0x1004`  |  `2`  | `A[0][1]` |
| `0x1008`  |  `3`  | `A[0][2]` |
| `0x100C`  |  `4`  | `A[1][0]` |
| `0x1010`  |  `5`  | `A[1][1]` |
| `0x1014`  |  `6`  | `A[1][2]` |

> If `int` is 4 bytes, each element takes 4 bytes, and rows are stored one after another.

---

### 1.5.3. Accessing Elements

To access a specific element:
`A[i][j]`   → element in the ith row and jth column

Example:
```c
A[1][2] = 99;        // sets the last element to 99
printf("%d", A[0][1]); // prints 2, int A[2][3] = { {1, 2, 3}, {4, 5, 99} };
```

---

### 1.5.4. Traversing a 2D Array

Nested loops are commonly used:
```c
for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
        printf("%d ", A[i][j]);
    }
    printf("\n");
}
```

---

### 1.5.5. Common Pitfalls

| Mistake                        | Explanation                                                      |
|-------------------------------|-------------------------------------------------------------------|
| Omitting column size           | `int A[][3]` is valid, but `int A[][]` is invalid                |
| Assuming A[i][j] = A[j][i]     | Only symmetric for square matrices (not always true)             |
| Using wrong dimensions         | Declaring `A[3][2]` and accessing `A[2][3]` → undefined behavior |

> In function parameters, the **number of columns must be specified**, because row size alone isn't enough to compute addresses.

---

**Summary**

- Multidimensional arrays store data in a **row-major linear memory block**.
- Access is done via multiple indices (e.g., `A[i][j]`).
- Column size is essential for correct memory calculations.
- Useful for matrices, grids, tables, and more.

---

## Section 1.6. Dynamic (Resizable) Arrays in C

### 1.6.1. Motivation

C arrays are fixed-size by default. Once an array is declared with a specific size, it cannot be resized.

However, many real-world applications require:
- **Variable-sized** inputs (e.g., user input, file contents)
- **Dynamic** data growth (e.g., appending items)

This is where dynamic memory allocation becomes necessary.

---

### 1.6.2. Allocating Dynamic Arrays

C provides the `<stdlib.h>` library functions for memory allocation:

- `malloc(size)` – allocate uninitialized memory
- `calloc(n, size)` – allocate and zero-initialize memory
- `realloc(ptr, new_size)` – resize previously allocated memory
- `free(ptr)` – release allocated memory

Example: Allocating an int array for `n` elements
```c
int *arr;
int n = 5;

arr = (int *)malloc(n * sizeof(int));
if (arr == NULL) {
    printf("Memory allocation failed\n");
    exit(1);
}
```

---

### 1.6.3. Using and Resizing

To access elements:
```c
arr[0] = 10;
arr[1] = 20;
```

To resize (e.g., double the size):
```c
n = 10;
arr = (int *)realloc(arr, n * sizeof(int));
if (arr == NULL) {
    printf("Reallocation failed\n");
    exit(1);
}
```

To release memory when done:
```c
free(arr);
```

---

### 1.6.4. Benefits and Risks

| Benefit                       | Risk                                    |
|-------------------------------|-----------------------------------------|
| Can grow or shrink at runtime | Manual memory management required       |
| Efficient use of memory       | Forgetting `free()` causes memory leaks |
| Flexible for input size       | Dangling pointers if misused            |

---

### 1.6.5. Comparison with Static Arrays

| Feature          | Static Array             | Dynamic Array                         |
|------------------|--------------------------|---------------------------------------|
| Size             | Fixed at compile time    | Determined at runtime                 |
| Memory           | Stack or data segment    | Heap (via malloc, realloc)            |
| Flexibility      | Inflexible               | Resizable                             |
| Bounds checking  | Not provided             | Still not provided                    |
| Lifetime         | Automatic (if local)     | Manual malloc/free needed             |

---

**Summary**

- C does not support built-in dynamic arrays like higher-level languages.
- You must use heap allocation functions like malloc() and realloc().
- Always call free() to prevent memory leaks.
- Dynamic arrays are essential for variable-size data.

---


## Section 1.7. Limitations of Arrays and Why Linked Lists Are Needed

### 1.7.1. Limitations of Static and Dynamic Arrays

Although arrays are efficient for indexed access, they have several limitations that make them less suitable for certain use cases:

| Limitation           | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| Fixed Size (Static)  | Static arrays cannot grow or shrink; their size is fixed at compile time.  |
| Manual Resizing      | Dynamic arrays require manual resizing using realloc(), which is costly.   |
| Costly Insertion     | Inserting an element in the middle requires shifting all subsequent items. |
| Costly Deletion      | Similarly, deletion also requires shifting elements to fill the gap.       |
| Fragmentation Risk   | realloc() may move the array in memory, breaking previous pointers.        |

---

### 1.7.2. Use Case Example: Inserting at the Beginning

Suppose we want to insert an element at the front of an array:
```c
    int A[5] = {10, 20, 30, 40, 50};
    
    // Insert 5 at A[0]; shift all elements
    for (int i = 4; i >= 0; i--) {
        A[i + 1] = A[i];
    }
    A[0] = 5;
```

This process is O(n) due to the shifting. If we frequently insert or delete at arbitrary positions, arrays are inefficient.

---

### 1.7.3. Why Linked Lists Help

**Linked lists** solve many of the above issues by using nodes and pointers rather than contiguous memory.

| Feature                     | Array                                | Linked List                         |
|-----------------------------|--------------------------------------|-------------------------------------|
| Size Flexibility            | Fixed (or manually resized)          | Grows or shrinks dynamically        |
| Insertion/Deletion          | Costly (shift required)              | Efficient at head or tail           |
| Memory Layout               | Contiguous                           | Non-contiguous (each node separate) |
| Random Access               | O(1)                                 | O(n) (must traverse)                |
| Memory Overhead             | Low                                  | Higher (pointer + data per node)    |

---

### 1.7.4. When to Choose Linked Lists

Linked lists are preferred when:
- The number of elements is unknown or changes frequently.
- Frequent insertions/deletions are expected at arbitrary positions.
- Memory fragmentation is not a concern.

> Note: Arrays are still preferable when fast indexing and low memory overhead are important.

---

### 1.7.5. Summary

- Arrays are simple and fast for indexed data access but become inefficient for frequent structural changes.
- Linked lists offer better flexibility at the cost of pointer overhead and slower access.
- Understanding their trade-offs is crucial before choosing one over the other.

---

## Section 1.8. Arrays vs Pointers in C

### 1.8.1. Conceptual Difference

| Feature           | Array                                     | Pointer                                |
|-------------------|--------------------------------------------|-----------------------------------------|
| Definition        | Collection of fixed-size, contiguous elements | Variable storing the address of another variable |
| Memory Allocation | Automatically allocates a block of memory  | Must be explicitly assigned or allocated |
| Reassignability   | Cannot reassign the array variable itself  | Pointer can be reassigned to another location |
| Syntax            | `int A[10];`                               | `int *p;` and `p = A;` or `p = malloc()` |

---

### 1.8.2. Array Name as a Pointer (When and How)

In most expressions, the name of an array is converted to a pointer to its first element:

```c
int A[3] = {1, 2, 3};
int *p = A;        // p points to A[0]

printf("%d", *(A + 1));  // prints 2
printf("%d", p[2]);      // prints 3
```

> Both `A[i]` and `*(A + i)` are valid and equivalent.
> However:
> `A = p;` is illegal (you can’t assign to an array name)
> `p = A;` is legal (you can assign an array address to a pointer)

---

### 1.8.3. sizeof Operator Difference

```c
int A[5];
int *p = A;

printf("%zu\n", sizeof(A)); // Output: 20 (if int = 4 bytes)
printf("%zu\n", sizeof(p)); // Output: 8 (on 64-bit systems)
```

> `sizeof(A)` = total memory size allocated for the array
> `sizeof(p)` = size of a pointer (not the array contents)

---

### 1.8.4. Pointer Arithmetic and Access

Both arrays and pointers support arithmetic operations like:
```c
*(p + i), A[i], p[i]
```
However, only pointers can be incremented:
```c
p++;       // valid
A++;       // invalid (compile error)
```

---

### 1.8.5. Function Parameter Behavior
When passing an array to a function, it decays to a pointer.
```c
void foo(int A[]) {
    // A is actually of type int*
}

void foo(int *A) {
    // Equivalent declaration
}
```
Therefore, you lose the size information unless it’s passed separately.

---

### 1.8.6. Summary

| Aspect                  | Array                        | Pointer                        |
|--------------------------|------------------------------|--------------------------------|
| Syntax                  | `int A[10];`                 | `int *p = A;`                  |
| Memory                  | Allocated at declaration     | Can be dynamic (via malloc)    |
| Reassignment            | Not allowed (`A = ...`)      | Allowed (`p = ...`)            |
| sizeof Operator         | Total memory of all elements | Size of the pointer itself     |
| Arithmetic              | Limited (`A++` illegal)      | Full pointer arithmetic allowed |
| Function Parameter Form | Decays to pointer            | Naturally a pointer            |

> **Conclusion:**
> Arrays and pointers in C share similar behaviors in terms of element access, but they are fundamentally different entities. Understanding their differences is crucial for safe memory manipulation and efficient programming in C.

---

## Section 1.10. Exercises

### 1.10.1. Polynomail with Array

### 1.10.2. Sparse Matrix with Array

---
**References**  
- Kernighan & Ritchie, *The C Programming Language*, 2nd Edition  
- ISO/IEC 9899:1999 
- CS50: Pointers and Memory Layout
- GeeksforGeeks: [Static Arrays in C](https://www.geeksforgeeks.org/arrays-in-c-cpp/)

---