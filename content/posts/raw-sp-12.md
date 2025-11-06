+++
date = '2025-11-06T15:18:35+09:00'
title = 'Raw Sp 12'
description = ""
categories = [""]
tags = [""]
slug = ""
math = true
draft = true
+++

# Chapter 00. 

> **Outline:**

---

## Contents

- [0.1.]() 

---

## Section 0.1.

자료에 나온 register , 명령어 > integer 기준 > floating point goto sp13

x86 arguments > 6 >> use stack

return value > rax > parants

many function > each private space need > stack frames >

register 겹침 > backup > regiter convention > x86 정해놓음

stack allocation 관련 명령어 3개 > sub,push, call > add is deallocation
push 대상 return addr > call 바로 밑 명령어


movl $0, %eax 
testq %rdi, %rdi ;유사 and, but condition code 만 바꿈  > rdi == 0 이면 0
je .L6 : 0 이면 탈출 그래서 rax에 미리 0

