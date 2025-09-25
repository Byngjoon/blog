+++
date = '2025-09-11T13:27:31+09:00'
title = '[Basic Knowledge] [01] Data Representation Part 01'
description = ""
categories = ["Computer Science/Basic Knowledge"]
tags = ["Basic Knowledge"]
slug = "basic-knowledge-01"
math = true
draft = true
+++

# Contents

---

## Topic 01: Bit (Binary Digit) and Byte

- **Definition:** 
  - Bit is binary digit. Each bit is `0` or `1`.
  - Byte is

---

### Section 1.1.1. Why Does Computer Use Binary Systems?

In computer field, binary systems를 사용하는 가장 큰 이유는 안정적이고 경제적이기 때문이다. 첫번째로 안정성의 측면에서 보자면, computer hardware uses electronic signal for implementation. 이때, electronic signal을 여러 단계로 구분하게 되면 (e.g. 0, 1, 2, and 3) noise에 취약해진다. 반면에 when recognize signal only 두 개 (actually `0` or `1`), `0`은 전압 없음 (0V 근처), `1`은 전압 있음 (system에 따라 5V, 3V, etc.)으로 구분하게 되며 noise에 강해진다.
In the other, binary system 이상의 다진법 체계에서는 회로의 구성이 복잡해지고 noise 안정화가 필요하므로 경제적으로 불리하다. 실제로 binary system은 basic logic gate in boolean algebra (AND, OR, NOT)의 조합으로 많은 회로를 구성할 수 있다.

---

### Section 1.1.2. What Does Each bit mean?

| bit |  hardware  | Logical |
|:---:|:----------:|:-------:|
|  0  |   off, 0V  | false   |
|  1  | on, not 0V | true    |

Computer data의 최소 (저장) 단위

> MSB:
> LSB:
---

### Section 1.1.3. Bit Manipulations

Use Boolean Algebra. True equal to `1` and false equal to `0`.

1. AND: & (Ampersand)
A & B = 1 when both A = 1 and B = 1.
| & | 0 | 1 |
|:-:|:-:|:-:|
| 0 | 0 | 0 |
| 1 | 0 | 1 |

2. OR: | (Vertical Bar)  
A | B = 1 when at least one of A or B = 1. (when either A = 1 or B = 1)

| \| | 0 | 1 |
|:--:|:-:|:-:|
| 0  | 0 | 1 |
| 1  | 1 | 1 |


3. NOT: ~ (Tilde)  
~A = 1 when A = 0, and 0 when A = 1.  

| A | ~A |
|:-:|:--:|
| 0 | 1  |
| 1 | 0  |


4. Exclusive-OR (XOR): ^ (Caret)  
A ^ B = 1 when A not equal to B. (when either A = 1 or B = 1, but not both equal to 1.)

| ^ | 0 | 1 |
|:-:|:-:|:-:|
| 0 | 0 | 1 |
| 1 | 1 | 0 |

---

```c
unsigned char some_function(unsigned char *x, unsigned char *y)
{
  *y = *x ^ *y;
  *x = *x ^ *y;
  *y = *x ^ *y;
  return 0;
}
```
> temp

---

**Boolean Algebra Basic Rules**

1. Identity Laws (항등법칙)  
- A + 0 = 0 + A = A  
- A · 1 = 1 · A = A  

2. Domination Laws (지배법칙)  
- A + 1 = 1  
- A · 0 = 0  

3. Idempotent Laws (멱등법칙)  
- A + A = A  
- A · A = A  

4. Complement Laws (보수법칙)  
- A + A' = 1  
- A · A' = 0  

5. Commutative Laws (교환법칙)  
- A + B = B + A  
- A · B = B · A  

6. Associative Laws (결합법칙)  
- (A + B) + C = A + (B + C)  
- (A · B) · C = A · (B · C)  

7. Distributive Laws (분배법칙)  
- A · (B + C) = (A · B) + (A · C)  
- A + (B · C) = (A + B) · (A + C)  

8. De Morgan’s Laws (드모르간 법칙)  
- (A · B)' = A' + B'  
- (A + B)' = A' · B'  

> If want more of Boolean Algebra, click here.

---

### Section 1.1.4. Shift Operations

1. Left Shift: x << y
  - Logical Left Shift and Arithmecit Left Shift
    - Shift bit-vector x left ypositions
    - Throw away extra bits on left
    - Fill with 0’s on right

| x | 11001001 |
|:-:|:--------:|
| Logical << 2    | 00100100 |
| Arithmetic << 2 | 00100100 |

> A << x: $A * 2^x$

---

2. Right Shift: x >> y
  - Logical Right Shift
    - Shift bit-vector x right ypositions
    - Throw away extra bits on right
    - Fill with 0’s on left
  - Arithmecit Right Shift
    - Shift bit-vector x right ypositions
    - Throw away extra bits on right
    - Replicate most significant bit on left

| x | 11001001 |
|:-:|:--------:|
| Logical >> 2    | 00110010 |
| Arithmetic >> 2 | 11110010 |

> A >> x: $A * 2^{-x}$

---

### Section 1.1.5.  Bit Vector

---

### Section 1.1.6. Hexadecimal Represetation

- Decimal code: Human-friendly
  - 235, -1, (201)10, etc.
- Binary code: Computer-friendly
  - 11101011, 11111111, (11001001)2, etc.
- Hexadecimal code: Intersection
  - 0xED, 0xFF, (C9)16, etc.

| Hexadecimal | Decimal | Binary |
|:-----------:|:-------:|:------:|
| `0` | `0`  | `0000` |
| `1` | `1`  | `0001` |
| `2` | `2`  | `0010` |
| `3` | `3`  | `0011` |
| `4` | `4`  | `0100` |
| `5` | `5`  | `0101` |
| `6` | `6`  | `0110` |
| `7` | `7`  | `0111` |
| `8` | `8`  | `1000` |
| `9` | `9`  | `1001` |
| `A` | `10` | `1010` |
| `B` | `11` | `1011` |
| `C` | `12` | `1100` |
| `D` | `13` | `1101` |
| `E` | `14` | `1110` |
| `F` | `15` | `1111` |

---

### Section 1.1.7. What is a Byte?

**Definition:** In mordern processors, Byte is used as 최소 address 단위. 1 Byte is usually 8 bits.

Word is CPU가 한 번에 처리하기 좋은 단위. For example, Word of 32-bit CPU is 4 Bytes, as known as 32 bits.

> In early age, the size of Byte는 정해지지 않았다. 그러나 ASCII code를 충분히 담을 수 있음과 동시에 the power of two와 일치하는 8 bits로 크기가 통일되었다.
> 모호성을 피하기 위해 일부 문서는 octet이라는 표현을 쓰기도 함.

---

**단위 표기**
| Prefix System (접두 체계) | Unit Example | Definition | Common Usage |
|:-------------:|:------------:|:-----------|:-------------|
| SI (Decimal)  | 1 KB, 1 MB   | 1 KB = 1,000 B<br>1 MB = 1,000,000 B | Networking equipment, storage manufacturers |
| IEC (Binary)  | 1 KiB, 1 MiB | 1 KiB = 1,024 B<br>1 MiB = 1,048,576 B | Operating systems, programming contexts |
| Recommendation| —            | Use KiB / MiB / GiB for binary units | To avoid confusion |

---

## Topic 02: Character Reprsentation

### Section 1.2.1. ASCII (American Standard Code for Information Interchange)
