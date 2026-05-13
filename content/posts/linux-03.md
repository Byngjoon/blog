+++
date = '2026-05-13T16:16:50+09:00'
title = 'Linux [03]: File'
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

# Contents

- [0.1.]() 

---

# Section 0.1.

**File is ...**
File is 전통적으로는 정보를 저장하는 most basic unit, 이때에는 단순히 data, program 등을 file로 생각한다. 그러나, modern os의 관점에서 file은 abstract object로 read and write라는 unified interface로 단순 data or program을 넘어 hardware device까지 다루기 위한 하나의 system이 되었다. file is stored storage device and 보통의 경우 kernel은 file을 a sequence of bytes로 생각하며 실제 그 file이 무엇인지는 application이 해석하게 된다.
- traditional definition vs modern OS concepts
    - In tradition, the most basic unit for storing infomation.
        - traditional definition for user.
        - data, programs, and etc. are naturally archived as file.
    - In modern concepts, abstract object to read and write data.
        - for modern OS concepts, especially in Linux/UNIX
        - extansion of concept of file
- a sequence of `m` byte
    - no matter what it means for OS, that is only for application
- unified interface to read and write data.
    - manage manythings as file => use same system call interface like read/write/open/close to access device and data
    - Uniform View => no matter where it is stored, what it is contained, what hardware system it is, same action to call (read, write, ...)
    - use `read` function, when read data on disk or take packet on network socket as well.
    - Physical devices also can be represented as file.
        - keyboard input => stdin => read like file
        - displaying to monitor => stdout => write like file
    - e.g., echo hello > /dev/tty
        - in user's perspect, just writing at `tty`
        - in real mechanism, write()
        → VFS
        → inode 확인
        → character device file 확인
        → tty driver 호출
        → terminal hardware 출력 => `hello` not be stored in `tty`
- Typically, stored on storage devices (e.g., SSD, HDD, Even Memory)


**Type of File**
1. Ordinary File (== Regular File)
    - store text or binary data.
    - is stored on secondary storage device.
    - kernel do not distinguish what it is, only application do
    - for kernel, it is just a sequence of m bytes.

2. Directory
    - a set(array) of directory entries.
    - directory entry is mapping of file-name and inode-number.
        - <file-name, inode-number>
        directory
        [
            ("a.txt", inode 15),
            ("b.txt", inode 29),
            ("dir", inode 40)
        ]
    - inode-number (index, refference) => inode
    - inode is a structure that contains 실체 and metadata about file.
        - not have file-name, have where it is on disk, file-size, ...
        - why is not file-name contained in inode => inode is identity of file.
        - "a.txt" → inode 3512, "b.txt" → inode 3512 => hard rink
    - for integrity, only kernel can have permission to write to directory.
    - is the pointer-like that contain other file's name and infomation to find it.
    - finally, it is 특정 format의 binary data를 가진 regular-like file
    - namespace == path 구조?? tree 형태로 된?
    - using directories to hierarchically organize files 
    - directory can contain other directories
        - dir_a[ ("dir_aa", inode nn) ]
        - dir_a: parent directory of `dir_aa`
        - dir_aa: sub-directory of `dir_a`

3. Special File (== Device File)
"device file은 regular file처럼 디스크 data block에 저장되는 파일이 아니라,
filesystem namespace 안에 존재하는 special entry이다.
write/read 시 filesystem storage로 가지 않고,
kernel은 inode의 device 정보를 통해 적절한 device driver(kernel code)를 호출한다.
따라서 device file의 실질적 동작은disk-backed data가 아니라, kernel memory 내부 subsystem과 연결되어 있다."
    - abstract hardware device as file for unified interface.
    - stored(reside) in memory => disk에storing 실제 data 하지 않음
        - regular file => mapping to storage
            - block pointer => where space of storage?
        - device file => mapping to device program
            - major number, minor number => what driver?
    - character device file vs block device file
        - c => like data stream, sequential acces, stream I/O 
        - b => fixed size unit data, random access, storage I/O

4. etc.) Symbolic Link, FIFO (Named Pipe), Socket
    - Symbolic Link: has other file's path-name as data
    - FIFO: for IPC(Inter-Process Communication)
    - Socket: for network

**Text File vs. Binary File**
- Text file
    - general file with ASCII characters 
    - documents, programs, shell scripts etc.
    - human-readable form
- Binary file
    - non-text file which has data in binary form
    - computer-readable form
    - typically contains data that is meaningful only when processed by a program (e.g., executable file)
- for example
    - ~ % file ./.zshrc => ./.zshrc: ASCII text
    -  ~ % file /bin/ls
    => /bin/ls: Mach-O universal binary with 2 architectures: [x86_64:Mach-O 64-bit executable x86_64] [arm64e:Mach-O 64-bit executable arm64e]
    /bin/ls (for architecture x86_64):	Mach-O 64-bit executable x86_64
    /bin/ls (for architecture arm64e):	Mach-O 64-bit executable arm64e

**File Mode and File Permission**
```bash
#e.g.
~ % ls -l test.c
-rwxr-xr-x  1 owner-name  staff  73 May 13 12:19 test.c
```
-rwxr-xr-x: file mod representation
- **file mode**: [file type][permission bit]
    => -: file type
    => rwxr-xr-x: permission bit
- **file type**: first charcter of file mode
| Symbol | File Type | Meaning |
|---|---|---|
| `-` | regular file | 일반 파일 |
| `d` | directory | 디렉터리 |
| `c` | character device | 문자 단위로 입출력하는 장치 파일 |
| `b` | block device | 블록 단위로 입출력하는 장치 파일 |
| `l` | symbolic link | 다른 파일/디렉터리를 가리키는 링크 |
| `p` | FIFO / pipe | 프로세스 간 통신용 파이프 |
| `s` | socket | 프로세스 간 네트워크/IPC 통신용 소켓 |

- **file permission**: Which users or a group of users can access a specific file/directory.
    - permission type
        - r: read permission
        - w: write permission
        - x: execution permission
        - -: no permission assigned
    - three user-based permission groups
        - owner(or user)(u): the owner permission apply only the owner of the file/diretory
        - (owner) group(g): the group permission apply only the group that has been assigned to the file/directory
        - others(o): the others permission apply to all other users on the system
    - the first three bits are for owner, the second ones are for group, and the last ones are for others.
        - rwxrwxrwx
        - e.g., rwxr-x-wx => owner: rwx / group: r-x / others: -wx
    - Octal representations
        - Each permission groups has three permission bits
        - => Can be represented octal number.
        - e.g., rwxr-x-wx => 111 101 011 => 753
    - Execution permission
        - for regular file: execute a file.
        - for directory: view the contents of a directory.



**Absolute Path vs. Relative Path**
- Absolute Path
    - /home/${USER}/a/b/c/d
- Relative Path
    - e.g., working diretory path: /home/${USER}/a/b/c/d
    - parent diretory: c => .. 
        - b => ../..
    - current directory: d => .
    - user's home directory: /home/${USER} => ~

###**=====Linux Commands=====**

1.



---
## References
- Kangwon National University Lecture Note (course: 48400009)
- Advanced Programming in the UNIX Environment [3rd Ed] - W. Richard Stevens, Stephen A. Rago
- Computer Systems (A Programmer's Perspective) [3rd Ed] - Randal E. Bryant, David R. O’Hallaron
- Operating System Concepts [10th Ed] - Abraham Silberschatz, Greg Gagne, Peter B. Galvin

## Acknowledgements
- OpenAI ChatGPT
- Google NotebookLM