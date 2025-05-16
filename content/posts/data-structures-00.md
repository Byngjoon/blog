+++
date = 2025-05-17T07:20:49+09:00
title = "[Data Structures] [00] Introduction to Data Structures"
description = "The preface and core concepts of Data Structures series"
categories = ["Computer Science/Algorithms & Data Structures"]
tags = ["Data Structures"]
math = true
draft = false
+++
# Contents
1. [Data Structures](#what-is-data-structures-about)
2. [Data Type vs Data Structure](#data-type-vs-data-structure)
3. [Abstract Data Type](#what-is-an-abstract-data-type-adt)

---

# What is Data Structures about?

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

## Classification of Data Structures

### 1. By Structural Form

| Type               | Description                           | Examples                        |
|--------------------|---------------------------------------|----------------------------------|
| **Linear Structure**     | Data elements are arranged sequentially | Array, Linked List, Stack, Queue |
| **Non-linear Structure** | Data elements have hierarchical(계층적인) or graph-like relationships | Tree, Graph, Heap |
| **Hash-based Structure** | Data is accessed via keys and hash functions | Hash Table, Hash Map, Hash Set |

---

### 2. By Storage Method

| Type                    | Description                              | Examples                      |
|-------------------------|------------------------------------------|-------------------------------|
| **Sequential Storage**  | Data is stored in contiguous memory      | Array, Static Queue           |
| **Linked Storage**      | Nodes are connected via pointers         | Linked List, Tree, Graph      |
| **Indexed Storage**     | Access is based on key/index positions   | Hash Table, Skip List, B-Tree |

---

### 3. By Access Method

| Type                     | Description                              | Examples                       |
|--------------------------|------------------------------------------|--------------------------------|
| **Random Access**        | Direct access using index/key            | Array, Hash Table              |
| **Sequential Access**    | Access data in order, one by one         | Linked List, Queue            |
| **Hierarchical Access**  | Access through parent-child relationships| Tree, Heap                    |
| **Unstructured Access**  | Access based on arbitrary connections    | Graph                         |

---

# Why Do We Learn Data Structures?

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

# Data Type vs Data Structure

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

# What is an Abstract Data Type (ADT)?

An **Abstract Data Type (ADT)** defines a logical model (object) and a set of operations for handling data, while hiding the internal implementation details(구현 상세).

- We can see **what it does** (interface).
- We cannot see **how it works** (implementation).
- Therefore, users can use an ADT **without knowing its internal mechanism**.

---

## ADT Must Define Two Components

| Component              | Description                                                                 |
|------------------------|----------------------------------------------------------------------------|
| **Object**             | The type of data being handled (e.g., integers, a set of characters, etc.) |
| **Collection of Operations** | The set of valid actions to perform on the data (insert, delete, search, etc.)  |

---

### Examples of ADTs

#### 1. Stack ADT

| Component       | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| **Object**      | A collection of ordered elements (e.g., integers, characters, etc.)         |
| **Operations**  | `push(x)`, `pop()`, `peek()`, `isEmpty()`, ...                              |
| **Characteristics** | Follows **LIFO (Last-In, First-Out)** principle; the most recently added element is removed first |

> The stack can be implemented using an **array** or a **linked list**,  
> but the user only needs to know the **interface**, not the implementation.

---

#### 2. Queue ADT

| Component       | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| **Object**      | A linear collection representing a waiting line                             |
| **Operations**  | `enqueue(x)`, `dequeue()`, `front()`, `isEmpty()`, ...                      |
| **Characteristics** | Follows **FIFO (First-In, First-Out)** principle; the earliest added element is removed first |

---

#### 3. List ADT

| Component       | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| **Object**      | A sequence of elements with index-based access                              |
| **Operations**  | `insert(i, x)`, `delete(i)`, `get(i)`, `find(x)`, ...                       |
| **Characteristics** | Supports **indexed access**; can be implemented with arrays or linked structures |

---

## ADT vs Data Structure

| Aspect    | ADT (Abstract Data Type)                        | Data Structure                                 |
|-----------|--------------------------------------------------|------------------------------------------------|
| Perspective | Conceptual interface (what it does)           | Concrete implementation (how it works)         |
| Examples  | Stack, Queue, List                              | Array, Linked List, Tree, Hash Table           |
| Focus     | What operations are supported                   | How those operations are implemented efficiently |
| Purpose   | Provide a simple and clear interface to users   | Optimize performance through implementation choices |

---

## Why Do We Use ADTs?

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