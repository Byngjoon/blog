+++
date = '2026-06-13T10:26:24+09:00'
title = '[UNIX/Linux] [04]: Shell'
description = ""
categories = [""]
tags = ["UNIX/Linux"]
slug = ""
math = true
draft = true
+++

# Chapter 04. Shell

> **Outline:**

---

# Contents

- [0.1.]() 

---

# Section 4.1. What is the Shell?

- Command interpreter (or command processor)

---

## Configuration File
- .bashrc 
    - Bash start-up file (zsh -> .zshrc)
    - When you log in to the bash shell, `.bashrc` is automatically referenced
    - You can run it explicitly using the `source` command (source .bashrc)
        - Update => re-loggin in or using source command
리눅스에서 . 으로 시작하는 파일 -> 숨김파일
If a filename starts with a dot(‘.’), it means the hidden file in Linux
모든 리눅스에 포함된 스타트업 파일
그러나 배포판마다 약간 다를 수 있다
(우분투에서는 .profile이 가장 먼저 실행)
쉘스크립트? linux에서는 #이 주석

---


# Section 4.2. File Descriptor and  Standard Streams
In the UNIX/Linux systems, program read and write, stream을 통해.
program이 시작될 때, shell or parent process는 child process의 stream을 생성하는데,
standard input, standard output, standard error를 3가지를 생성하게 된다.

그리고 kernel은 이러한 stream을 관리하기 위해 file descriptor라는 small non-negative integer를 사용하는데, 
이들은 사실 kernel이 이러한 stream이 어디로 향할 지 기록해놓은 file descriptor table의 index라고 볼 수 있다.
conventionally, standard input, standard output, standard error 라는
개념적인 concepts(I/O objects: device, socket, pipe, ...)는 각각 mapping on 0, 1, 2
즉, file descriptor는 kernel-level의 I/O object abstraction이다.

그러나, program들은 buffer의 사용과 kernel mode changing overhead를 피해 효율적으로 작동하기 위해,
user space에서 stream을 바라봐야하는데, c language로 작성된 c program들은 이러한 기능으로 standard stream을 사용한다.
standard stream은 C standard I/O library에 FILE * stream의 형태로 구현되어 있는 I/O object로 file descriptor와 buffer 등을 감싸고 있는 high-level abstraction이다.
즉, standard stream인 stdin, stdout, stderr는 각각 file descriptor 0, 1, 2와 mapping

shell의 redirection은 file descriptor와 mapping된 I/O object를 바꾸는데,
기본적으로 process는 처음 시작할 때, 0, 1, 2 모두 terminal 과 연결되어있다.
이러한 shell의 redirection은 standard stream <-> file descriptor <-> I/O object의 관계 중 file descriptor <-> I/O object 의 mapping을 바꾸는 것이므로 standard stream을 사용하는 program들 또한 당연히 영향을 받는다.

e.g., stdin <-> 0 <-> terminal input 에서 rediretion으로 0 <-> file 이 된다면
stdin 을 통해 input stream을 제어하던 process는 당연하게도 termianl input이 아닌
file로 부터 input을 받는다.

3부터의 fd는 process에 따라 동적으로 할당되는데, 가장 작은 unused fd부터 할당된다.
만약 0, 1, 2를 close()한다면 0, 1, 2또한 동적으로 할당할 수 있다.

pipe는 두개의 stream을 제어하게 되는데 pipe write end and pipe read end를 제어하는 것이다.
```bash
cmd1 | cmd
```
는 shell이 cmd1의 fd 1을 pipe write end로 연결하고 cmd2의 fd 0 를 pipe read end로 연결하게 되어 
두 process의 write stream과 read stream이 연결되어 inter-process communication이 가능해지는 것이다.


---
# Section 4. Shell Syntax (Shell Command Language)
- can title 'UNIX Shell Command Line Processing' or 'Shell Metacharacters and Operators'

The syntax used in shell command line.

---
<!--

> : output redirection
stdout을 파일로 보냄, 기존 내용 덮어씀
>> : output redirection (append)
stdout을 파일 뒤에 이어 붙임
< : input redirction
stdin을 키보드 대신 파일에서 받음
\`cmd\` : command substitution
cmd 실행 결과를 문자열로 삽입
$(cmd) : command substitution
위와 같지만 현대적으로 권장
| : pipe
&& : AND conditional execution
|| : OR conditional execution
전부 shell metacharacter / shell operator야. 핵심은 이것들이 ls, grep, cat 같은 프로그램 자체의 기능이 아니라, 대부분 shell이 command를 실행하기 전에 해석하는 문법

---

Shell command language / Shell syntax
- Command structure / Word parsing
    - command name
    - options
    - arguments
    - quoting
        - single quote '...' : 모든 shell metacharacter의 특별한 의미를 제거
        - double quote "..." : 일부 expansion은 허용하면서 word splitting과 glob을 억제
        - escape \ : 바로 뒤 문자 하나의 특별한 의미를 제거

- Metacharacters : shell parser가 특별히 해석할 수 있는 문자들 (|, &, ;, <, >, (, ), $, `, \, ", ', *, ?, [...])

- Operators
    - Redirection operators
        - > : stdout을 file로 redirect
        - >> : stdout을 file 뒤에 append
        - < : file을 stdin으로 redirect
        - 2> : stderr를 file로 redirect
        - 2>&1 : stderr를 stdout이 가리키는 곳으로 redirect
    - Pipeline operator
        - | : 앞 process의 stdout을 뒤 process의 stdin으로 연결
    - Command list / Control operators
        - && : 앞 command가 성공하면 뒤 command 실행
        - || : 앞 command가 실패하면 뒤 command 실행
        - ; : 앞 command 종료 후 뒤 command 실행
        - & : command를 background에서 실행

- Expansion constructs
    - Parameter / Variable expansion
        - $VAR : variable 값으로 치환
        - $HOME : home directory 값으로 치환
        - $PATH : executable search path 값으로 치환
        - $? : 직전 command의 exit status 값으로 치환
    - Command substitution
        - `cmd` : cmd의 stdout 결과로 치환
        - $(cmd) : cmd의 stdout 결과로 치환
    - Arithmetic expansion
        - $((expr)) : arithmetic expression의 계산 결과로 치환
    - Pathname expansion / Filename expansion / Shell glob
        - * : 임의의 문자열
        - ? : 임의의 문자 하나
        - [...] : bracket 안의 문자 집합 중 하나

- Compound commands
    - if : 조건에 따라 command 실행
    - for : list를 순회하면서 command 반복 실행
    - while : 조건이 참인 동안 command 반복 실행
    - case : pattern에 따라 branch 선택
    - function : command들을 하나의 function으로 정의




---

grep '\.c$' < files.txt | wc -l > count.txt

grep, wc             : command
'\.c$', -l           : argument
< files.txt          : input redirection
|                    : pipeline
> count.txt          : output redirection
'\.c$'               : quoting된 문자열

Shell syntax는 command, argument, quoting, variable expansion, command substitution, redirection, pipeline, conditional execution, glob 등을 모두 포함하는 큰 문법 체계
-->

