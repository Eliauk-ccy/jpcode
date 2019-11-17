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

1. 基本结构 
	``` SQL 
		select
			字段列表
		from
			表名列表
		where
			条件列表
	    group by
	    	分组字段
	    having
	    	分组之后的条件
	    order by
	    	排序
	    limit
	    	分页限定
	```
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
8. 用选择限制行(条件查询 where子句后跟条件)
   
    * `select * from emp where job = clerk;`
    
    * 运算符:
        *  >	<	>=	<=	=	<>
		* BETWEEN  AND
		* IN(集合)
		* LIKE
		* IS NULL
		* AND 或者 &&
		* OR  或者 ||
		* NOT 或者 !
9. 模糊查询
	* 占位符
		* _:单个任意字符
		* %:多个任意字符
		* 示例:
			1. 从学生表中查询姓马的同学;
				* ` select * from student where name like '马%';`
			2. 从学生表中查询第二个字是"化"的同学;
				* `select * from student where name like '_化%';`
			3. 从学生表中查询姓名是三个字的同学;
				* `select * from student where name like '___';`
			4. 查询姓名中包含"德"的同学;
				* `select * from student where name like '德';`
10. 字符串和日期
   
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

* 概念： 对表中的数据进行限定，保证数据的正确性、有效性和完整性。	

* 分类：
		
	1. 主键约束：`primary key`
	2. 非空约束：`not null`
	3. 唯一约束：`unique`
	4. 外键约束：`foreign key`

###### 1. 非空约束：`not null，值不能为null`

1. 创建表时添加约束

	``` SQL
	CREATE TABLE stu(
		id INT,
		NAME VARCHAR(20) NOT NULL -- name为非空
	);
	```
2. 创建表完后，添加非空约束`ALTER TABLE stu MODIFY NAME VARCHAR(20) NOT NULL;`

3. 删除name的非空约束`ALTER TABLE stu MODIFY NAME VARCHAR(20);`	

###### 2. 唯一约束：unique，值不能重复

1. 创建表时，添加唯一约束
	```SQL
	CREATE TABLE stu(
		id INT,
		phone_number VARCHAR(20) UNIQUE -- 添加了唯一约束
	);
	-- 注意mysql中，唯一约束限定的列的值可以有多个null
	```
2. 删除唯一约束`ALTER TABLE stu DROP INDEX phone_number;`
3. 在创建表后，添加唯一约束`ALTER TABLE stu MODIFY phone_number VARCHAR(20) UNIQUE;`

###### 3. 主键约束：primary key。

1. ==注意：==
	1. 含义：非空且唯一
	2. 一张表只能有一个字段为主键
	3. 主键就是表中记录的唯一标识

2. 在创建表时，添加主键约束
	``` SQL
	create table stu(
		id int primary key,-- 给id添加主键约束
		name varchar(20)
	);
	```
3. 删除主键
	==-- 错误 alter table stu modify id int ;==
	`ALTER TABLE stu DROP PRIMARY KEY;`

4.  创建完表后，添加主键
	`ALTER TABLE stu MODIFY id INT PRIMARY KEY;`

5.  自动增长:
	
	1. 概念：如果某一列是数值类型的，使用 auto_increment 可以来完成值得自动增长
	2. 在创建表时，添加主键约束，并且完成主键自增长
	
	```SQL
		create table stu(
				id int primary key auto_increment,-- 给id添加主键约束
				name varchar(20)
		);
	```

	3. 删除自动增长`ALTER TABLE stu MODIFY id INT;`
	
	4. 添加自动增长`ALTER TABLE stu MODIFY id INT AUTO_INCREMENT;`

###### 4.外键约束:foreign key,让表于表产生关系，从而保证数据的正确性。

1. 在创建表时，可以添加外键

	``` SQL
    create table 表名(
	....
	外键列
	constraint 外键名称 foreign key (外键列名称) references 主表名称(主表列名称)
);
	```
2. 删除外键ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;

3. 创建表之后，添加外键

    **==ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称);==**

4. 级联操作

    1. 添加级联操作
       
        * 语法：
        
	```SQL
		ALTER TABLE 表名 ADD CONSTRAINT 外键名称 
		FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称) ON
		UPDATE CASCADE ON DELETE CASCADE;
	```
	```
	2. 分类：
        1. 级联更新：`ON UPDATE CASCADE `
        2. 级联删除：`ON DELETE CASCADE `
    ```

##### 3.多表之间的关系

###### 1.分类
1. 一对一(了解)：
    * 如：人和身份证
    * 分析：一个人只有一个身份证，一个身份证只能对应一个人

2. 一对多(多对一)：

    * 如：部门和员工

    * 分析：一个部门有多个员工，一个员工只能对应一个部门

3. 多对多：

    * 如：学生和课程

    * 分析：一个学生可以选择很多门课程，一个课程也可以被很多学生选择

###### 2.实现关系
1. 一对多(多对一)：
	* 如：部门和员工
	* 实现方式：在多的一方建立外键，指向一的一方的主键。
2. 多对多：
	* 如：学生和课程
	* 实现方式：多对多关系实现需要借助第三张中间表。中间表至少包含两个字段，这两个字段作为第三张表的外键，分别指向两张表的主键
