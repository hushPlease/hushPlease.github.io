---
layout: post
title: "MySQL Crash Course Take-Down"
modified:
categories: blog
excerpt: "MySQL Crash Course take-down."
tags: [MySQL, Notes]
image:
  feature: bg\7.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/
date: 2016-07-19 23:41:27
modified: 2016-07-27 11:54:56
share: true
---

**数据库(database)**：保存有组织的数据的容器(通常是一个文件或一组文件)。

**表(table)**：某种特定类型数据的结构化清单。

**模式(schema)**：关于数据库和表的布局及特性的信息。

**列(column)**：表中的一个字段。所有表都是由一个或多个列组成的。

**数据类型(datatype)**：所容许的数据的类型。每个表列都有相应的数据类型，它限制(或容许)该列中存储的数据。

**行(row)**：表中的一个记录。

**主键(primary key)**：一列(或一组列)，其值能够唯一区分表中每个行。

> 命令用`;`或`\g`结束，换句话说，仅按Enter不执行命令

**关键字(key word)**：作为MySQL语言组成部分的一个保留字。决不要用关键字命名一个表或列。

`USE crashcourse;`

> `USE`语句并不返回任何结果。依赖于使用的客户机，显示某种形式的通知。

`SHOW DATABASES;`

> 返回可用数据库的一个列表。

`SHOW TABLES;`

> 返回当前选择的数据库内可用表的列表。

`SHOW COLUMNS FROM customers;`

> `SHOW COLUMNS`要求给出一个表名，它对每个字段返回一行，行中包含字段名、数据类型、是否允许NULL、键信息、默认值以及其他信息(如某字段的`auto_increment`)。

> MySQL支持用`DESCRIBE`作为`SHOW COLUMNS FROM`的一种快捷方式。

`SELECT prod_name FROM products;`

> 上述语句利用`SELECT`语句从products表中检索一个名为prod_name的列。所需的列名在`SELECT`关键字之后给出，`FROM`关键字指出从其中检索数据的表名。

> 多条SQL语句必须以分号`;`分隔。

> SQL语句不区分大小写。许多SQL开发人员喜欢对所有SQL关键字使用大写，而对所有列和表名使用小写，这样做使代码更易于阅读和调试。

`SELECT prod_id, prod_name, prod_price FROM products;`

> 这条语句使用`SELECT`语句从表products中选择数据。在这个例子中，指定了3个列名，列名之间用逗号分隔。

`SELECT * FROM products;`

> 如果给定一个通配符`*`，则返回表中所有列。

`SELECT DISTINCT vend_id FROM products;`

> `SELECT DISTINCT vend_id`告诉MySQL只返回不同(唯一)的vend_id行。如果使用`DISTINCT`关键字，它必须直接放在列名的前面。

`SELECT prod_name FROM products LIMIT 5;`

> 此语句使用`SELECT`语句检索单个列。`LIMIT 5`指示MySQL返回不多于5行。

`SELECT prod_name FROM products LIMIT 5, 5;`

> `LIMIT 5, 5`指示MySQL返回从行5开始的5行。第一个数为开始位置，第二个数为要检索的行数。

> 检索出来的第一行为行0而不是行1.因此，`LIMIT 1, 1`将检索出第二行而不是第一行。

> `LIMIT`中指定要检索的行数为检索的最大行数。如果没有足够的行(例如，给出`LIMIT 10, 5`，但只有13行)，MySQL将只返回它能返回的那么多行。

> `LIMIT 3, 4`的含义是从行4开始的3行还是从行3开始的4行？如前所述，它的意思是从行3开始的4行，这容易把人搞糊涂。由于这个原因，MySQL 5支持`LIMIT`的另一种替代语法。`LIMIT 4 OFFSET 3`意为从行3开始取4行，就像`LIMIT 3, 4`一样。

`SELECT products.prod_name FROM products;`  
`SELECT products.prod_name FROM crashcourse.products;`

> 完全限定：同时使用表名和列字

**子句(clause)**：SQL语句由子句构成，有些子句是必需的，而有的是可选的。一个子句通常由一个关键字和所提供的数据组成。

`SELECT prod_name FROM products ORDER BY prod_name;`

> `ORDER BY`子句指示MySQL对prod_name列以字母顺序排序数据。

`SELECT prod_id, prod_price, prod_name FROM products ORDER BY prod_price, prod_name;`

> 检索三个列，并按其中两个列对结果进行排序，首先按价格，然后再按名称排序。

