+++
date = '2025-09-06T07:20:49+09:00'
title = '[Data Structures] [00] Introduction to Data Structures [KR]'
description = "'Data Structures'에 대한 기본 개념과 전반적인 흐름을 정리한다."
categories = ["Computer Science/Algorithms & Data Structures"]
tags = ["Data Structures"]
slug = "introduction-to-data-structures-kr"
math = true
draft = true
+++

# Chapter 00. Introduction to Data Structures

> **Outline:** 'Data structure'와 'Abstract data type'이란 무엇인지, 두 개념의 차이는 무엇인지에 대한 내용을 다루며, 추가적으로 C 언어로 각 자료구조를 구현하기 위해 기본적으로 필요한 개념들을 담았다. 마지막으로는 이후에 다룰 내용들의 전반적인 흐름을 기술한다.

---

## Contents

-[]

---

## Section 0.1. 'Data Structure'란 무엇인가?

> - **Definition:** 
    - 1. 'Data structure'란 data를 효율적으로 저장하고 조직하여, data를 다루는 다양한 연산(탐색, 삽입, 삭제, etc.)을 효과적으로 수행(*)할 수 있도록 하는 data의 구조적 표현 방식이다.
    - 2. Data와 그 data를 다루는 operations의 집합
> *: 보다 더 적은 자원(time, memory, energy)을 소모하여 연산을 수행

---

### 0.1.1 Core Concepts

Data를 구조화하는 것은 4 Layers로 이루어져 있는데, 순서대로 'Abstract Layer', 'Logical Data structure', 'Physical Data Structure' 'Implementation Layer'가 있다.
첫번째로 Abstract Layer에서는 흔히 말하는 ADT(*)에 대한 내용을 다룬다. 이 단계에서는 무엇을 다루며 어떠한 연산을 할 수 있는지 언어와 구현에 관계없이 추상적으로 정의하는 단계이다. 예를 들어 List ADT에 대해 생각한다면 아래와 같은 구조로 정의할 수 있다.
- Data: 순서가 잇는 원소들의 유한한 집합
- Operations:
  - insert(L, pos, x): 리스트 L의 특정 위치에 원소 x를 삽입
  - delete(L, pos): 리스트 L의 특정 위치에 저장된 원소를 삭제
  - get(L, pos): 리스트 L의 특정 위치에 저장된 원소를 반환
  - size(L): 리스트 L의 크기를 반환
  - etc.

> 이 layer의 결과로 data type과 operations의 interface, 전제/사후조건, 불변식이 산출되어야 한다. 허나 아직 내 공부가 부족하므로 다음에 수정하자.

---

Abstract Layer를 거치고 나면 다음 Layer는 Logical Data Structure이다. 이 계층에서는 implemetation을 위해 abstract concepts를 logical concepts으로 구체화한다. 즉, ADT를 구체적으로 조직하며 data 간의 논리적 관계를 다루지만 아직 구현에 대한 세부사항(memory 표현)으로 진입하지 않는다. 이 과정에서 다음 사항들을 고려하게 되는데, 첫번째 사항으로는 구조적 속성이 있다. 구조적 속성이란 data들의 관계가 선형인지 아니면 다른 형태(*)인지 정하게 된다. 두번째로 연산과 변형이 일어나는 지점에 대해 고려한다. 예를 들어, insertion이나 deletion은 앞, 뒤, 임의 위치 등에서 작동할 수 있는데, 현재 problem에 어떤 방식이 가장 유리할지 생각하는 것이다. 마지막으로(**) 구체화된 만큼 새로운 조건에 대해 생각한다. 이와 같은 과정을 반영하여 예시를 들면 List ADT에 대한 특성을 다음과 같이 추가하게 된다.
- 구조적 특성
  - 원소들이 선형적으로 나열됨
  - index 또는 pointer를 이용해 순서를 유지함
- 제약 조건
 - insertion과 deletion은 특정 위치를 기반으로 수행됨
 - 크기는 유동적임.

> *: linear or non-linear -> non-linear: like tree, graph, or hash
> **: 잘 모르겠으니 공부 더 필요.
---

다음으로 Physical Data Structure Layer를 진행하게 된다. 이 계층에서는 physical environment(e.g. memory)를 고려하여 data의 어떤 구조로 구현할지 정하게 된다. 가장 중요한 요소는 


실제 data structure라고 부르는 layer는 second and third layers지만 앞서 나온 a
