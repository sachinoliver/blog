---
title: Stack-Based Buffer Overflow Linux x86
author: Sachin
date: 2019-08-08 11:33:00 +0800
categories: [BOF, Linux x86]
tags: [shellcode, BOF, ExploitDev]
math: true
mermaid: true
image:
  src: ![](/assets/img/posts/bufferoverflow/LinuxBOF.jpg)

  width: 850
  height: 585
---

This is a walkthrough of the HTB Academy Module for Stack-Based Buffer Overflow on Linux X86.


## Buffer Overflow Introduction:

Buffer overflows are among the most common security vulnerabilities in software applications that can be exploited over the Internet. In short, buffer overflows are caused by incorrect program code, which cannot process too large amounts of data correctly by the CPU and can, therefore, manipulate the CPU's processing.
