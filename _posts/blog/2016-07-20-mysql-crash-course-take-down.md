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
modified: 2016-07-26 00:06:59
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

`SELECT prod_name, prod_price FROM products WHERE prod_price = 2.50;`

> 这条语句从products表中检索两个列，但不返回所有行，只返回prod_price值为2.50的行。

**在同时使用ORDER BY和WHERE子句时，应该让ORDER BY位于WHERE之后，否则将会产生错误。**

`SELECT prod_name, prod_price FROM products WHERE prod_name = 'fuses';`

> 检查WHERE prod_name = 'fuses' 语句，它返回prod_name的值为Fuses的一行。MySQL在执行匹配时默认不区分大小写，所以fuses与Fuses匹配。

`SELECT prod_name, prod_price FROM products WHERE prod_price < 10;`  
`SELECT prod_name, prod_price FROM products WHERE prod_price <= 10;`

`SELECT vend_id, prod_name FROM products WHERE vend_id <> 1003;`

> 列出不是由供应商1003制造的所有产品。

> 如果仔细观察上述WHERE子句中使用的条件，会看到有的值括在单引号内（如前面使用的'fuses'），而有的值未括起来。单引号用来限定字符串。如果将值与串类型的列进行比较，则需要限定引号。用来与数值列进行比较的值不用引号。

`SELECT prod_name, prod_price FROM products WHERE prod_price BETWEEN 5 AND 10;`

> 在使用BETWEEN时，必须指定两个值，所需范围的低端值和高端值。这两个值必须用AND关键字分隔。BETWEEN匹配范围中所有的值，包括指定的开始值和结束值。

**NULL**：无值(no value)，它与字段包含0、空字符串或仅仅包含空格不同。

`SELECT cust_id FROM customers WHERE cust_email IS NULL;`

> 返回customers表中cust_email为空值的cust_id列

> 在通过过滤选择出不具有特定值的行时，你可能希望返回具有NULL值的行。但是，不行。因为未知具有特殊的含义，数据库不知道它们是否匹配，所以在匹配过滤或不匹配过滤时不返回它们。因此，在过滤数据时，一定要验证返回数据中确实给出了被过滤列具有NULL的行。

**操作符(operator)**：用来联结或改变WHERE子句中的子句的关键字。也称为逻辑操作符(logical operator)。

`SELECT prod_id, prod_price, prod_name FROM products WHERE vend_id = 1003 AND prod_price <= 10;`

> 此SQL语句检索由供应商1003制造且价格小于等于10美元的所有产品的名称和价格。AND指示DBMS只返回满足所有给定条件的行。还可以添加多个过滤条件，每添加一条就要使用一个AND。

**AND**：用在WHERE子句中的关键字，用来指示检索满足所有给定条件的行。

`SELECT prod_name, prod_price FROM products WHERE vend_id = 1002 OR vend_id = 1003;`

> 此SQL语句检索由任一个指定供应商制造的所有产品的产品名和价格。OR操作符告诉DBMS匹配任一条件而不是同时匹配两个条件。

**OR**：WHERE子句中使用的关键字，用来表示检索匹配任一给定条件的行。

**SQL（像多数语言一样）在处理OR操作符前，优先处理AND操作符。**

`SELECT prod_name, prod_price FROM products WHERE (vend_id = 1002 OR vend_id = 1003) AND prod_price >= 10;`

> 因为圆括号具有较AND或OR操作符高的计算次序，DBMS首先过滤圆括号内的OR条件。这时，SQL语句变成了*选择由供应商1002或1003制造的且价格都在10美元（含）以上的任何产品*，这正是我们所希望的。

`SELECT prod_name, prod_price FROM products WHERE vend_id IN (1002, 1003) ORDER BY prod_name;`

> 此SELECT语句检索供应商1002和1003制造的所有产品。IN操作符后跟逗号分隔的合法值清单，整个清单必须括在圆括号中。

**IN**：WHERE自居中华用来指定要匹配值的清单的关键字，功能与OR相当。

为什么要使用IN操作符？其优点具体如下。