---
## Meta character
    - metacharacter는 ordinary character로 취급되지 않고, in the shell syntax, the character which has special meaning
    - |  &  ;  <  >  (  )  $  `  \  "  '  *  ?  [  ]  space  tab  newline
    - `>` is not what make computer print character `>`. it is interpreted output redirection operator by shell
    - If you want to has system print character `>`, must use quoting or escaping
metacharacter는 특정 한 가지 branch가 아니라, 여러 branch에서 사용되는 “특수 문자 집합”에 가까워
metacharacter는 기능 이름이 아니라,
shell syntax를 구성하는 특수 문자들의 성격이다.

```bash
$ echo hello > out.txt
```
metacharacter `>`는 parser에게 이런 의미
“데이터 문자`>`로 해석하지 말고, 문법 구조를 만드는 기호(redirection)로 해석.”
```bash
$ cmd1 | cmd2
```
`|`는 cmd1의 argument도 아니고 cmd2의 argument도 아님. shell parser가 이걸 보고 pipeline 구조를 만듦.

---


Operator와 metacharacter의 차이
metacharacter = 특별한 의미를 가질 수 있는 문자
operator      = 문법적으로 실제 동작을 나타내는 연산자/구문 단위

> 는 shell metacharacter이다.
> 는 output redirection operator이기도 하다.
& 는 shell metacharacter이다.
&& 는 AND control operator이다.
> 는 shell metacharacter이다.
>> 는 append redirection operator이다.
> 한 글자 자체는 metacharacter이고, >>라는 두 글자 token은 operator

---

token, metacharacter, operator의 관계
더 정확히는 shell이 command line을 읽을 때 문자를 모아서 token을 만들어
grep '\.c$' < files.txt | wc -l > count.txt
shell 관점에서 중요한 token들은 대략:
grep
'\.c$'
<
files.txt
|
wc
-l
>
count.txt


token |  역할
grep: command name
'\.c$': argument
<: redirection operator
files.txt: redirection target
`|`: pipeline
wc: command name
-l: argument
>: redirection operator
count.txt: redirection target

이때 <, |, >는 metacharacter로 이루어진 operator token이야.
반면 grep, files.txt, wc, -l은 ordinary word token이야

---

## Operator
metacharacter가 “특수한 문자”라면, shell operator는 그 문자들이 모여 만들어진 “문법적 연산자”
Shell syntax는 shell command line 전체 문법이고,
metacharacter는 그 문법에서 특별한 의미를 갖는 문자
shell operator는 metacharacter로 구성된 문법 연산자

> 는 metacharacter이면서 redirection operator다.
| 는 metacharacter이면서 pipeline operator다.
&& 는 & metacharacter 두 개로 된 AND control operator다.
조금 더 정확히 말하면 &&, ||, >>는 한 글자짜리 metacharacter라기보다는 metacharacter로 구성된 compound operator라고 보는 게 좋아.

---

### I/O Redirection

grep "error" log.txt > result.tx
grep은 >를 직접 처리하지 않아. shell이 먼저 >를 해석해서 stdout을 result.txt로 연결한 뒤, 그 상태에서 grep 프로세스를 실행

---

1. `>`: output redirection
- command의 standard output(stdout, file descriptor 1) 을 화면이 아니라 파일로 보내는 문법
- same as `1>`
```bash
command > file
```
```bash
$ ls > files.txt
```
> ls의 출력 결과를 터미널에 보여주지 말고 files.txt에 저장해라

```bash
$ echo hello > a.txt
$ echo world > a.txt
$ cat a.txt
world
```
> 기존 파일 내용을 덮어쓴다
> open 할 때 새로 열리고 내용을 작성하기 때문

---
2. `>>`: output redirection append
- stdout을 파일로 보내지만, 기존 내용을 지우지 않고 뒤에 이어 붙인다.

```bash
command >> file
```

```bash
$ echo hello > a.txt
$ echo world > a.txt
$ cat a.txt
hello
world
```
> open the file in append mode?

---
3. `<`: input redirection
- command의 standard input(stdin, file descriptor 0) 을 keyboard가 아니라 file에서 받게 함
- same as `0<`

```bash
$ wc -l < a.txt
```
> a.txt의 내용을 wc -l의 입력으로 넣어라
```bash
$ wc -l a.txt
3 a.txt
$ wc -l < a.txt
3
```
- 비슷해보이지만 다름: wc는 첫번째경우 gets file name as argument, 두번째경우 gets file contents as stdin; do not know file name 

---
4. `2>`: command의 standard error를 redirection
- 처음에 stderr(fd 2)는 terminal로 연결되어 있음.


---
5. `&`: interpreted to indicate file descriptor
- redirection 문맥에서 &가 뒤에 오는 숫자를 파일 이름이 아니라 file descriptor number로 해석하게 한다.
echo hello >1
이것은 이름이 1인 파일에 출력fd 1 -> file named "1"
echo hello >&1
fd 1 -> fd 1이 가리키는 대상

cat /etc/sudoers | wc -l
cat stdout -> pipe -> wc
cat stderr -> terminal
cat /etc/sudoers 2>&1 | wc -l
cat stdout -> pipe -> wc
cat stderr -> pipe -> wc






### Pipeline

command1의 stdout을 command2의 stdin으로 연결
```bash
command1 | command2
```

---

```bash
$ ls | grep ".c"
```
> ls의 출력 결과를 grep의 입력으로 넘기고, 그중 ".c"가 들어간 줄만 출력
ls stdout ──pipe──> grep stdin

내부적으로 pipe는 파일이 아니라 kernel 안의 pipe buffer를 통해 process 간 데이터를 전달해. OS 관점에서는 process communication의 한 방식이고, 시스템 호출 수준에서는 보통 pipe(), fork(), dup2(), execve()가 함께 사용


---
```bash
$ ls | grep ".c"
```
pipe로 들어간 input과 ".c"의 차이는?
grep의 argv[1]  = ".c"
grep의 stdin    = ls의 출력 결과
".c"는 command-line argument이고, ls의 결과는 standard input stream

shell은 grep ".c"를 실행할 때 grep 프로그램에 이런 식으로 인자를 넘겨
argv[0] = "grep"
argv[1] = ".c"
그리고 동시에 pipe를 통해 grep의 stdin을 ls의 stdout에 연결
ls stdout ─────pipe─────> grep stdin
                          grep argv[1] = ".c"

|요소| 예시 | grep 입장에서의 의미|
|---|---|
|pipe로 들어온 데이터| ls의 출력 결과| 검색 대상 text|
|".c"| command-line argument | 검색할 pattern|

ls의 결과 = 검사할 시험지 묶음
".c"      = 채점 기준
grep      = 채점하는 사람

실제 내부 동작은 비유처럼 “시험지”가 객체로 넘어가는 게 아니라, ls process가 stdout에 byte stream을 쓰고, kernel pipe buffer를 통해 grep process가 stdin에서 byte stream을 읽는 구조

---

pipe와 >, >>, <의 차이는?

redirection은 process와 file을 연결한다.
pipe는 process와 process를 연결한다.

ls > files.txt
ls stdout ====> files.txt
ls | grep '\.c$'
ls stdout ==pipe==> grep stdin

grep '\.c$' < files.txt > result.txt
files.txt ====> grep stdin
grep stdout ====> result.txt

운영체제 내부 관점에서는 둘 다 file descriptor를 바꿔 끼우는 방식으로 이해할 수 있어
UNIX process는 기본적으로 다음 세 file descriptor를 가지고 시작
| fd | 이름 | 기본 연결 |
|---|---|---|
| 0 | stdin | terminal input |
| 1 | stdout | terminal output |
| 2 | stderr | terminal error output|
APUE는 shell이 새 program을 실행할 때 관례적으로 standard input, standard output, standard error 세 descriptor를 열어 두며, 특별한 조작이 없으면 terminal에 연결된다고 설명한다. 또한 shell은 이 descriptor들을 file로 redirect할 수 있고, 예를 들어 ls > file.list는 ls의 standard output을 file.list로 redirect한다고 설명
pipe의 경우에는 file이 아니라 kernel이 만든 pipe object가 중간에 생긴다. Operating System Concepts는 ls | less 예시에서 |가 앞 command의 output을 뒤 command의 input으로 넘기도록 shell이 설정하며, pipe는 한 process가 한쪽 끝에 write하고 다른 process가 다른 쪽 끝에서 read하는 구조라고 설명한다
>   : fd 1을 file에 연결
>>  : fd 1을 file에 append mode로 연결
<   : fd 0을 file에 연결
|   : 앞 process의 fd 1과 뒤 process의 fd 0을 kernel pipe로 연결

---


### Conditional Execution

1. &&: AND conditional execution
command1 && command2
앞 command가 성공했을 때만 뒤 command를 실행
“성공”은 출력 내용이 아니라 exit status가 0인지로 판단
```bash
$ mkdir build && cd build
```
mkdir build가 성공하면 cd build를 실행해라
왜 유용하냐면, 앞 단계가 실패했는데 뒤 단계를 실행하면 위험한 경우가 많기 때문
```bash
$ gcc main.c -o main && ./main
```
컴파일 실패 시 오래된 실행 파일을 실수로 실행하는 일을 막을 수 있

2. ||: OR conditional execution
command1 || command2
앞 command가 실패했을 때만 뒤 command를 실행
```bash
$ cd project || echo "project 디렉터리로 이동 실패"
```
cd project가 실패하면 에러 메시지를 출력해라
```bash
$ grep "ERROR" log.txt || echo "ERROR 없음"
```
grep은 matching line을 찾으면 exit status 0, 못 찾으면 보통 1을 반환해. 그래서 "ERROR"가 없으면 뒤의 echo가 실행

3. exit status
shell에서는 command가 끝날 때 숫자 상태값을 반환
0: success
non-zero: failure 또는 특수 상태
확인은 $?로 할 수 있어
```bash
$ ls
$ echo $?
0
```
성공한 경우임

&&, ||는 출력 문자열을 보는 게 아니라 직전 command의 exit status를 보고 판단

process가 종료될 때 parent process에게 전달하는 termination status 중 하나
exit status는 parent process, 특히 shell이 child process의 종료 결과를 판단할 수 있도록 설계된 프로세스 종료 상태 정보


---
## Expansion

---

### Command Substitution
- command substitution은 command를 먼저 실행한 뒤, 그 출력 결과를 현재 command line 안에 문자열로 끼워 넣는 기능

---

- \`cmd\` (surrounded by backticks, cmd is 약어 of command)
```bash
$ pwd
/home/{$USER}/a
$ echo pwd
pwd
$ echo `pwd`
/home/{$USER}/a
$ echo "Working directory is `pwd`"
Working directory is /home/{$USER}/a
```

1. shell이 `pwd`를 먼저 실행
2. pwd의 stdout 결과를 가져옴
3. 그 결과를 원래 command line에 삽입
4. 최종 command 실행

```bash
$ echo `dirname `pwd``   # 읽기 어렵고 오류 가능성 큼
```
backtick 방식은 중첩이 불편 => 현대 shell script에서는 보통 $(cmd)를 더 권장

---

- $(cmd)
- 더 읽기 쉽고 중첩 easy
```bash
$ pwd
/home/{$USER}/a
$ echo "현재 디렉터리 이름: $(basename "$(pwd)")"
a
```

---

### Pathname Expansion

== Shell glob => link to regex documentary
shell glob은 그중 특정 metacharacter를 이용한 filename expansion 기능이다.
shell glob은 *, ?, [...] 같은 metacharacter를 이용한 pathname expansion 기능이다.
Regex는 shell glob과 비슷해 보이지만 shell이 아니라 grep 같은 프로그램이 해석하는 별도의 pattern language다.

shell glob은 metacharacter를 사용하는 것이 맞다. 하지만 metacharacter를 사용한다고 해서 전부 glob은 아니다.

glob은 정확히는 filename expansion / pathname expansion을 뜻해


---

## Examples
```bash
$ grep "error" < input.log > error.log
```
input.log를 grep의 stdin으로 넣고,
"error"가 들어간 줄을 error.log에 저장한다.
```bash
$ grep "error" input.log | wc -l
```
input.log에서 "error"가 들어간 줄을 찾고,
그 결과 줄 수를 센다.
```bash
$ gcc main.c -o main && ./main
```
컴파일 성공 시에만 실행한다.
```bash
$ cd project || exit 1
```
project 디렉터리 이동에 실패하면 script를 종료한다.
```bash
$ echo "Today is $(date)"
```
date command를 먼저 실행하고,
그 출력 결과를 echo 문자열 안에 넣는다.




# Section 4. Shell Script

- Shell script is a program(or a list of commands) that is written the scripting language provided by Linux shell and can be interpreted by Linux shell.
-  Capabilities of Shell Script
    - Programming:
        -The shell script provides the concepts of variables, array, conditional statement, loop statement, comments, and etc
        - Not support class, pointer, threading, etc..
    - Batch jobs: A series of commands which be entered in CLI can be
executed automatically using a shell script
- It is much faster to write a code in shell script than in other programming languages, so useful for prototyping



---
<!--
In Linux/UNIX, program은 
    - keyboard (terminal input)에서 읽고 terminal output에 출력이라고 직접 생각하지 않음. 
    - 정해진 번호의 file descriptor에 대해 read/write 한다고 생각. 
    - 프로그램은 file descriptor number(0, 1, 2)가 실제로 무엇에 연결되어 있는지몰라도 됨.
    - Shell은 command을 실행하기 전에 그 번호들이 어디를 가리킬지 정해줌. 
    - 그래서 같은 cat, wc, grep 명령도 input이 terminal일 수도 있고 file, pipe일 수도 있음.

Standard streams는 progam이 시작될 때 기본적으로 열려 있는 세 개의 I/O channel

In UNIX-like systems, 새 프로그램이 실행될 때,
shell이 보통 이 세 descriptor를 열어 둔다. 
아무 redirection을 하지 않으면 세 개 모두 terminal에 연결된다. 
APUE도 “shell은 새 프로그램을 실행할 때 standard input, standard output, standard error 세 descriptor를 연다”고 설명



|Name|File Descriptor Number|C Standard I/O Name|Meaning|
|---|---|---|---|
|standard input| 0 | stdin | input을 읽는 통로|
|standard output| 1 | stdout | 정상 output을 쓰는 통로|
|standard error| 2 | stderr | error message를 쓰는 통로|    

`ls`를 실행하면 대략 다음 상태
fd 0 stdin  -> terminal keyboard input
fd 1 stdout -> terminal screen output
fd 2 stderr -> terminal screen output


stream을 file처럼 다룬다: Linux kernel 입장에서는 terminal, regular file, pipe, socket, device 등이 모두 file descriptor라는 공통 인터페이스로 다루어진


read(0, buf, size);     // stdin에서 읽기
write(1, buf, n);       // stdout에 쓰기
write(2, err, n);       // stderr에 쓰기


 cat은 “파일을 읽어서 화면에 출력하는 프로그램”처럼 보이지만, 내부적으로는 더 일반적으로 “입력을 읽어서 출력을 쓰는 프로그램
cat의 관점:
read(input_fd) -> write(output_fd)

input_fd가 terminal인지, file인지, pipe인지는 중요하지 않음


cat file > log
1. shell이 명령어를 parsing한다.
2. redirection 기호 > log 를 해석한다.
3. log 파일을 연다.
4. child process를 만든다.
5. child process의 fd 1(stdout)을 log 파일로 바꾼다.
6. child process에서 cat을 exec한다.
7. cat은 그냥 stdout(fd 1)에 write한다.
8. 그런데 fd 1이 terminal이 아니라 log 파일을 가리키므로 log에 기록된다.


$ cat file > log
cat: file: No such file or directory
$ cat file 1> log
cat: file: No such file or directory
$ cat log
$ cat file 2> log
byungjoonkim@Agapornis ~ % cat log
cat: file: No such file or directory
byungjoonkim@Agapornis ~ % wc < log
       1       7      37
byungjoonkim@Agapornis ~ % wc 0< log
       1       7      37

>는 stdout만 redirect
cat: file: No such file or directory 이 오류 메시지는 stdout(1)이 아니라 stderr(2)로
>는 fd 1만 바꾸므로, 오류 메시지는 여전히 terminal
cat file > log

fd 0 stdin  -> terminal
fd 1 stdout -> log
fd 2 stderr -> terminal
1>는 “file descriptor 1을 redirect하라”는 뜻
2>는 stderr redirect  stderr를 log로 
fd 0 stdin  -> terminal
fd 1 stdout -> terminal
fd 2 stderr -> log

<는 stdin redirect
wc는 기본적으로 standard input에서 데이터를 읽는다. 아무 redirection이 없으면 terminal에서 사용자가 입력하는 내용을 읽는다
0<도 stdin redirect


cat log와 cat < log의 차이
cat log
이 경우 log는 command-line argument
argv[0] = "cat"
argv[1] = "log"
cat < log
이 경우 log는 cat의 argument가 아니다
argv[0] = "cat"
대신 shell이 미리 log를 열어서 fd 0, 즉 stdin에 연결한다. 그러면 cat은 argument가 없으므로 stdin을 읽는다
결과는 같을 수 있지만 책임 주체가 다르다
cat log
    cat이 log 파일을 직접 open

cat < log
    shell이 log 파일을 열어 stdin으로 연결
    cat은 stdin을 읽을 뿐

stdout과 stderr를 분리하는 이유
find / -name test > result.txt
이 명령은 정상 검색 결과를 result.txt에 저장한다. 그런데 권한 없는 directory를 만나면 오류가 발생할 수 있다
Permission denied
이 오류까지 result.txt에 섞이면 나중에 결과 파일을 처리하기 어렵다

필요하면 오류만 버릴 수도 있다
find / -name test 2> /dev/null
또는 정상 출력과 오류를 둘 다 파일로 보낼 수도 있다.
command > out.txt 2> err.txt
또는 둘을 같은 파일로 합칠 수도 있다.
command > all.txt 2>&1
2>&1은 “fd 2를 fd 1이 현재 가리키는 곳으로 duplicate하라”는 뜻

다음 두 명령은 다르다.
command > all.txt 2>&1
1. stdout을 all.txt로 보낸다.
2. stderr를 현재 stdout이 가리키는 곳, 즉 all.txt로 보낸다.

stdout -> all.txt
stderr -> all.txt
command 2>&1 > all.txt
1. stderr를 현재 stdout이 가리키는 곳, 즉 terminal로 보낸다.
2. stdout을 all.txt로 보낸다.
stdout -> all.txt
stderr -> terminal
redirection은 단순 선언이 아니라 왼쪽에서 오른쪽 순서대로 적용되는 descriptor 조작으로 이해

Pipe와 redirection의 관계
ls | wc
이 명령에서 shell은 pipe라는 kernel object를 만들고 다음처럼 연결
ls의 stdout(fd 1) -> pipe write end

wc의 stdin(fd 0)  -> pipe read end
그래서 ls는 화면에 출력한다고 생각하고 fd 1에 write하지만, 실제로는 pipe로 들어간다. wc는 keyboard에서 읽는다고 생각하고 fd 0에서 read하지만, 실제로는 pipe에서 읽는다
Operating System Concepts도 |는 앞 command의 output을 뒤 command의 input으로 전달하도록 shell이 pipe를 설정한다고 설명

stdin(0)
    process의 기본 입력 통로
    보통 keyboard/terminal
    < file 또는 0< file 로 바꿀 수 있음

stdout(1)
    process의 정상 출력 통로
    보통 terminal
    > file 또는 1> file 로 바꿀 수 있음

stderr(2)
    process의 오류 출력 통로
    보통 terminal
    2> file 로 바꿀 수 있음

redirection
    shell이 command 실행 전에 file descriptor 연결을 바꾸는 기능

pipe
    앞 process의 stdout을 뒤 process의 stdin에 연결하는 기능

프로그램은 stdin/stdout/stderr라는 고정된 file descriptor에 read/write할 뿐이고,
그 descriptor가 terminal, file, pipe 중 어디를 가리킬지는 shell이 실행 전에 결정한다.
Shell의 redirection은 기본적으로 file descriptor를 바꾼다
cat file > log
이 명령에서 shell은 cat을 실행하기 전에 child process의 fd table을 이렇게 바꾼다
fd 0 -> terminal
fd 1 -> log
fd 2 -> terminal
그 다음 cat이 실행된다.

만약 cat 내부에서 C library의 stdout을 사용한다면, 그 stdout은 fd 1을 감싸고 있으므로 결과적으로 log로 출력된다.

즉 redirection의 직접 대상은file descriptor이고, standard stream은 그 file descriptor 위에 올라가 있기 때문에 영향을 받는다


### File Descriptor vs Standard Stream
file descriptor
file descriptor는 kernel 수준의 작은 non-negative integer (0, 1, 2, 3, 4, ...)
file descriptor는 kernel이 관리하는 lower-level I/O handle이
file descriptor는 kernel-level abstraction
fd 0
fd 1
fd 2
fd 3
...
각 process마다 file descriptor table이 있고, 각 fd는 kernel 내부의 open file description 같은 I/O object를 가리킨다.

e.g.
Process file descriptor table

fd 0 -> terminal input
fd 1 -> terminal output
fd 2 -> terminal output
fd 3 -> some opened file

read, write, open, close, dup2 같은 system call은 file descriptor를 직접 사용한



standard stream
C 언어의 stdin, stdout, stderr는 C standard I/O library의 FILE * stream
stdin
stdout
stderr
standard stream은 C library가 제공하는 higher-level I/O object이
```c
FILE *stdin;
FILE *stdout;
FILE *stderr;
```
이 FILE * object는 단순히 fd 번호만 들고 있는 것이 아니라, 보통 다음 정보도 함께 관리
- underlying file descriptor
- user-space buffer
- current buffer position
- EOF/error state
- buffering mode
그래서 printf, scanf, fgets, fprintf, fread, fwrite 같은 함수는 kernel에 매번 바로 system call을 하는 것이 아니라, C library의 buffer를 거쳐서 동작



relation between them
둘은 대응
stdin  -> descriptor 0
stdout -> descriptor 1
stderr -> descriptor 2
C 프로그램은 stdin, stdout, stderr라는 세 stream으로 시작하며, 각각 descriptor 0, 1, 2에 대응한다고 설명한다. 또한 FILE * stream은 file descriptor와 buffer를 감싼 abstraction

Kernel level:
    file descriptor 0, 1, 2

C library level:
    stdin, stdout, stderr


File descriptor와 standard stream이 대응되는 거면 두 용어의 차이는 그냥 os관점인지 c library 관점인지 의 차이이고 본질은 같은 것을 부르는 말인거야?

보통 stdin, stdout, stderr는 각각 file descriptor 0, 1, 2 위에 만들어진다.
둘은 강하게 대응되지만 같은 object는 아니다

file descriptor는 kernel에게 “몇 번 I/O 통로를 써라”라고 알려주는 작은 정수 번호
```c
read(0, buf, size);
write(1, buf, n);
write(2, err, n);
```

standard stream은 C library가 제공하는 FILE * object
```c
fgets(buf, size, stdin);
fprintf(stdout, "hello\n");
fprintf(stderr, "error\n");
```
stdin, stdout, stderr는 내부적으로 각각 어떤 file descriptor를 감싸고 있다
stdin  -> usually wraps fd 0
stdout -> usually wraps fd 1
stderr -> usually wraps fd 2

다음 두 코드는 비슷해 보이지만 계층이 다르다
```c
write(1, "hello\n", 6);
```
이 코드는 kernel의 file descriptor 1에 직접 쓴다
```c
printf("hello\n");
```

이 코드는 C library의 stdout stream에 쓴다. 그 후 C library가 buffering 상황에 따라 내부적으로 write(1, ...)를 호출할 수 있다
printf()
    -> stdout FILE object
        -> buffer
            -> write(fd 1)
                -> kernel
stdout과 fd 1은 연결되어 있지만, stdout == 1은 아니다
같은 object를 다른 관점에서 부르는 말은 아니고, file descriptor는 kernel-level handle, standard stream은 C library-level buffered object
file descriptor:
    OS가 관리하는 I/O 번호

standard stream:
    C library가 제공하는 FILE* stream

관계:
    standard stream이 내부적으로 file descriptor를 사용한다.

file descriptor = process 안에서 배관을 가리키는 번호표
standard stream = 그 번호표를 감싼 C library의 수도꼭지/필터 장치
actual I/O object = 실제 배관이 연결된 대상
                 예: terminal, file, pipe, socket, device

실제 배관에 해당하는 것은 kernel 내부의 open file description, terminal device, pipe, regular file 같은 I/O object 쪽에 가깝다

일반적으로 shell이 프로그램을 실행할 때 다음처럼 만들어 준다
stdin   -> fd 0 -> terminal input
stdout  -> fd 1 -> terminal output
stderr  -> fd 2 -> terminal output
APUE는 file descriptor를 “kernel이 process가 접근하는 file을 식별하기 위해 사용하는 작은 non-negative integer”라고 설명하고, shell이 새 프로그램을 실행할 때 standard input, standard output, standard error 세 descriptor를 연다고 설명해
또한 fd 0, 1, 2가 각각 standard input, standard output, standard error와 연결되는 것은 kernel 자체의 기능이라기보다 shell과 application이 따르는 convention이라고 설명

command > file
변경 전:
stdout -> fd 1 -> terminal

변경 후:
stdout -> fd 1 -> file
그래서 결과적으로 프로그램 입장에서는 여전히 stdout에 출력하지만, 그 출력은 terminal이 아니라 file로 간다

stdin  -> fd 0 -> terminal input side
stdout -> fd 1 -> terminal output side
stderr -> fd 2 -> terminal output side
실제 terminal은 keyboard와 screen을 단순히 따로따로 직접 연결한 물건이라기보다, kernel이 관리하는 terminal device이고, 그 terminal device를 통해 입력과 출력이 오가기 때문
CS:APP도 ls > foo.txt 같은 redirection은 shell이 ls의 standard output을 disk file로 redirect하는 것이며, 내부적으로는 dup2를 사용해 descriptor table entry를 바꾸는 방식으로 설명한다. 특히 dup2(4, 1) 후에는 fd 1이 기존 terminal이 아니라 file을 가리키게 되고, 이후 standard output에 쓰는 데이터가 file로 간다고 설명
file descriptor는 process의 descriptor table에서 I/O object를 가리키는 번호다.

standard stream은 C library가 제공하는 FILE * object이고,
보통 stdin은 fd 0, stdout은 fd 1, stderr는 fd 2를 감싼다.

shell redirection은 stdout 자체를 직접 바꾸는 것이 아니라,
command 실행 전에 fd 1이 가리키는 대상을 terminal에서 file로 바꾼다.

그 결과 stdout -> fd 1 -> file 구조가 되므로,
프로그램이 stdout에 출력한 내용이 file로 간다.
 fd 0, 1, 2만 특별한 convention이 있고, fd 3부터는 고정 mapping이 없다.
즉 fd 3 = 어떤 파일, fd 4 = 어떤 pipe처럼 정해져 있는 것이 아니라, process가 실행 중에 무엇을 open(), pipe(), socket(), dup() 했느냐에 따라 동적으로 정해진다
일반적인 시작 상태는 다음과 같다
fd 0 -> terminal input
fd 1 -> terminal output
fd 2 -> terminal output
fd 3부터는 “남는 번호 중 가장 작은 번호”가 배정
```c
int fd = open("log.txt", O_WRONLY | O_CREAT, 0644);
```

이미 0, 1, 2가 열려 있다면 보통 반환값은 3
fd 0 -> terminal input
fd 1 -> terminal output
fd 2 -> terminal output
fd 3 -> log.txt
또 다른 파일을 열면 보통 4
```c
int fd2 = open("data.txt", O_RDONLY);
```

fd 0 -> terminal input
fd 1 -> terminal output
fd 2 -> terminal output
fd 3 -> log.txt
fd 4 -> data.txt
CS:APP도 process는 stdin, stdout, stderr에 해당하는 descriptor 0, 1, 2로 시작하고, open은 가장 낮은 unused descriptor를 반환하므로 첫 번째 open은 보통 3을 반환한다고 설명
 fd 번호 자체에는 의미가 없다
 fd 3 자체가 log.txt라는 뜻은 아니다.
fd 4 자체가 data.txt라는 뜻도 아니다.
fd 번호는 그냥 process 안의 descriptor table index
예를 들어 어떤 process에서는:
fd 3 -> log.txt
fd 4 -> pipe read end
fd 5 -> socket
다른 process에서는:
fd 3 -> database.db
fd 4 -> terminal
fd 5 -> config.json
일 수 있다.
즉 fd mapping은 process마다 다르다.
왜 fd 3부터 시작하는 경우가 많을까?

0, 1, 2가 이미 standard input/output/error로 사용 중이기 때문이다. 그래서 첫 번째로 새 파일을 열면 가장 작은 빈 번호인 3이 배정되는 경우가 많다.

하지만 항상 3이라고 보장하면 안 된다.

예를 들어 프로그램 시작 전에 fd 3이 이미 열려 있거나, shell이 extra fd를 열어 둔 상태라면 첫 번째 open()이 4, 5 등을 반환할 수도 있다.

또는 fd 1을 닫고 파일을 열면?
```c
close(1);
int fd = open("out.txt", O_WRONLY | O_CREAT, 0644);
```

그러면 가장 낮은 빈 번호가 1이므로 새 파일이 fd 1에 배정될 수 있다.
fd 0 -> terminal input
fd 1 -> out.txt
fd 2 -> terminal output
이게 redirection의 핵심 원리와 연결
pipe()는 보통 fd 두 개를 만든다

pipe는 read end와 write end가 필요하므로 fd를 두 개 만든다.
```c
int p[2];
pipe(p);
```

보통 이미 0, 1, 2가 열려 있다면:
p[0] = 3   // pipe read end
p[1] = 4   // pipe write end
fd 0 -> terminal input
fd 1 -> terminal output
fd 2 -> terminal output
fd 3 -> pipe read end
fd 4 -> pipe write end
그리고 shell이 ls | wc를 만들 때는 대략 이런 식으로 fd를 바꾼다
ls process:
    fd 1 -> pipe write end

wc process:
    fd 0 -> pipe read end
    socket()도 fd를 반환한다

network socket도 fd로 다룬다.
```c
int s = socket(AF_INET, SOCK_STREAM, 0);
```
이미 0, 1, 2만 열려 있다면 보통:
fd 3 -> socket그래서 Linux/UNIX에서는 regular file, terminal, pipe, socket, device를 모두 fd로 다룰 수 있다.
fd 3 -> regular file
fd 4 -> pipe
fd 5 -> socket
fd 6 -> device file
런 식으로 process마다 다르게 mapping된다.
 stdin, stdout, stderr가 fd 0, 1, 2를 “open해주는” 주체는 보통 C standard library가 아니라 shell/parent process 쪽이야.

C standard library는 이미 열려 있는 fd 0, 1, 2를 바탕으로 stdin, stdout, stderr라는 FILE * stream object를 초기화해서 감싸는 역할

1. 프로그램 시작 전: shell이 fd 0, 1, 2를 준비한다
shell 또는 parent process가 child process를 만들고, 그 child process가 보통 다음 fd table을 물려받는다
APUE는 shell이 새 프로그램을 실행할 때 standard input, standard output, standard error 세 descriptor를 열어 둔다고 설명한다. 즉, 0, 1, 2는 보통 프로그램이 시작되기 전에 이미 존재
2. 프로그램 시작 후: C library가 standard stream을 준비한다

C 프로그램이 시작되면 C runtime / C standard library 쪽에서 다음과 같은 FILE * stream을 사용할 수 있게 해준다
stdin
stdout
stderr
이들은 일반적으로 다음 fd를 감싼다.
stdin  wraps fd 0
stdout wraps fd 1
stderr wraps fd 2
 C library가 하는 일은 대략 이것이다.
 이미 열려 있는 fd 0, 1, 2를 보고
그 위에 FILE * stream object를 만든다.
그래서 printf()는 직접 fd 1에 쓰는 함수가 아니라 stdout에 쓰는 함수고, stdout은 내부적으로 fd 1을 사용
CS:APP도 standard I/O는 Unix I/O file descriptor와 buffer를 감싼 higher-level abstraction으로 설명한다.
redirection이 있으면 shell이 실행 전에 바꾼다
./a.out > result.txt
이 경우 shell이 result.txt를 열고, child process의 fd 1이 그 파일을 가리키게 만든 뒤 exec한다.
그 다음 C library의 stdout은 fd 1을 감싸므로, 결과적으로 stdout -> result.txt가 된다.
read/write

read()와 write() system call은 실제 kernel I/O를 수행한다.

C library 함수는 내부적으로 필요할 때 read/write를 호출한다.

예를 들어:
fgets(buf, sizeof(buf), stdin);
은 개념적으로:
stdin FILE stream
    -> fd 0
        -> read(0, ...)

printf("hello\n");
stdout FILE stream
    -> fd 1
        -> write(1, ...)

다만 실제로는 C library buffering 때문에 printf() 한 번이 곧바로 write() 한 번으로 이어진다고 항상 보장되지는 않는다.

shell / parent process:
    fd 0, fd 1, fd 2를 terminal/file/pipe 등에 연결해 둔다.

exec:
    새 프로그램이 같은 fd table을 가지고 시작한다.

C runtime / C standard library:
    fd 0을 감싸서 stdin을 제공한다.
    fd 1을 감싸서 stdout을 제공한다.
    fd 2를 감싸서 stderr를 제공한다.

C program:
    scanf/fgets는 stdin을 사용한다.
    printf/puts는 stdout을 사용한다.
    fprintf(stderr, ...)는 stderr를 사용한다.

C library:
    필요할 때 read(0, ...), write(1, ...), write(2, ...) 같은 system call을 호출한다.

open:
    보통 C standard library가 fd 0, 1, 2를 open하는 것이 아니다.
    shell/parent process가 이미 열어 둔 fd 0, 1, 2를 프로그램이 물려받는다.

read/write:
    C standard library의 stdin/stdout/stderr 함수들은 내부적으로 fd 0, 1, 2에 대해
    read/write system call을 사용할 수 있다.

standard stream:
    fd 0, 1, 2를 감싼 C library-level FILE * object다.
standard stream은 C standard library가 fd 0, 1, 2를 새로 open해주는 것이 아니라, 이미 열려 있는 fd 0, 1, 2를 감싸서 buffered I/O interface로 제공하는 것이


standard stream은 C standard library가 fd 0, 1, 2를 새로 open해주는 것이 아니라, 이미 열려 있는 fd 0, 1, 2를 감싸서 buffered I/O interface로 제공하는 것이

FILE *fp = fopen("log.txt", "w");

이 경우는 C library의 fopen()이 내부적으로 대략 다음을 한다
open("log.txt", ...)
    -> 새 fd 획득, 예: fd 3

fd 3을 감싸는 FILE * stream 생성
    -> fp
    그래서 이 경우에는 C library가 open()을 호출해서 새 fd를 얻고, 그 fd를 감싸는 FILE *를 만든다고 볼 수 있다.
fp -> fd 3 -> log.txt
하지만 stdin, stdout, stderr는 보통 이미 준비된 fd 0, 1, 2를 감싸는 특수한 기본 stream


File descriptor
    kernel-level I/O handle
    small non-negative integer
    예: 0, 1, 2, 3, 4, ...

Standard stream
    C standard I/O library-level abstraction
    FILE * object
    예: stdin, stdout, stderr

관계
    stdin  wraps fd 0
    stdout wraps fd 1
    stderr wraps fd 2

stdin  -> FILE * stream -> fd 0 -> terminal input / file / pipe / ...
stdout -> FILE * stream -> fd 1 -> terminal output / file / pipe / ...
stderr -> FILE * stream -> fd 2 -> terminal output / file / pipe / ...

S:APP도 standard I/O를 file descriptor와 buffer를 감싼 higher-level abstraction으로 설명

read/write는 file descriptor를 직접 사용하는 low-level Unix I/O이고,
stdin/stdout/stderr는 그 fd 0/1/2를 감싼 C standard I/O stream이다.

단, “완전히 같은 동작”은 아니다

개념적으로 같은 방향의 I/O를 가리키지만, 실제 동작은 다를 수 있어. 이유는 buffering 때문이야.

예를 들어:
```c
write(1, "A", 1);
```
이건 바로 kernel의 write() system call로 내려간다.
```c
printf("A");
```
이건 stdout의 C library buffer에 먼저 들어갈 수 있다. 화면에 바로 보일 수도 있고, newline이 나오거나 fflush(stdout)이 호출되거나 프로그램이 종료될 때 실제 write(1, ...)가 발생할 수도 있다.
read(0, buf, size)는 fd 0에서 직접 읽는 low-level Unix I/O이고,
fgets(buf, size, stdin) 또는 fread(..., stdin)은 stdin FILE * stream을 통해 읽는 C standard I/O이다.

stdin은 내부적으로 fd 0과 buffer를 감싸는 abstraction이므로,
개념적으로 stdin을 통한 입력은 fd 0을 통한 입력 위에 올라간 형태라고 볼 수 있다.

마찬가지로 write(1, buf, size)는 fd 1에 직접 쓰는 low-level Unix I/O이고,
fprintf(stdout, ...) 또는 fwrite(..., stdout)은 stdout FILE * stream을 통해 쓰는 C standard I/O이다.
stdout은 내부적으로 fd 1과 buffer를 감싼다.


standard stream = file descriptor + α 를 감싼 high-level wrapper
여기서 α에 들어가는 것이 바로 C standard I/O library가 관리하는 추가 정보
FILE * stream
    ├── underlying file descriptor
    ├── user-space buffer
    ├── current buffer position
    ├── EOF state
    ├── error state
    ├── buffering mode
    └── 기타 C library가 필요한 metadata
    그래서 stdin, stdout, stderr는 단순히 0, 1, 2의 다른 이름이 아니라, 각각 fd 0, 1, 2를 감싼 FILE * object라고 보는 게 정확

    Low-level Unix I/O는 file descriptor를 직접 사용
```c
read(0, buf, size);
write(1, buf, n);
```
    High-level C standard I/O는 stream을 사용
```c
fgets(buf, size, stdin);
fprintf(stdout, "hello\n");
```
fprintf(stdout, "hello\n")
    -> stdout FILE * stream
    -> C library buffer
    -> 필요할 때 write(1, ...)
    -> kernel
fgets(buf, size, stdin)
    -> stdin FILE * stream
    -> buffer에 읽어 둔 데이터가 있는지 확인
    -> 없으면 read(0, ...)
    -> buffer에서 사용자 buf로 복사

 왜 + α가 필요할까?
 가장 큰 이유는 buffering이야.

write(1, "A", 1)은 바로 kernel system call로 내려간다. 그런데 printf("A")는 일단 C library의 stdout buffer에 저장될 수 있다.




write(1, ...)
    -> kernel로 바로 감

printf(...)
    -> stdout buffer에 모음
    -> newline, buffer full, fflush, program exit 등에서 write(1, ...) 호출
    이렇게 하면 system call 횟수를 줄일 수 있어서 성능이 좋아진다. System call은 user mode에서 kernel mode로 넘어가는 비용이 있기 때문

A standard stream is a high-level C standard I/O abstraction implemented as a FILE * object. It wraps an underlying file descriptor together with a user-space buffer and stream state such as EOF/error flags and buffering mode.
Standard stream은 C standard I/O library가 제공하는 high-level wrapper이며, 내부적으로 file descriptor에 더해 buffer, EOF/error 상태, buffering mode 같은 추가 정보를 함께 관리하는 FILE * object이다.
다만 standard stream = file descriptor + α라고 할 때, 이것이 kernel 내부 구조라는 뜻은 아니야
file descriptor
    kernel-level 개념

FILE * stream
    user-space C library-level 개념

즉 FILE *의 buffer와 상태 정보는 보통 process의 user space 안에서 C library가 관리한다. Kernel은 stdin, stdout이라는 이름 자체를 모른다. Kernel은 기본적으로 fd 0, 1, 2 같은 정수만 본다.

APUE도 file descriptor는 kernel이 process의 file 접근을 식별하기 위해 사용하는 작은 non-negative integer라고 설명하고, standard input/output/error는 shell이 프로그램 실행 시 열어 두는 descriptor convention으로 설명
 α는 주로 buffering과 stream state라고 보면 된다.

 근데 c standard io library는 c lang으로 만들때 쓰는 거 아냐? 다른 언어를 쓰거나 c standard io library를 안 쓰먄 어떡해? c standard io library가 stdio.h에 구현되어있는거야?
 맞아. C standard I/O library는 C 언어로 프로그램을 작성할 때 주로 쓰는 user-space library야. 그래서 다른 언어를 쓰거나 C에서 stdio를 안 쓰면 stdin, stdout, stderr라는 FILE * stream abstraction을 반드시 쓰는 것은 아니야
 Kernel
    file descriptor: 0, 1, 2, 3, ...

C standard I/O library
    FILE * stream: stdin, stdout, stderr

Other language runtime
    각 언어가 제공하는 input/output abstraction


1. C standard I/O library를 안 쓰면?

C에서도 stdio.h를 안 쓰고 Unix system call을 직접 사용할 수 있어.
```c
#include <unistd.h>

