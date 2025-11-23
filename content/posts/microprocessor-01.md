+++
date = '2025-09-24T18:40:00+09:00'
title = 'Understanding Microprocessors - from Programming to Processor Design: ch01 마이크로프로세서의 프로그램 실행 원리'
description = ""
categories = [""]
tags = [""]
slug = ""
math = true
draft = true
+++
제 1부 Assembly Language and Machine Language
ch 01 - ch 04
# Chapter 01. 

> **Outline:**

---

## Contents

- [0.1.]() 
마이크로프로세서와 어셈블리 언어
마이크로프로세서의 명령어 실행
기계어 코드의 표현
수의 표현
비트 수 왁장
캐리와 오버플로
논리 연산
문자의 표현

---

## Section 1.1. Microprocessoers and Assembly Language



2의보수 장점 > 나머지는 안 그런가?

And a b result
 0 0 0
 0 1 1
 1 0 1
 1 1 1

0 0 0 
 0 1 0
 1 0  0 
 1 1 1

음수 lsr > 음수 보수 1의 의미 어떤 결과가 펼쳐지나 예측가능한가?


2의 보수 -(0 자릿수 합 +1)