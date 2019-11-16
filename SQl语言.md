### SQl语言
#### 一. SQL语言基础

#####  1. 什么是SQL语言

结构化查询语言(Structures Query Language)，是一种数据库查询和程序设计语言，用于存取数据以及查询、更新和管理==关系型数据库==系统，也是数据库脚本文件的文件名。

##### 2. SQl能做什么

1. 面向数据库进行增删改查的操作
2. 创建数据库、数据表
3. 在数据库中创建存储过程
4. 在数据库中创建视图
5. 可以设置表、存储过程和视图的权限

##### 3. SQL标准

比较有代表性的几个版本：
1. SQL86  
2. SQL92
3. SQL99
ps ：大部分数据库程序都有自己的私有扩展

##### 4. SQL语言结构

1. 数据查询语言(DQL:DataQuerylanguage)
	* 常用关键字:==SELECT	WHERE	ORDER BY	GROUP BY	HAVING==
	* `select......from tableName where `**查询条件**
2. 数据操作语言(DML:Data Manipulation Language)
    * 常用关键字:==INSERT	UPDATE	DELETE==
    * ` insert into tableName (字段1, 字段2, 字段3...) values(值1, 值2, 值...)`
    * ` update tableName set 字段 = 值, 字段 = 值 where 条件`
    * `delete from tableName where 条件`
3. 事务处理语言(TCL:Transaction Control Language)
    * commit...事务提交
    * rollback...事务回滚
    * savepoint...设置回滚点
4. 数据控制语言(DCL: Data Control Language)
    * grant...授予用户权限
    * revork...撤销用户权限
5. 数据定义语言(DDL: Data Definition Language)
    * creat...创建数据库对象
    * alter...修改数据库对象
    * drop...删除数据库对象
    * rename...修改数据库对象名称
    
#### 二. DQL语言
##### 1. 查询语句

###### 1.基本结构和常用操作

1. 基本结构 ` select ... from ... `
2. SELECT中的算数表达式

	* 可以在查询的字段上进行算数运算(+, -, *, /);

3. 定义空值

	* 所有空值经过运算后依然为空;

4. 定义列别名

    * ` select 字段1 别名1,字段2 别名2,...from tableName;`
    * ` select 字段1 as 别名1, 字段2 as 别名2,...from tableName;`
    * 对别名格式有要求 : ` select 字段as(或空格)"别名"...from tablename;`

5. 连字运算符
    * 连接列或者字符串到其他的列

    * 用双竖线表示(||)

    * 构造一个字符表达式的合成列
    
      * 示例 : `select last_name || first_name as"姓名" from tablename` 
6. 文字字符串
	使用连字符加入文字日期或者数字
	* 示例: `select last_name || ' is a ' || empNo as "empDecs" from tablename`
7. 去除重复行
    * DISTINCT关键字(查询多个字段时,对结果集去重,不是针对某一个字段)
    * 示例: `select deptNo from dept`    and   `select distinct deptNo from dept`
8. 用选择限制行
    * `select * from emp where job = clerk;`
9. 字符串和日期
    * 要求必须放在单引号中字符值区分大小写,日期值格式敏感

###### 2. 排序查询

*  语法: order by 子句
	* ` order by 排序字段1 排序方式1,排序字段2 排序方式2,...排序方式;`
	* 排序方式:
		1. 升序:asc(默认);
		2. 降序:desc;
	
	* 注意 : 如果有多个排序条件,则当前边的条件值相同时,才会判断第二条件

###### 3. 聚合函数

* 将一列数据作为一个整体,进行纵向的计算
    1. count:计算个数
        * ` select count(字段) from 表名;`
		* ` select count(ifnull(字段, 0)) from 表名;`如果为空就设置为0;
		* 一般选择非空列(主键)
		* count( * )==不推荐==
    2. max:计算最大值
        * select max(字段) from 表名;
    3. min:计算最小值
        * select min(字段) from 表名;
    4. sum:计算和
    	* select sum(字段) from 表名;
    5. avg:计算平均值
        * select avg(字段) from 表名;
* 注意:聚合函数的计算会在排除null值
* 解决方案:
	1. 选择不包含空列进行计算
	2. ifnull
###### 4. 分组查询

1. 语法: group by 分组字段;
2. 注意:
    1. 分组之后查询的字段:分组字段,聚合函数;
    2. 分组之前可以进行条件限定,例如对70分以上的同学进行分组
    3. 分组之后的条件限定可以使用having关键字来限定
        * where和having的区别
            1. where在分组之前进行限定,如果不满足条件,则不参与分组;having在分组之后进行限定,如果不满足条件,则不会被查询.
            2. where后面不能跟聚合函数,having之后可以进行聚合函数的判断;

