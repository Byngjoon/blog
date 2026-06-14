+++
date = '2026-05-15T13:30:09+09:00'
title = 'Regular Expressions'
description = ""
categories = ["etc./"]
tags = ["regexp"]
slug = ""
math = true
draft = false
+++

# Topic. Regular Expressions

> **Outline:**

---

# Contents

- [0.1.]() 

---

# Section 1. What is the Reular Expressions?

---

## Regular Expression (regex or regexp) is...
- string의 pattern을 표현하는 pattern language
- 해당 pattern에 맞는 string을 모두 match (**pattern matching**)
- String set을 표현하는 것 (matching되는 문자열들이 여러개 그것을 표현)

---
e.g.
`hello` == match => `hello`
`h.llo` == match => `hello`, `hallo`, `hxllo`, `h.llo`, ...
- `.` is not just match `.`. 
- `.` means any single character.
---
- used in searching, replacement, and input 검증.

---

## Standard
- There are many standards and implementations for regular expressions.
- There is no only one universial standard, but exist important standards
- Standard
    - POSIX Regular Expression
        - POSIX Basic Regular Expression (BRE)
        - POSIX Extended Regular Expression (ERE)
    - Shell glob
    - VIM regex
    - Perl Compatible Regular Expression (PCRE)
    - ...
- So, 어떤 regex flvor (standard?)를 사용하는 지 먼저 확인
- 그 다음 regex가 잘 표현되었는 지 생각.

---

## Meta Characters
- have special meaning or matching in some syntax.
- Some syntax => Regular expression(POSiX, PCRE, ...), shell syntax, ...
- 어떤 문자가 metacharacter인지는 문맥에 따라 달라진다.
metacharacter는 특정 언어 하나의 고유 용어가 아니라,
“그 문법 안에서 일반 문자 이상의 특별한 의미를 갖는 문자”를 가리키는 일반 용어다.
metacharacter라는 말은 regex에도 있고, shell에도 있고, glob에도 있어
어떤 문자가 metacharacter인지는 문맥에 따라 달라진다



---
e.g.
`a.c` == match ==> `a` + `any single character` + `c`
`.` means any single character

---