int main(void)
{
    char buf[100];
    ssize_t n;

    n = read(0, buf, sizeof(buf));
    write(1, buf, n);

    return 0;
}
```

2. 다른 언어를 쓰면 어떻게 되나?

다른 언어도 결국 운영체제와 통신해야 하므로, UNIX/Linux에서는 내부적으로 대개 fd 0, 1, 2를 사용한다. 다만 그 위에 각 언어 runtime이 자기만의 wrapper를 제공한다.

```python
import sys

sys.stdin
sys.stdout
sys.stderr
```
```java
System.in
System.out
System.err
```
```rust
std::io::stdin()
std::io::stdout()
std::io::stderr()
```
```node.js
process.stdin
process.stdout
process.stderr
```

이것들은 C의 FILE *와 같은 object는 아니지만, 역할은 비슷해.
Python sys.stdout
    -> Python runtime wrapper
    -> underlying fd 1
    -> kernel

Java System.out
    -> JVM / Java library wrapper
    -> underlying stdout handle/fd
    -> OS

C stdout
    -> FILE * wrapper
    -> fd 1
    -> kernel

즉, 언어가 바뀌면 FILE *는 안 쓸 수 있지만, OS level의 standard file descriptor convention은 여전히 남아 있는 경우가 많다
stdio.h는 보통 header file이야. 즉, 함수와 타입의 선언을 제공
#include <stdio.h>
를 하면 사용할 수 있는 것들:
FILE
stdin
stdout
stderr
printf()
fprintf()
fgets()
fread()
fwrite()
fopen()
fclose()
실제 구현 코드는 보통 stdio.h 안에 들어 있지 않아.
stdio.h
    declarations
    type definitions
    macros
    function prototypes

libc
    actual implementation
    예: glibc, musl, FreeBSD libc, Apple libc 등

printf("hello\n");
를 컴파일할 때 compiler는 stdio.h를 보고 “printf라는 함수가 이런 형태로 존재하는구나”를 안다. 그리고 link 단계에서 실제 printf 구현은 C standard library, 즉 libc에서 연결

stdin  -> FILE * object wrapping fd 0
stdout -> FILE * object wrapping fd 1
stderr -> FILE * object wrapping fd 2
하지만 실제 구현 방식은 libc마다 다를 수 있어. 어떤 구현에서는 stdin이 macro처럼 정의되어 있을 수도 있고, 어떤 구현에서는 external object를 가리킬 수도 있어. 중요한 것은 C programmer 입장에서는 stdin, stdout, stderr를 FILE * stream처럼 사용한다는 점
그래서 command > out.txt가 C 프로그램, Python 프로그램, Java 프로그램에 모두 비슷하게 적용되는 이유는 redirection이 각 언어의 high-level stream을 직접 바꾸는 것이 아니라, process의 fd 1을 바꾸기 때문
Application code

C program using stdio
    printf("hello\n")
        -> stdout FILE *
        -> libc buffer
        -> write(1, ...)
        -> kernel fd 1

C program using Unix I/O directly
    write(1, "hello\n", 6)
        -> kernel fd 1

Python program
    print("hello")
        -> Python sys.stdout
        -> underlying fd 1
        -> kernel

Shell redirection
    command > out.txt
        -> shell changes fd 1 to out.txt
        -> program's stdout abstraction follows fd 1

stdin/stdout/stderr는 C에서는 FILE * stream으로 제공되지만, 다른 언어에서는 각 언어 runtime의 I/O object로 제공된다. 그러나 UNIX/Linux에서 그 아래쪽에는 보통 fd 0, 1, 2라는 공통 기반

---
summary


# Standard Streams, File Descriptors, Redirection, Pipe

## 1. Core Idea

In Linux/UNIX, a program does not need to directly know whether it is reading from keyboard, file, pipe, socket, or device.

Instead, a program usually performs I/O through file descriptor numbers.

The important idea is:

    Program:
        read/write to file descriptors

    Shell:
        decides what each file descriptor points to before executing the command

    Kernel:
        manages actual I/O objects such as terminal, regular file, pipe, socket, device

Therefore, the same command such as cat, wc, grep can receive input from:

    - terminal input
    - regular file
    - pipe
    - socket
    - device file

and can send output to:

    - terminal output
    - regular file
    - pipe
    - socket
    - device file

The program does not have to know the exact connection target of fd 0, fd 1, fd 2.

High-level summary:

    fd 0:
        standard input

    fd 1:
        standard output

    fd 2:
        standard error

    Shell redirection:
        changes what fd 0, fd 1, fd 2 point to

    Pipe:
        connects one process's fd 1 to another process's fd 0

---

## 2. Standard Streams

Standard streams are the three default I/O channels that are normally available when a program starts.

In UNIX-like systems, when a new program is executed, the shell or parent process normally prepares three descriptors:

    - standard input
    - standard output
    - standard error

If no redirection is used, all three are usually connected to the terminal.

| Name | File Descriptor Number | C Standard I/O Name | Meaning |
|---|---:|---|---|
| standard input | 0 | stdin | input을 읽는 통로 |
| standard output | 1 | stdout | 정상 output을 쓰는 통로 |
| standard error | 2 | stderr | error message를 쓰는 통로 |

When running a simple command:

```bash
ls
```

the process usually starts with this mapping:

```txt
fd 0 -> terminal input
fd 1 -> terminal output
fd 2 -> terminal output
```

In C standard I/O terms:

```txt
stdin  -> fd 0 -> terminal input
stdout -> fd 1 -> terminal output
stderr -> fd 2 -> terminal output
```

More precise terminal wording:

```txt
stdin  -> fd 0 -> terminal input side
stdout -> fd 1 -> terminal output side
stderr -> fd 2 -> terminal output side
```

The terminal is not simply “keyboard + screen” at the kernel level. It is closer to a terminal device managed by the kernel, through which input and output are handled.

---

## 3. File Descriptor

A file descriptor is a small non-negative integer used by the kernel to identify an open I/O object for a process.

Examples:

```txt
0, 1, 2, 3, 4, ...
```

A process has its own file descriptor table.

Example:

```txt
Process file descriptor table

