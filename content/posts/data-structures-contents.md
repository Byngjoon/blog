+++
date = '2025-05-17T04:16:57+09:00'
title = '[Data Structures] Contents'
description = ""
categories = ["Computer Science/Algorithms & Data Structures"]
tags = ["Data Structures"]
math = true
draft = false
toc = false
+++

# Data Structures Study Outline with C Language Implementation

---

## Chapter 00. [Introduction to Data Structures]({{< relref "posts/data-structures-00.md" >}})
- Section 0.1. What Is the Study of Data Structures?
- Section 0.2. Data Type vs Data Structure
- Section 0.3. Learn about Abstract Data Types (ADT)
- Section 0.4. Classification of Data Structures
	- By Structural Form, By Storage Method, By Access Pattern, By Usage Level
- Section 0.5. C Language Essentials for Data Structures

---

## Chapter 01. [Array ADT and Implementation]({{< relref "posts/data-structures-01.md" >}})
- Section 1.1. Array Abstract Data Type (ADT)
- Section 1.2. What Is an Array in C?
- Section 1.3. Implementing Static Arrays in C
- Section 1.4. Memory Model and Pointer Behavior in Arrays
- Section 1.5. Multidimensional Arrays
- Section 1.6. Dynamic (Resizable) Arrays in C
- Section 1.7. Limitations of Arrays and Why Linked Lists Are Needed
- Section 1.8. Arrays vs Pointers in C (optional)

---

## Chapter 02. [List ADT and Linked List Implementation]({{< relref "posts/data-structures-02.md" >}})
- Section 2.1. Linked List Abstract Data Type (ADT)
- Section 2.2. Singly Linked List
- Section 2.3. Doubly Linked List
- Section 2.4. Circular Linked List
- Section 2.5. Linked List Operations in C
- Section 2.6. Time and Space Complexity
- Section 2.7. Array vs Linked List
- Section 2.8. Common Interview Questions on Linked Lists

---
<!--

## Chapter 03. Stack
- Section 3.1. LIFO Principle
- Section 3.2. Implementation (Array vs Linked List)
- Section 3.3. Applications of Stack
- Section 3.4. Time and Space Complexity

---

## Chapter 04. Queue
- Section 4.1. FIFO Principle
- Section 4.2. Linear and Circular Queue
- Section 4.3. Deque (Double-Ended Queue)
- Section 4.4. Priority Queue
- Section 4.5. Applications and Complexity

---

## Chapter 05. Recursion
- Section 5.1. Concept and Stack Relation
- Section 5.2. Base Case and Recursive Case
- Section 5.3. Tail Recursion
- Section 5.4. Recursion vs Iteration

---

## Chapter 06. Tree
- Section 6.1. Terminology and Properties
- Section 6.2. Binary Tree and Traversal
- Section 6.3. Binary Search Tree
- Section 6.4. Balanced Trees (AVL, Red-Black)
- Section 6.5. Heap

---

## Chapter 07. Graph
- Section 7.1. Representation (Matrix vs List)
- Section 7.2. Traversal (DFS, BFS)
- Section 7.3. Shortest Paths (Dijkstra)
- Section 7.4. Minimum Spanning Tree (Kruskal, Prim)

---

## Chapter 08. Hash Table
- Section 8.1. Hash Functions
- Section 8.2. Collision Resolution
- Section 8.3. Hash Maps vs Sets
- Section 8.4. Applications

---

## Chapter 09. String Algorithms
- Section 9.1. Memory Representation
- Section 9.2. Pattern Matching (KMP, Rabin-Karp, Boyer-Moore)
- Section 9.3. Practical Applications

---

## Chapter 10. Trie
- Section 10.1. Prefix Tree Concept
- Section 10.2. Insertion and Search
- Section 10.3. Use Cases in Auto-completion and Dictionaries

---

## Chapter 11. Segment Tree
- Section 11.1. Motivation and Structure
- Section 11.2. Range Query and Update
- Section 11.3. Complexity Analysis

