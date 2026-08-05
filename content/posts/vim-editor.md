+++
date = '2026-05-11T16:30:05+09:00'
title = 'VIM Basic'
description = ""
categories = ["etc./"]
tags = ["vim"]
slug = ""
math = true
draft = true
+++

# Topic. VIM Basic Manuals

> **Outline:**

---

# Contents

- [0.1.]() Moving cursor

---

# Section 1. What is the VIM?

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


# Section 2. VIM Basic Command


## Move Cursor
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


## Switch into Input Mode
(in Command Mode)

- i: insert in front of the current cursor position.
- I: insert in the first position of the current line.
- a: insert behind the current cursor position.
- A: insert in the end position of the current line.
- o: insert below the current line.
- O: insert above the current line.
    - o, O: make new line and insert.


## Contents Modification
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


## Split Screen
(in command mode)

1. :[n]split [file-name] (e.g. :80sp test.c) (or :[n]sp [file-name])
    - horizontal spliting (상, 하 두개로 분리됨)
    - [n]: height size, 없으면 절반으로 split
    - [file-name]: 열고 싶은 파일, 없으면 현재 file
        - ./ 기준 path, 다른 diretory file 은 access by path
2. :[n]vs [file-name]
    - vertical spliting (좌, 우 두개로 분리됨)

3. [ctrl + w] + [...]: move cursur to ...
    w : next screen
    W : previous screen
    h, j, k, l: 해당 방향으로 이동

4. [ctrl + w] + [...]: resizing
    - =: all screen, same size
    - `_`: present window, maximum height
    - `|`: present window, maximum width
    - [n] >: present window, + n width
    - [n] <: present window, - n width
    - [n] +: present window, + n height (or :resize +[n])
    - [n] -: presnet window, - n height (or

5. 
    - :wq, :q, ... => present window
    - :qa => all window
    - [ctrl + W] + o => all window excluded present one

6.  [ctrl + w] + r : 다음 화면과 위치 바꿈

    
    
<!--
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
-->



---
## References
- Kangwon National University Lecture Note (course: 48400009)


## Acknowledgements
- OpenAI ChatGPT
- Google NotebookLM
