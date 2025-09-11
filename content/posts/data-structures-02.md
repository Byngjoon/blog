+++
date = '2025-06-02T14:32:06+09:00'
title = '[Data Structures] [02] List ADT and Linked List Implementation Part 01'
description = "Understanding the List Abstract Data Type in Data Structures and Its Implementation Using Linked Lists in C"
categories = ["Computer Science/Algorithms & Data Structures"]
tags = ["Data Structures"]
slug = "linked-list-adt"
math = true
draft = true
+++

# Chapter 02. List ADT and Linked List Implementation

> **Outline:** We study the abstract List ADT and its implementation using Linked Lists. This includes singly, doubly, and circular linked lists, their operations, and performance trade-offs compared to array-based lists.

---

## Contents

- [2.1. What Is the List ADT?](#section-21-what-is-the-list-adt)
- [2.2. Array ADT vs List ADT](#section-22-array-adt-vs-list-adt)
- [2.3. What Is an Array List?](#section-23-what-is-an-array-list)
- [2.4. What Is a Linked List?](#section-24-what-is-a-linked-list)
- [2.5. Is a Linked List an ADT or an Implementation?](#section-25-is-a-linked-list-an-adt-or-an-implementation)
- [2.6. Why Use Linked Lists?](#section-26-why-use-linked-lists)
- [2.7. Singly Linked List](#section-27-singly-linked-list)
- [2.8. Doubly Linked List](#section-28-doubly-linked-list)
- [2.9. Circular Linked List](#section-29-circular-linked-list)
- [2.10. Linked List Operations in C](#section-210-linked-list-operations-in-c)
- [2.11. Time and Space Complexity](#section-211-time-and-space-complexity)
- [2.12. Array-based List vs Linked List](#section-212-array-based-list-vs-linked-list)
- [2.13. Common Interview Questions on Linked Lists](#section-213-common-interview-questions-on-linked-lists)

---

## Section 2.1. What Is the List ADT?

### 2.1.1. Definition of the List ADT

The **List Abstract Data Type (ADT)** represents a **linear**, **ordered** collection of elements, where the position of each element matters.  
It supports a set of abstract operations such as insertion, deletion, and traversal.

> Unlike stacks or queues, a list allows access and modification at **arbitrary positions**, not just the front or rear.

---

**Essential Properties of List ADT**

| Property          | Description                                              |
|-------------------|----------------------------------------------------------|
| **Linear Order**  | Elements have a specific order from first to last        |
| **Position-based**| Operations can refer to specific positions (e.g., index) |
| **Variable Size** | Can grow or shrink dynamically                           |

---

### 2.1.2. List ADT Specification

A **List ADT** is a linear collection of elements with a **finite, ordered sequence**.  
Each element has a position, and the list supports both **value-based** and **position-based** operations.

---

- **Object:**  
    Let `L` be a list of elements `⟨e₀, e₁, ..., eₙ₋₁⟩`.

| Component    | Description                                   |
|--------------|-----------------------------------------------|
| `L[i]`       | Element at index `i`, where `0 ≤ i < size(L)` |
| `size(L)`    | Number of elements in the list                |
| `L.empty`    | Indicates whether the list is empty           |

> **Note:** In the context of Abstract Data Types (ADTs), an object component represents an *abstract property*, not a *concrete field*.  
> - `size(L)`: This is a logical property that is fundamental to many operations. In actual implementations, it may be stored explicitly(명시적으로) as a field (e.g., `L.size`).  
> - `L.empty`: This abstract property can be represented as a function such as `isEmpty(L)` in implementation.
---

- **Operations:**

    - `create()`  
      ::= Initializes and returns an empty list.

    - `insert(L, i, x)`  
      ::= Inserts element `x` at index `i` in list `L`.

    - `delete(L, i)`  
      ::= Deletes the element at index `i` from list `L`.

    - `get(L, i)`  
      ::= Returns the element at index `i` in list `L`.

    - `set(L, i, x)`  
      ::= Replaces the element at index `i` with `x` in list `L`.

    - `traverse(L)`  
      ::= Visits and processes all elements in list `L` from start to end.

    - `search(L, x)`  
      ::= Returns the index of element `x` in list `L`, or -1 if not found.

    - `size(L)`  
      ::= Returns the total number of elements in list `L`.

    - `isEmpty(L)`  
      ::= Returns true if list `L` contains no elements; otherwise false.

> These operations define the abstract behavior of a list, regardless of its underlying implementation.

---

**Summary of operations**

| Operation   | Time Complexity  | Notes                                                  |
|-------------|------------------|--------------------------------------------------------|
| `create()`  | O(1)             | Constant-time initialization                           |
| `insert(i)` | O(n)             | Depends on implementation; O(1) for head in linked list |
| `delete(i)` | O(n)             | May require traversal to index                         |
| `get(i)`    | O(n) or O(1)     | O(1) for array, O(n) for linked list                   |
| `set(i)`    | O(n) or O(1)     | Same as above                                          |
| `search(x)` | O(n)             | Linear search                                          |
| `traverse()`| O(n)             | Visit all elements                                     |

> Note: These complexities depend on the **underlying implementation**:  
> - **Array List** → Fast access (`O(1)`) but expensive insert/delete  
> - **Linked List** → Efficient insert/delete (`O(1)` at head), but slow access (`O(n)`)

---

**Summary**  
The List ADT defines a flexible structure for managing linear data.  
Its abstract operations are common across all implementations, but **their efficiency varies** by choice of data structure.

---


### 2.1.3. When to Use List ADT

The List ADT is useful when:
- You need a flexible, linear structure to insert/delete at arbitrary positions
- You don’t know the number of elements in advance
- The order of elements is important

---

## Section 2.2. Array ADT vs List ADT

### 2.2.1. Conceptual Comparison

The **Array ADT** and the **List ADT** are both abstract data types used to model linear collections of elements.  
However, they differ in flexibility, memory behavior, and supported operations.

| Feature               | Array ADT                                       | List ADT                                        |
|------------------------|--------------------------------------------------|-------------------------------------------------|
| **Structure**          | Indexed sequence                                | Ordered collection                              |
| **Size**               | Fixed at creation                               | Dynamic (can grow/shrink)                       |
| **Access**             | Random access by index                          | Sequential access by traversal                  |
| **Indexing Support**   | Required (0-based integer index)                | Optional; defined by position conceptually      |
| **Insertion/Deletion** | Inefficient except at end (due to shifting)     | Efficient at arbitrary positions                |
| **Element Type**       | Homogeneous (same type)                         | Typically homogeneous (but not strictly required)|
| **Abstraction Level**  | Abstract model, not tied to physical memory     | Same – logical model, memory-independent        |

> **Note:** Both ADTs define logical models for organizing data.  
> Their differences lie in access patterns, mutability, and structural flexibility—not in implementation.

---

### 2.2.2. Example Operation Differences

| Operation       | Array ADT                     | List ADT                                  |
|------------------|-------------------------------|--------------------------------------------|
| `insert(A, i, x)`| O(n) – shift required         | O(1) at head (if Linked List)              |
| `delete(A, i)`   | O(n) – shift required         | O(1) at head (if Linked List)              |
| `get(A, i)`      | O(1) – direct access          | O(n) – must traverse from front            |
| `size(A)`        | O(1)                          | O(1) or O(n), depending on implementation  |

---

### 2.2.3. When to Use Each ADT

- **Use Array ADT**:
  - When the number of elements is known in advance
  - When constant-time access by index is required
  - When memory locality matters (e.g., cache-friendly)

- **Use List ADT**:
  - When the number of elements changes frequently
  - When insertions and deletions occur frequently at arbitrary positions
  - When you want to avoid resizing overhead

---

### 2.2.4. Summary

- The **Array ADT** is a specialized form of the List ADT with additional constraints:
    - Fixed size
    - Contiguous conceptual layout
    - Fast indexed access
- The **List ADT** is more general and abstract, supporting a wider variety of implementations such as **linked lists**, **array lists**, etc.

> In short, **Array ADT = List ADT + Fixed Size + Homogeneous Index-Based Access Model**.

---

## Section 2.3. What Is an Array List?

### 2.3.1. Definition

An **Array List** is a **concrete implementation** of the List ADT using a **contiguous block of memory**, typically realized as an underlying array.  
It supports **index-based access** and provides **dynamic resizing** when capacity is exceeded.

Internally, an array list maintains two separate concepts:

- **Size** (`n`): the current number of elements stored
- **Capacity** (`c`): the maximum number of elements the current array can hold

---

### 2.3.2 Key Points

**Core Properties**

| Property             | Description                                                  |
|----------------------|--------------------------------------------------------------|
| **Underlying Structure** | Array (contiguous memory)                             |
| **Resizable**        | Grows (and sometimes shrinks) as needed                     |
| **Indexed Access**   | Provides fast O(1) access via array indexing                |
| **Insert/Delete**    | Costly at arbitrary positions due to element shifting       |
| **Capacity and Size** | Maintains separate notions of logical size and capacity     |

---

**Key Differences from Related Structures:**

| Comparison Target | Array List vs Target                               |
|-------------------|----------------------------------------------------|
| **Static Array**  | Array List resizes dynamically; static array does not |
| **Linked List**   | Array List provides O(1) indexed access; linked list provides O(1) insertion/deletion (at ends) |
| **Array ADT**     | Array ADT is abstract; Array List is a concrete realization with resizing strategy |

---

**Advantages and Limitations**

| Aspect               | Advantage                                     | Limitation                                        |
|----------------------|-----------------------------------------------|---------------------------------------------------|
| **Access**           | Constant-time indexed access (O(1))           |                                                   |
| **Insertion (end)**  | Amortized O(1) when appending at the end      | Reallocation may be costly in some scenarios      |
| **Insertion (middle)**| Requires shifting elements (O(n))            |                                                   |
| **Memory Efficiency**| Pre-allocated space reduces frequent copying  | May use extra space due to reserved capacity      |

---

### 2.3.3. Why Contiguous Memory Is Required for Array Lists

Array List implementations are based on arrays and therefore **require elements to be stored in contiguous memory**. This is an essential property that enables efficient index-based access and memory operations.

---

**Key Reasons**

| Reason                        | Explanation                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| **Indexed Access in O(1)**   | Given index `i`, address = `base + i × size`; works only with contiguous layout |
| **Efficient Resizing**       | Data must be copied to a new array during reallocation; contiguous memory is needed |
| **CPU Cache Efficiency**     | Sequential layout improves spatial locality and speeds up traversal         |
| **Language-level Constraints** | Array-based structures in C/C++/Java are natively contiguous                |

---

**Address Calculation Example**

    address_of(arr[i]) = base_address + i × sizeof(element)

This formula only works if all elements are laid out continuously in memory.

---

**Comparison**

| Structure       | Memory Layout        | Indexed Access | Dynamic Resizing | Cache Efficiency |
|----------------|----------------------|----------------|------------------|------------------|
| **Array List** | Contiguous (Required)| O(1)           | Yes (with copy)  | High             |
| Linked List     | Non-contiguous       | O(n)           | Yes (node-based) | Low              |

---

**Summary**

Contiguous memory layout is **non-negotiable** for array lists. It directly enables:

- Constant-time random access (`get(i)`, `set(i, x)`)
- Fast copy and reallocation for dynamic growth
- Improved performance due to better cache usage

---

### 2.3.4. Abstract View

Let `A` be an array list of size `n` and capacity `c`.

- Elements: `⟨A[0], A[1], ..., A[n-1]⟩`  
- Capacity: Total allocated space (`c ≥ n`)
- Size: Number of actual elements stored (`n ≤ c`)

Resize Strategy (typical):  
When size `n` reaches capacity `c` (i.e., `n == c`), the array list **automatically resizes** by:
1. Allocating a larger block of memory (commonly 2× the previous capacity),
2. Copying all existing elements to the new array,
3. Releasing the old memory,
4. Updating the internal reference to the new array.

> It bridges the gap between fixed-size arrays and flexible lists by resizing the array when necessary.

---

### 2.3.5. When to Use

Use an **Array List** when:

- You need frequent **random access** (e.g., get/set by index)
- The number of elements changes, but not drastically
- You prefer simpler memory management over fine-grained control

Avoid when:

- Frequent insertions/deletions occur at arbitrary positions
- Predictable memory usage is critical (due to resizing overhead)

---

**Summary**  
Array List is a hybrid between arrays and lists:  
It retains fast indexed access while offering dynamic growth, making it ideal for many general-purpose use cases.

---

### 2.3.6. Example of implementation in C


---
## Section 2.4. What Is a Linked List?

### 2.4.1. Basic Concepts

A **linked list** is a concrete implementation of the list ADT, in which elements (called **nodes**) are connected by reference (like **pointers**), not stored contiguously in memory like array-based lists. Each node contains two components:
- **Data**: the element’s value (i.e., the value stored in the node).
- **Link**: a reference (like pointer) to the next(or previous) node in the list.

> It defines a collection of elements arranged in a **linear sequence**.

---

**Basic node structure:**

    ⟨data₁, next₁⟩ → ⟨data₂, next₂⟩ → ... → ⟨dataₙ, NULL⟩

---

**Variants of Linked List**

| Type                  | Description                                            |
|-----------------------|--------------------------------------------------------|
| **Singly Linked List**| Each node points to the next only                      |
| **Doubly Linked List**| Each node points to both next and previous             |
| **Circular Linked List**| Last node points back to the first                   |

> Other implementations of the List ADT include **Array List**, **Vector (in C++)**, and **Dynamic Arrays**.

---

### 2.4.2. Key Points

**Key characteristics:**

| Feature                  | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| Dynamic memory allocation | Nodes are allocated individually on the heap                              |
| Non-contiguous storage    | Nodes may reside anywhere in memory, linked through pointers              |
| Variable size             | The list can grow or shrink during runtime                                |
| Sequential access only    | No direct indexing; must traverse from head to access an element          |
| Efficient insert/delete   | Especially at the beginning (head) or middle, compared to arrays          |
| Extra memory overhead     | Each node needs additional space for a pointer field                      |

---

**Limitations**

- Accessing an element at a given position requires traversal from the head.
- Extra memory usage due to pointer storage in each node.
- Complex pointer manipulation is error-prone (e.g., memory leaks or dangling pointers).

---

### 2.4.3. Abstract View

- **Objects**:  
  A sequence of nodes, where each node contains **data** and a **link** (reference) to the next node.

- **Operations**:

    - `create()`  
      ::= Initializes an empty linked list.

    - `insert(L, i, x)`  
      ::= Inserts element `x` at position `i` in linked list `L`.

    - `delete(L, i)`  
      ::= Deletes the node at position `i` in linked list `L`.

    - `search(L, x)`  
      ::= Returns the position of element `x` in `L`, if found.

    - `traverse(L)`  
      ::= Visits each node in the list from head to tail.

    - `isEmpty(L)`  
      ::= Returns true if list `L` has no nodes.

    - `size(L)`  
      ::= Returns the number of nodes in `L`.

---

**Summary**

| Operation | Signature            | Time Complexity | Remarks                                                |
|-----------|----------------------|------------------|-------------------------------------------------------|
| Create    | `create()`           | O(1)             | Initializes an empty list                             |
| Insert    | `insert(L, i, x)`    | O(n)             | Efficient at head (O(1)); needs traversal for middle  |
| Delete    | `delete(L, i)`       | O(n)             | Requires traversal to reach index                     |
| Search    | `search(L, x)`       | O(n)             | Linear search; returns position if found              |
| Traverse  | `traverse(L)`        | O(n)             | Visits all nodes in sequence                          |
| isEmpty   | `isEmpty(L)`         | O(1)             | Checks if head pointer is NULL                        |
| Size      | `size(L)`            | O(n) or O(1)*     | O(n) if counted manually; O(1) if size is tracked    |

> *If a `size` field is maintained during insert/delete, the `size()` operation becomes O(1).
> Note: Position-based operations typically assume **0-based indexing** unless specified otherwise.

---

### 2.4.4. Comparison to Array List

| Aspect            | Linked List                                  | Array List                              |
|-------------------|-----------------------------------------------|------------------------------------------|
| **Memory layout** | Non-contiguous                                | Contiguous                              |
| **Access time**   | O(n) (sequential access only)                 | O(1) (random access by index)           |
| **Insert/delete** | O(1) at head; O(n) at arbitrary position      | O(n) due to shifting elements           |
| **Size**          | Dynamic (no fixed size)                       | Dynamic but involves costly resizing    |
| **Pointer usage** | Requires extra pointer per node              | No extra pointer overhead               |
| **Use case**      | Frequent insertions/deletions                | Frequent indexed access                 |

---

**Summary**

A **linked list** is an efficient structure when frequent **insertions and deletions** are expected, especially when the size of the list is not known in advance.  
However, for fast **indexed access**, array lists are more suitable due to their contiguous memory layout and constant-time indexing.

---

### 2.4.5. When to Use

Use a linked list when:
- You need frequent insertions and deletions
- You don’t know the number of elements in advance
- Memory efficiency in terms of resizing is more important than random access

Avoid when:
- You need fast random access
- Memory overhead from pointers is undesirable

---

### 2.4.6. Summary

- The Linked List is a flexible, dynamic linear data model.
- It defines a sequence of connected nodes with support for basic list operations.
- Understanding the ADT is essential before diving into specific implementations like singly, doubly, or circular linked lists.

---

## 2.5. Is a Linked List an ADT or an Implementation?

The term **linked list** is often used in two different contexts:

- As a **concrete implementation** of the **List ADT**
- As a **specialized abstract model** when its structural properties are considered essential

---

### 2.5.1 Interpretation as an Implementation
In most cases, a **linked list** refers to a **non-contiguous, pointer-based implementation** of the more general **List ADT**. It supports the same core operations: `insert`, `delete`, `get`, `set`, `size`, etc., but with different performance characteristics.

### 2.5.2 Interpretation as a Specialized ADT
In certain educational or analytical contexts, a **Linked List ADT** is treated as a **specialized abstract data type**, with the following defining properties:
- Nodes are connected by pointers
- Sequential access only (no random access)
- Dynamic size
- Emphasis on structural behaviors such as **node traversal**, **insertion at head**, etc.

This viewpoint is helpful when comparing **Singly**, **Doubly**, and **Circular** variants, each of which may have their own formal specification and interface.

In this perspectives, the **List ADT** is further divided into two concrete subtypes depending on the implementation strategy: **Array List ADT** and **Linked List ADT**.

---

#### 1. Array List ADT
- The list is implemented using a **contiguous block of memory** (array-based).
- Characteristics:
  - **Contiguous memory layout**
  - **O(1)** time for random access
  - **O(n)** time for insertion/deletion at arbitrary positions
  - Usually fixed or dynamically resized capacity

#### 2. Linked List ADT
- The list is implemented using **linked nodes** in **non-contiguous memory**.
- Characteristics:
  - **Non-contiguous memory layout**
  - **O(n)** time for access
  - **O(1)** time for insertion/deletion at known positions
  - Requires extra memory for storing pointers

---

#### Summary

While both are implementations of the **same abstract List ADT**, they are sometimes treated as **sub-abstract types** for practical analysis. This distinction is useful when:
- Comparing **time/space complexity**
- Understanding **implementation trade-offs**
- Selecting an appropriate structure for a given use case

Formally, both **Array List** and **Linked List** are **concrete representations** (not distinct ADTs), but this split is pedagogically(교육학적으로) and practically meaningful.

> While a linked list is typically considered an *implementation* of the List ADT, it can also be analyzed as a *specialized ADT* in its own right when the linked structure becomes an essential part of the abstraction.

> Whether a linked list is treated as an implementation or as an ADT, it is clear that a linked list is closely related to the List ADT and shares its core properties.

---

[To the part 02...]