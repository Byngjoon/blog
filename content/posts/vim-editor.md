+++
date = '2026-05-11T16:30:05+09:00'
title = 'VIM Basic'
description = ""
categories = ["etc./"]
tags = ["vim"]
slug = ""
math = true
draft = false
+++

# Chapter 00. VIM Basic Manuals

> **Outline:**

---

# Contents

- [0.1.]() Moving cursor

---

# Section 0.1. What is the VIM?

- VIM
    - VIM = Vi-IMproved: an enhanced version of vi editor
    - is cross-platform
    - vim.org: customize, plugin
    - ~/.vimrc: VIM configuration file
    - Visual Mode <-[v, ctrl + v / esc]-> Command Mode <-[esc / i,I,a,A,o,O,s,S]-> Input Mode
    - VIM Start -[vim file-name]-> Command Mode -[:q, :q!, :wq, :wq!,  ZZ]-> VIM End
    - Command Mode
        - Everything you type are commands (interpeted by VIM as commands)
    - Input Mode
        - Everything you type are contents
        - Changing contents are stored in editing butter (in memory, not disk)
    - Disk(=file) <-[save command(:w, :wq, :wq!) / open new file or input mode]-> Memory(=editing buffer)
    - When open file, all of contents are  uploaded to editing buffer.
    - When you do save, write back from the file in memory to the file in disk.


======VIM Basic Command======


==Move Cursor==
(in Command Mode and Visual Mode)

1. move cursor one space to...
    - h: left 
    - j: down
    - k: up 
    - l: right
- for example
this is example
this [i]s example
this is example
- after moving
this [i]s example   -> k
this[]i[s] example  -> h, l
this [i]s example   -> j
    - you can use the arrow keys

2. move cursor to the first character on... (except for white space)
    - -: the previous line
    - ^: the current line
    - +: the next line
    - `enter(return)` key: next line
- for example
    this is example
    this [i]s example
    this is example
- after moving
    [t]his is example   -> -
    [t]his is example   -> ^
    [t]his is example   -> +, enter

3. move cursor to ... (do not except for white space)
    - 0: the first position on the current line
    - $: the end position on the current line
- for example
    this [i]s example
- after moving
[]    this is example   -> 0
    this is example   []-> $

4. move cursor to the first character of... (except for white space)
    - w: the next word
    - b: the previous word
- for example
this [i]s example
- after moving
this is [e]xample   -> w
[t]his is example   -> b

5. move cursor to...
    - {: the previous top empty line of paragraph
    - }: the next bottom empty line of paragraph
- paragraph: contents surrounded by empty line
(top empty line)
this is a example
this is a example
this is a example
(bottom empty line)
    - empty line: do not contain any contents. (do not except for white space)

6. move cursor to the first chractor of...
    - (: the previous sentence
    - ): the next sentence
- sentence: [., !, ?] + ['white space' or 'new line']
    - [., !, ?] + [", ), ], }] +  ['white space' or 'new line']
- combination example
    - d): deletion + next sentence
    - y(: copy + previous sentence
    - c): rewrite + next sentence

7. move cursor to the first chractor of... (except for white space)
    - H: the top of the screen
    - M: the middle of the screen
    - L: the bottom of the screen
    - gg: the first line of the editing buffer
    - G: the last line of the editing buffer
        - [number]G: to the n-th line of the editing buffer (e.g., 34G)
        - :[number]: to the n-th line of the editing buffer (e.g., :34)

8. move a screen 
    - ctrl + f: down
    - ctrl + d: half-down
    - ctrl + b: up
    - ctrl + u: half-up
        - f, u: cursor is the first charactor of the first line
        - b, d: cursor is the first charactor of the last line
    - VIM display a part of the editing buffer as appropriate on the screen
    - We move the screen to see other parts of the editing buffer
        - depending on the current size of your screen


==Switch into Input Mode==
(in Command Mode)

- i: insert in front of the current cursor position.
- I: insert in the first position of the current line.
- a: insert behind the current cursor position.
- A: insert in the end position of the current line.
- o: insert below the current line.
- O: insert above the current line.
    - o, O: make new line and insert.