fd 0 -> terminal input
fd 1 -> terminal output
fd 2 -> terminal output
fd 3 -> some opened file
fd 4 -> pipe read end
fd 5 -> socket
```

Important points:

    - file descriptor is kernel-level
    - file descriptor is process-specific
    - file descriptor number itself has no universal meaning except conventional fd 0, 1, 2
    - fd 3 and above are assigned dynamically
    - file descriptors are used directly by system calls such as open, read, write, close, dup, dup2, pipe, socket

Low-level Unix I/O uses file descriptors directly:

```c
read(0, buf, size);
write(1, buf, n);
write(2, err, n);
```

Meaning:

```txt
read(0, buf, size)
    -> read from fd 0

write(1, buf, n)
    -> write to fd 1

write(2, err, n)
    -> write to fd 2
```

If fd 4 is validly open in the current process, this is also possible:

```c
read(4, buf, size);
write(4, buf, n);
```

But arbitrary numbers do not automatically work.

For example:

```c
read(999, buf, size);
```

If fd 999 is not open in the current process, the system call fails, usually with EBADF.

---

## 4. Standard Stream

A standard stream is a high-level C standard I/O abstraction implemented as a FILE * object.

In C:

```c
FILE *stdin;
FILE *stdout;
FILE *stderr;
```

Standard streams are not the same objects as file descriptors.

They are wrappers around file descriptors.

Conceptually:

```txt
stdin  -> FILE * stream -> fd 0
stdout -> FILE * stream -> fd 1
stderr -> FILE * stream -> fd 2
```

A FILE * stream usually manages:

```txt
FILE * stream
    ├── underlying file descriptor
    ├── user-space buffer
    ├── current buffer position
    ├── EOF state
    ├── error state
    ├── buffering mode
    └── other C library metadata