---

## Chapter 12. Fenwick Tree (Binary Indexed Tree)
- Section 12.1. Introduction and Comparison with Segment Tree
- Section 12.2. Prefix Sums
- Section 12.3. Update and Query Operations

---

## Chapter 13. Union-Find (Disjoint Set)
- Section 13.1. Union and Find Operations
- Section 13.2. Path Compression and Union by Rank
- Section 13.3. Applications (e.g. Kruskal)

---

## Chapter 14. B-Tree and B+ Tree
- Section 14.1. Structure and Properties
- Section 14.2. Use in Databases and File Systems

---

## Chapter 15. Complexity Analysis
- Section 15.1. Big-O, Big-Ω, Big-Θ Notations
- Section 15.2. Time and Space Comparison Table

---

## Chapter 16. Data Structure Selection Guide
- Section 16.1. Choosing the Right Structure Based on Use Case
- Section 16.2. Memory vs Speed Trade-offs

---


<!--
## Chapter 01. Linear Data Structures
- Section 1.1. Array
- Section 1.2. Linked List
  - Section 1.2.1. Singly Linked List
  - Section 1.2.2. Doubly Linked List
  - Section 1.2.3. Circular Linked List
- Section 1.3. Stack
- Section 1.4. Queue
  - Section 1.4.1. Linear Queue
  - Section 1.4.2. Circular Queue
  - Section 1.4.3. Deque (Double-Ended Queue)
  - Section 1.4.4. Priority Queue

## Chapter 02. Recursion and Stack Applications
- Section 2.1. Understanding Recursion
- Section 2.2. Relation between Recursion and Stack
- Section 2.3. Space and Time Complexity in Recursion

## Chapter 03. Tree Structures
- Section 3.1. Basic Terminology and Concepts
- Section 3.2. Binary Tree and Traversal Techniques
  - Section 3.2.1. Preorder, Inorder, Postorder, Level-order
- Section 3.3. Binary Search Tree (BST)
- Section 3.4. Balanced Binary Trees
  - Section 3.4.1. AVL Tree
  - Section 3.4.2. Red-Black Tree
- Section 3.5. Heap

## Chapter 04. Graph Structures
- Section 4.1. Definitions and Representations
  - Section 4.1.1. Adjacency Matrix
  - Section 4.1.2. Adjacency List
- Section 4.2. Graph Traversal Algorithms
  - Section 4.2.1. Depth-First Search (DFS)
  - Section 4.2.2. Breadth-First Search (BFS)
- Section 4.3. Weighted Graphs and Shortest Paths
  - Section 4.3.1. Dijkstra’s Algorithm
- Section 4.4. Minimum Spanning Tree (MST)
  - Section 4.4.1. Kruskal’s Algorithm
  - Section 4.4.2. Prim’s Algorithm

## Chapter 05. Hashing
- Section 5.1. Hash Tables and Hash Functions
- Section 5.2. Collision Resolution Techniques
  - Section 5.2.1. Chaining
  - Section 5.2.2. Open Addressing
- Section 5.3. Hash Maps vs Hash Sets

## Chapter 06. String Data Structures
- Section 6.1. String Representation in Memory
- Section 6.2. String Matching Algorithms
  - Section 6.2.1. KMP Algorithm
  - Section 6.2.2. Rabin-Karp Algorithm
  - Section 6.2.3. Boyer-Moore Algorithm

## Chapter 07. Advanced Data Structures
- Section 7.1. Trie (Prefix Tree)
- Section 7.2. Segment Tree
- Section 7.3. Fenwick Tree (Binary Indexed Tree)
- Section 7.4. Union-Find (Disjoint Set)
- Section 7.5. B-Tree and B+ Tree

## Chapter 08. Complexity Analysis
- Section 8.1. Big-O, Big-Ω, Big-Θ Notations
- Section 8.2. Time and Space Complexity of Major Structures

