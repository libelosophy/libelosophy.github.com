---
layout: post
title: "Ubuntu install &amp; use emacs24"
date: 2013-09-15 00:37
comments: true
categories: note sh emacs
---

###1. Ubuntu install emacs24 from source code

	# get source code   	
	wget http://mirrors.ustc.edu.cn/gnu/emacs/emacs-24.3.tar.xz
	
	# extract
	tar -xvf emacs-24.3.tar.xz
	cd emac-24.3

	# install x toolkit support lib and other (libtinfo is required)
	sudo apt-get install libgtk2.0-dev
	sudo apt-get install libtinfo-dev

	# configure 
	./configure --with-xpm=no --with-jpeg=no --with-gif=no --with-tiff=no

	# make 
	make 

	# Test if emacs works
	src/emacs -Q

	# install 
	sudo make install 

	# Test if install is succed
	emacs

	# clean the output
	make clean

	# save the source code 
	sudo mv emacs-24.3 /usr/local/src

###2. Basic usage

* 一般用法 CONTROL + &lt;chr> 
	两种 CONTROL ：
	+ CTRL /CTL ：Ctrl
	+ META: Meta / Edit / Alt
* 退出 编辑的session ： C-c C-x
* 下一页： C-v (View next page)
* 上一页： M-v
* 页内移动：
	1. previous : C-p 前一行
	2. next : C-n 后一行
	3. backward : C-b 前移
	4. forword : C-f 后移 中央聚焦： C-l 使光标所在处显示在屏幕中央
	5. 字移动 ：M-b 以字为为单位向后移动（中文是移到下个标点，下同） : M-f word forward

	6. C-a, C-e : 移动到行开始，行结束

	7. M-a, M-e : 移动到上一句，下一句

	8. M-< : 文字开始 Alt+ shift + ,

	9. M-> : 文字结束 Alt+ shift + .
* 重复： C-u 数字 C-&lt;chr> 例外： C-u &lt;num> C-v/M-v 是卷动 num 行，而不是 num 页

* 停止/取消数字参数/ 撤销ESC： C-g


