---
layout: post
title: "MySQL Crash Course Take-Down"
modified:
categories: blog
excerpt: "MySQL Crash Course take-down."
tags: [Notes]
image:
  feature: bg\7.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/
date: 2016-07-19 23:41:27
modified: 2016-07-19 23:41:27
share: true
---

**数据库(database)**：保存有组织的数据的容器（通常是一个文件或一组文件）。

**表(table)**：某种特定类型数据的结构化清单。

**模式(schema)**：关于数据库和表的布局及特性的信息。

**列(column)**：表中的一个字段。所有表都是由一个或多个列组成的。

**数据类型(datatype)**：所容许的数据的类型。每个表列都有相应的数据类型，它限制（或容许）该列中存储的数据。

**行(row)**：表中的一个记录。

**主键(primary key)**：一列（或一组列），其值能够唯一区分表中每个行。

> 命令用;或\g结束，换句话说，仅按Enter不执行命令

**关键字(key word)**：作为MySQL语言组成部分的一个保留字。决不要用关键字命名一个表或列。

`USE crashcourse;`

> USE语句并不返回任何结果。依赖于使用的客户机，显示某种形式的通知。
