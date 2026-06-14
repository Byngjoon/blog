+++
date = '2026-06-12T23:40:44+09:00'
title = '[UNIX/Linux] [02]: Basic Commands'
description = ""
categories = [""]
tags = ["UNIX/Linux"]
slug = ""
math = true
draft = false
+++

# Chapter 02. UNIX/Linux Basic Commands

> **Outline:**

---

# Contents

- [0.1.]() 

---

# Section 2.1.
Basic Commands

- 'date' : to check the date and time
- 'who' : to verify who is currently logged in
- 'ls' : to list directories and files
- 'cat', 'more' : to view file contents
- 'passwd' : to modify password information
- 'last' : to see login history
- 'man' : to see the manual for commands
- 'info' : to see information for commands
- 'which' : to determine the location of commands
- 'hostname' : to check hostname
- 'uname' : to check system information


- `date`: Checking the date and time
	- date -u

```bash
~$ date
Thu Jun 11 12:29:17 KST 2026
~$ date -u
Thu Jun 11 03:29:20 UTC 2026
```

- `who`: Veryfing who is currently logged in
mac
```bash
~$ who
user-name     console      May 18 23:51 
user-name     ttys000      Jun 11 12:08 
user-name     ttys001      Jun 11 12:28 
```
ubuntu
```bash
~$ who
user-name pts/0        2026-06-11 12:35 
```

- `ls`: Listing directories and files
```
~$ ls
HW#6  linux-5.11.3  linux-5.11.3.tar.xz  proj  snap  syscall.c  test01
```
    - -l

- `cat`: Viewing file contents
```bash
~/linux-5.11.3/lib$ cat plist.c
// SPDX-License-Identifier: GPL-2.0-or-later
/*
 * lib/plist.c
 *
 * Descending-priority-sorted double-linked list
 *
 * (C) 2002-2003 Intel Corp
 * Inaky Perez-Gonzalez <inaky.perez-gonzalez@intel.com>.
 *
 * 2001-2005 (c) MontaVista Software, Inc.
 * Daniel Walker <dwalker@mvista.com>
 *
 * (C) 2005 Thomas Gleixner <tglx@linutronix.de>
 *
 * Simplifications of the original code by
 * Oleg Nesterov <oleg@tv-sign.ru>
 *
 * Based on simple lists (include/linux/list.h).
 *
 * This file contains the add / del functions which are considered to
 * be too large to inline. See include/linux/plist.h for further
 * information.
 */

#include <linux/bug.h>
#include <linux/plist.h>

#중략...


module_init(plist_test);

#endif
~/linux-5.11.3/lib$
```


- `more`: Viewing file contents
```bash
~/linux-5.11.3/lib$ more plist.c
// SPDX-License-Identifier: GPL-2.0-or-later
/*
 * lib/plist.c
 *
 * Descending-priority-sorted double-linked list
 *
 * (C) 2002-2003 Intel Corp
 * Inaky Perez-Gonzalez <inaky.perez-gonzalez@intel.com>.
 *
 * 2001-2005 (c) MontaVista Software, Inc.
 * Daniel Walker <dwalker@mvista.com>
 *
 * (C) 2005 Thomas Gleixner <tglx@linutronix.de>
 *
 * Simplifications of the original code by
 * Oleg Nesterov <oleg@tv-sign.ru>
 *
 * Based on simple lists (include/linux/list.h).
 *
 * This file contains the add / del functions which are considered to
 * be too large to inline. See include/linux/plist.h for further
 * information.
 */

#include <linux/bug.h>
#include <linux/plist.h>

#ifdef CONFIG_DEBUG_PLIST

static struct plist_head test_head;
--More--(12%)
```
    - cat: 너무 길면 잘림
    - more: 페이지를 넘어가며 볼 수 있다 전체를

- passwd
	- Changing your password
	- A general guideline, passwords should consist of at least 6 characters including one or more characters from each of the following sets
		- combinations between upper and lower case alphabets
		- digit 0 thru 9
		- special characters (e.g., !@#$%^&*)
```bash
~$ passwd
Changing password for user-name.
Current password: 
New password: 
Retype new password: 
passwd: password updated successfully
```

- login history (last)
```bash
~$ last
agaporni pts/0        222.237.147.59   Fri Jun 12 23:10   still logged in
agaporni pts/0        172.30.1.254     Fri Jun 12 17:49 - 18:13  (00:23)
agaporni pts/0        210.110.128.77   Thu Jun 11 12:42 - 15:10  (02:28)
agaporni pts/0        210.110.128.77   Thu Jun 11 12:35 - 12:42  (00:07)
reboot   system boot  6.17.0-35-generi Mon Jun  8 05:00   still running
reboot   system boot  6.17.0-29-generi Mon Jun  1 05:00 - 05:00 (6+23:59)
#중략
```
    - You can use with `more` `last | more`


- Manual for a command ('man')
```bash
LAST(1)                                 User Commands                                LAST(1)

NAME
       last, lastb - show a listing of last logged in users

SYNOPSIS
       last [options] [username...] [tty...]

       lastb [options] [username...] [tty...]

DESCRIPTION
       last searches back through the /var/log/wtmp file (or the file designated by the -f
       option) and displays a list of all users logged in (and out) since that file was
       created. One or more usernames and/or ttys can be given, in which case last will show
       only the entries matching those arguments. Names of ttys can be abbreviated, thus
       last 0 is the same as last tty0.
#중략
```

- Information for a command ('info)'
	- similar to 'man' command
	- info ls



- Simple command information ('whatis')
- checking the location of a command ('which')
```bash
~$ which last
/usr/bin/last
```

- checking hostname('hostname' and 
```bash
~$ hostname
bolborhynchus
```

- `uname`: system informatiion
```bash
~$ uname
Linux
~$ uname -a
Linux 6.17.0-35-generic #35~24.04.1-Ubuntu SMP PREEMPT_DYNAMIC Tue May 26 19:30:42 UTC 2 x86_64 x86_64 x86_64 GNU/Linux
```

wc
wc < log
1 7 37
line count   word count   byte count
1            7            37




---
## References
- Kangwon National University Lecture Note (course: 48400009)
- Advanced Programming in the UNIX Environment [3rd Ed] - W. Richard Stevens, Stephen A. Rago
- Computer Systems (A Programmer's Perspective) [3rd Ed] - Randal E. Bryant, David R. O’Hallaron
- Operating System Concepts [10th Ed] - Abraham Silberschatz, Greg Gagne, Peter B. Galvin

## Environment
- Ubuntu 24.04.3 LTS
- Linux Kernel 6.17.0-35-generic
- x86_64 Architecture
- GNU bash, version 5.2.21

## Acknowledgements
- OpenAI ChatGPT
- Google NotebookLM