```

Therefore:

```txt
standard stream = file descriptor + alpha
```

where alpha mainly means:

```txt
- user-space buffer
- EOF/error state
- buffering mode
- current buffer position
- C library metadata
```

Important distinction:

```txt
file descriptor
    kernel-level I/O handle

FILE * stream
    user-space C library-level wrapper
```

The kernel does not know the names stdin, stdout, stderr.

The kernel mainly sees integer file descriptors such as 0, 1, 2.

---

## 5. File Descriptor vs Standard Stream

| Category | File Descriptor | Standard Stream |
|---|---|---|
| Level | kernel-level | C library-level |
| Type | int | FILE * |
| Examples | 0, 1, 2, 3, 4 | stdin, stdout, stderr |
| Used by | Unix system calls | C standard I/O functions |
| Functions | read, write, open, close, dup2 | printf, scanf, fgets, fprintf, fread, fwrite, fopen |
| Buffering | no C stdio buffer | has C library buffer |
| Main role | identifies open I/O object | high-level buffered I/O abstraction |

Correct low-level Unix I/O:

```c
read(0, buf, size);
write(1, buf, n);
write(2, err, n);
```

Correct C standard I/O:

```c
fgets(buf, size, stdin);
fprintf(stdout, "hello\n");
fprintf(stderr, "error\n");
```

Incorrect expression in actual C code:

```c
read(stdin, buf, size);
write(stdout, buf, n);
```

Reason:

```txt
read/write expect int file descriptor.
stdin/stdout/stderr are FILE * streams.
```

However, conceptually:

```txt
read(0, ...)
    ≈ low-level input from standard input path