* 在使用长的合法选项清单时，IN操作符的语法更清楚而且直观。
* 在使用IN时，计算的次序更容易管理（因为使用的操作符更少）。
* IN操作符一般比OR操作符清单执行更快。
* IN的最大优点是可以包含其他SELECT语句，使得能够更动态地建立WHERE子句。

**NOT**：WHERE子句中用来否定后跟条件的关键字。

`SELECT prod_name, prod_price FROM products WHERE vend_id NOT IN (1002,1003) ORDER BY prod_name;`

> 这里的NOT否定跟在它之后的条件，因此，MySQL不是匹配1002和1003的vend_id，而是匹配1002和1003之外供应商的vend_id。

> MySQL支持使用NOT对IN、BETWEEN和EXISTS子句取反，这与多数其他DBMS允许使用NOT对各种条件取反有很大的差别。

**通配符(wildcard)**：用来匹配值的一部分的特殊字符。

**搜索模式(search pattern)**：由字面值、通配符或两者组合构成的搜索条件。

**在搜索串中，%表示任何字符出现任意次数。**

`SELECT prod_id, prod_name FROM products WHERE prod_name LIKE 'jet%';`

> 此例子使用了搜索模式'jet%'。在执行这条语句时，将检索任意以jet起头的词。%告诉MySQL接受jet之后的任意字符，不管它有多少字符。

`SELECT prod_id, prod_name FROM products WHERE prod_name LIKE '%anvil%';`

> 搜索模式'%anvil%'表示匹配任何位置包含文本anvil的值，而不论它之前或之后出现什么字符。

**虽然似乎%通配符可以匹配任何东西，但有一个例外，即NULL。**

`SELECT prod_id, prod_name FROM products WHERE prod_name LIKE '_ ton anvil';`

> 此WHERE子句中的搜索模式给出了后面跟有文本的两个通配符。

**与%能匹配0个字符不一样，_总是匹配一个字符，不能多也不能少。**

`SELECT prod_name FROM products WHERE prod_name REGEXP '1000' ORDER BY prod_name;`

> REGEXP后所跟的东西作为正则表达式（与文字正文1000匹配的一个正则表达式）处理。

`SELECT prod_name FROM products WHERE prod_name REGEXP '.000' ORDER BY prod_name;`

> 这里使用了正则表达式.000。.是正则表达式语言中一个特殊的字符。它表示匹配任意一个字符。

* LIKE匹配整个列。如果被匹配的文本在列值中出现，LIKE将不会找到它，相应的行也不被返回（除非使用通配符）。
* REGEXP在列值内进行匹配，如果被匹配的文本在列值中出现，REGEXP将会找到它，相应的行将被返回。

> MySQL中的正则表达式匹配（自版本3.23.4后）不区分大小写（即，大写和小写都匹配）。为区分大小写，可使用BINARY关键字，如`WHERE prod_name REGEXP BINARY 'JetPack .000';`。

`SELECT prod_name FROM products WHERE prod_name REGEXP '1000|2000' ORDER BY prod_name;`

> |为正则表达式的OR操作符。它表示匹配其中之一，因此1000和2000都匹配并返回。可以给出两个以上的OR条件。

`SELECT prod_name FROM products WHERE prod_name REGEXP '[123] Ton' ORDER BY prod_name;`

> [123]定义一组字符，它的意思是匹配1或2或3。

**字符集合也可以被否定，即，它们将匹配除指定字符外的任何东西。为否定一个字符集，在集合的开始处放置一个^即可。因此，尽管[123]匹配字符1、2或3，但[^123]却匹配除这些字符外的任何东西。**

**可使用-来定义一个范围，如[0-9]。范围不限于完整的集合，[1-3]和[6-9]也是合法的范围。此外，范围不一定只是数值的，[a-z]匹配任意字母字符。**

**为了匹配特殊字符，必须用\\为前导。\\-表示查找-，\\.表示查找.。**

`SELECT vend_name FROM vendors WHERE vend_name REGEXP '\\.' ORDER BY vend_name;`

#### 空白元字符

| 元字符 | 说明 |
|:--------|--------:|
| \\f | 换页 |
| \\n | 换行 |
| \\r | 回车 |
| \\t | 制表 |
| \\v | 纵向制表 |
{: .table}