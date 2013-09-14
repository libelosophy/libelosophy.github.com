---
layout: post
title: "Ubuntu install  emacs24.3"
date: 2013-09-14 22:24
comments: true
categories:  note sh
---

Ubuntu install emacs24 from source code
----------------------------------------

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

	
	
	 
	