==Contents Modification==
(in Command Mode)
this asdfxample. 
    - r: ready to overwrite the current character (staying in the command mode)
    - R: ready to overwrite the contents from the current cursor position (switch into the input mode like REPLACE mode)
- for example
this [i]s example.
- after `ra`
this [a]s example.
- after 'Rasdf'
this asd[f]xample.

    - s: ready to wrtie after removing a character in the current cursor position (switch into the input mode)
    - C: ready to write from the current cursor position after removing the current line from the current cursor position to the end of the line (switch into the input mode)
    - cc: ready to write from the first cursor position after removing the current line (switch into the input mode)
    - cw: ready to write from the current cursor position after removing the current word (switch into the input mode)

(in Visual Mode)
    - r: ready to overwrite the current character (staying in the command mode)
    - R: ready to overwrite the contents from the current cursor position (switch into the input mode)
    - s: ready to wrtie after removing a character in the current cursor position (switch into the input mode)
    - C: ready to write from the current cursor position after removing the current line from the current cursor position to the end of the line (switch into the input mode)
    - cc: ready to write from the first cursor position after removing the current line (switch into the input mode)
    - cw: ready to write from the current cursor position after removing the current word (switch into the input mode)







mon mar 16
linux programming

폰노이만 아키텍처 -> 인스트럭션을 읽고 처리하다가 데이터가 필요하면 데이터를  읽어서 실행(스토리지와 직접적아님)
그러나 메모리는 한정적 -> 필요시 올리고 노필요시 내림 (버추얼 메모리)

루트


mon, mar 23
x X ~~ buffer에 저장됨
:set ts=4 "tab size tabstop = space 4times
:set sts=4 "
:set sw=4 "indentation 수정 increase decrease width
:set textwidth=80 "한 라인에 몇캐릭터 허용
:set smartindent "auto indentation
:source filename "동적으로 
:shell "shell로 나감 -> foreground = fg 다시 돌아온다(ctrl z로 나가면?
:!명령어 ->
:help

:vne "[w]은 optional / vertical new -> / :o filename
vim plug in 사용하기 -> /vim/pulgin/ 에 파일 복붙 확장자 상관 
linux는 여러 파일 시스템을 사용가능
특정 운영체제의 파ㅣㅇㄹ 시스템마다 인코딩 방식이 다르다 다르면 힘들다

Mon, mar 30 
Linux programming

File? -> ?: single char, any character
File* -> *: any characters
$ cat file2 | grep -i “from” == grep -I “from” file2
파이프라인을 통해서 더 느림 앞에가
프로그램 두개를 실행한것

Dir
. == ./
../  super dir
~/ home
/ root

Fine -o -> or: 

memory에만 있는 파일
Ls -> 스토리지에 ㅣㅇㅅ는 파일만
프록 파일? 시스 파일? -> 커널이 메모리에 생성해줌
셧다운 명령어로 끄면 사라짐

Dir -> 파일로써 다뤄짐


Mon, Apr 27 
p.20 
program counter -> address of the next instruction (text section)
stack -> temporal data, local variables (-> non initializing)
data section -> global variables (-> initializing to 0)
heap -> malloc 할때마다 반환하는 값은 점점 increase (to the max)
stack -> 나중에 할당 받은 stack (to the 0)
stack and heap -> process terminate시에 사라짐 -> readelf 에서 no find
text and data section 
p.21 
memory layout of the process in Linux is elf -> use readelf
p.22
os 마다 process states different



Mon, May 4
complier: 아직 영어임 어셈블리
obj file-> cpu는 이해할 수 있지만 아직 실행은 못
--save-temps: 중간 결과물 temporal files를 저장
preprocessor: env var, macro keyword (#...)
linker: linking=> 
.o => 바로 linking 앞에 거 할 이유가 없
다른 코드들도 시스템이 필요한 거 같이 링킹 내가 작성한거 이외에

---
## References
- Kangwon National University Lecture Note (course: 48400009)


## Acknowledgements
- OpenAI ChatGPT
- Google NotebookLM