`SELECT prod_id, prod_price, prod_name FROM products ORDER BY prod_price DESC, prod_name;`

> 以降序排序产品(最贵的在最前面)，然后再对产品名排序

> `DESC`关键字只应用到直接位于其前面的列名。如果想在多个列上进行降序排序，必须对每个列指定`DESC`关键字。

> 与`DESC`相反的关键字是`ASC`(ASCENDING)，在升序排序时可以指定它。但实际上，`ASC`没有多大用处，因为升序是默认的(如果既不指定`ASC`也不指定`DESC`，则假定为`ASC`)。

**使用`ORDER BY`和`LIMIT`的组合，能够找出一个列中最高或最低的值。**

`SELECT prod_price FROM products ORDER BY prod_price DESC LIMIT 1;`

> `prod_price DESC` 保证行是按照由最昂贵到最便宜检索的，而`LIMIT 1`告诉MySQL仅返回一行。

`SELECT prod_name, prod_price FROM products WHERE prod_price = 2.50;`

> 这条语句从products表中检索两个列，但不返回所有行，只返回prod_price值为2.50的行。

**在同时使用`ORDER BY`和`WHERE`子句时，应该让`ORDER BY`位于`WHERE`之后，否则将会产生错误。**

`SELECT prod_name, prod_price FROM products WHERE prod_name = 'fuses';`

> 检查`WHERE prod_name = 'fuses'`语句，它返回prod_name的值为Fuses的一行。MySQL在执行匹配时默认不区分大小写，所以fuses与Fuses匹配。

`SELECT prod_name, prod_price FROM products WHERE prod_price < 10;`  
`SELECT prod_name, prod_price FROM products WHERE prod_price <= 10;`

`SELECT vend_id, prod_name FROM products WHERE vend_id <> 1003;`

> 列出不是由供应商1003制造的所有产品。

> 如果仔细观察上述`WHERE`子句中使用的条件，会看到有的值括在单引号内(如前面使用的'fuses')，而有的值未括起来。单引号用来限定字符串。如果将值与串类型的列进行比较，则需要限定引号。用来与数值列进行比较的值不用引号。

`SELECT prod_name, prod_price FROM products WHERE prod_price BETWEEN 5 AND 10;`

> 在使用`BETWEEN`时，必须指定两个值，所需范围的低端值和高端值。这两个值必须用`AND`关键字分隔。`BETWEEN`匹配范围中所有的值，包括指定的开始值和结束值。

**NULL**：无值(no value)，它与字段包含0、空字符串或仅仅包含空格不同。

`SELECT cust_id FROM customers WHERE cust_email IS NULL;`

> 返回customers表中cust_email为空值的cust_id列

> 在通过过滤选择出不具有特定值的行时，你可能希望返回具有NULL值的行。但是，不行。因为未知具有特殊的含义，数据库不知道它们是否匹配，所以在匹配过滤或不匹配过滤时不返回它们。因此，在过滤数据时，一定要验证返回数据中确实给出了被过滤列具有NULL的行。

**操作符(operator)**：用来联结或改变`WHERE`子句中的子句的关键字。也称为逻辑操作符(logical operator)。

`SELECT prod_id, prod_price, prod_name FROM products WHERE vend_id = 1003 AND prod_price <= 10;`

> 此SQL语句检索由供应商1003制造且价格小于等于10美元的所有产品的名称和价格。`AND`指示DBMS只返回满足所有给定条件的行。还可以添加多个过滤条件，每添加一条就要使用一个`AND`。

**AND**：用在`WHERE`子句中的关键字，用来指示检索满足所有给定条件的行。

`SELECT prod_name, prod_price FROM products WHERE vend_id = 1002 OR vend_id = 1003;`

> 此SQL语句检索由任一个指定供应商制造的所有产品的产品名和价格。`OR`操作符告诉DBMS匹配任一条件而不是同时匹配两个条件。

**OR**：`WHERE`子句中使用的关键字，用来表示检索匹配任一给定条件的行。

**SQL(像多数语言一样)在处理`OR`操作符前，优先处理`AND`操作符。**

`SELECT prod_name, prod_price FROM products WHERE (vend_id = 1002 OR vend_id = 1003) AND prod_price >= 10;`

> 因为圆括号具有较`AND`或`OR`操作符高的计算次序，DBMS首先过滤圆括号内的`OR`条件。这时，SQL语句变成了选择由供应商1002或1003制造的且价格都在10美元(含)以上的任何产品，这正是我们所希望的。

