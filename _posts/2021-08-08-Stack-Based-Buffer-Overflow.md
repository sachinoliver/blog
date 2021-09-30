---
title: Stack-Based Buffer Overflow Linux x86
author: Sachin
date: 2021-08-08 11:33:00 +0800
categories: [BOF, Linux x86]
tags: [shellcode, BOF, ExploitDev]
math: true
mermaid: true
---
![](/assets/img/posts/bufferoverflow/bof.png)

> This is a walkthrough of the HTB Academy Module for Stack-Based Buffer Overflow on Linux x86.


## Buffer Overflow Introduction:

Buffer overflows are among the most common security vulnerabilities in software applications that can be exploited over the Internet. In short, buffer overflows are caused by incorrect program code, which cannot process too large amounts of data correctly by the CPU and can, therefore, manipulate the CPU's processing.

A buffer overflow can cause the program to crash, corrupt data, or harm data structures in the program's runtime. The last of these can overwrite the specific program's `return address` with arbitrary data, allowing an attacker to execute commands with the `privileges of the process` vulnerable to the buffer overflow by passing arbitrary machine code. This code is usually intended to give us more convenient access to the system to use it for our own purposes. Such buffer overflows in common servers, and Internet worms also exploit client software.

A particularly popular target on Unix systems is root access, which gives us all permissions to access the system. However, as is often misunderstood, this does not mean that a buffer overflow that "only" leads to the privileges of a standard user is harmless. Getting the coveted root access is often much easier if you already have user privileges.

Buffer overflows, in addition to programming carelessness, are mainly made possible by computer systems based on the Von-Neumann architecture.

The most significant cause of buffer overflows is the use of programming languages that do not automatically monitor limits of memory buffer or stack to prevent (stack-based) buffer overflow. These include the `C` and `C++` languages, which emphasize performance and do not require monitoring.

For this reason, developers are forced to define such areas in the programming code themselves, which increases vulnerability many times over. These areas are often left undefined for testing purposes or due to carelessness. Even if they were used for testing purposes, they might have been overlooked at the end of the development process.


## Exploit Development Introduction

Exploit development comes in the Exploitation Phase after specific software and even its versions have been identified. The Exploitation Phase goal is to use the information found and its analysis to exploit the potential ways to gain interaction and/or access to the target system.

Developing our own exploits can be very complex and requires a deep understanding of CPU operations and the software's functions that serve as our target. Many exploits are written in different programming languages. One of the most popular programming languages for this is Python because it is easy to understand and easy to write with. In this module, we will focus on basic techniques for exploit development, as a fundamental understanding must be developed before we can deal with the various security mechanisms of memory.

Before we run any exploits, we need to understand what an exploit is. An exploit is a code that causes the service to perform an operation we want by abusing the found vulnerability. Such codes often serve as proof-of-concept (POC) in our reports.

There are two types of exploits. One is unknown (0-day exploits), and the other is known (N-day exploits).

### 0-Day Exploits

An 0-day exploit is a code that exploits a newly identified vulnerability in a specific application. The vulnerability does not need to be public in the application. The danger with such exploits is that if the developers of this application are not informed about the vulnerability, they will likely persist with new updates.

### N-Day Exploits

If the vulnerability is published and informs the developers, they will still need time to write a fix to prevent them as soon as possible. When they are published, they talk about N-day exploits, counting the days between the publication of the exploit and an attack on the unpatched systems.

Also, these exploits can be divided into four different categories:

   `> Local
    > Remote
    > DoS
    > WebApp`

### Local Exploits

Local exploits / Privilege Escalation exploits can be executed when opening a file. However, the prerequisite for this is that the local software contains a security vulnerability. Often a local exploit (e.g., in a PDF document or as a macro in a Word or Excel file) first tries to exploit security holes in the program with which the file was imported to achieve a higher privilege level and thus load and execute `malicious code / shellcode` in the operating system. The actual action that the exploit performs is called `payload`.

### Remote Exploits

The remote exploits very often exploit the buffer overflow vulnerability to get the payload running on the system. This type of exploits differs from local exploits because they can be executed over the network to perform the desired operation.

### DoS Exploits

DoS (`Denial of Service`) exploits are codes that prevent other systems from functioning, i.e., cause a crash of individual software or the entire system.

### WebApp Exploits

A Web application exploit uses a vulnerability in such software. Such vulnerabilities can, for example, allow a command injection on the application itself or the underlying database.

