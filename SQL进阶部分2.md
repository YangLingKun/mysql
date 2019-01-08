# SQL进阶2

## 表之间关系

### 一对一

### 一对多

- 一个人可以拥有多辆汽车
- 创建Person表

- 创建Car表

### 多对多

- 学生选课，一个学生可以选修多门课程，每门课程可供多个学生选择
- 一个学生可以有多个老师，一个老师也可以有多个学生
- 创建老师表

	-  

- 创建学生表

- 创建学生与老师关系表

- 添加外键

- 关系图

### 为什么要拆分表

- 避免大量冗余数据的出现

## 多表查询

### 合并结果集

- 什么是合并结果集

	- 合并结果集就是把两个select语句的查询结果合并到一起

- 合并结果集的两种方式

	- UNION

		- 合并时去除重复记录

	- UNION ALL

		- 合并时不去除重复记录

- 格式

	- UNION

		- SELECT * FROM 表1 UNION SELECT * FROM 表2
		- SELECT *FROM 表1 UNION ALL SELECT * FROm 表2

- 示例

	- 创建表

		- -- CREATE TABLE A(name VARCHAR(10),score int );
-- Create TABLE B(name VARCHAR(10),score int );
-- --
-- INSERT INTO A VALUES ('a',10),('b',20),('c',30);
-- INSERT INTO B VALUES ('a',10),('b',20),('c',40);

	- UNION

		- SELECT * FROM A UNION SELECT * FROM B;

	- UNION ALL

		- SELECT * FROM A UNION ALL SELECT * FROM B;

- 注意事项

	- 被合并的两个结果，列数，列类型必须相同

### 连接查询

- 什么是连接查询

	- 也可以叫跨表查询，需要关联多个表进行查询

- 什么是笛卡尔集

	- 假设集合A={a,b},集合B={0，1，2}
	- 则两个集合的笛卡尔集为{（a,0),(a,1),(a,2),(b,0)(b,1),(b,2)}
	- 可以扩展到多个集合的情况

- 同时查询两个表，出现的就是笛卡尔集结果
- 查询时给表起别名

	- SELECT * FROM stu st,score sc;

- 多表联查，如何保证数据正确

	- 在查询时要把主键和外键保持一致
	- 主表中的数据参照字表中的数据

- 根据连接方式分类

	- 内连接

		- 等值连接

			- 两个表同时出现的id才显示
			- SELECT * FROM stu  st INNER JOIN score ac ON st.id = sc.sid
			- 与多表联查约束主外键是一样的只是写法改变了
			- ON后面只写主外键
			- 如果还有条件直接在后面写where
			- 多表联查后面还有条件就直接写and

		- 多表连接

			- 建立学生，分数，科目表
			- 使用99连接法

				- SELECT st.name,sc,score ,c.name FROM stu st,score sc,course c WHERE st.id = sc.sid AND sc.cid = c.cid

			- 使用内联查询

				- SELECT st.name ,sc.score,c.name FROM stu st 
