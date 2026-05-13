+++
date = '2026-04-08T16:13:42+09:00'
title = 'Lec Os 01'
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

tue mar 17 
operating system
실행 상태인 프로그램 즉 프로세스를 엄청 자주 엄청 짧게 스위칭 -> 동시에 사용되는 일루전
interrupt -> scheduling 중 다른 프로그램의 인터럽트가 발생한다면 ?
분기마다 스케줄러가 현재 상황을 보고 프로세스를 선택 ->
보통 인터럽트가 발생하면 원래 프로세스 정보 컨텍스트를 백업 (컨텍스트는 보통 레지스터) -> 전부 메모리에 저장 
메모리는 두영역
프로그램들은 유저 스페이스에
인터럽트 벡터, 스케줄러 는 커널 스페이스 ->커널 영역중에서도 커널 스택에 프로세서 컨텟그트도 커널 스페이스
kmalloc

multi tasking - 
vs 
multi processing
메모리 파일 모두 접근 가능하자만 한순간에 하나만 -> 프로세스가 다른 프로세스의 공간에 침범할 수도 있음
프로텍션이 필요 -> 운영체제 공간을 지키는게 제일 중요
프로세스 컨덱스트 블록 
듀얼 모드
low hammer attack 
타이머 (하드웨어 장치)
특정 프로세서가 리소스를 독점하거나 인피니트 루프를 막기위함
특정시간이 지나면 타이머 인터럽트를 발생 시킴
더 자주 일어난다면 응답성이 빨라짐 (전환이 잘됨) 단점은 인터럽트 처리 오버헤드가 자주 일어남
휴리스틱 250 적당
커널 코드 변수 = y -> 컴파일 시 이미지안에 포함 
m -> 이미지 포함 안됨 -> 모듈 사용시 동적으로?



Tue, Apr 14 Operation systems
next wed exam

ex) 4 threads program -> even split data
    - dependancy

data parallism -> simd 

serial -> single thread must

user level thread 
kernel level thread -> scheduling, ...

many to one -> app -> 1 kernel -> parallism limit

one to one -> use many resource , too much cost, linux?
many to many -> kernel number limit 

many to one -> mapping thread lib -> os dont know

cscope -> cs find c -> caution) define many time function

assyc cancelation -> resource deallo not, 

