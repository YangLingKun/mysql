# SQL进阶部分1

## 分组查询

### 什么是分组查询

- 将查询结果按照一个或多个字段进行分组，字段值相同的为一组

### 分组使用

- SELECT gender FROM employee GROUP BY gender
- 根据gender字段来分组，gender字段的全部值只有两个（‘男’和女‘），所以分为了两组
- 当group by单独使用时，只显示出每一组的第一条记录
- 所以group by单独使用时的实际意义不大

### 分组注意事项

- 使用分组时，select后面直接跟的字段一般都出现在group by后

### group by + group_concat()

- group_concat(字段名) 可以作为一个输出字段来使用
- 表示分组之后，根据分组结果，使用group_concat（）来放置每一组的某字段的值的集合
- SELECT gender，GROUP_CONCAT(name) from employee GROUPP BY gender

### group by+聚合函数

- 通过group_concat()的启发，我们既然可以统计出每个分组的某字段的值的集合，那么我们也可以通过聚合函数来对这个”值的集合“做一些操作
- 使用

	- 查询每个部门的部门名称和每个部门的工资和

		- SELECT department,SUM(salary) FROM employee GROUP BY department;

	- 查询每个部门的部门名称以及每个部门的人数

		- SELECT department,COUNT(*) FROM employee GROUP BY department;

	- 查询每个部门的部门名称以及每个部门工资大于1500的人数

		- SELECT department,COUNT(*) FROM employee WHERE salary>1500 GROUP BY department ;

### group by +having

- 用来分组查询后指定一些条件来输出查询结果
就是对分组查询后的结果进行筛选
- having作用和where一样，但是having只能用于group by
- 查询工资中和大于等于9000的部门的名称以及工资和

	- SELECT department FROM employee GROUP BY department HAVING SUM(salary)>=9000

- having与where的区别

	- having是在分组后进行数据结果进行筛选
	- where是在分组前对数据进行筛选
	- having后面是可以使用聚合函数
	- where后面不可以使用聚合函数
	- where是对

- 查询工资大于2000的，工资总和大于6000的部门名称以及工资和

	- SELECT department,SUM(salary) FROM employee  WHERE salary >2000 GROUP BY department HAVING SUM(salary)>6000

### 书写顺序

### 执行顺序

## LIMIT

### 从哪一行开始查，总共要查几行

### Limit 参数1，参数2

- 参数1：从哪一行开始查
- 参数2：查多少条数据

### 角标是从0开始

### 格式

- SELECT * FROM 表名 LIMIT 0，5；

### 分页思路

## 数据完整性

### 什么是数据完整性

- 保证用户输入的数据保存到数据库中是正确的

### 如何添加数据完整性

- 在创建表时给表中添加约束

### 完整性分类

- 实体完整性
- 域完整性
- 引用完整性

## 实体完整性

### 什么是实体完整性

- 表中的一行就称为一个实体

### 实体完整性的作用

- 标识每一行数据不重复，行级约束

### 约束类型

- 主键约束
- 唯一约束
- 自动增长列

### 主键约束

- 特点：

	- 每个表中要有一个主键
	- 数据唯一，且不能为null

- 添加方式：

	- CREATE TABLE 表名 （字段名1 数据类型  primary ley，字段名2 数据类型.....);
	- CREATE TABLE 表名 （字段1 数据类型，字段2 数据类型,..... primary key(要设置主键的字段));
	- 联合主键

		- 两个字段数据同时相同，才违反联合主键约束，其中主键2字段的数据可以为空
		- CREATE TABLE 表名（字段1 数据类型，字段2 数据类型，....primary key (主键1，主键2）);

	- 1、先创建表
2，再去修改表
ALTER TABLE  student ADD CONSTRAINT PRIMARY KEY(id)

### 唯一约束

- 特点

	- 制定的列的数据不能重复
	- 可以为空

- 格式

	- CREATE TABLE 表名（字段1 数据类型，字段2 数据类型  UNIQUE)

### 自动增长列

- 特点

	- 指定列的数据自动增长
	- 即使数据删除，还是从删除的序号继续往下

- 格式

	- CREATE TABLE 表名 （字段1 数据类型 PRIMARY KEY AUTO_INCREMENT）

## 域完整性

### 使用

- 限制此单元格的数据正确，不对照此列的其他单元格比较
- 域代表当前单元格

### 域完整性约束

- 数据类型

	- 数值类型，日期类型，字符串类型

- 非空约束

	- CREATE TABLE 表名 （字段1 数据类型 PRIMARY KEY AUTO_INCREMENT,字段2 数据类型 UNIQUE NOT NULL）

- 默认值约束

## 参照完整性

### 什么是参照完整性

- 是指表与表之间的一种的对应关系
- 通常情况下可以通过设置两表之间的主键，外键关系，或者编写两表的触发器来实现
- 有对应参照完整性的两张表格，在对他们进行数据插入、更新、删除的过程中，系统都会被修改表格与另外一张对应表格进行对照，从而阻止一些不正确的数据的操作

### 数据库的主键和外键类型一定要一致

### 两表必须都要是innoDB类型

### 设置参照完整性后，外键当中打的内值，必须得是主键当中的内容

### 一个表设置当中的字段设置为主键，设置主键的为主表

### 创建表时，设置外键，设置外键的为字表

*XMind: ZEN - Trial Version*