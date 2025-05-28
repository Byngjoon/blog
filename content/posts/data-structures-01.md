+++
date = '2025-05-17T07:27:31+09:00'
title = '[Data Structures] [01] Array Abstract Data Type (ADT)'
description = "Understanding the Array Abstract Data Type in Data Structures"
categories = ["Computer Science/Algorithms & Data Structures"]
tags = ["Data Structures"]
slug = "array-adt"
math = true
draft = true
+++

# Chapter 01. Array Abstract Data Type (ADT)

> **Outline:** This chapter introduces the logical concept of the Array ADT and connects it to concrete implementations in C. It covers the concepts of arrays, memory layout, pointer relationships, and discusses the limitations of arrays that motivate the use of linked lists.

---

## 📑 Contents

- [1.1. Array Abstract Data Type (ADT)](#array-abstract-data-type-adt)
- [1.2. What is an Array in C?](#what-is-an-array-in-c)
- [1.3. One-dimensional Arrays](#one-dimensional-arrays)
- [1.4. Memory Layout of Arrays](#memory-layout-of-arrays)
- [1.5. Array vs Pointer](#array-vs-pointer)
- [1.6. Multidimensional (Nested) Arrays](#multidimensional-nested-arrays)
- [1.7. Limitations of Arrays and Motivation for Linked Lists](#limitations-of-arrays-and-motivation-for-linked-lists)

---

## Section 1.1. Array Abstract Data Type (ADT)
An **Array ADT** is a collection of ordered pairs **⟨index, value⟩**, where each index maps to a corresponding value.
**Logical model** of data that allows indexed access to a sequence of elements.

- Objects: A **fixed-size**, **indexed** sequence of elements of the **same type**.
- Operations:
    - `create(size)` ::= Creates an array that can hold `size` number of elements.
    - `get(A, i)` ::= Returns the element at index `i` from array `A`.
    - `set(A, i, v)` ::= Stores value `v` at index `i` in array `A`.

> Indices(index 복수) are typically zero-based, and valid indices range from `0` to `size - 1`.
> Key points in array **'ADT'**: Indexed Access, Fixed Size(<- create(size)), Homogeneous(동종의) Elements (Same Type)

---

## Section 1.02. What is an Array in C?
An **array in C** is a **fixed-size** collection of elements of the **same data type**, stored in **contiguous block** of memory. It allows **indexed access** to each element using square brackets `[]`.

---

### Declaration

```c
int numbers[5];           // declares an array of 5 integers
char name[10];            // array of 10 characters (useful for strings)
```

- The size must be a **constant** at compile time.
- Indexing starts at `0` (i.e., the first element is `arr[0]`, the last is `arr[size - 1]`).

---

### Initialization

```c
int scores[3] = {90, 80, 70};        // full initialization
int zeros[5] = {0};                 // initializes all to 0
```

- Uninitialized elements are filled with `0` only if((충족)한다면) at least one initializer is provided.

---

### Access and Assignment

```c
scores[1] = 85;                     // update value
printf("%d", scores[1]);           // access value
```

- A contiguous block of memory allows for efficient random access to array elements using index arithmetic.
    - (\text{Address of } arr[i] = \text{base\_address} + (i \times \text{element\_size}))
- Accessing an out-of-bounds index leads to **undefined behavior**, due to the lack of built-in bounds checking in C.

---

### Characteristics

| Feature              | Description                            |
|----------------------|----------------------------------------|
| Fixed size           | Must be declared with a known size     |
| Static allocation    | Memory allocated at compile time       |
| Same-type elements   | All elements must be of one data type  |
| Index-based access   | Direct access via zero-based indexing  |

---

### Array ADT vs Array in C

| Feature                         | Array ADT (Abstract)                              | Array in C (Implementation)                              |
|----------------------------------|----------------------------------------------------|-----------------------------------------------------------|
| **Definition Level**             | Logical model                                      | Language-level memory construct                          |
| **Size**                         | Fixed at creation (`create(size)`)                | Fixed at declaration (compile-time constant)             |
| **Element Type**                 | Homogeneous (same data type)                      | Must be same type (enforced by compiler)                 |
| **Indexing**                     | Must support indexed access (e.g., `get(i)`)      | Zero-based indexing with `arr[i]`                        |
| **Memory Layout**                | Abstract – does not specify how memory is arranged | Contiguous memory layout                                 |
| **Bounds Checking**              | Not defined (depends on implementation)           | ❌ No built-in bounds checking                           |
| **Mutability**                  | Allows `set(i, value)` operation                   | Allows mutation via `arr[i] = value`                     |
| **Language Independence**        | Yes                                               | No (specific to C)                                        |


---

> Arrays in C provide efficient random(임의) access due to their contiguous memory layout,  
> but they have limitations such as a **fixed size** and **the lack of built-in bounds checking**.

---

## Section 1.03. One-dimensional Arrays

* Store linear sequences of elements
* Typical operations: traverse, update, sum, search
* Loop-based access using index variable

## Section 04. Memory Layout of Arrays

* Stored in contiguous memory
* Access via offset: `arr[i] == *(arr + i)`
* Supports pointer arithmetic
* Memory layout impacts performance

## Section 05. Array vs Pointer

* Arrays decay to pointers when passed to functions
* `arr[i]` is equivalent to `*(arr + i)`
* But arrays and pointers are not exactly the same (arrays have fixed size)

## Section 06. Multidimensional (Nested) Arrays

* Declared as `int matrix[3][4];`
* Stored row-major in memory
* Access via `matrix[i][j]`

## Section 07. Limitations of Arrays and Motivation(동기) for Linked Lists(linked list 사용 이유)

* Fixed size at compile time
* Expensive insertion/deletion in the middle
* Static memory allocation
* Leads to the need for dynamic structures like Linked Lists
