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
modified: 2016-07-24 21:53:24
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

`SHOW DATABASES;`

> SHOW DATABASES;返回可用数据库的一个列表。

`SHOW TABLES;`

> SHOW TABLES;返回当前选择的数据库内可用表的列表。

`SHOW COLUMNS FROM customers;`

> SHOW COLUMNS要求给出一个表名，它对每个字段返回一行，行中包含字段名、数据类型、是否允许NULL、键信息、默认值以及其他信息（如某字段的auto_increment）。

> MySQL支持用DESCRIBE作为SHOW COLUMNS FROM的一种快捷方式。

`SELECT prod_name FROM products;`

> 上述语句利用SELECT语句从products表中检索一个名为prod_name的列。所需的列名在SELECT关键字之后给出，FROM关键字指出从其中检索数据的表名。

> 多条SQL语句必须以分号(;)分隔。

> SQL语句不区分大小写。许多SQL开发人员喜欢对所有SQL关键字使用大写，而对所有列和表名使用小写，这样做使代码更易于阅读和调试。

`SELECT prod_id, prod_name, prod_price FROM products;`

> 这条语句使用SELECT语句从表products中选择数据。在这个例子中，指定了3个列名，列名之间用逗号分隔。

`SELECT * FROM products;`

> 如果给定一个通配符(*)，则返回表中所有列。

`SELECT DISTINCT vend_id FROM products;`

> SELECT DISTINCT vend_id告诉MySQL只返回不同（唯一）的vend_id行。如果使用DISTINCT关键字，它必须直接放在列名的前面。

`SELECT prod_name FROM products LIMIT 5;`

> 此语句使用SELECT语句检索单个列。LIMIT 5指示MySQL返回不多于5行。

`SELECT prod_name FROM products LIMIT 5, 5;`

> LIMIT 5, 5指示MySQL返回从行5开始的5行。第一个数为开始位置，第二个数为要检索的行数。

> 检索出来的第一行为行0而不是行1.因此，LIMIT 1, 1将检索出第二行而不是第一行。

> LIMIT中指定要检索的行数为检索的最大行数。如果没有足够的行（例如，给出LIMIT 10, 5，但只有13行），MySQL将只返回它能返回的那么多行。

> LIMIT 3, 4的含义是从行4开始的3行还是从行3开始的4行？如前所述，它的意思是从行3开始的4行？如前所述，它的意思是从行3开始的4行，这容易把人搞糊涂。由于这个原因，MySQL 5支持LIMIT的另一种替代语法。LIMIT 4 OFFSET 3意为从行3开始取4行，就像LIMIT 3, 4一样。

`SELECT products.prod_name FROM products;`  
`SELECT products.prod_name FROM crashcourse.products;`

> 完全限定：同时使用表名和列字

**子句(clause)**：SQL语句由子句构成，有些子句是必需的，而有的是可选的。一个子句通常由一个关键字和所提供的数据组成。

`SELECT prod_name FROM products ORDER BY prod_name;`

> ORDER BY子句指示MySQL对prod_name列以字母顺序排序数据。

`SELECT prod_id, prod_price, prod_name FROM products ORDER BY prod_price, prod_name;`

> 检索三个列，并按其中两个列对结果进行排序，首先按价格，然后再按名称排序。

`SELECT prod_id, prod_price, prod_name FROM products ORDER BY prod_price DESC, prod_name;`

> 以降序排序产品（最贵的在最前面），然后再对产品名排序

> DESC关键字只应用到直接位于其前面的列名。如果想在多个列上进行降序排序，必须对每个列指定DESC关键字。

> 与DESC相反的关键字是ASC(ASCENDING)，在升序排序时可以指定它。但实际上，ASC没有多大用处，因为升序是默认的（如果既不制定ASC也不指定DESC，则假定为ASC）。

**使用ORDER BY和LIMIT的组合，能够找出一个列中最高或最低的值。**

`SELECT prod_price FROM products ORDER BY prod_price DESC LIMIT 1;`

> prod_price DESC 保证行是按照由最昂贵到最便宜检索的，而LIMIT 1告诉MySQL仅返回一行。