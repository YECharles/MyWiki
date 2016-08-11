---
title: "Git"
date: 2016-08-07 10:35
---

[TOC]

# Git #

git是一个分布式的版本控制系统和代码管理工具。`github`,`gitlab`是一个基于git的项目托管平台，它提供了web界面，你可以在上面创建资源仓库来存放你的项目。

初始化项目两种方式：

通过远程新建仓库，并克隆到本地：git clone URI，一般可用两种协议：ssh或https
    
    $ git clone -b branch URI   # 克隆指定branch到当前目录
    $ git clone -b branch URI dirc   # 克隆指定branch到指定目录dirc

通过本地新建仓库，并推送远程：

    $ cd target_dic
    $ git init
    $ git add .
    $ git commit -m "commnet"
    $ git remote add origin URI   #一般可用两种协议：ssh或https
    $ git push -u origin branch

git URI两种形式(`ssh`和`https`):

    git@github.com:YECharles/MyWiki.git
    https://github.com/YECharles/MyWiki.git

## 本地版本控制 ##

### 三个状态 ###

Working Diretory(or Untracted Files) -> Staging Area -> Repository

撤销Working Directory修改：

    $ git checkout [file | directory]

撤销Untracted Files:

    $ rm file/directory
    $ git clean -dxf

Working Diretory(or Untracted Files) to  Staging Area:

    $ git add [-A | file | directory]

Staging Area to Working Diretory(or Untracted Files):

    $ git reset HEAD [file | ]

Staging Area to Repository:

    $ git commit -m "comment"

### 版本之间 ###

回退到上一个版本，HEAD指向当前版本：

    $ git reset --hard HEAD^

回退两个版本，HEAD指向当前版本：

    $ git reset --hard HEAD^

跳转到任意版本：

    $ git reset --hard commit_id


## 分支管理 ##

新建分支：

    $ git checkout -b branch   #在当前分支基础上新建本地分支branch
    $ git checkout -b branch origin/branch   #在远程origin/branch的基础上新建对应的本地分支branch
    $ git push origin branch   #在本地分支branch基础上，在远程创建对应远程分支origin/branch

删除分支:

    $ git branch -d branch_name   #删除本地分支

合并分支，合并前确保相应的修改已提交本地版本库:

    $ git merge branch_name   #合并分支branch_name到当前分支

合并冲突：两个分支相对于分支起点（新分支创建点的版本），对同一个文件做了不同修改，此时需要手动合并。合并分支步骤：

    1. 当前分支feature开发完成，并提交到本地仓库
    2. 跳转回主分支dev(需要合并到的分支)
    3. 更新主分支dev到最新状态: git pull origin dev
    4. 合并分支feature到主分支dev: git merge feature
    5. 如有冲突，需手动解决
    6. 推送最总版本到远程分支: git push origin dev


## 远程仓库 ##

远程库是软件发布的主要库，多人协作后最红将最终版本推送到远程库，由远程库管理员进行review和发布

远程库和本地库对应关系：branch->origin/branch->origin branch

    branch: 本地版本库
    origin/branch指向本地和远程上一次交互的版本(本地库），并非真正远程库
    origin branch: 远程版本库

git pull可分为以下两步：

    git fetch: 从远程库拉代码，origin/branch指向最新版本
    git merge: 合并origin/branch指向的版本与当前最新的版本

git puch:向远程推送版本,origin/branch会指向最新推送的版本


## Others ##

### 常用命令###
    $ git status
    $ git diff
    $ git log   # 当前分支的log
    $ git log file   # 涉及到当前文件的log
    $ git show commit_id 


## Reference ##

* [Pro Git](https://git-scm.com/book/zh/v2)
* [廖雪峰](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)


