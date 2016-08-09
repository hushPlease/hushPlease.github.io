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
