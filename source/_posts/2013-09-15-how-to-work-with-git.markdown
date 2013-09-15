---
layout: post
title: "How to Work with Git"
date: 2013-09-15 12:18
comments: true
categories: note git
---

如何使用GIT 
--------------------------------------------------------

*  註冊:  到 [github](https://github.com "github") 註冊一個帳號。
* 在你的github 頁面新建一個 repository

![create repo]( /images/blog/create_repo.png)

點擊中間那個帶有 + 的圖標，爲repo 取名，添加描述，確認。

假設repo 名爲*project*。 

*  安裝 git ：

+ Windows ： 下載  [msysgit](https://code.google.com/p/msysgit/downloads/list "msysgit")

+ Linux : 

  - ubuntu : 

	  sudo apt-get install git 

* git 本地操作。
	
 window 打開git-bash.bat, linux 打開終端。執行以下操作：
	
	mkdir workspace
	cd workspace
	git clone https://github.com/libelosophy/AndroidFileExplorer.git 
	cd AndroidFileExplorer
	git remote add origin https://github.com/*你的用戶名*/project.git # project 爲repo 名
	git add .
	git commit -m "提交說明，可以隨便寫“
	
	# 代碼push 到你的 github 遠程repo 上。
	git push origin master 

然後在eclipse 中導入項目，目錄選擇AndroidFileExplorer.
完成後進行開發。
	
	
