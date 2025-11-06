+++
date = '2025-11-06T13:52:02+09:00'
title = 'Raw Algo 07: Dynamic programming'
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


점화식 만들기 빡셈 > 좌변 정의가 관건 > 우변은 좌변을 논리적으로 분석하면 접근가능
initial problem, sub problem,

knapsack > 무게 w, 가치 v (자료 상에서는 시간으로 나와았음)

무게의 합 < W (무게의 한계) 를 만족 > value  최대

naive: 2^n > 조합 다 때려넣기

the other: 무게 대비 밸류 높은 것부터 > 밸류/무게 > is not optimal > counter ex 생각
\> fractial knapsack에서는 optimal : 아이템을 비율만큼만 구매가능한 경우(라잌 빝코인)

0-1 kbapsack > 아이템을 선택하거나 말거나 둘 중 하나
optimal:
step 01: c[...] > when (...), total value 
step 02: c(i,j) > i: what item, j: capacity
step 03: right hand > i-1 > j - (some item weight) > pre c + item value + now c
the other: 포함하지 않는 경우도 생각 > 둘중에 큰경우 선택