fgets(..., stdin)
    ≈ high-level input from standard input stream

write(1, ...)
    ≈ low-level output to standard output path

fprintf(stdout, ...)
    ≈ high-level output to standard output stream
```

The conceptual relation is:

```txt
fgets(buf, size, stdin)
    -> stdin FILE * stream
    -> check C library buffer
    -> if needed, call read(0, internal_buffer, ...)
    -> copy data to user buffer

fprintf(stdout, ...)
    -> stdout FILE * stream
    -> write to C library buffer
    -> if needed, call write(1, internal_buffer, ...)
```

So:

```txt
read(0, ...) == read(stdin)
```

is syntactically wrong, but the intuition is acceptable if it means:

```txt
stdin-based input is built on top of fd 0-based input.
```

Likewise:

```txt
stdout-based output is built on top of fd 1-based output.
stderr-based output is built on top of fd 2-based output.
```

---

## 6. Buffering

The biggest practical difference between file descriptor I/O and stream I/O is buffering.

Low-level Unix I/O:

```c
write(1, "A", 1);
```

This directly invokes a write system call.

C standard I/O:

```c
printf("A");
```

This may first store "A" in the stdout buffer.

The actual write system call may happen later, such as when:

```txt
- newline is printed
- buffer becomes full
- fflush(stdout) is called
- program exits normally
```

Conceptual flow:

```txt
write(1, ...)
    -> kernel immediately