JOIN score sc ON st.id = sc.sid 
JOIN course c ON sc. cid = c.cid;

		- 非等值连接

			- 示例表

			- 建表语句

				- CREATE TABLE `emp` (
  `empno` int(11) NOT NULL,
  `ename` varchar(255) DEFAULT NULL,
  `job` varchar(255) DEFAULT NULL,
  `mgr` varchar(255) DEFAULT NULL,
  `hiredate` date DEFAULT NULL,
  `salary` decimal(10,0) DEFAULT NULL,
  `comm` double DEFAULT NULL,
  `deptno` int(11) DEFAULT NULL,
  PRIMARY KEY (`empno`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

					- INSERT INTO `emp` VALUES (7369, '孙悟空', '职员', '7902', '2010-12-17', 800, NULL, 20);
INSERT INTO `emp` VALUES (7499, '孙尚香', '销售人员', '7698', '2011-2-20', 1600, 300, 30);
INSERT INTO `emp` VALUES (7521, '李白', '销售人员', '7698', '2011-2-22', 1250, 500, 30);
INSERT INTO `emp` VALUES (7566, '程咬金', '经理', '7839', '2011-4-2', 2975, NULL, 20);
INSERT INTO `emp` VALUES (7654, '妲己', '销售人员', '7698', '2011-9-28', 1250, 1400, 30);
INSERT INTO `emp` VALUES (7698, '兰陵王', '经理', '7839', '2011-5-1', 2854, NULL, 30);
INSERT INTO `emp` VALUES (7782, '虞姬', '经理', '7839', '2011-6-9', 2450, NULL, 10);
INSERT INTO `emp` VALUES (7788, '项羽', '检查员', '7566', '2017-4-19', 3000, NULL, 20);
INSERT INTO `emp` VALUES (7839, '张飞', '总裁', NULL, '2010-6-12', 5000, NULL, 10);
INSERT INTO `emp` VALUES (7844, '蔡文姬', '销售人员', '7698', '2011-9-8', 1500, 0, 30);
INSERT INTO `emp` VALUES (7876, '阿珂', '职员', '7788', '2017-5-23', 1100, NULL, 20);
INSERT INTO `emp` VALUES (7900, '刘备', '职员', '7698', '2011-12-3', 950, NULL, 30);
INSERT INTO `emp` VALUES (7902, '诸葛亮', '检查员', '7566', '2011-12-3', 3000, NULL, 20);
INSERT INTO `emp` VALUES (7934, '鲁班', '职员', '7782', '2012-1-23', 1300, NULL, 10);

				- CREATE TABLE `dept` (
  `deptno` bigint(2) NOT NULL AUTO_INCREMENT COMMENT '表示部门编号，由两位数字所组成',
  `dname` varchar(14) DEFAULT NULL COMMENT '部门名称，最多由14个字符所组成',
  `local` varchar(13) DEFAULT NULL COMMENT '部门所在的位置',
  PRIMARY KEY (`deptno`)
) ENGINE=InnoDB AUTO_INCREMENT=41 DEFAULT CHARSET=utf8;

					- INSERT INTO `dept` VALUES (10, '财务部', '北京');
INSERT INTO `dept` VALUES (20, '调研部', '上海');
INSERT INTO `dept` VALUES (30, '销售部', '王者峡谷');
INSERT INTO `dept` VALUES (40, '运营部', '腾讯大楼');

				- CREATE TABLE `salgrade` (
  `grade` bigint(11) NOT NULL AUTO_INCREMENT COMMENT '工资等级',
  `lowSalary` int(11) DEFAULT NULL COMMENT '此等级的最低工资',
  `highSalary` int(11) DEFAULT NULL COMMENT '此等级的最高工资',
  PRIMARY KEY (`grade`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8;

					- INSERT INTO `salgrade` VALUES (1, 700, 1200);
INSERT INTO `salgrade` VALUES (2, 1201, 1400);
INSERT INTO `salgrade` VALUES (3, 1401, 2000);
INSERT INTO `salgrade` VALUES (4, 2001, 3000);
INSERT INTO `salgrade` VALUES (5, 3001, 9999);

			- 查询所有员工的姓名，工资，所在部门的名称以及工资的等级

				- 1.查询所有员工的姓名，工资

				- 2.查询所有员工的姓名，工资和所有部门

				- 3.查询所有员工的姓名，工资和所在部门及工资等级

	- 外连接

		- 左连接

			- 使用LEFT JOIN 关键字 ,左边的表的数据全部查询出来，右边满足条件的查询出来

		- 右连接

			- 使用RIGHT JOIN关键字 就会把右边表中的所有数据查询出来，左表只显示满足条件的

	- 自然连接

		- 连接查询会产生无用笛卡尔集，我们通常使用主外键关系等式来去除他
		- 而自然连接无需你去给出主外键等式，它会自动找到这一等式
		- 也就是说不用去写条件
		- 要求

			- 两张连接的表中列名称和类型完全一致的列作为条件
			- 去除重复的列

### 子查询

- 什么是子查询

	- 一个select语句中包含另一个完整的select语句
	- 或两个以上SELECT，那么就是子查询语句了

- 子查询出现的位置

	- where后，把select查询出的结果当作另一个select的条件值
	- from后，把查询出的结果当作一个新表

- 使用

	- 查询与项羽同一部门的所有员工

		- SELECT ename From emp WHERE deptno = (SELECT deptno FROM emp WHERE ename = '项羽')

	- 查询工资高于程咬金的员工

		- SELECT ename FROM emp WHERE salary > (SELECT salary FROM emp WHERE ename = '程咬金')

	- 工资高于30号部门所有人的员工信息

		- SELECT * FROM emp WHERE salary > all(SELECT salary FROM emp WHERE deptno = 30)

	- 查询工作和工资与妲己完全相同的员工信息

		- SELECT * FROM emp WHERE (salary,job) = (SELECT salary ,job FROM emp WHERE ename = '妲己')

	- 有2个以上直接下属的员工信息

		- SELECT * FROM emp WHERE empno in (
SELECT mgr FROM emp GROUP BY mgr HAVING COUNT(mgr)>2)

	- 查询员工编号为7788的员工名称，员工工资，部门名称，部门地址

		- SELECT ename,salary,dname,local FROM dept join emp
ON dept.deptno = emp.deptno
WHERE empno = 7788

### 自连接

- 通过给自己取别名来连接自己
- T t1 JOIN T t2 ON
- 求7369员工编号，姓名，经理编号和经理姓名

	- SELECT e1.empno,e1.ename,e2.empno,e2.ename from emp e1 join emp e2
WHERE e1.mgr = e2.empno AND
e1.empno = 7369

*XMind: ZEN - Trial Version*