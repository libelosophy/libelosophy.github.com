---
layout: post
title: "Unix programming "
date: 2013-09-19 10:00
comments: true
categories: unix 
---


## 书籍
* Adcanced Progamming in the UNIX Environment (Second Edition) --W.Richard Stevens , Stephen A. Rago

* Advanced UNIX Programming (Second Edition)  --Marc J. Rochking 

* Linux 程序员手册 通过 man 命令可查看

## UNIX 高级环境编程的内容

A.  系统调用接口

B. (标准C)库函数


两本书中,有一本只准备讲系统调用,而故意忽略标准Ｃ库函数.那么系统掉调用和库函数的区别在哪儿呢?

 + 各种版本的UNIX 实现都提供了定义明确、数量有限、可直接进入内核的入口点。这些入口点就称为系统调用（System Call）
 + UNIX  为每个系统调用在标准Ｃ库中设置一个具有同样名字的函数，这些函数可能会调用一个或多个系统调用。
 + 系统调用会产生两次模式切换（用户--内核，内核拥有最高级别权限）,但是不一定会产生上下文切换[?wiki](http://en.wikipedia.org/wiki/System_call#Processor_mode_and_context_switching "进程模型和上下文切换")
 + 而库函数调用[本身不会产生模式切换](http://en.wikipedia.org/wiki/System_call#The_library_as_an_intermediary "系统调用作为中介"),因为它工作在用户模式.不过如果该库函数调用系统调用,则会产生.
 + 系统调用通常提供一种最小接口,而库函数通常提供比较复杂的功能.
 + POSIX 标准中包含 ISO C.
 + 几个例子说明系统调用和库函数的区别:(UNIX高级环境编程)
	1. malloc 存储器分配函数调用了 sbrk 系统调用实现了一种特定的存储分配方式,不过你也可以用 sbrk 实现其他的存储分配方式
	2. UNIX 系统只提供一个获取时间的系统调用,该系统调用返回国际标准时间 1970.1.1 零点以来经过的所有秒数,而各种库函数则可以对这个数值进行各种解释,如转换为人类可读的形式,或者夏時制算法等等.


##unix 标准化

*  ISO C

ISO: International Organizaition for Standardization 国际标准化组

提供Ｃ 程序的可移植性,使其适合于大量不同操作系统
定义了Ｃ 程序语言的设计语法和语义 及 其标准库

*  IEEE POSIX

IEEE : Institute of Electrical and Electronics Engineers 电子与电气工程师协会

POSIX: Portable Operating System Interface 可移植操作系统接口 X表示对ＵＮＩＸ API 的传承

提高应用程序在各ＵＮＩＸ 系统环境之间的可移植性. 
定义了遵从ＰＯＳＩＸ 的操作系统所必须提供的各种服务.

* Single UNIX Specification
单一UNIX 规范 ,是POSIX.1 标准的一个超集. 亦称(XSI) X/Open System Interface

## UNIX 基础之 文件系统
文件:
	* 常规文件
	* 目录
	* 符号连接
	* 特殊文件
	* 命名管道(FIFO)
	* 套接字文件(socket)


## 文件 I/O (不带缓冲的I/O)

不带缓冲: 每个read 和 write 都调用内核中的一个系统调用

* 内容:
	+ open
	+ create
	+ close
	+ lseek
	+ read
	+ write
	+ dup dup2
	+ sync fsync fdatasync
	+ fcntl
	+ ioctl
	
