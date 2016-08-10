---
layout: post
title: "GitHub Take-Down"
categories: blog
excerpt: "GitHub take-down."
tags: [GitHub, Notes]
image:
  feature: bg\8.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/
date: 2016-08-09 10:45:37
modified: 
share: true
---

##### 集中型

以**Subversion**为代表的集中型,会将仓库集中存放在服务器之中,所以只存在一个仓库。这就是为什么这种版本管理系统会被称作集中型。

集中型将所有数据集中存放在服务器当中,有便于管理的优点。但是一旦开发者所处的环境不能连接服务器,就无法获取最新的源代码,开发也就几乎无法进行。服务器宕机时也是同样的道理,而且万一服务器故障导致数据消失,恐怕开发者就再也见不到最新的源代码了。

##### 分散型

以**Git**为代表的分散型,GitHub将仓库Fork给了每一个用户。Fork就是将GitHub的某个特定仓库复制到自己的账户下。Fork出的仓库与原仓库是两个不同的仓库,开发者可以随意编辑。

> GitHub中公开的代码大部分都是以Mac或Linux中的LF(Line Feed)换行。然而,由于Windows中是以CRLF(Carriage Return + Line Feed)换行的,所以在非对应的编辑器中将不能正常显示。

* 设置姓名和邮箱地址
`$ git config --global user.name "Firstname Lastname"`  
`$ git config --global user.email "your_email@example.com"`

* 提高命令输出的可读性
`$ git config --global color.ui auto`
> 将color.ui设置为auto可以让命令的输出拥有更高的可读性

`$ ssh-keygen -t rsa -C "your_email@example.com"`

**`id_rsa`文件是私有密钥,`id_rsa.pub`是公开密钥。**

`id_rsa.pub`的内容可以用如下方法查看:

    $ cat ~/.ssh/id_rsa.pub
    ssh-rsa 公开密钥的内容 your_email@example.com

* Add .gitignore

**该文件用来描述Git仓库中不需管理的文件与目录。**这个设定会帮我们把不需要你在Git仓库中进行版本管理的文件记录在.gitignore文件中,省去了每次根据框架进行设置的麻烦。

##### MIT许可协议

被授权人权利:被授权人有权利使用、复制、修改、合并、出版发行、散布、再授权和/或贩售软件及软件的副本,及授予被供应人同等权利,唯服从以下义务。

被授权人义务:在软件和软件的所有副本中都必须包含以上版本声明和本许可声明。

其他重要特性:此许可协议并非属copyleft的自由软件许可协议条款,允许在自由及开放源代码软件或非自由软件(proprietary software)所使用。

MIT的内容可依照程序著作权者的需求更改内容。此亦为MIT与BSD(The BSD license, 3-clause BSD license)本质上不同处。

MIT许可协议可与其他许可协议并存。另外,MIT条款也是自由软件基金会(FSF)所认可的自由软件许可协议条款,与GPL兼容。

1. 基本操作
   * git init —— 初始化仓库
   * git status —— 查看仓库的状态
   * git add —— 向暂存区中添加文件
   * git commit —— 保存仓库的历史记录
   * git log —— 查看提交日志
   * git diff —— 查看更改前后的区别
2. 分支的操作
   * git branch —— 显示分支一览表
   * git checkout -b —— 创建、切换分支
   * git merge —— 合并分支
