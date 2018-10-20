---
layout:     post
title:      GiT的基本认识
subtitle:   git
date:       2018-3-31
author:     Peng
header-img: img/post-bg-2015.jpg
keywords_post:  "git,版本管理"
catalog: true
tags:
    - git
---

#### 一.GIT简介
1比较CVS或SVN（弥补了CVS的不足），SVN最大的好处是解决了冲突，但是必须通过网络操作  
2.在整个SVN过程中，如果要将开发者的代码保存到服务器上，必须保证SVN可以正常使用  
3.有可能存在这么一种情况：有一个软件的开发项目，需要进行一个一个版本开发，需要回退到某一个版本时，需要从服务器进行恢复操作  
4.git工具的优势是可以使用分支进行版本控制问题，而且是一个免费软件
![image](FCAF7879E8C143028478687335FA00E8)
#### 二.安装GIT
1.官方下载页面：[https://www.git-scm.com/](https://www.git-scm.com/)  
2.在windows命令行下进行GIT操作  
![image](E6691D6B06B644C9BAD85BABCD70ADC5)

#### 三.GIT简单的命令行
1.设置开发者的姓名和邮箱
```
<!--可以进行全局信息设置    
如果想要协作开发,必须要存在开发者的环境配置-->
git config --global user.name 'pengelite'
git config --global user.email '537083337@qq.com'
```  
2.取得全部的全局信息
```
git config --list
git config -l
```
此时会返回git的全局信息

```
core.symlinks=false
core.autocrlf=true
core.fscache=true
color.diff=auto
color.status=auto
color.branch=auto
color.interactive=true
help.format=html
rebase.autosquash=true
http.sslcainfo=C:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt
http.sslbackend=openssl
diff.astextplain.textconv=astextplain
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
credential.helper=manager
user.name='pengelite'
user.email='537083337@qq.com'
```

#### 四.创建仓库
```
1.创建目录:
E:\>md e:\gitpro
2.进入该目录
cd gitpro
3.初始化仓库:
方法一:git init 
提示信息Initialized empty Git repository in E:/.git/,会生成一个隐藏文件夹
方法二:git init --bare
可以发现此目录中不在生成".git"的隐藏目录,而同时E:\gitpro将保存所有配置信息
```
#### 五.软件的版本控制操作
在GIT之中,可以监控的而范围就是仓库信息(e:\gitpro就是一个仓库),那么在这个仓库里编写代码就可以了.  
1.编写一串代码

```
命令:E:\gitpro>git status
提示信息:
No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        Area.java

nothing added to commit but untracked files present (use "git add" to track)
```
2.添加文件到暂存区中
```
<!--GIT发现仓库之中增加或者修改了文件,就需要提交到GIT的文件管理系统-->
//命令
git add Area.java
//提示信息
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   Area.java

```
此时GIT就知道了当前目录中有一个需要使用的新文件:Hello.java    

3.将文件提交到版本库中并添加注释信息  

```
git commit -m"Create New File Area.java"
提示信息:[master (root-commit) ddc706c] Create New File Area.java
 1 file changed, 40 insertions(+)
 create mode 100644 Area.java
```

 4.同时提交多个新文件时

```
E:\gitpro>git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        "Area - \345\211\257\346\234\254 (2).java"
        "Area - \345\211\257\346\234\254.java"

nothing added to commit but untracked files present (use "git add" to track)
```
git add .


```
E:\gitpro>git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   "Area - \345\211\257\346\234\254 (2).java"
        new file:   "Area - \345\211\257\346\234\254.java"
```
5.进行版本库的提交  
范例:
git commit -m "Add To Files"

```
[master 1f6123e] Add To Files
 2 files changed, 80 insertions(+)
 create mode 100644 "Area - \345\211\257\346\234\254 (2).java"
 create mode 100644 "Area - \345\211\257\346\234\254.java"
```

自动add并修改到版本库中
当文件产生修改时,查询状态后直接将修改后的文件提交到版本库  
不区分版本库和暂存库
```
git commit -a -m "Change Emp.java File"
```

#### 六.修改仓库文件 
    如果针对仓库文件进行修改的话,修改了文件中的内容,此时如果比较前后文件的改变
    
```
git diff Area1.java
```
此时会看到前后文件的差异,用+代表增加的代码,-代表减去的代码.此时可以用Q退出.使用这个工具可以帮助用户进行代码修改前后的区分.但是修改完的代码最终依然需要将其进行提交.
git commit -a -m "In Area.java File Add Two Statement"
那么到此时为止已经出现了很多次提交,查看提交历史
git log Area1.java
提醒信息:注意commitId

```
commit b26a162e79efb7eb0771f31e4c2ae88d335d3b43 (HEAD -> master)
Author: pengelite <537083337@qq.com>
Date:   Wed Sep 5 20:18:15 2018 +0800

    In Area.java File Add Two Statement

commit 06e4abf859bd30f12e7bdcaf56a6471ad3c5dcd1
Author: pengelite <537083337@qq.com>
Date:   Wed Sep 5 18:07:14 2018 +0800

    Change Emp.java File

commit 6ce7e838a187b9420d04b326af651069a60b6bd2
Author: pengelite <537083337@qq.com>
Date:   Wed Sep 5 17:57:37 2018 +0800
```
#### 七.认识工作区,暂存区,版本库(仓库) 
工作区是整个GIT之中对于文件操作一共提供三个区域:  
工作区(用户所编写的代码文件夹):所有的文件操作都以工作区为主  
GIT仓库:  
|-暂存库:只是将工作区中的未保存文件保存到暂存区中,此部分由GIT维护  
|-版本库:真正进行项目发布的代码  
首先用户要在工作区之中编写所需要的程序文件,但是此时的文件并不能真正的保存在GIT的仓库之中,但是在这一个区域中所进行的文件的创建 修改 删除等操作并不会影响到最终的软件版本发布;就好比是一个临时区域.将这个临时区域的内容保存到最终发布的软件版本中,就需要首先将其加到暂存区(此时没有发布到版本库中表示可以撤销)
###### 1.工作区的操作  
![image](1B2D3959CEB94B47A340FA241CC6B951)
###### 2.加入暂存区的操作,工作区中的新文件被删除  
![image](3D75192EC66F49F3B44B465D9679327A)  
###### 3.暂存区
暂存区里的内容只能说是暂时需要的,那么可能也需要被删除掉.项目在Master分支上(版本库),才能够被其他人所使用.
###### 4.commit ID
由于一个项目可能会被发布多次,所以在GIT里面进行了保存之中,都回生成一个commit ID,用于版本回退
#### 八.操作步骤 
###### 1.修改Hello.java文件
现在的文件内容在工作区中给修改,这个文件不能真正的在项目中被使用,现在工作区的状态就发生了变化。
    此时输入命令
    
```
git status
```
返回提示信息  
![image](5C55140668F0443A81A4BF065D2FD902)
###### 2.此时进行暂存区的保存

```
git add .
```
保存完成之后  
![image](E911B0DBD2D04638BDA2EDF3925CCBD5)  
git reset HEAD
暂存区的代码只代表暂时不改动，仍然可以恢复
###### 3.此时再次修改文件，没有使用add命令，修改的时工作区域的代码
![image](A347CBA72F364090BFAFB86055B7FE1F)  
此时出现两行提示，暂存区的文件还没有发布到分支上，工作区的文件也同时发生了变化。  
如果此时提交项目到版本库中（Master分支中），工作区的修改不被提交，查询工作区中的内容不被受到影响。  

```
git commit -m "Commit Work Dir File"
```

![image](F5128F1569204B91B23140D54EFD59F9)  


#### 八.版本穿越

GIT中最强大的操作就在于可以进行版本的回退以及签禁状态下的切换。再任何的开发之中，对于软件的操作代码都很难保证其不恢复到原始状态。因为新增加的程序可能会因为某些原因，从而导致失败，此时必须要能够进行快速的版本恢复。
GIT进行版本穿越的核心概念在于CommitID

```
git log

或者
 git log --pretty=oneline
```
git 有一个head指针，head指的是当前最新的版本号
修改HEAD到历史版本号，就回退到了之前的版本号
git reset --hard HEAD~1
![image](388B7D3073FA4470A3376752E73B9615)  
回滚，需要查找提交点的位置。只能删除提交点的日志
git reflog
找到版本号
git reset --hard ddc706c

#### 九.撤销修改

######   情况I：在工作区中发生了改变，但是现在没有提交到暂存区  
恢复原来的代码，可以使用checkout操作  
（1）首先使用git status查看当前状态
    git status 会提示文件已经被修改
    给出了一个参考命令，这是需要重新检出已有的代码，则需要使用git checkout Hello.java进行恢复
    
 
```
git checkout Hello.java
```
只要执行完了这两条语句，就会表现当前的状态已经恢复
    
######   情况二：已经添加到了暂存区，但是没有提交到Master分支
    
1.将保存到暂存区

```
git add .
```

将保存在暂存区中的Hell.java恢复到工作区中

```
git reset HEAD Hello.java
```


```
git status
```

这个状态已经改了两个文件，hello由暂存区被推送到了工作区里
对于几个区域的操作：

```
工作区——>暂存区：   git add
暂存区——>Master分支 git commit
暂存区——>工作区：git reset HEAD 文件
```

#### 十.文件删除
删除工作区中的内容。删除Hello.java文件

```
del Hello.java
```
    随后查询当前的状态
    


此时已经检查到了hello.java文件已经被删除了。MASTER分支上依然有Hello.java文件，所以必须进行更新提交

```
git commit -a -m "Delete Hello.java File"
```
此时Master分支上面的文件被删了。只要此时更新一旦提交，就表示不存在了。如果此时开发者认为Hello.java文件删除错了，此时可以进行恢复。

在工作区中把文件删了，master分支上依然存在hello.java文件
```
git reset checkout -- Hello.java
```
两种情况
工作区的删除可以利用checkout重新检出，master分支上的删除必须
利用版本穿越来进行


