---
title: Stack-Based Buffer Overflow Linux x86
author: Sachin
date: 2019-08-08 11:33:00 +0800
categories: [BOF, Linux x86]
tags: [shellcode, BOF, ExploitDev]
math: true
mermaid: true
---
![](/assets/img/posts/bufferoverflow/bof.png)

This is a walkthrough of the HTB Academy Module for Stack-Based Buffer Overflow on Linux x86.


## Buffer Overflow Introduction:

Buffer overflows are among the most common security vulnerabilities in software applications that can be exploited over the Internet. In short, buffer overflows are caused by incorrect program code, which cannot process too large amounts of data correctly by the CPU and can, therefore, manipulate the CPU's processing.

A buffer overflow can cause the program to crash, corrupt data, or harm data structures in the program's runtime. The last of these can overwrite the specific program's `return address` with arbitrary data, allowing an attacker to execute commands with the `privileges of the process` vulnerable to the buffer overflow by passing arbitrary machine code. This code is usually intended to give us more convenient access to the system to use it for our own purposes. Such buffer overflows in common servers, and Internet worms also exploit client software.

A particularly popular target on Unix systems is root access, which gives us all permissions to access the system. However, as is often misunderstood, this does not mean that a buffer overflow that "only" leads to the privileges of a standard user is harmless. Getting the coveted root access is often much easier if you already have user privileges.

Buffer overflows, in addition to programming carelessness, are mainly made possible by computer systems based on the Von-Neumann architecture.

The most significant cause of buffer overflows is the use of programming languages that do not automatically monitor limits of memory buffer or stack to prevent (stack-based) buffer overflow. These include the `C` and `C++` languages, which emphasize performance and do not require monitoring.

For this reason, developers are forced to define such areas in the programming code themselves, which increases vulnerability many times over. These areas are often left undefined for testing purposes or due to carelessness. Even if they were used for testing purposes, they might have been overlooked at the end of the development process.
