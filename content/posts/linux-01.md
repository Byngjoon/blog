+++
date = '2026-03-09T14:07:47+09:00'
title = 'Linux [01]: OS & Linux Basic'
description = ""
categories = [""]
tags = [""]
slug = ""
math = true
draft = false
+++

# Chapter 00. 

> **Outline:**

---

## Contents

- [0.1.]() 

---

## Section 0.1.
Operating system is ...
1) One of the most sophiscated(복잡한) software structure
2) Resource manager -> manage software component and hardware (like device driver)

flow of running computer (top-down)
1. User: the person who uses computer
=====Interface (User Interface)
2. Applications (=user program)
    - User Interfaces (UI): User-Computer interface 
	    - Graphical User Interface (GUI): click the mouse, icon, window, ...
	    - Command Line Interface (CLI): ls, cd, gcc, ... 
	    - Batch Interface: shell script, ... 명령을 한번에 모아서 자동실행
	    - UI 는 개념, GUI, CLI, Batch 는 구현방식 느낌
        - program 중 user와 만나는 부분에 대한 개념
    - (shell, app)
=====Interface (System Call)===== 
3. Operating System (OS)
    - System Calls: user program-os interface 
	    -(open(), read(), fork(), ...)
    - kernel
	- Program execution: program을 memory에 올리고 실행되게 해줌
	- I/O Systems: help using Input Output device 
	- File systems: manage files and directories
	- Communication: data moving between each process or computer
	- resource allocation: 결정 to give resource like CPU, memory, disk,... to whom how much
	- accounting: notes and manages who use resource how much
	- error detextion: finding error in programs and device
	- protection and security: protect files and systems from program or other user
4. Hardware

UNIX/Linux key features
1. Interactive systems
2. Multi-user systems
3. Multi-tasking systems
4. High portability, scalability(확장성), openness(개방성)
5. Hierarchical file-systems

Portable Operating System Interface (POSIX): Unix standardization

shell and kernel
Shell: Command line interpreter(해석기?)
	- is not component of OS
	- is just porgram (Application)
	- allows user to command kernel -> interpreter
	- the reason why Linux is interactive system(깜빡깜빡)
	- sh, csh, ksh, zsh, bash - 인터프리터인데 many variation
Kernel: A main(core) component of OS
	- loaded on memory at boot time (is in /boot dirtory)
	- manege memory, process, divice, file-system, network, ...
	- Linux kernel is composit source written C and Assembly language
	- /arch -> written Assembly becuase control architecture
- Shell: User <-> Program
- System Call: Program <-> Kernel
- Kernel: actual running (control hardware)

Linux is multi-user system: multiple users can use a system in the same time
    - users have each account
    - each account's files and process are protected
- flow
Login: the process of obtaining(획득) permission to use the system
-> input user-ID and password -> 인증 -> system 접근 허용
-> execute shell and allocation resource 
-> move to home directory
-> stay for command -> 작업 수행 -> 
Logout (terminate session)
    - logout: terminate login session / run in login shell
    - exit: terminate 현재 shell / run in all of shell
        - subshell -> parent shell -> ... -> login shell -> logout
    - Ctrl + D: input EOF / all of shell / shell 종료 유도
        - EOf: end of file -> end of input -> terminate shell
    - resource deallocation (reclaim)

- user permission
    - nomal user / super user
    - nomal user
        - permition of os 필
    - super user (= administrator, root)
        - management and maintenance system
        - higher-level of system permission
        - 뭐든지 할 수 있다.


---
## References
- Kangwon National University Lecture Note (course: 48400009)
- Advanced Programming in the UNIX Environment [3rd Ed] - W. Richard Stevens, Stephen A. Rago
- Computer Systems (A Programmer's Perspective) [3rd Ed] - Randal E. Bryant, David R. O’Hallaron
- Operating System Concepts [10th Ed] - Abraham Silberschatz, Greg Gagne, Peter B. Galvin

## Acknowledgements
- OpenAI ChatGPT
- Google NotebookLM