printf(...)
    -> stdout FILE * stream
    -> C library buffer
    -> later write(1, ...)
    -> kernel
```

Why buffering exists:

```txt
System calls require transition from user mode to kernel mode.
This transition has overhead.
Buffering reduces the number of system calls.
Therefore, buffered I/O can improve performance.
```

---

## 7. Who Opens fd 0, fd 1, fd 2?

stdin, stdout, stderr do not usually open fd 0, fd 1, fd 2 themselves.

In a normal shell environment:

```txt
shell / parent process:
    prepares fd 0, fd 1, fd 2

exec:
    new program starts with inherited file descriptor table

C runtime / C standard library:
    wraps fd 0 as stdin
    wraps fd 1 as stdout
    wraps fd 2 as stderr
```

So:

```txt
C standard I/O library does not usually create fd 0, fd 1, fd 2 from scratch.
It wraps already-open fd 0, fd 1, fd 2 as FILE * streams.
```

Example without redirection:

```txt
Before program starts:

fd 0 -> terminal input
fd 1 -> terminal output
fd 2 -> terminal output

After C runtime initializes standard streams:

stdin  -> fd 0 -> terminal input
stdout -> fd 1 -> terminal output
stderr -> fd 2 -> terminal output
```

Example with redirection:

```bash
./a.out > result.txt
```

Shell sets up:

```txt
fd 0 -> terminal input
fd 1 -> result.txt
fd 2 -> terminal output
```

Then the C library wraps them:

```txt
stdin  -> fd 0 -> terminal input
stdout -> fd 1 -> result.txt
stderr -> fd 2 -> terminal output
```

Therefore:

```c
printf("hello\n");
```

writes to stdout, and stdout ultimately uses fd 1, which points to result.txt.

---

## 8. fopen and Additional Streams

stdin, stdout, stderr are special default streams.

But C library can also create new streams.

Example:

```c
FILE *fp = fopen("log.txt", "w");
```

Conceptual flow:

```txt
fopen("log.txt", "w")
    -> internally calls open("log.txt", ...)
    -> gets new fd, for example fd 3
    -> creates FILE * stream wrapping fd 3
```

Result:

```txt
fp -> FILE * stream -> fd 3 -> log.txt
```

Therefore:

```txt
stdin/stdout/stderr:
    usually wrap already-open fd 0, 1, 2

fopen:
    opens a new file and creates a new FILE * stream around the new fd
```

---

## 9. fd 3 and Higher

Only fd 0, fd 1, fd 2 have conventional standard meanings.

```txt
fd 0 -> standard input
fd 1 -> standard output
fd 2 -> standard error
```

fd 3 and higher have no fixed meaning.

They depend on what the process opened or created.

Example:

```c
int fd = open("log.txt", O_WRONLY | O_CREAT, 0644);
```

If fd 0, 1, 2 are already open, the returned fd is often 3:

```txt
fd 0 -> terminal input
fd 1 -> terminal output
fd 2 -> terminal output
fd 3 -> log.txt
```

Another open:

```c
int fd2 = open("data.txt", O_RDONLY);
```

Often:

```txt
fd 0 -> terminal input
fd 1 -> terminal output
fd 2 -> terminal output
fd 3 -> log.txt
fd 4 -> data.txt
```

General rule:

```txt
open returns the lowest available unused file descriptor.
```

But fd 3 is not guaranteed.

If fd 1 is closed first:

```c
close(1);
int fd = open("out.txt", O_WRONLY | O_CREAT, 0644);
```

then the new file may become fd 1:

```txt
fd 0 -> terminal input
fd 1 -> out.txt
fd 2 -> terminal output
```

This principle is closely related to shell redirection.

---

## 10. Actual I/O Objects

A file descriptor is not the actual file or pipe itself.

A standard stream is not the actual file or pipe itself either.

More precise model:

```txt
standard stream:
    C library wrapper

file descriptor:
    process-local integer index

actual I/O object:
    kernel-managed object
    examples:
        - open file description
        - terminal device
        - regular file
        - pipe
        - socket
        - device file
```

Analogy:

```txt
file descriptor:
    number tag for a pipe inside a process

standard stream:
    faucet/filter installed on top of that number tag by C library

actual I/O object:
    the real pipe or destination managed by the kernel
```

But remember: this is only an analogy. Internally, the OS uses file descriptor tables and kernel objects, not literal pipes.

---

## 11. Shell Redirection

Shell redirection changes file descriptor mappings before executing a command.

Example:

```bash
cat file > log
```

Conceptual steps:

```txt
1. shell parses the command
2. shell recognizes redirection: > log
3. shell opens log
4. shell creates a child process
5. in the child process, shell redirects fd 1 to log
6. shell executes cat using exec
7. cat writes to stdout or fd 1
8. fd 1 points to log, so output goes to log
```

Before redirection:

```txt
fd 0 -> terminal input
fd 1 -> terminal output
fd 2 -> terminal output
```

After:

```txt
fd 0 -> terminal input
fd 1 -> log
fd 2 -> terminal output
```

If cat uses C standard I/O:

```txt
stdout -> fd 1 -> log
```

So stdout is not directly changed by the shell.

More precise statement:

```txt
Shell redirection changes fd 1.
stdout is a C library wrapper around fd 1.
Therefore stdout output follows the new fd 1 target.
```

---

## 12. stdout Redirection: > and 1>

The following two commands are equivalent:

```bash
cat file > log
cat file 1> log
```

Meaning:

```txt
redirect fd 1 to log
```

Result:

```txt
fd 0 -> terminal input
fd 1 -> log
fd 2 -> terminal output
```

Important point:

```txt
> redirects stdout only.
> does not redirect stderr.
```

Example:

```bash
cat file > log
```

If file does not exist:

```txt
cat: file: No such file or directory
```

This error message goes to stderr, not stdout.

Therefore it still appears on the terminal:

```txt
fd 1 -> log
fd 2 -> terminal output
```

Same for:

```bash
cat file 1> log
```

---

## 13. stderr Redirection: 2>

The command:

```bash
cat file 2> log
```

redirects fd 2, that is stderr, to log.

Result:

```txt
fd 0 -> terminal input
fd 1 -> terminal output
fd 2 -> log
```

If file does not exist, the error message goes to log.

Example:

```bash
cat file 2> log
cat log
```

Output:

```txt
cat: file: No such file or directory
```

---

## 14. stdin Redirection: < and 0<

The following two commands are equivalent:

```bash
wc < log
wc 0< log
```

Meaning:

```txt
redirect fd 0 from log
```

Result:

```txt
fd 0 -> log
fd 1 -> terminal output
fd 2 -> terminal output
```

wc normally reads from standard input.

Without redirection:

```bash
wc
```

wc reads from terminal input.

With redirection:

```bash
wc < log
```

wc reads from log through fd 0.

Example:

```bash
wc < log
```

Output:

```txt
1 7 37
```

Meaning:

```txt
line count   word count   byte count
1            7            37
```

---

## 15. cat log vs cat < log

These two commands can produce the same output, but their internal behavior is different.

Command 1:

```bash
cat log
```

Here, log is a command-line argument.

```txt
argv[0] = "cat"
argv[1] = "log"
```

Meaning:

```txt
cat itself opens log.
```

Command 2:

```bash
cat < log
```

Here, log is not cat's argument.

```txt
argv[0] = "cat"
```

Meaning:

```txt
shell opens log
shell connects log to fd 0
cat reads from stdin
```

Comparison:

```txt
cat log
    -> cat receives "log" as argv[1]
    -> cat opens the file directly

