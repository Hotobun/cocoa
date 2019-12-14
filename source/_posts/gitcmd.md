---
title: git常用命令
date: 2019-12-14 18:12:52
tags: 
- git
categories:
cover: /img/gitcmd.jpg
---


git仓库理解为3个区域   
工作区 暂存区 版本库
* `$ git add file` 将文件放进暂存区 并没有提交
* `$ git commit -m "xxx"`	 commit 将暂存区的内容写进版本库
* 文件被写入版本库 实际是上面两步
* `$ git init` 创建git仓库
* `$ git add filename` 添加文件 
* `$ git commit -m "说明本次更改"` 提交事务
* `$ git status` 查看状态
* `$ git diff filename` 比较新旧文件差异
    *  --- 减号表示原来的值
	*  +++ 加号表示新增修改
* `$ git log` 查看日志
* `$ git reflog`显示你每一次命令 找到版本号 再回多次

* 版本回退：
    * reset方法：回到某一个时间轴 该版本后面的修改都丢失 向后退
        首先要找到想要回退的版本id或者前第几个版本
        `$ git reset id`将暂存区内容和该版本已提交内容恢复到未缓存状态 
        不影响工作区
        `$ git reset --soft id` 将该版本的已提交内容回滚到暂存区 不影响本地
        `$ git reset --hard id` 将该版本的已提交内容回滚到本地 不可恢复
         可选id或者HEAD~i	i为数字 意为前第几个版本  
    * revert方法：在时间轴最后加一个版本 不丢失更改 向前进
        `$ git revert -n id` 
        `$ git commit -m "massage"`
        生成一个新版本 版本号不一样 内容一样 


* 丢弃工作区的修改：
    * `$ git checkout -- filename`  
	 丢弃工作区修改 
	 恢复这个文件到最近一次commit 或者 add时的状态
	
	* `$ git reset HEAD filename` 
	 把HEAD指向版本的文件 放到工作区 HEAD默认指向最新版
