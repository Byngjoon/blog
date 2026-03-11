+++
date = '2026-03-09T14:08:51+09:00'
title = 'Lec Raw'
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

vm = 컨테이너 = 프로그램 > 입출력, behavior 제공 
vmm = 가상 머신 위에서 연산 수행 > vm 매니저 느낌

타입 1 > 하드웨어 바로 위 os와 거의 구분 불가능할 정도
app > guest os > vmm > hardwere

타입 2 > os 위 / 이 수업에서는 이런식 / 운영체제 입장에서는 하나의 어플리케이션

app > guest os > vmm > native > hardwere (layer + 1) (코드 복잡도 규모 up > 보안 취약점 + a)

porting > hardwere 와의 상호작용 시 필요 

virtual box > x86 시스템위에서만 돌아감

에뮬레이션 vs virtualization 

instruction
source file > compile > object file (binary file)
cpu 마다 명령어집합이 다름 사용하는

virtualization > 컨테이너와 실제 하드웨어의 명령어 집합이 같음
에뮬레이션 > 명령어집합이 다름

virtual box > vmm


tue mar 10
os
user, app 의 하드웨어 리소스 사용 관리 (리눅스 유저가 요청할 수 있는 기능이 있음)
버스 위에 컴퓨터 시스템이 다 연결되어있다. 각각의 디바이스는 독립적으로 실행
디바이스 안에는 로컬 버퍼 존재
디바이스 드라이버가 통제
로컬 버퍼가 메모리와 연결 버퍼에 올라와있는 데이터가 레지스터로 이동 처리장치가 처리
인터럽트를 발생시켜 종료를 알림
인터럽트 벡터 넘버는 시피유마다 다름
인터럽트 벡터 테이블에 모아놓고 해결할 수 있는 펑션의 시작주소를 저장

1. 블록킹 아이오
2. 논 블로킹

쓰루풋 처리량?

assymetric: 두 프로세서의 역할이 다름, 동등하지 않음
symetric: 모든 프로세서가 동일한 역할을 함 : 장점 3가지 관점에서 더 훌륭
uniforem memory access UMA 모든 프로세서가 같은 메인 메모리

wed mar 11 os
numa 로컬메모리에 균등하게 배분해놓기(분산) 장점: 많은 메모리 엑세스 -> 쾌적한

코어사이의 스케줄링 - 네트워크 온 칩

부트스트랩 - 부트로더 바이오스 펌웨어 오에스
컴퓨터 실행시 사용자가 사용가능한 수준까지 초기화 담당

바이오스 어쩌고 한다음에 커널을 메모리에 올림 -> 