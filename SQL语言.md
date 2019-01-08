# SQL语言

## 字符集

### 字符集的由来

- 计算机 只能识别二进制代码无论是计算机程序还是数据，都会转换成二进制，计算机才能认识。
- 为了计算机不止能做科学计算，也能处理文字信息。
人们想出来给每一个文字符号编码以便于计算识别处理的办法，这就是计算机字符集的由来

### ASSCII

- 一套文字符号及其编码，比较规则的集合

	- 20世纪六十年代初，没过标准化组织ANSI发布了第一个字符集。ASCII后来进一步变成了国际标准ISO-646

- 各大字符集

	- 自ASCII后，为了处理不同的文字，各大计算机公司，各国，标准化政府，组织先后发明了几百种字符集

		- UTF-8
		- GB2312-80
		- GBK
		- BIG5

	- 由于字符集规则不同，需要统一字符编码

### unicode

- 为了统一字符编码，国际化标准组织ISO制定了新的国际字符集标准
- ISO-10646发布后，找到了没过计算机公司的反对
- 1991年推出了Unicode1.0
- 1991.10ISO将unicode收编，起名为BMP

### UTF-16

- 万一使用BMP之后的文字怎么办，Unicode提出了UTF—16

### UTF-8

- 但是UTF-16在传输和处理中，都存在问题
- 于是又提出了UTF-8的解决文案
- UTF-8按一定的规则，将一个ISO10646或Unicode转换成1至4个字节的编码
- 其中ASCII转成单字节编码，也就兼容了ASCII字符集
- UTF-8的234字节用以转换ISO-10646标准的UCS-4原始码

### 汉字的一些常见的字符集

- GB2312
- GB13000
- GBK
- GB18030

## MySql的存储引擎

### 数据库对象

- 存储，管理和使用数据的不同结构形式，如：表，视图，存储过程，函数，触发器，事件等

### 数据库

- 存储数据库对象的容器

### 什么是存储引擎

- MySQL中的数据用不同的技术存储在文件或内存中
- 每一种技术都是用不同的存储机制、索引技巧、锁定水平并且最终提供广泛的不同的功能和能力。
- 通过选择不同的技术，你能获得额外的速度或者功能，从而改善你的应用的整体功能
- 不同的存储引擎性能是不一样的

### 什么是事务

- 是指作为单个逻辑工作单元执行的一系列操作，要么全部执行成功，要么全部不成功

### MYSIAM

- 它不支持事务，也不支持外键，优点是其访问速度快，对事务完整性没有要求或者以SELECT、INSERT为主的应用可以优先考虑使用该存储引擎
- 每个MySiAM在磁盘上存储成三个文件，其中文件名和表明都相同，但是扩展名分别为

	- MYD（MYData,存储数据
	- .frm（存储表定义）
	- MYI(MYIndex,存储索引）

### InnoDB

- InnoDB存储引擎提供里具有提交，回滚和崩溃恢复的事务安全。但是对比于MyISAM的存储引擎，InnoDB写的处理效率差一些并且会占用更多的资源

### MEMORY

- memory类型的表访问非常狂，因为它的数据是放在内存中

## 什么是SQL

### SQL是Structured Query Language（结构化查询语言）的简写

### SQL是专为数据库而建立的操作命令集，是一种功能齐全的数据库语言

### 在使用它时，只需要发出“做什么”的命令，“怎么做”是不用使用者考虑的

## SQL功能分类

### DDL：数据定义语言

- 用来定义数据库对象：创建库，表，列等

	- CREATE（创建）、DROP（删除）、ALTER（修改）等语句

### DML:数据操作语言

- 用来操作数据库表中的记录

	- INSERT （插入）UPDATE(修改）DELETE(删除)语句

### DQL：数据查询语言

- 用来查询数据

	- SELECT （查询)语句

### DCL:数据控制语言

- 用来定义访问权限和安全级别

	- GRANT、REVOKE、COMMIT、ROLLBACK

## SQL数据类型

### MySQL中定义数据字段的类型对你数据库优化是非常重要的

### MySQL支持所有标准SQL数值数据类型

### MySQL支持多种类型，大致可以分为三类

- 数值类型
- 字符串类型
- 日期和时间类型

### 常用数据类型

- double:浮点型，例如double（5，2）表示最多5位，而且必须有两位小数，即最大值为999.99；
- char：固定长度字符串类型；char(10)'abc   '（会补充空格）
- varchar:可变长度字符串类型；varchar（10）‘abc’（不会补充空格）
- test：字符串类型；长文本文件
- blob：二进制类型；
- date：日期类型，格式为：yyyy-MM-dd；
- datetime：日期时间格式yyyy-MM-dd hh:mm:ss

### 在mysql中，字符串类型和日期类型都要用单引号括起来。‘Myxq’   ’2020 -01-01‘

## DML

### DML是对表中的数据进行增删改操作

### 插入操作

- INSERT  INTO 表名（字段1，字段2，...) VALUES (字段值1，字段值2, ...)
- 注意事项

	- 列名与列值的类型，个数是要一一对应的
	- 值不要超出列定义的长度
	- 插入的日期和字符一样都是用引号括起来

