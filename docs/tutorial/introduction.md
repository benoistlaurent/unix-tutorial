---
---

# Introduction

## What is the shell?

The shell is a program which purpose is to run other programs.
The most popular unix shell is Bash, but zsh, csh and tcsh are still often
installed on machines.

## Anatomy of a command

A command is composed of the **program**'s name and optionnaly it's **arguments**.
There are some special arguments called **options** or **flags** which starts
with `-` or ``--``.

Example:

![image]({{ site.url }}/unix_tutorial/assets/img/tutorial/command_example.001.jpeg)


## Special names

There are some special names which can be used in name
and place of files and directories.

- `.` current directory 
- `..` parent directory
- `*` all files and directories

## Getting help

### From the `man`

Probably the most important unix command is `man`, which provides a command's
manual.

Example:

```bash
man ls
```

```bash
LS(1)                                                                      User Commands                                                                     LS(1)



NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List information about the FILEs (the current directory by default).  Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

       Mandatory arguments to long options are mandatory for short options too.

       -a, --all
              do not ignore entries starting with .

       -A, --almost-all
              do not list implied . and ..
# [...]
```

Importantly, you can seach in the manual by typing `/` followed by the keyword
you're looking for.

### From the `--help` option

Most unix programs will have a `-h/--help` option which provides help
in a more of less long format.

Example:

```bash
$ ls --help                                                                                                                                                               [15:38:21]
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
      --author               with -l, print the author of each file
  -b, --escape               print C-style escapes for nongraphic characters
      --block-size=SIZE      scale sizes by SIZE before printing them; e.g.
# [...]
```

### From the Internet

It's essential to get into the habit of asking to the Internet.
Typing the right keywords in a search engine very often goes a long way, as
many problems have been encountered by many users and reported many times.
Hence, it is often very fast to get answers to problems, even some that can be
quite tricky to solve.