###### 5. 分页查询

1. 语法: limit 开始的索引,每页查询的条数;

2. ==分页公式: 起始索引 = (当前页码 - 1) * 每页显示的条数==
3. 分页操作在不同的数据库中有不同的语法,limit只针对MySQL;

##### 2.约束

##### 3.多表之间的关系

##### 4.范式

##### 5.数据库的备份和还原

#### 三. DML
##### 1.添加数据

* 语法: ` insert into 表名 (字段1, 字段2, ...字段n)  values (值1, 值2, ...值n);`
* 注意:
    1. 字段名和值需要一一对应;
    2. 表名后不定义字段名,默认给所有值添加信息;` insert into 表名 values(值1, 值2, ...值n);`
    3. 除了数字类型,其他类型需要使用引号引起来(单双都可以);

##### 2.删除数据

* 语法: ` delete from 表名 [where条件]` 
* 注意:
    1. 如果不添加条件,则删除表中所有数据;(慎用)
    
    2. 如果要删除所有记录,不推荐使用delete from 表名,执行多次,效率低!
       
         ` truncate table 表名` -- 删除表,然后创建一个一样的空表;

##### 3.修改数据

* 语法:` update 表名 set 字段1 = 值1, 字段2 = 值2, ...[where 条件]`
* 注意
    1. 如果不加任何条件,则会将表中所有记录全部修改;

#### 四. DDL

#####  1.  操作数据库 : CRUD

1. C(Create) : 创建
	``` sql
		create database [if not exists(不存在就创建)] tableName [character set utf8(默认)]
		create database db1; -- 基本语法
		create database db2 character set gbk; -- 按照规定的字符集创建数据库
		create database if not exists db3; -- 判断,如果不存在就创建 
		create database if not exists db4 character set gbk; -- 判断并制定字符集为gbk
	```
3. R(Retrieve) : 查询
	* 查询所有数据库的名称 `show databases`
	* 查询某个数据库的字符集 : 查询某个数据库的创建语句
	` show create database 数据库名称 ; `
	
4. U(Update) : 修改

    * 修改数据库的字符集	`alter database dbName character set charsetName`

5. D(Delete) : 删除

    * 删除数据库	
	``` SQL
		drop database dbName;
		drop database if exists dbName;-- 判断数据库是否存在,存在再删除
	```

6. 使用数据库

	``` SQL
		-- 查询当前正在使用的数据库
		select database();
		-- 选择数据库
		use dbName;
	```

#####  2.操作数据库表

1. C(Create) : 创建

	* 语法:
	``` SQL
		create table tableName (
		字段名1 数据类型1,
		字段名2 数据类型2,
		...
		字段名n 数据类型n
		)
		-- 最后一行不需要加逗号
	```
	* 数据类型:
		1. int: 整数类型` age int`
		2. double: 小数类型 `score double(5,2)`<!--一共5位,小数点后保留两位--> 
		3. date: 日期, 质保汉年月日,yyyy-MM-dd;
		4. datetime: 日期,包含年月日时分秒 yyyy-MM-dd  HH:mm:ss;
		5. timestamp: 时间戳类型, 包含年月日时分秒 yyyy-MM-dd  HH:mm:ss;
		    * ==如果不给这个字段赋值,或者赋值为null,则默认使用当前的系统时间来自动赋值;==
		6. varchar: 字符串 `name varchar(20)`<!-- 最大字符数量 -->
	* 示例 : 
	``` SQL
		create table student(
		id int,
		name varchar(32),
		age int,
		score double(4,1),
		birthday date,
		insert_time timestamp
		);
	```
	* 复制一张表 ` create table 表名1 like 表名2;`
	
2. R(Retrieve) : 查询

	* 查询某个数据库中所有的表名称	` show tables;`
	* 查询表结构	` desc 表名;`

3. U(Update) : 修改
	1.修改表名	` alter table 表名1 rename to 表名2;`
	2.修改字符集	` alter table 表名 character set 字符集;`
	3.添加一列	` alter table 表名add 字段名 数据类型;`
	4.修改字段名(列)以及类型:
	
	​	` alter table 表名 change 列名 新列名 新数据类型`<!-- 修改列名和数据类型-->
	
	​	` alter table 表名 modify 列名 新数据类型`<!-- 修改列名-->
	
	5.删除列	`  alter table 表名 drop 列名`
	
4. D(Delete) : 删除
  * 删除数据表 ` drop table tableName`
  * 判断是否存在,存在就删除 ` drop table if exists tableName;`





