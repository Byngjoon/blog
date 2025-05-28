+++
date = '2025-05-17T07:20:49+09:00'
title = '[Data Structures] [00] Introduction to Data Structures'
description = "The preface and core concepts of Data Structures series"
categories = ["Computer Science/Algorithms & Data Structures"]
tags = ["Data Structures"]
slug = "introduction-to-data-structures"
math = true
draft = false
+++

# Chapter 00. Introduction to Data Structures

> **Outline:** This chapter provides a foundational overview of what data structures are, how they differ from data types, and why Abstract Data Types (ADTs) are essential. It also introduces basic C language concepts that are prerequisites(사전에 필요한) for understanding and implementing data structures.

---

## Contents
- [0.1. What is Data Structures about?](#section-01-what-is-data-structures-about)
- [0.2. Data Type vs Data Structure](#section-02-data-type-vs-data-structure)
- [0.3. What is an Abstract Data Type (ADT)?](#section-03-what-is-an-abstract-data-type-adt)
- [0.4. C Language Essentials for Data Structures](#section-04-c-language-essentials-for-data-structures)

---

## Section 0.1. What is Data Structures about?

Data Structures is the study of how to organize, store, and manage data **efficiently** in a computer system.

---

It focuses on designing ways to:
1.	Store data (**structure**)
    How to structure data (Arrays, Linked Lists, Trees, Graphs, Hash Tables, etc.)

2.	Access and modify data (**operations**)
    How to insert, delete, search, sort, and traverse data

3.	Optimize performance (**time & space complexity**)
    Measuring performance using time & space complexity (Big-O notation)
    Choosing the right data structure for different problems (e.g., using stacks for undo history)


---

### Classification of Data Structures

#### 1. By Structural Form

| Type               | Description                           | Examples                        |
|--------------------|---------------------------------------|----------------------------------|
| **Linear Structure**     | Data elements are arranged sequentially | Array, Linked List, Stack, Queue |
| **Non-linear Structure** | Data elements have hierarchical(계층적인) or graph-like relationships | Tree, Graph, Heap |
| **Hash-based Structure** | Data is accessed via keys and hash functions | Hash Table, Hash Map, Hash Set |

---

#### 2. By Storage Method

| Type                    | Description                              | Examples                      |
|-------------------------|------------------------------------------|-------------------------------|
| **Sequential Storage**  | Data is stored in contiguous memory      | Array, Static Queue           |
| **Linked Storage**      | Nodes are connected via pointers         | Linked List, Tree, Graph      |
| **Indexed Storage**     | Access is based on key/index positions   | Hash Table, Skip List, B-Tree |

---

#### 3. By Access Method

| Type                     | Description                              | Examples                       |
|--------------------------|------------------------------------------|--------------------------------|
| **Random Access**        | Direct access using index/key            | Array, Hash Table              |
| **Sequential Access**    | Access data in order, one by one         | Linked List, Queue            |
| **Hierarchical Access**  | Access through parent-child relationships| Tree, Heap                    |
| **Unstructured Access**  | Access based on arbitrary connections    | Graph                         |

---

### Why Do We Learn Data Structures?

To solve problems **efficiently** and **reliably**.

Even with a good algorithm, choosing the wrong data structure can waste **time** and **memory resources**.

---

| Problem Scenario              | Recommended Data Structure       |
|------------------------------|----------------------------------|
| Fast search                  | Hash Map                         |
| Frequent insertions/removals | Linked List                      |
| Undo feature                 | Stack                            |
| Ordered access               | Array, List                      |

---

## Section 0.2. Data Type vs Data Structure

**Data Type**: Defines the form and allowed operations for a single piece of data.  
- `int`: Represents a single integer value; supports arithmetic(산술) operations like addition, subtraction, etc.  
- `char`: Represents a single character; supports character encoding operations (e.g., ASCII manipulation)

**Data Structure**: Organizes, stores, accesses, and manages a **collection of data**.  
- `Array`: Stores elements in contiguous(인접한) memory locations  
- `Linked List`: Connects nodes using pointers to form a linear structure

| Aspect   | Data Type                         | Data Structure                                |
|----------|-----------------------------------|-----------------------------------------------|
| Purpose  | Define the kind of a single value | Organize and manage a group of related values |
| Examples | `int`, `float`, `char`, etc.      | `Array`, `Stack`, `Queue`, `Linked List`, etc.|
| Unit     | A single value                    | A collection of values                        |
| Focus    | The data itself                   | The relationship and operations among data    |

---

## Section 0.3. What is an Abstract Data Type (ADT)?

An **Abstract Data Type (ADT)** defines a logical model (object) and a set of operations for handling data, while hiding the internal implementation details(구현 상세).

- We can see **what it does** (interface).
- We cannot see **how it works** (implementation).
- Therefore, users can use an ADT **without knowing its internal mechanism**.

---

### ADT Must Define Two Components

| Component              | Description                                                                 |
|------------------------|----------------------------------------------------------------------------|
| **Object**             | The type of data being handled (e.g., integers, a set of characters, etc.) |
| **Collection of Operations** | The set of valid actions to perform on the data (insert, delete, search, etc.)  |

---

#### Examples of ADTs

##### 1. Stack ADT

| Component       | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| **Object**      | A collection of ordered elements (e.g., integers, characters, etc.)         |
| **Operations**  | `push(x)`, `pop()`, `peek()`, `isEmpty()`, ...                              |
| **Characteristics** | Follows **LIFO (Last-In, First-Out)** principle; the most recently added element is removed first |

> The stack can be implemented using an **array** or a **linked list**,  
> but the user only needs to know the **interface**, not the implementation.

---

##### 2. Queue ADT

| Component       | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| **Object**      | A linear collection representing a waiting line                             |
| **Operations**  | `enqueue(x)`, `dequeue()`, `front()`, `isEmpty()`, ...                      |
| **Characteristics** | Follows **FIFO (First-In, First-Out)** principle; the earliest added element is removed first |

---

##### 3. List ADT

| Component       | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| **Object**      | A sequence of elements with index-based access                              |
| **Operations**  | `insert(i, x)`, `delete(i)`, `get(i)`, `find(x)`, ...                       |
| **Characteristics** | Supports **indexed access**; can be implemented with arrays or linked structures |

---

### ADT vs Data Structure

| Aspect    | ADT (Abstract Data Type)                        | Data Structure                                 |
|-----------|--------------------------------------------------|------------------------------------------------|
| Perspective | Conceptual interface (what it does)           | Concrete implementation (how it works)         |
| Examples  | Stack, Queue, List                              | Array, Linked List, Tree, Hash Table           |
| Focus     | What operations are supported                   | How those operations are implemented efficiently |
| Purpose   | Provide a simple and clear interface to users   | Optimize performance through implementation choices |

---

### Why Do We Use ADTs?

1. **Abstraction**  
   Users can use data structures without knowing internal details.

2. **Modularity (Flexibility)**  
   If the ADT interface remains the same, the internal implementation can be changed without affecting user code.

3. **Reusability**  
   ADT-based designs can be reused in various problem domains with minimal modification.

4. **Data Protection**  
   The internal state is hidden, so users cannot tamper with it directly, ensuring consistency and integrity.

---

> **In summary**:  
> An ADT defines **what** data and operations are available, not **how** they are performed.  
> This separation allows for clean, maintainable, and flexible software design.

---

## Section 0.4. C Language Essentials for Data Structures

We will implement data structures using the C programming language.  
To do this effectively, we need to understand three core concepts:

- [What is a **struct** type in C?](#what-is-struct-type-in-c)
- [How do we use **pointers** in C?](#how-do-we-use-pointers-in-c)
- [How do we perform **dynamic memory allocation** in C?](#how-do-we-perform-dynamic-memory-allocation-in-c)
---

### What is `struct` type in C?

A `struct` (short for **structure**) in C is a **user-defined data type** that allows you to group variables of **different types** under a single name.

Unlike arrays, which access elements by index, a `struct` uses **named fields** to access its internal data.  
To access these fields, you use the **dot operator (`.`)**.

#### Example:

```c
struct Node {        // 'Node' is the struct type name
    int data;        // field
    struct Node* next; // field
};

struct Node node1;
node1.data = 10;     // Accessing the 'data' field using the dot operator
```
---

#### Memory Allocation of 'struct' Type

- A `struct` is stored in a **contiguous block of memory**, and its fields are laid out **in the order they are declared**.
- However, the **total memory size** of a `struct` may be **larger than the sum of its fields’ sizes** due to:
    - **Padding**: extra space inserted between fields
    - **Alignment rules**: used to optimize memory access performance on most architectures
    - You can check the actual memory allocated for a struct using sizeof(struct) in C.
  
These rules ensure that each field starts at a memory address aligned to its size (e.g., `int` on 4-byte boundaries, `double` on 8-byte boundaries).

##### Example:

```c
struct studentInfo {
    char name[10];
    int age;
    double gpa;
};
```
| Field       | Type         | Size (bytes) | Memory Offset | Notes                                     |
|-------------|--------------|--------------|----------------|-------------------------------------------|
| `name`      | `char[10]`   | 10           | 0–9            | Starts at offset 0                        |
| **padding** | —            | 2            | 10–11          | To align `int` to a 4-byte boundary       |
| `age`       | `int`        | 4            | 12–15          | 4-byte aligned                            |
| `gpa`       | `double`     | 8            | 16–23          | 8-byte aligned                            |
| **total**   | —            | **24 bytes** | —              | `sizeof(struct studentInfo) == 24`        |

---

### 'typedef' in C

- `typedef` is used to assign a custom alias(별칭) to an existing type.
- It helps simplify complex type names and improve code readability, especially with `struct`.

#### Example

```c
// typedef <type definition> <alias>
typedef struct Node {          // 'Node' is the struct tag
    int data;
    struct Node* next;
} Node;                        // 'Node' is now a type alias

typedef struct {
    char name[10];
    int age;
    double gpa;
} studentInfo;                 // Anonymous struct with alias 'studentInfo'

Node node1;
studentInfo s1;
```
>In this example:
>`Node` can now be used like a built-in type to declare variables
>`studentInfo` represents a structure without an explicit tag name

---
### How Do We Use Pointers in C?

A **pointer** is a variable that stores the **memory address** of another variable.

#### Basic Pointer Example

```c
int a = 10;
int *p;     // Declare a pointer to an int
p = &a;     // '&' (address-of operator): gets the address of variable 'a'
*p = 11;    // '*' (dereference operator): access or modify the value pointed to by 'p'
```

#### Type-Specific Pointer Examples

```c
double *pf;   // pf points to a double variable
char *pc;     // pc points to a char variable
double **ppf; // ppf is a pointer to a pointer to a double
char *ppc[];  // ppc is an array of pointers to char (e.g., array of strings)
```

> Pointer arithmetic depends on the size of the data type.  
> For example, `pf + 1` increases the address by `sizeof(double)` (typically 8 bytes),  
> while `pc + 1` increases by `sizeof(char)` (1 byte).

---

#### Special Types of Pointers

| Type           | Description |
|----------------|-------------|
| **NULL Pointer** | A pointer that doesn't point to any valid memory location (used for safety checks) |
| **`void *` Pointer (Generic Pointer)** | A pointer that can hold the address of any data type. It cannot be directly dereferenced without type casting, but can be automatically cast during assignment. |

```c
void *vp;
int x = 5;
vp = &x;        // okay: implicit cast to void*
printf("%d", *(int *)vp);  // must cast back to correct type to dereference
```

---

#### Summary

- `*` is used to declare a pointer and to dereference it.
- `&` gives the address of a variable.
- Pointers are powerful tools in C, essential for dynamic memory, arrays, structs, and efficient data structures.

---

### How Do We Perform Dynamic Memory Allocation in C?

**Dynamic memory allocation** means allocating memory **during the execution** of a program (at runtime), rather than at compile time.

- Memory is allocated **as needed**, and can be **released** once no longer required.
- This enables **efficient memory usage**, especially for data structures with variable size (e.g., linked lists, trees, etc.).

---

#### Basic Example

```c
#include <stdlib.h>

int *p;
p = (int *)malloc(sizeof(int)); // malloc returns void*, so explicit type casting is needed in C
if (p != NULL) {
    *p = 10; // assigning value to dynamically allocated memory
}

free(p); // Always free allocated memory after use to prevent memory leaks
```

---

#### Key Functions in `stdlib.h`

| Function | Purpose |
|----------|---------|
| `malloc(size)` | Allocates uninitialized memory of `size` bytes |
| `calloc(n, size)` | Allocates memory for `n` elements and initializes all to zero |
| `realloc(ptr, new_size)` | Resizes previously allocated memory block |
| `free(ptr)` | Frees the memory previously allocated by `malloc`, `calloc`, or `realloc` |

---

#### Notes

- Always check if `malloc()` or `calloc()` returns `NULL` (allocation failed).
- Memory leaks can occur if `free()` is forgotten.
- Memory allocated with `malloc()` remains until manually freed.