3. 一对一(了解)：
	* 如：人和身份证
	* 实现方式：一对一关系实现，可以在任意一方添加唯一外键指向另一方的主键。
###### 3.案例

```SQL
-- 创建旅游线路分类表 tab_category
-- cid 旅游线路分类主键，自动增长
-- cname 旅游线路分类名称非空，唯一，字符串 100
CREATE TABLE tab_category (
	cid INT PRIMARY KEY AUTO_INCREMENT,
	cname VARCHAR(100) NOT NULL UNIQUE
);

-- 创建旅游线路表 tab_route
/*
rid 旅游线路主键，自动增长
rname 旅游线路名称非空，唯一，字符串 100
price 价格
rdate 上架时间，日期类型
cid 外键，所属分类
*/
CREATE TABLE tab_route(
	rid INT PRIMARY KEY AUTO_INCREMENT,
	rname VARCHAR(100) NOT NULL UNIQUE,
	price DOUBLE,
	rdate DATE,
	cid INT,
	FOREIGN KEY (cid) REFERENCES tab_category(cid)
);

/*创建用户表 tab_user
uid 用户主键，自增长
username 用户名长度 100，唯一，非空
password 密码长度 30，非空
name 真实姓名长度 100
birthday 生日
sex 性别，定长字符串 1
telephone 手机号，字符串 11
email 邮箱，字符串长度 100
*/
CREATE TABLE tab_user (
	uid INT PRIMARY KEY AUTO_INCREMENT,
	username VARCHAR(100) UNIQUE NOT NULL,
	PASSWORD VARCHAR(30) NOT NULL,
	NAME VARCHAR(100),
	birthday DATE,
	sex CHAR(1) DEFAULT '男',
	telephone VARCHAR(11),
	email VARCHAR(100)
);

/*
创建收藏表 tab_favorite
rid 旅游线路 id，外键
date 收藏时间
uid 用户 id，外键
rid 和 uid 不能重复，设置复合主键，同一个用户不能收藏同一个线路两次
*/
CREATE TABLE tab_favorite (
	rid INT, -- 线路id
	DATE DATETIME,
	uid INT, -- 用户id
	-- 创建复合主键
	PRIMARY KEY(rid,uid), -- 联合主键
	FOREIGN KEY (rid) REFERENCES tab_route(rid),
	FOREIGN KEY(uid) REFERENCES tab_user(uid)
);
```
##### 4.范式
###### 1.概念：

* 设计数据库时，需要遵循的一些规范。要遵循后边的范式要求，必须先遵循前边的所有范式要求,设计关系数据库时，遵从不同的规范要求，设计出合理的关系型数据库，这些不同的规范要求被称为不同的范式，各种范式呈递次规范，越高的范式数据库冗余越小。目前关系数据库有六种范式：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、第四范式(4NF）和第五范式（5NF，又称完美范式）。

###### 2.分类：
1. 第一范式（1NF）：每一列都是不可分割的原子数据项
2. 第二范式（2NF）：在1NF的基础上，非码属性必须完全依赖于码（在1NF基础上消除非主属性对主码的部分函数依赖）

    * 几个概念：

        1. 函数依赖：A-->B,如果通过A属性(属性组)的值，可以确定唯一B属性的值。则称B依赖于A\
            * 例如：学号-->姓名。  （学号，课程名称） --> 分数

        2. 完全函数依赖：A-->B， 如果A是一个属性组，则B属性值得确定需要依赖于A属性组中所有的属性值。
            * 例如：（学号，课程名称） --> 分数

        3. 部分函数依赖：A-->B， 如果A是一个属性组，则B属性值得确定只需要依赖于A属性组中某一些值即可。
            * 例如：（学号，课程名称） -- > 姓名

        4. 传递函数依赖：A-->B, B -- >C . 如果通过A属性(属性组)的值，可以确定唯一B属性的值，在通过B属性（属性组）的值可以确定唯一C属性的值，则称 C 传递函数依赖于A
            * 例如：学号-->系名，系名-->系主任

        5. 码：如果在一张表中，一个属性或属性组，被其他所有属性所完全依赖，则称这个属性(属性组)为该表的码
            * 例如：该表中码为：（学号，课程名称）

        6. 主属性：码属性组中的所有属性

        7. 非主属性：除过码属性组的属性

3. 第三范式（3NF）：在2NF基础上，任何非主属性不依赖于其它非主属性（在2NF基础上消除传递依赖）

##### 5.数据库的备份和还原

* 语法：
		* 备份： mysqldump -u用户名 -p密码 数据库名称 > 保存的路径
	* 还原：
		1. 登录数据库
		2. 创建数据库
		3. 使用数据库
		4. 执行文件。source 文件路径

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

4. D(Delete) : 删除

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
	
	` alter table 表名 change 列名 新列名 新数据类型`<!-- 修改列名和数据类型-->
	` alter table 表名 modify 列名 新数据类型`<!-- 修改列名-->
	
	5.删除列	`  alter table 表名 drop 列名`
	
4. D(Delete) : 删除
  * 删除数据表 ` drop table tableName`
  * 判断是否存在,存在就删除 ` drop table if exists tableName;`