- 批量插入

	- INSERT INTO 表名 （字段1，字段2，...）VALUES
（字段值1，字段值2，....)，
（字段值1，字段值2，....)；

### 更新操作

- UPDATE 表名 SET 字段名1=字段值1，字段名2=字段值2.....WHERE  字段名 = 字段值
- 把所有同学分数改为90

	- UPDATE student SET score = 90

- 把张三的分数改为60

	- UPDATE student SET score = 60 WHERE name = ‘张三’

- 把姓名为李四的年龄改为20和分数改为70

	- UPDATE　student SET age = 20 ,score = 70 WHERE name = ‘李四’

- 把wc的年龄在原来基础上加一岁

	- UPDATE student SET age = age +1 WHERE name = 'wc'

- 修改数据库密码

	- UPDATE mysql.user SET authentication_string = password('root') WHERE user = 'root' AND Host = 'localhost'
	- flush  privileges;刷新MySQL的系统权限相关表

### 删除操作

- DELETE FROM 表名 【WHERE 字段名=字段值】
- TRUNCATE TABLE 表名
- DELETE和TRUNCATE的区别

	- DELETE删除表中的数据，表结构还在，删除后的数据可以找回
	- TRUNCATE 删除是把表直接DROP掉，然后再创建一个空表，删除的数据不能找回，执行速度比DELETE快

## DDL

### 创建数据库

- CREATE DATABASE  数据库名 CHARACTER SET UTF-8

### 创建表

### 添加一列

- ALTER TABLE 表名  ADD 字段名 数据类型 【约束】 

### 查看表的字段信息

- DESC 表名

### 修改一个表的字段类型

- ALTER TABLE  表名 MODIFY 字段名 数据类型

### 删除一列

- ALTER TABLE 表名 DROP 字段名

### 修改表名

- RENAME TABLE 原始表名 TO 要修改的表名

### 查看表的创建细节

- SHOW CREATE TABLE 表名

### 修改表的字符集为GBK

- ALTER TABLE 表名 CHARACTER SET BGK

### 修改表的列名

- ALTER TABLE 表名 CHANGE 原始列名 新列名 数据类型

### 删除表

- DROP TABLE 表名

## DQL

### 查询所有的数据

- SELECT * FROM 表名

### 结果集

- 数据库执行DQL语句不糊对数据进行改变，而是让数据库发送结果集给客户端
- 查询返回的结果集是一张虚拟表

### 查询指定的列

- SELECT 字段名1，字段名2 FROM 表名

### 条件查询

- 条件查询就是再查询时给出WHERE字句，再WHERE子句中可以使用一些运算符及关键字
- 条件查询运算符及关键字

	- =等于、！=不等于、<>不等于、<小于、<=小于等于、>大于、>=大于等于
	- BETWEEN---AND；值在什么范围之间
	- IN（set）固定的范围值
	- IS NULL：为空 IS  NOT NULL 不为空
	- AND：与
	- OR：或
	- NOT：非

- 使用

	- 查询性别为男，并且年龄为20的学生记录

		- SELECT * FROM student WHERE sex = '男' and age = 20;

	- 查询学号为1001或者名为张三的记录

		- SELECT * FROM student WHERE id =1001 or name = '张三'

	- 查询学号为1001，1002，1003的记录

		- SELECT * FROM student WHERE id = 1001 or id = 1002 or id =1003
		- SELECT * FROM student WHERE id in (1001,1002,1003)

	- 查询年龄为null的记录

		- SELECT * FROM student WHERE age IS NULL
		- SELECT * FROM student WHERE ISNULL(age)

	- 查询年龄在18-20之间的学生记录

		- SELECT * FROM student WHERE age BETWEEN 18 AND 20

	- 查询性别非男的学生记录

		- SELECT * FROM student WHERE sex !='男'

	- 查询姓名不为null的记录

		- SELECT * FROM student WHERE `name` IS NOT NULL;
		- SELECT * FROM student WHERE NOT ISNULL(`name`)