## Chapter 09. Data Structure Selection Guide
- Section 9.1. Choosing the Right Data Structure
- Section 9.2. Trade-offs Between Memory and Speed
-->

<!--
Chapter 02. Linked Lists
	•	Understand node-based storage using pointers
	•	Explore singly, doubly, and circular linked lists
	•	Compare linked lists with arrays in terms of performance and use cases

Chapter 03. Stacks and Queues
	•	Learn the principles of LIFO (Stack) and FIFO (Queue)
	•	Implement stack and queue using arrays and linked lists
	•	Understand real-world applications like Undo, BFS, etc.

Chapter 04. Recursion & Call Stack
	•	Understand how recursion uses the call stack
	•	Compare iterative and recursive approaches
	•	Optimize recursive functions and avoid stack overflow

Chapter 05. Trees
	•	Learn tree terminology (root, leaf, height, etc.)
	•	Explore binary trees and traversal methods
	•	Understand binary search trees (BST) and balanced trees
	•	Study heaps and priority queue implementation

Chapter 06. Hashing
	•	Learn how hash tables map keys to values
	•	Understand hash functions and collision resolution techniques
	•	Apply hash maps in real-world problems

Chapter 07. Graphs
	•	Explore graph representations: adjacency matrix and list
	•	Implement DFS and BFS for traversal
	•	Understand directed/undirected and weighted/unweighted graphs
	•	Apply graph algorithms: shortest path, topological sort

Chapter 08. Advanced Structures
	•	Study trie for prefix-based string search
	•	Learn disjoint set (union-find) and its use in connectivity problems
	•	Understand segment trees and Fenwick trees for range queries
	•	Get a glimpse of B-Trees and skip lists

Chapter 09. Complexity & Trade-Offs
	•	Analyze time and space complexity of data structures
	•	Learn how to choose the right data structure for a given problem
	•	Discuss trade-offs between speed, memory, and implementation complexity

Chapter 10. Practice & Implementation
	•	Implement core data structures in code (C/Python/Java)
	•	Solve problems on platforms like LeetCode, Baekjoon, etc.
	•	Practice debugging and test-driven development
	•	Learn how to recognize and apply structures in real-world scenarios



- check complexity -> algorithms
- recursion -> after stack and with call stack


## Chapter 04. Stacks
- Stack ADT and use cases
- Array-based stack implementation
- Linked list-based stack implementation
- Stack applications (undo, parentheses checker, etc.)

## Chapter 05. Queues
- Queue ADT and use cases
- Linear Queue and Circular Queue
- Array vs Linked List implementations
- Deque and Priority Queue (basic)

## Chapter 06. Trees
- Tree terminology and representation
- Binary Tree and Traversal (Pre/In/Post-order)
- Binary Search Tree (BST)
- Tree applications and recursive implementation
- Brief intro to AVL/Red-Black Trees

## Chapter 07. Heaps & Priority Queues
- Max Heap / Min Heap
- Array representation of heaps
- Heap sort
- Priority Queue ADT and its applications

## Chapter 08. Hashing
- Hash functions and collision handling
- Open Addressing / Separate Chaining
- Hash Tables in C
- Applications (lookup, duplicate detection)

## Chapter 09. Graphs
- Graph representation (adjacency list/matrix)
- DFS & BFS (recursive & iterative)
- Directed/undirected, weighted/unweighted graphs
- Applications: shortest path (intro), topological sort

## Chapter 10. Advanced Structures
- Trie (Prefix Tree)
- Disjoint Set (Union-Find)
- Segment Tree / Fenwick Tree (optional)
- Skip List / B-Tree (conceptual overview)

## Chapter 11. Complexity & Design Trade-offs
- Time and Space Complexity of each structure
- Choosing the right data structure
- Trade-offs: speed vs memory vs simplicity

## Chapter 12. Practice & Implementation
- Coding common structures in C
- Debugging dynamic memory (Valgrind, etc.)
- LeetCode / 백준 / 프로그래머스 추천 문제
- Structuring reusable modules in C

-->