**일반적인 regex에서 자주 보이는 metacharacters**
- `.`: any single character
- `*`: zero or more repetitions of the preceding pattern (>= 0, 앞 pattern)
- `+`: one or more repetitions of the preceding pattern (>= 1)
- `?`: zero or one occurrence of the preceding pattern ( == 0 or == 1)
- `^`: start of a line or string
- `$`: end of a line or string
- `[]`: character set (including set 포함하는 set)
- `[^]`: negated character set (excluding set 제외하는 set)
- `{m,n}`: between m and n repetitions (>= m and <= n)
- `()`: grouping
- `|`: alternation
- `\`: escape character
---
e.g.
`^[0-9]+$`: 처음부터 끝까지 only number == match ==> `0`, `1232`, ...
`12a23`, ... are not matched.

---
# Section 2. Shell glob
- is 일부 of shell syntax => process 전에 shell이 해석
- pathname(filename) expansion에서 사용되는 pattern shell pattern matching notation

- bash 등에서는 extended glob 가능 (더 강력, 복잡)

```bash
% pwd
/home/{$USER}/a
% ls
main.c test.c util.c aa.d src/
% ls *.c
main.c test.c util.c
```
1. user input: ls *.c
2. shell이 먼저 수행:
    현재 directory에서 *.c에 맞는 filename을 찾음
3. actually, ls가 받는 형태:
    ls main.c test.c util.c

## Ordinary Character
자기자신과 match
`a` == match ==> `a`
`-` == match ==> `-`
`.` == match ==> `.`
`/` == match ==> `/` (in directory system, `/` has special meaning. it 

## Pattern Special Character
- like meta character

### ?
- is any single character
---
e.g.
`?.c` == match ==> `a.c`, `b.c`, ...
`ab.c`, ... are not matched
---

### *
- is any zero or more characters
---
e.g.
`*.c` == match ==> `a.c`, `main.c`, `test01.c`, ...
matching the file whose name is finished as `.c`.

---
- `*` in shell globbing.
    - any zero or more characters
- `*` in POSIX regex
    - 바로 앞 atom의 0회 이상 반복
    - regex로 비슷하게 쓰면, `.*\.c$`

---

### []
- is bracket expression
- matching single character among characters in [].
    - []안의 문자들 중 하나와 matching, 하나의 문자
---
e.g.

`file[123].txt`
== match ==> `file1.txt`, `file2.txt`, `file3.txt`
`file4.txt`, `file12.txt`, ... are no match
---

**[! ]** or **[^ ]**
- non-matching list
- any single character excluding characters in []. 

---
e.g.
`file[!0-9].txt` (file + 숫자가 아닌 문자 하나 + .txt)
== match ==> `filea.txt`, `fileX.txt`, ...
`file8.txt`, `fileAA.txt` are no match.
---
**-**
- `a-z`, `A-Z`, `0-9`, ... => set notation
---
> POSIX 문서의 bracket expression 규칙은 regular expression의 bracket expression 규칙과도 연결돼 있고, shell pattern 안에서 ?, *, [ 같은 special character는 bracket expression 내부에서 special meaning을 잃는다고 설명된다.
---

### Important Rules

1. `/` must explicitly match
`/` is directory separator

---
e.g.
`*.c` == match ==> `a.c`, ...
`src/a.c` is not matched
`src/*.c` == match ==> `src/a.c`, ...
---

2. leading `.` must explicitly match
In UNIX/Linux file systems, hidden file`s name is started with `.`.

---
e.g.
`.*` == match ==> 
.profile
.gitignore
.env

`*` no match
---

3.  pattern이 아무 파일에도 match되지 않으면, 그 pattern이 그대로 command에 전달될 수 있음. (설정에 따라 다름)

---

## 핵심 Examples

- Quoting에 대해 이야기하고 있음

1. Shell이 먼저 확장하는 경우.

```bash
$ pwd
/home/{$USER}/a
$ ls
main.c test.c util.c aa.d src/
$ echo *.c
main.c test.c util.c
```
> Firstly, shell expansion file name notation. `*.c` == matching by shell ==> `main.c`, `test.c`, `util.c`

---

2. Quote 표현, No regexp
- The notation surrounded by quote is not expanded by shell.

```bash
$ pwd
/home/{$USER}/a
$ ls
main.c test.c util.c aa.d src/
$ echo "*.c"
*.c
```

---

3. Quoted, regexp
- Shell transmits the notation surrounded by quote to the process that uses regex.
---
```bash
$ find . -name "*.c" 
```
이 명령은 *.c를 shell이 확장하지 않고, find에게 그대로 전달해.
find가 -name pattern으로 *.c를 해석함

---
```bash
$ pwd
/home/{$USER}/a
$ ls
main.c test.c util.c aa.d src/
$ find . -name *.c
```
shell이 먼저 확장==> find . -name main.c test.c util.c ==> error 발생 가능, programmer가 원하는 결과가 아님.

---
grep "main" *.c
grep "*.c" filelist.txt
find . -name "*.c"
find . -name *.c

---
> The Open Group Base Specifications Issue 8, Chapter 2

---
# Section 3. POSIX Basic Regular Expression (BRE)

- is regular expression used in the old UNIX tools (grep, sed, ...)

기본적으로는 대부분 문자가 자기 자신을 match한다.
일부 문자만 특별한 의미를 가진다.
그런데 grouping, interval, backreference 등은 backslash를 붙여야 특별해진다.

---

## BRE Ordinary Character

- It matches to 자기자신

---
e.g.
hello == match ==> hello
---

## BRE Special Character

- It has special mean in BRE.
- `.`, `[`, `\`, `*`, `^`, `$` 

---

### `.`

- It means any single character excluded `NULL`



- The Open Group Base Specifications Issue 8, Chapter 9
---
# POSIX Extended Regular Expression (ERE)

- The Open Group Base Specifications Issue 8, Chapter 9
---
# VIM regex

Vim 자체의 pattern syntax
Vim 자체의 pattern syntax

Vim regex가 독특한 이유는 magic mode 개념이 있기 때문이야.

예를 들어 Vim에서는 다음 같은 prefix가 regex 해석 방식을 바꿔.
\v    " very magic
\m    " magic
\M    " nomagic
\V    " very nomagic


- :help pattern.txt
---
POSIX BRE/ERE: text pattern matching 표준
shell glob: filename/pathname expansion 표준
Vim regex: Vim editor 내부 검색/치환용 자체 문법




---
**References**
- The Open Group Base Specifications Issue 8
- VIM pattern.txt

**Acknowledgements**
- OpenAI ChatGPT
- Google NotebookLM
