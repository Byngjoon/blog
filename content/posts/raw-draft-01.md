+++
date = '2025-09-21T14:07:31+09:00'
title = '[Basic Knowledge] [02] Data Representation Part 02'
description = ""
categories = ["Computer Science/Basic Knowledge"]
tags = ["Basic Knowledge"]
slug = "basic-knowledge-02"
math = true
draft = true
+++

# Chapter 00. 

> **Outline:**

---

## Contents

- [0.1.]() 

---

## Topic 03: Integers Representation

> **Outline:** In real world, Human uses decimal system for integer, but computer uses binary system. Therefore, we faces difference between idea and implemetation in computing.

### Section 1.3.1. Unsigned Integer

Unsigned integer only have greater than and equal to 0 values. 

Given binary code A. A is w-bit set, $x_i$ is i-th elements of set A. (i = 0, 1, ...) (e.g. if A = {1, 2, 3}, then $x_0 = 3$)

Decimal value mapped from A is equal to $\sum_{i=0}^{w-1} x_i2^i$

Let us see example below.

| A | Decode | Decimal Value |
|:-:|:------:|:-------------:|
|0110| $0*2^3 + 1*2^2 + 1*2^1 + 0*2^0$ | 6|

---

### Section 1.3.2. Signed Integer