`SELECT prod_name, prod_price FROM products WHERE vend_id IN (1002, 1003) ORDER BY prod_name;`

> 此`SELECT`语句检索供应商1002和1003制造的所有产品。`IN`操作符后跟逗号分隔的合法值清单，整个清单必须括在圆括号中。

**IN**：`WHERE`子句中用来指定要匹配值的清单的关键字，功能与`OR`相当。

为什么要使用`IN`操作符？其优点具体如下。

* 在使用长的合法选项清单时，`IN`操作符的语法更清楚而且直观。
* 在使用`IN`时，计算的次序更容易管理(因为使用的操作符更少)。
* `IN`操作符一般比`OR`操作符清单执行更快。
* `IN`的最大优点是可以包含其他`SELECT`语句，使得能够更动态地建立`WHERE`子句。

**NOT**：`WHERE`子句中用来否定后跟条件的关键字。

`SELECT prod_name, prod_price FROM products WHERE vend_id NOT IN (1002,1003) ORDER BY prod_name;`

> 这里的`NOT`否定跟在它之后的条件，因此，MySQL不是匹配1002和1003的vend_id，而是匹配1002和1003之外供应商的vend_id。

> MySQL支持使用`NOT`对`IN`、`BETWEEN`和`EXISTS`子句取反，这与多数其他DBMS允许使用`NOT`对各种条件取反有很大的差别。

**通配符(wildcard)**：用来匹配值的一部分的特殊字符。

**搜索模式(search pattern)**：由字面值、通配符或两者组合构成的搜索条件。

**在搜索串中，`%`表示任何字符出现任意次数。**

`SELECT prod_id, prod_name FROM products WHERE prod_name LIKE 'jet%';`

> 此例子使用了搜索模式`'jet%'`。在执行这条语句时，将检索任意以jet起头的词。`%`告诉MySQL接受jet之后的任意字符，不管它有多少字符。

`SELECT prod_id, prod_name FROM products WHERE prod_name LIKE '%anvil%';`

> 搜索模式`'%anvil%'`表示匹配任何位置包含文本anvil的值，而不论它之前或之后出现什么字符。

**虽然似乎`%`通配符可以匹配任何东西，但有一个例外，即NULL。**

`SELECT prod_id, prod_name FROM products WHERE prod_name LIKE '_ ton anvil';`

> 此`WHERE`子句中的搜索模式给出了后面跟有文本的两个通配符。

**与`%`能匹配0个字符不一样，`_`总是匹配一个字符，不能多也不能少。**

`SELECT prod_name FROM products WHERE prod_name REGEXP '1000' ORDER BY prod_name;`

> `REGEXP`后所跟的东西作为正则表达式(与文字正文1000匹配的一个正则表达式)处理。

`SELECT prod_name FROM products WHERE prod_name REGEXP '.000' ORDER BY prod_name;`

> 这里使用了正则表达式`.000`。`.`是正则表达式语言中一个特殊的字符。它表示匹配任意一个字符。

* `LIKE`匹配整个列。如果被匹配的文本在列值中出现，`LIKE`将不会找到它，相应的行也不被返回(除非使用通配符)。
* `REGEXP`在列值内进行匹配，如果被匹配的文本在列值中出现，`REGEXP`将会找到它，相应的行将被返回。

> MySQL中的正则表达式匹配(自版本3.23.4后)不区分大小写(即，大写和小写都匹配)。为区分大小写，可使用`BINARY`关键字，如`WHERE prod_name REGEXP BINARY 'JetPack .000';`。

`SELECT prod_name FROM products WHERE prod_name REGEXP '1000|2000' ORDER BY prod_name;`

> `|`为正则表达式的`OR`操作符。它表示匹配其中之一，因此1000和2000都匹配并返回。可以给出两个以上的`OR`条件。

`SELECT prod_name FROM products WHERE prod_name REGEXP '[123] Ton' ORDER BY prod_name;`

> `[123]`定义一组字符，它的意思是匹配1或2或3。

**字符集合也可以被否定，即，它们将匹配除指定字符外的任何东西。为否定一个字符集，在集合的开始处放置一个`^`即可。因此，尽管`[123]`匹配字符1、2或3，但`[^123]`却匹配除这些字符外的任何东西。**

**可使用`-`来定义一个范围，如`[0-9]`。范围不限于完整的集合，`[1-3]`和`[6-9]`也是合法的范围。此外，范围不一定只是数值的，`[a-z]`匹配任意字母字符。**