cat < log
    -> shell opens log
    -> shell redirects fd 0 to log
    -> cat reads from stdin
```

Same result, different responsibility.

---

## 16. Why Separate stdout and stderr?

stdout and stderr are separated so that normal output and error messages do not get mixed.

Example:

```bash
find / -name test > result.txt
```

Normal search results go to result.txt.

But permission errors such as:

```txt
Permission denied
```

go to stderr and still appear on terminal.

This is useful because result.txt contains only normal data, not error messages.

To discard only errors:

```bash
find / -name test 2> /dev/null
```

To save stdout and stderr separately:

```bash
command > out.txt 2> err.txt
```

Result:

```txt
fd 1 -> out.txt
fd 2 -> err.txt
```

To merge stdout and stderr:

```bash
command > all.txt 2>&1
```

Meaning:

```txt
1. redirect fd 1 to all.txt
2. duplicate current fd 1 target into fd 2
```

Result:

```txt
fd 1 -> all.txt
fd 2 -> all.txt
```

---

## 17. Redirection Order Matters

The following two commands are different:

```bash
command > all.txt 2>&1
```

Order:

```txt
1. fd 1 -> all.txt
2. fd 2 -> current fd 1 target, which is all.txt
```

Result:

```txt
stdout -> all.txt
stderr -> all.txt
```

But:

```bash
command 2>&1 > all.txt
```

Order:

```txt
1. fd 2 -> current fd 1 target, which is terminal
2. fd 1 -> all.txt
```

Result:

```txt
stdout -> all.txt
stderr -> terminal
```

Therefore:

```txt
redirection is not just a declaration.
redirection is descriptor manipulation applied from left to right.
```

---

## 18. Pipe

A pipe connects the stdout of one process to the stdin of another process.

Example:

```bash
ls | wc
```

The shell creates a pipe kernel object and connects descriptors:

```txt
ls process:
    fd 1 -> pipe write end

wc process:
    fd 0 -> pipe read end
```

So:

```txt
ls writes to fd 1
    -> actually writes into pipe

wc reads from fd 0
    -> actually reads from pipe
```

From each program's perspective:

```txt
ls:
    just writes to stdout

wc:
    just reads from stdin
```

But the shell connected them through a pipe.

A pipe usually requires two file descriptors:

```c
int p[2];
pipe(p);
```

Typically:

```txt
p[0] = pipe read end
p[1] = pipe write end
```

If fd 0, 1, 2 are already open, the pipe may become:

```txt
fd 3 -> pipe read end
fd 4 -> pipe write end
```

Then the shell can use descriptor duplication to produce:

```txt
ls:
    fd 1 -> pipe write end

wc:
    fd 0 -> pipe read end
```

---

## 19. Socket and Device Files

In Linux/UNIX, file descriptors are not limited to regular files.

They can refer to:

```txt
- terminal
- regular file
- directory-related object
- pipe
- FIFO
- socket
- device file
```

Example:

```c
int s = socket(AF_INET, SOCK_STREAM, 0);
```

If fd 0, 1, 2 are already open, the socket may be assigned fd 3:

```txt
fd 3 -> socket
```

This is why Unix I/O is powerful:

```txt
read(fd, ...)
write(fd, ...)
```

can operate on many different I/O objects through the same descriptor interface, although exact behavior depends on the object type.

---

## 20. C Standard I/O Library, stdio.h, and libc

C standard I/O library is mainly used when programming in C.

It provides high-level I/O functions and types such as:

```txt
FILE
stdin
stdout
stderr
printf
fprintf
fgets
fread
fwrite
fopen
fclose
```

To use them:

```c
#include <stdio.h>
```

But stdio.h is usually not where the actual implementation lives.

More accurate structure:

```txt
stdio.h
    - declarations
    - type definitions
    - macros
    - function prototypes

libc
    - actual implementation
    - examples:
        glibc
        musl
        FreeBSD libc
        Apple libc
```

When compiling:

```c
printf("hello\n");
```

the compiler uses stdio.h to know that printf exists and what its function prototype looks like.

At link time, the actual implementation is linked from libc.

Important:

```txt
stdio.h declares.
libc implements.
```

---

## 21. What If We Do Not Use C Standard I/O?

C programs do not have to use stdio.

They can use Unix system calls directly.

Example:

```c
#include <unistd.h>

int main(void)
{
    char buf[100];
    ssize_t n;

    n = read(0, buf, sizeof(buf));
    write(1, buf, n);

    return 0;
}
```

This program does not use:

```txt
stdin
stdout
stderr
printf
fgets
FILE *
```

It directly uses:

```txt
fd 0
fd 1
read
write
```

So:

```txt
C standard I/O is optional in C.
File descriptors are the lower-level OS interface.
```

---

## 22. What About Other Programming Languages?

Other languages do not necessarily use C FILE * streams.

But on UNIX/Linux, they usually still run on top of fd 0, fd 1, fd 2.

Examples:

Python:

```python
import sys

sys.stdin
sys.stdout
sys.stderr
```

Java:

```java
System.in
System.out
System.err
```

Rust:

```rust
std::io::stdin()
std::io::stdout()
std::io::stderr()
```

Node.js:

```javascript
process.stdin
process.stdout
process.stderr
```

These are not C FILE * objects.

They are language/runtime-specific I/O abstractions.

Conceptual layering:

```txt
Python print("hello")
    -> Python sys.stdout
    -> underlying fd 1
    -> kernel

Java System.out.println("hello")
    -> Java/JVM output stream
    -> underlying OS stdout handle/fd
    -> kernel

Rust println!("hello")
    -> Rust std::io::stdout()
    -> underlying fd 1
    -> kernel

C printf("hello\n")
    -> C stdout FILE *
    -> fd 1
    -> kernel
```

That is why shell redirection works across many languages.

Example:

```bash
python script.py > out.txt
java Main > out.txt
./c_program > out.txt
node app.js > out.txt
```

In all cases, the shell changes fd 1 before the program starts.

The language runtime's stdout abstraction follows fd 1.

---

## 23. Overall Layer Model

```txt
Application Code

    C using stdio:
        printf("hello\n")
            -> stdout FILE *
            -> C library buffer
            -> write(1, ...)
            -> kernel fd 1

    C using Unix I/O directly:
        write(1, "hello\n", 6)
            -> kernel fd 1

    Python:
        print("hello")
            -> sys.stdout
            -> underlying fd 1
            -> kernel

    Java:
        System.out.println("hello")
            -> Java output stream
            -> underlying stdout handle/fd
            -> OS

Shell Redirection

    command > out.txt
        -> shell changes fd 1 to out.txt before exec
        -> program's stdout abstraction follows fd 1
```

---

## 24. Final Summary

```txt
File descriptor:
    kernel-level small non-negative integer
    process-local I/O handle
    examples: 0, 1, 2, 3, 4

Standard stream:
    C standard I/O library-level FILE * stream
    examples: stdin, stdout, stderr
    high-level wrapper around fd 0, 1, 2

stdin:
    wraps fd 0

stdout:
    wraps fd 1

stderr:
    wraps fd 2

fd 0, 1, 2:
    conventional standard descriptors

fd 3 and above:
    dynamically assigned
    no fixed universal meaning

read/write:
    low-level Unix I/O
    use file descriptors directly

printf/fgets/fprintf:
    high-level C standard I/O
    use FILE * streams

redirection:
    shell changes file descriptor mapping before executing command

pipe:
    shell connects one process's fd 1 to another process's fd 0

C standard I/O:
    implemented in libc
    declared through stdio.h

Other languages:
    use their own runtime I/O wrappers
    but usually still rely on fd 0, 1, 2 underneath on UNIX/Linux
```

One-sentence version:

```txt
In Linux/UNIX, programs perform I/O through file descriptors; C standard streams such as stdin, stdout, and stderr are high-level FILE * wrappers around fd 0, fd 1, and fd 2; shell redirection and pipes work by changing the file descriptor mappings before the program starts.
```


---
- Standard streams are ...
    - Input and output channels that handle data from/to I/O devices or applications
    - Established when a Linux command is executed
- All the streams are treated as if they were files in Linux, so we can read/write data from these streams like files
---
-->




---
## References
- Kangwon National University Lecture Note (course: 48400009)
- Advanced Programming in the UNIX Environment [3rd Ed] - W. Richard Stevens, Stephen A. Rago
- Computer Systems (A Programmer's Perspective) [3rd Ed] - Randal E. Bryant, David R. O’Hallaron
- Operating System Concepts [10th Ed] - Abraham Silberschatz, Greg Gagne, Peter B. Galvin

## Acknowledgements
- OpenAI ChatGPT
- Google NotebookLM