### 模糊查询

- 根据指定的关键字进行查询
- 使用LIKE关键字后面加上通配符
- 通配符

	- _ ：任意一个字符
	- % ：任意0-n个字符

- 使用

	- 查询姓名由五个字符构成的学生记录

		- SELECT * FROM student WHERE `name` LIKE '_____';

	- 查询姓名由五个字母构成，并且5个字母为‘s'的学生记录

		- SELECT * FROM student WHERE `name`LIKE '_____' AND `name` = 'sssss'

	- 查询姓名以’m'开头的学生记录

		- SELECT * FROM student WHERE `name` LIKE 'm%';

	- 查询姓名中包含‘s'字母的学生记录

		- SELECT * FROM student WHERE `name` LIKE '%s%';

### 字段控制查询

- 去除重复记录（DISTINCT）

	- SELECT DISTINCT name FROM student

- 把查询字段的结果进行运算，必须都要是数值类型

	- SELECT *，字段1+字段2 FROM 表名
	- 列有很多记录的值为NULL，因为任何东西与NULL相加结果还是NULL，所以结算结果可能会出现NULL。
下面使用了把NULL转换成数值0的函数IFNULL；
	- SELECT *,IFNULL(age,0)+IFNULL(score,0) FROM student;

- 对查询结果取别名

	- SELECT  字段名 AS 别名  FROM student;
	- 其中AS可以去掉，但是建议加上去，更加直观

### 排序

- 创建表

	- CREATE TABLE `employee` (
  `id` int(11) NOT NULL,
  `name` varchar(50) DEFAULT NULL,
  `gender` varchar(1) DEFAULT NULL,
  `hire_date` date DEFAULT NULL,
  `salary` decimal(10,0) DEFAULT NULL,
  `performance` double(255,0) DEFAULT NULL,
  `manage` double(255,0) DEFAULT NULL,
  `dpartment` varchar(255) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


- 对查询结果进行排序
- 使用关键字ORDER BY
- 排序类型

	- 升序ASC（默认）
	- 降序DESC

- 使用

	- 根据员工薪资对结果进行升序显示

		- SELECT * from employee ORDER BY salary

	- 根据薪资进行降序，id进行升序显示结果

		- SELECT * from employee ORDER BY salary DESC，id，ASC

### 聚合函数

- 对查询结果进行统计计算
- 常用聚合函数

	- COUNT（）：统计指定列不为NULL的记录行数
	- MAX（）：计算指定列的最大值，如果指定列是字符串类型那么使用字符串排序运算
	- MIN（）：计算指定列的最小值，如果指定列是字符串类型那么使用字符串排序运算
	- SUM（）：计算指定列的数值和，如果指定类型不是数值类型，那么计算结构为0
	- AVG（）；计算指定列的平均值，如果指定列类型不是数值类型，那么计算结果为0；

- 使用

	- COUNT

		- 查询员工表的记录数

			- SELECT COUNT(*) FROM employee

		- 查询员工表中有绩效的人数

			- SELECT COUNT(performance) FROM employee

		- 查询员工表中月薪大于2500的人数

			- SELECT COUNT(*) FROM employee WHERE salary>2500

		- 统计月薪与绩效之和大于5000元的人数

			- SELECT COUNT(*) FROM employee WHERE (IFNULL（salary，0）+IFNULL（performance，0）)>5000

		- 查询有绩效的人数，和有管理费的人数

			- SELECT COUNT(performance),COUNT(manage) FROM employee 

	- SUM和AVG

		- 查询所有雇员月薪和

			- SELECT SUM(salary) FROM employee 

		- 查询所有雇员月薪和，以及所有雇员绩效和

			- SELECT SUM(salary),SUM(performance) FROM employee 

		- 查询所有雇员月薪+绩效和

			- SELECT SUM(salary)+SUM(performance)  FROM employee 

		- 统计所有员工平均工资

			- SELECT AVG(salary) FROM employee 

*XMind: ZEN - Trial Version*