**为了匹配特殊字符，必须用`\\`为前导。`\\-`表示查找`-`，`\\.`表示查找`.`。**

`SELECT vend_name FROM vendors WHERE vend_name REGEXP '\\.' ORDER BY vend_name;`

| 空白元字符 | 说明 |
|:--------|--------:|
| \\\f | 换页 |
| \\\n | 换行 |
| \\\r | 回车 |
| \\\t | 制表 |
| \\\v | 纵向制表 |
{: .table}

**为了匹配反斜杠`\`字符本身，需要使用`\\\`。**

> 多数正则表达式实现使用单个反斜杠转义特殊字符，以便能使用这些字符本身。但MySQL要求两个反斜杠(MySQL自己解释一个，正则表达式库解释另一个)。

| 字符类 | 说明 |
|:--------|--------:|
| [:alnum:] | 任意字母和数字(同[a-zA-Z0-9]) |
| [:alpha:] | 任意字符(同[a-zA-Z]) |
| [:blank:] | 空格和制表(同[\\\t]) |
| [:cntrl:] | ASCⅡ控制字符(ASCⅡ 0到31和127) |
| [:digit:] | 任意数字(同[0-9]) |
| [:graph:] | 与[:print:]相同，但不包含空格 |
| [:lower:] | 任意小写字母(同[a-z]) |
| [:print:] | 任意可打印字符 |
| [:punct:] | 既不在[:alnum:]又不在[:cntrl:]中的任意字符 |
| [:space:] | 包括空格在内的任意空白字符(同[\\\f\\\n\\\r\\\t\\\v]) |
| [:upper:] | 任意大写字母(同[A-Z]) |
| [:xdigit:] | 任意十六进制数字(同[a-fA-F0-9])
{: .table}

| 重复元字符 | 说明 |
|:----------|----------:|
| * | 0个或多个匹配 |
| + | 1个或多个匹配(等于{1,}) |
| ? | 0个或1个匹配(等于{0,1}) |
| {n} | 指定数目的匹配 |
| {n,} | 不少于指定数目的匹配 |
| {n,m} | 匹配数目的范围(m不超过255) |
{: .table}

`SELECT prod_name FROM products WHERE prod_name REGEXP '\\([0-9] sticks?\\)' ORDER BY prod_name;`

> `\\(`匹配`(`，`[0-9]`匹配任意数字，`sticks?`匹配stick和sticks(s后的`?`使s可选，因为`?`匹配它前面的任何字符的0次或1次出现)，`\\)`匹配`)`。

`SELECT prod_name FROM products WHERE prod_name REGEXP '[[:digit:]]{4}' ORDER BY prod_name;`  
`SELECT prod_name FROM products WHERE prod_name REGEXP '[0-9][0-9][0-9][0-9]' ORDER BY prod_name;`

> 如前所述，`[:digit:]`匹配任意数字，因而它为数字的一个集合。`{4}`确切地要求它前面的字符(任意数字)出现4次，所以`[[:digit:]]{4}`匹配连在一起的任意4位数字。

| 定位元字符 | 说明 |
|:----------|----------:|
| ^ | 文本的开始 |
| $ | 文本的结尾 |
| [[:<:]] | 词的开始 |
| [[:>:]] | 词的结尾 |
{: .table}

`SELECT prod_name FROM products WHERE prod_name REGEXP '^[0-9\\.]' ORDER BY prod_name;`

> `^`匹配串的开始。因此，`^[0-9\\.]`只在.或任意数字为串中第一个字符时才匹配它们。没有`^`，则还要多检索出4个别的行(那些中间有数字的行)。

**`^`有两种用法。在集合中(用`[`和`]`定义)，用它来否定该集合，否则，用来指串的开始处。**

##### 简单的正则表达式测试

可以在不使用数据库表的情况下用`SELECT`来测试正则表达式。`REGEXP`检查总是返回0(没有匹配)或1(匹配)。可以用带文字串的`REGEXP`来测试表达式，并试验它们。相应的语法如下：  
`SELECT 'hello' REGEXP '[0-9]';`  
这个例子显然将返回0(因为文本hello中没有数字)。

**字段(field)**：基本上与列(column)的意思相同，经常互换使用，不过数据库列一般称为列，而术语字段通常用在计算字段的连接上。

**拼接(concatenate)**：将值联结到一起构成单个值。

> 多数DBMS使用`+`或`||`来实现拼接，MySQL则使用`Concat()`函数来实现。当把SQL语句转换成MySQL语句时一定要把这个区别铭记在心。

`SELECT Concat(vend_name, ' (', vend_country, ')') FROM vendors ORDER BY vend_name;`

> `Concat()`拼接串，即把多个串连接起来形成一个较长的串。

上面的`SELECT`语句连接以下4个元素：

* 存储在vend_name列中的名字；
* 包含一个空格和一个左圆括号的串；
* 存储在vend_country列中的国家；
* 包含一个右括号的串。

`SELECT Concat(RTrim(vend_name), ' (', RTrim(vend_country), ')') FROM vendors ORDER BY vend_name;`

> `RTrim()`函数去掉值右边的所有空格。MySQL还支持`LTrim()`(去掉串左边的空格)以及`Trim()`(去掉串左右两边的空格)。

**别名(alias)**：一个字段或值的替换名。用AS关键字赋予。有时也称为**导出列(derived column)**。

    SELECT Concat(RTrim(vend_name), ' (', RTrim(vend_country), ')') AS vend_title
    FROM vendors ORDER BY vend_name;

    SELECT prod_id, quantity, item_price, quantity*item_price AS expanded_price
    FROM orderitems WHERE order_num = 20005;

##### 如何测试计算

`SELECT`提供了测试和试验函数与计算的一个很好的办法。虽然`SELECT`通常用来从表中检索数据，但可以省略`FROM`子句以便简单地访问和处理表达式。例如，`SELECT 3*2;`将返回6，`SELECT Trim('abc');`将返回abc，而`SELECT Now();`利用`Now()`函数返回当前日期和时间。通过这些例子，可以明白如何根据需要使用SELECT进行试验。

##### 常用的文本处理函数

| 函数 | 说明 |
|:---------|---------:|
| Left() | 返回串左边的字符 |
| Length() | 返回串的长度 |
| Locate() | 找出串的一个子串 |
| Lower() | 将串转换为小写 |
| LTrim() | 去掉串左边的空格 |
| Right() | 返回串右边的字符 |
| RTrim() | 去掉串右边的空格 |
| Soundex() | 返回串的SOUNDEX值 |
| SubString() | 返回子串的字符 |
| Upper() | 将串转换为大写 |
{: .table}

**SOUNDEX**是一个将任何文本串转换为其语音表示的字母数字模式的算法。`SOUNDEX`考虑了类似的发音字符和音节，使得能对串进行发音比较而不是子母比较。

##### 常用日期和时间处理函数

| 函数 | 说明 |
|:---------|---------:|
| AddDate() | 增加一个日期(天、周等) |
| AddTime() | 增加一个时间(时、分等) |
| CurDate() | 返回当前日期 |
| CurTime() | 返回当前时间 |
| Date() | 返回日期时间的日期部分 |
| DateDiff() | 计算两个日期之差 |
| Date_Add() | 高度灵活的日期运算函数 |
| Date_Format() | 返回一个格式化的日期或时间串 |
| Day() | 返回一个日期的天数部分 |
| DayOfWeek() | 对于一个日期，返回对应的星期几 |
| Hour() | 返回一个时间的小时部分 |
| Minute() | 返回一个时间的分钟部分 |
| Month() | 返回一个日期的月份部分 |
| Now() | 返回当前日期和时间 |
| Second() | 返回一个时间的秒部分 |
| Time() | 返回一个日期时间的时间部分 |
| Year() | 返回一个日期的年份部分 |
{: .table}

`SELECT cust_id, order_num FROM orders WHERE Date(order_date) = '2005-09-01';`

> 日期必须为格式yyyy-mm-dd。这是首选的日期格式，因为它排除了多义性，

    SELECT cust_id, order_num
    FROM orders
    WHERE Date(order_date) BETWEEN '2005-09-01' AND '2005-09-30';

> `BETWEEN`操作符用来把2005-09-01和2005-09-30定义为一个要匹配的日期范围。
另一种检索出2005年9月份订单的方法如下所示：

    SELECT cust_id, order_num
    FROM orders
    WHERE Year(order_date) = 2005 AND Month(order_date) = 9;
    
##### 常用数值处理函数

| 函数 | 说明 |
|:---------|---------:|
| Abs() | 返回一个数的绝对值 |
| Cos() | 返回一个角度的余弦 |
| Exp() | 返回一个数的指数值 |
| Mod() | 返回除操作的余数 |
| Pi() | 返回圆周率 |
| Rand() | 返回一个随机数 |
| Sin() | 返回一个角度的正弦 |
| Sqrt() | 返回一个数的平方根 |
| Tan() | 返回一个角度的正切 |
{: .table}

**聚集函数(aggregate function)**：运行在行组上，计算和返回单个值的函数。

##### SQL聚集函数

| 函数 | 说明 |
|:---------|---------:|
| AVG() | 返回某列的平均值 |
| COUNT() | 返回某列的行数 |
| MAX() | 返回某列的最大值 |
| MIN() | 返回某列的最小值 |
| SUM() | 返回某列值之和 |
{: .table}

`SELECT AVG(prod_price) AS avg_price FROM products WHERE vend_id = 1003;`

> `AVG()`函数忽略列值为NULL的行。

`SELECT COUNT(*) AS num_cust FROM customers;`  
`SELECT COUNT(cust_email) AS num_cast FROM customers;`

> 如果指定列名，则指定列的值为空的行被`COUNT()`函数忽略，但如果`COUNT()`函数中用的是星号`*`，则不忽略。

`SELECT MAX(prod_price) AS max_price FROM products;`

> 在用于文本数据时，如果数据按相应的列排序，则`MAX()`返回最后一行。`MAX()`函数忽略值为NULL的行。

`SELECT MIN(prod_price) AS min_price FROM products;`

> 在用于文本数据时，如果数据按相应的列排序，则`MIN()`返回最前面的行。`MIN()`函数忽略值为NULL的行。 

`SELECT SUM(item_price*quantity) AS total_price FROM orderitems WHERE order_num = 20005;`

> `SUM()`函数忽略值为NULL的行。

以上5个聚集函数都可以如下使用：

* 对所有的行执行计算，指定`ALL`参数或不给参数(因为ALL是默认行为)；
* 只包含不同的值，指定`DISTINCT`参数。

`SELECT AVG(DISTINCT prod_price) AS avg_price FROM products WHERE vend_id = 1003;`

> 如果指定列名，则`DISTINCT`只能用于`COUNT()`。`DISTINCT`不能用于`COUNT(*)`，因此不允许使用`COUNT(DISTINCT)`，否则会产生错误。类似地，`DISTINCT`必须使用列名，不能用于计算或表达式。

`SELECT vend_id, COUNT(*) AS num_prods FROM products GROUP BY vend_id;`

> `GROUP BY`子句指示MYSQL按vend_id排序并分组数据。这导致对每个vend_id而不是整个表计算num_prods一次。

* `GROUP BY`子句可以包含任意数目的列。这使得能对分组进行嵌套，为数据分组提供更细致的控制。
* 如果在`GROUP BY`子句中嵌套了分组，数据将在最后规定的分组上进行汇总。换句话说，在建立分组时，指定的所有列都一起计算(所以不能从个别的列取回数据)。
* `GROUP BY`子句中列出的每个列都必须是检索列或有效的表达式(但不能是聚集函数)。如果在SELECT中使用表达式，则必须在`GROUP BY`子句中指定相同的表达式。不能使用别名。
* 除聚集计算语句外，`SELECT`语句中的每个列都必须在`GROUP BY`子句中给出。
* 如果分组列中具有NULL值，则NULL将作为一个分组返回。**如果列中有多行NULL值，它们将分为一组。**
* **`GROUP BY`子句必须出现在`WHERE`子句之后，`ORDER BY`子句之前。**

使用`WITH ROLLUP`关键字，可以得到每个分组以及每个分组汇总级别(针对每个分组)的值，如下所示：

`SELECT vend_id, COUNT(*) AS num_prods FROM products GROUP BY vend_id WITH ROLLUP;`

**`WHERE`过滤行，而`HAVING`过滤分组。**`WHERE`在数据分组前进行过滤，`HAVING`在数据分组后进行过滤。

`SELECT cust_id, COUNT(*) AS orders FROM orders GROUP BY cust_id HAVING COUNT(*) >= 2;`

##### SELECT子句及其顺序

| 子句 | 说明 | 是否必须使用 |
|:---------|---------|---------:|
| SELECT | 要返回的列或表达式 | 是 |
| FROM | 从中检索数据的表 | 仅在从表选择数据时使用 |
| WHERE | 行级过滤 | 否 |
| GROUP BY | 分级说明 | 仅在按组计算聚集时使用 |
| HAVING | 组级过滤 | 否 |
| ORDER BY | 输出排序顺序 | 否 |
| LIMIT | 要检索的行数 | 否 |
{: .table}