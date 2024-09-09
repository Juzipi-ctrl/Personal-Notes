# MySQL1

## 数据导出与导入

### 1.导出整个数据库

```mysql
mysqldump -u 用户名 -p 数据库名 > 导出的文件名
mysqldump -u dbuser -p dbname > dbname.sql
```

### 2.导出一个表

```mysql
mysqldump -u 用户名 -p 数据库名 表名> 导出的文件名
mysqldump -u dbuser -p dbname users> dbname_users.sql
```

### 3.导出一个数据库结构

```mysql
mysqldump -u dbuser -p -d --add-drop-table dbname >d:/dbname_db.sql
-d 没有数据 --add-drop-table 在每个create语句之前增加一个drop table
```

### 4.导入数据库

```mysql
# 常用source 命令
# 进入mysql数据库控制台，如
mysql -u root -p
mysql>use 数据库
# 然后使用source命令，后面参数为脚本文件(如这里用到的.sql)
mysql>source d:/dbname.sql

mysql -uroot -p -t mysql数据
```

 

## 1、SQL 基础

#### 1.连接数据库

语法：链接到 MySQL 服务器

```mysql
mysql -u root -p
```

以上命令中，mysql 代表客户端命令，-u 后面跟连接的数据库用户， -p 表示需要输入密码。

#### 2.创建数据库命令

```mysql
create databse tname;

mysql> create database test1;
Query OK, 1 row affected (0.00 sec)
```

#### 3.查询存在数据库

```mysql
show databases;

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema 
| sys                |
| test1              |
+--------------------+
5 rows in set (0.04 sec)
```

#### 4.选择数据库

```mysql
use dbname;

mysql> use test1;
Database changed
```

#### 5.查看数据表

```mysql
show tables;

mysql> show tables;
+-----------------+
| Tables_in_test1 |
+-----------------+
| emp             |
+-----------------+
1 row in set (0.00 sec)
```

#### 6.删除数据库

```mysql
drop database dbname;

mysql> drop database test1; 
Query OK, 0 rows affected (0.00 sec)
```

#### 7.创建表

```mysql
# 格式
create table [if not exists] `表名` (
    `字段名` 列属性 [属性] [索引] [注释]
)[表类型] [字符集设置] [注释]


CREATE TABLE tablename (
    column_name_1 
    column_type_1 
    constraints，
	column_name_2
	column_type_2
	constraints
	，
	……column_name_n
	column_type_n
	constraints
 );
```

columc_name 是列的名字，columnn_type 是列的数据类型， contraints 是这个列的约束。

#### 8.查看表定义

```mysql
desc tablename;		# tablename 是表名

mysql> desc emp;
+----------+---------------+------+-----+---------+-------+
| Field    | Type          | Null | Key | Default | Extra |
+----------+---------------+------+-----+---------+-------+
| ename    | varchar(20)   | YES  |     | NULL    |       |
| hiredate | date          | YES  |     | NULL    |       |
| sal      | decimal(10,2) | YES  |     | NULL    |       |
| deptno   | int           | YES  |     | NULL    |       |
+----------+---------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

#### 9.查看完整表定义

```mysql
show create table tablename \G;

mysql> show create table emp \G;
*************************** 1. row ***************************
       Table: emp
Create Table: CREATE TABLE `emp` (
  `ename` varchar(20) DEFAULT NULL,
  `hiredate` date DEFAULT NULL,
  `sal` decimal(10,2) DEFAULT NULL,
  `deptno` int DEFAULT NULL,
  `age` int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
1 row in set (0.01 sec)

ERROR:
No query specified
```

#### 10.删除表

```mysql
drop table tablename;  # 当这张表不存在的时候会报错！

drop table if existe tablename;		# 如果这张表存在的话，删除。

mysql> drop table emp;
Query OK, 0 rows affected (0.00 sec)
```

#### 11.修改表

修改表类型，语法如下：

```mysql
ALTER TABLE tablename MODIFY [COLUMN] column_definition [FIRST | AFTER col_name];
# 例如：修改emp的ename字段定义，将 varchar(10) 改为 varchar(20)
alter table emp modify ename varchar(20);

alter table emp modify ename varchar(20);
Query OK, 0 rows affected (0.03 sec)
Records: 0 Duplicates: 0 Warnings: 0
```

#### 12.增加字段

语法如下：

```mysql
ALTER TABLE tablename ADD [COLUMN] column_definition [FIRST | AFTER col_name]
# 例如： 表 emp 上增加字段 age， 类型为 Int(3)：
alter table emp add column age int(3);

mysql> alter table emp add column age int(3);
Query OK, 0 rows affected (0.03 sec)
Records: 0 Duplicates: 0 Warnings: 0
```

#### 13.删除字段（数据）

语法如下：

```mysql
# 方法一： 效率低
delete from 表名;
	# 删除后可以回滚
rollback;

# 方法二：效率高
# 使用truncate语句进行删除，但要注意的是此种方法删除后无法使用 rollback 进行回滚恢复。
truncate table 表名； #（这种操作属于 ddl）


# 方法三：
ALTER TABLE tablename DROP [COLUMN] col_name
# 例如：将字段 age 删除掉：
alter table emp drop column age;

mysql> alter table emp drop column age;
Query OK, 0 rows affected (0.04 sec)
Records: 0 Duplicates: 0 Warnings: 0
```

#### 14.字段改名

语法如下：

```mysql
ALTER TABLE tablename CHANGE [COLUMN] old_col_name column_definition [FIRST|AFTER col_name]
# 例如： 将 age 改名为 age1， 同时修改字段类型为 int(4):
alter table emp change age age1 int(4);

mysql> alter table emp change age age1 int(4) ;
Query OK, 0 rows affected (0.02 sec)
Records: 0 Duplicates: 0 Warnings: 0
```

注意：change 和 modify 都可以修改表的定义，不同的是 change 后面需要写两次列名，不方便。但是 change 的优点是可以修改列名称， modify 则不能。

#### 15.修改字段排列顺序

前面的字段增加和修改语法（ADD/CHANGE/MODIFY）中，都有一个可选择 `first|after` columu_name,这个选项可以用来修改字段在表中的位置，默认 add 增加的新字段是加在表的最后位置，而 change/modify 默认都不会改变字段的位置。

- first 放置到最前。
- arter 可指定放置。

例如1：将新的字段 birth data 加在 ename 之后：

```mysql
alter table emp add birth date after ename;

mysql> alter table emp add birth date after ename;
Query OK, 0 rows affected (0.07 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc emp;
+----------+---------------+------+-----+---------+-------+
| Field    | Type          | Null | Key | Default | Extra |
+----------+---------------+------+-----+---------+-------+
| ename    | varchar(20)   | YES  |     | NULL    |       |
| birth    | date          | YES  |     | NULL    |       |
| hiredate | date          | YES  |     | NULL    |       |
| sal      | decimal(10,2) | YES  |     | NULL    |       |
| deptno   | int           | YES  |     | NULL    |       |
| age      | int           | YES  |     | NULL    |       |
+----------+---------------+------+-----+---------+-------+
6 rows in set (0.01 sec)
```

例如2：修改字段 age， 将它放在最前面：

```mysql
alter table emp modify age int(3)  first;

mysql> alter table emp modify age int(3) first;
Query OK, 0 rows affected, 1 warning (0.08 sec)
Records: 0  Duplicates: 0  Warnings: 1

mysql> desc emp;
+----------+---------------+------+-----+---------+-------+
| Field    | Type          | Null | Key | Default | Extra |
+----------+---------------+------+-----+---------+-------+
| age      | int           | YES  |     | NULL    |       |
| ename    | varchar(20)   | YES  |     | NULL    |       |
| birth    | date          | YES  |     | NULL    |       |
| hiredate | date          | YES  |     | NULL    |       |
| sal      | decimal(10,2) | YES  |     | NULL    |       |
| deptno   | int           | YES  |     | NULL    |       |
+----------+---------------+------+-----+---------+-------+
6 rows in set (0.00 sec)
```

#### 16.表改名

语法如下：

```mysql
ALTER TABLE tablename RENAME [TO] new_tablename

mysql> alter table emp rename emp1;
Query OK, 0 rows affected (0.00 sec)
```

#### 17.查看数据库版本号

```mysql
select version();

mysql> select version();
+-------------------------+
| version()               |
+-------------------------+
| 8.0.33-0ubuntu0.22.04.2 |
+-------------------------+
1 row in set (0.00 sec)
```

#### 18.查看当前使用的数据库

```mysql
select database();

mysql> select database();
+------------+
| database() |
+------------+
| test1      |
+------------+
1 row in set (0.00 sec)
```

#### 19.创建用户

```mysql
# 创建用户 create user 用户名 identified by '密码'
create user caibai identified by '123456';

# 修改密码（修改当前用户密码）
set password = password('密码');

# 修改密码 （修改指定用户密码）
set password for 用户名 = password('密码');

# 重命名
rename user 旧名 to 新名;

# 用户授权 全部的权限  to 用户名
grant all privileges on *.* to 用户名;

# 查看权限
show grants for 用户名;   # GRANT USAGE ON *.* TO `caibai`@`%`

# 撤销权限
revoke all privileges on *.* from 用户名;
```

#### 20.修改表中的特定某一个值

```mysql
# 语法
UPDATE table_name
SET column_name = new_value
WHERE condition;

# 解析
UPDATE 		#语句用于更新表中的数据。
table_name 	#是要更新的表名。
column_name #是要修改的字段名。
new_value 	#是要将字段修改为的新值。
WHERE 		#子句是可选的，用于指定更新的条件。只有符合条件的行才会被更新，如果省略 WHERE 子句，则会更新表中所有行。

# 示例
UPDATE employees
SET salary = 5000
WHERE id = 1;

# 解析：这个示例将名为 "employees" 的表中，ID 为 1 的员工的薪水字段（假设为 "salary"）修改为新值 5000。只有符合条件的行（ID = 1 的员工）会受到影响。
```





## 1、DML 语句

DML 操作是指针对数据库中表记录的操作，主要包括表记录的插入（insert）、更新（update）、删除（delete）和查询（select）。

#### 1.插入记录

插入记录，基本语法如下：

```mysql
INSERT INTO tablename (field1,field2,……fieldn) VALUES(value1,value2,……valuesn);
```

例如：向表 emp 中插入记录：ename 为 zzx1, hiredate 为 2000-01-01， sal 为 2000， deptno 为 1， 命令如下：

```mysql
insert into emp (ename, hiredate, sal, deptno) values('zzx1', '2000-01-01', '2000', 1);

mysql> insert into emp (ename, hiredate, sal, deptno) values('zzx1', '2000-01-01', '2000', 1);

Query OK, 1 row affected (0.02 sec)
```

也可以不指定字段名称，但是 values 后面的顺序应该和字段的排列顺序一致：

```mysql
insert into emp values('lisa', '2003-02-01', '3000', 2);

mysql> insert into emp values('lisa', '2003-02-01', '3000', 2);
Query OK, 1 row affected (0.02 sec)
```

对于含可空字段、非空但是含有默认值的字段、自增字段，可以不用在 insert 后的字段列表里面出现，values 后面只写对应字段名称的 value，这些没写的字段可以自动设置为 NULL、默认值、自增的下一个数字，这样在某些情况下可以大大缩短 SQL 语句的复杂性。例如，只对表中的 ename 和 sal 字段显式插入值：

```mysql
insert into emp (ename,sal) values('dony',1000);

mysql> insert into emp (ename,sal) values('dony',1000);
Query OK, 1 row affected (0.02 sec)
```

查看：

```mysql
mysql> select * from emp;
+-------+------------+---------+--------+
| ename | hiredate   | sal     | deptno |
+-------+------------+---------+--------+
| zzx1  | 2000-01-01 | 2000.00 |      1 |
| lisa  | 2003-02-01 | 3000.00 |      2 |
| dony  | NULL       | 1000.00 |   NULL |
+-------+------------+---------+--------+
3 rows in set (0.00 sec)
```

果然，设置为可空的两个字段都显示为 NULL。

在 MySQL 中， insert 语句还有一个很好的特性，可以一次性插入多条记录，语法如下：

```mysql
INSERT INTO tablename (field1, field2,……fieldn)
VALUES
(record1_value1, record1_value2,……record1_valuesn),
(record2_value1, record2_value2,……record2_valuesn),
……
(recordn_value1, recordn_value2,……recordn_valuesn)
;
```

可以看出，每条记录之间都用逗号进行了分隔。

以下例子中，对表 dept 一次插入两条记录：

```mysql
insert into emp (ename, sal) values('dept5',5),('dept6',6);

mysql> insert into emp (ename, sal) values('dept5',5),('dept6',6);
Query OK, 2 rows affected (0.00 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from emp;
+-------+------------+---------+--------+
| ename | hiredate   | sal     | deptno |
+-------+------------+---------+--------+
| zzx1  | 2000-01-01 | 2000.00 |      1 |
| lisa  | 2003-02-01 | 3000.00 |      2 |
| dony  | NULL       | 1000.00 |   NULL |
| dept5 | NULL       |    5.00 |   NULL |
| dept6 | NULL       |    6.00 |   NULL |
+-------+------------+---------+--------+
5 rows in set (0.00 sec)
```

#### 2.更新记录

对于表里的记录值，可以通过 update 命令进行更改，语法如下：

```mysql
UPDATE tablename SET field1=value1，field2.=value2，……fieldn=valuen [WHERE CONDITION]
例如： 将表 emp 中 ename 为 “lisa” 的薪水 （sal） 从 3000 更改为 4000；
update emp set sal=4000 where ename='lisa';

mysql> update emp set sal=4000 where ename='lisa';
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from emp;
+-------+------------+---------+--------+
| ename | hiredate   | sal     | deptno |
+-------+------------+---------+--------+
| zzx1  | 2000-01-01 | 2000.00 |      1 |
| lisa  | 2003-02-01 | 4000.00 |      2 |
| dony  | NULL       | 1000.00 |   NULL |
| dept5 | NULL       |    5.00 |   NULL |
| dept6 | NULL       |    6.00 |   NULL |
+-------+------------+---------+--------+
5 rows in set (0.00 sec)

```

在 mysql中，update 命令可以同时更新多个表中数据，语法如下：

```mysql
UPDATE t1,t2…tn set t1.field1=expr1,tn.fieldn=exprn [WHERE CONDITION]
例如：同时更新表 emp 中的字段 sal 和表 dept 中的字段 deptname:

mysql> select * from emp;
+--------+------------+---------+--------+
| ename | hiredate | sal | deptno |
+--------+------------+---------+--------+
| zzx | 2000-01-01 | 100.00 | 1 |
| lisa | 2003-02-01 | 200.00 | 2 |
| bjguan | 2004-04-02 | 100.00 | 1 |
| dony | 2005-02-05 | 2000.00 | 4 |
+--------+------------+---------+--------+
4 rows in set (0.00 sec)


mysql> select * from dept;
+--------+----------+
| deptno | deptname |
+--------+----------+
| 1 | tech |
| 2 | sale |
| 5 | fin |
+--------+----------+
3 rows in set (0.00 sec)

update emp a,dept b set a.sal=a.sal*b.deptno,b.deptname=a.ename where a.deptno=b.deptno;

mysql>update emp a,dept b set a.sal=a.sal*b.deptno,b.deptname=a.ename where a.deptno=b.deptno;
Query OK, 3 rows affected (0.04 sec)
Rows matched: 5 Changed: 3 Warnings: 0

mysql> select * from emp;
+--------+------------+---------+--------+
| ename | hiredate | sal | deptno |
+--------+------------+---------+--------+
| zzx | 2000-01-01 | 100.00 | 1 |
| lisa | 2003-02-01 | 400.00 | 2 |
| bjguan | 2004-04-02 | 100.00 | 1 |
| dony | 2005-02-05 | 2000.00 | 4 |
+--------+------------+---------+--------+
4 rows in set (0.01 sec)

mysql> select * from dept;
+--------+----------+
| deptno | deptname |
+--------+----------+
| 1 | zzx |
| 2 | lisa |
| 5 | fin |
+--------+----------+
3 rows in set (0.00 sec)
```

#### 3.删除记录

如果记录不再需要，可以用 delete 命令进行删除，语法如下：

```mysql
DELETE FROM tablename [WHERE CONDITION]
例如：再emp中将 ename 为 ‘dony’ 的记录全部删除，命令如下：
mysql> delete from emp where ename='dony';
Query OK, 1 row affected (0.00 sec)
```

再 mysql 中可以一次删除多个表的数据，语法如下：

```mysql
DELETE t1,t2…tn FROM t1,t2…tn [WHERE CONDITION]
```

如果 from 后面的表名用别名，则 delete 后面的也要用相应的别名，否则会提示语法错误。

再下列中，将表 emp 和 dept 中 deptno 为 3 的记录同时都删除：

```mysql
mysql> select * from emp;
+--------+------------+---------+--------+
| ename | hiredate | sal | deptno |
+--------+------------+---------+--------+
| zzx | 2000-01-01 | 100.00 | 1 |
| lisa | 2003-02-01 | 200.00 | 2 |
| bjguan | 2004-04-02 | 100.00 | 1 |
| bzshen | 2005-04-01 | 300.00 | 3 |
| dony | 2005-02-05 | 2000.00 | 4 |
+--------+------------+---------+--------+
5 rows in set (0.00 sec)

mysql> select * from dept;
+--------+----------+
| deptno | deptname |
+--------+----------+
| 1 | tech |
| 2 | sale |
| 3 | hr |
| 5 | fin |
+--------+----------+
4 rows in set (0.00 sec)

mysql> delete a,b from emp a,dept b where a.deptno=b.deptno and a.deptno=3;
Query OK, 2 rows affected (0.04 sec)

mysql> select * from emp;
+--------+------------+---------+--------+
| ename | hiredate | sal | deptno |
+--------+------------+---------+--------+
| zzx | 2000-01-01 | 100.00 | 1 |
| lisa | 2003-02-01 | 200.00 | 2 |
| bjguan | 2004-04-02 | 100.00 | 1 |
| dony | 2005-02-05 | 2000.00 | 4 |
+--------+------------+---------+--------+
4 rows in set (0.00 sec)
mysql> select * from dept;
+--------+----------+
| deptno | deptname |
+--------+----------+
| 1 | tech |
| 2 | sale |
| 5 | fin |
+--------+----------+
3 rows in set (0.00 sec)
```

注意：不管是单表还是多表，不加 where 条件将会把表的所有记录删除，所以操作是一定要小心。

#### 4.查询记录

数据插入到数据库中后，就可以用 select 命令进行各种各样的查询，使得输出的结果符合要求。

语法：

```mysql
SELECT * FROM tablename [WHERE CONDITION]

select * form emp;

mysql> select * from emp;
+-------+------------+---------+--------+
| ename | hiredate   | sal     | deptno |
+-------+------------+---------+--------+
| zzx1  | 2000-01-01 | 2000.00 |      1 |
| lisa  | 2003-02-01 | 4000.00 |      2 |
| dony  | NULL       | 1000.00 |   NULL |
| dept5 | NULL       |    5.00 |   NULL |
| dept6 | NULL       |    6.00 |   NULL |
+-------+------------+---------+--------+
5 rows in set (0.02 sec)

mysql> desc Student;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| s_id    | varchar(20) | NO   | PRI | NULL    |       |
| s_name  | varchar(20) | NO   |     |         |       |
| s_birth | varchar(20) | NO   |     |         |       |
| s_sex   | varchar(10) | NO   |     |         |       |
+---------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

完整语法：

```mysql
select 
	...
where
	...
group by
	...
having
	...
order by
	...
limit 
	...
```





##### 查询学生名字

```mysql
select s_name from Student;

mysql> select s_name from Student;
+--------+
| s_name |
+--------+
| 赵雷   |
| 钱电   |
| 孙风   |
| 李云   |
| 周梅   |
| 吴兰   |
| 郑竹   |
| 王菊   |
+--------+
8 rows in set (0.00 sec)
```

##### 多字段查询

使用多字段查询可以使用逗号隔开；

```mysql
select s_id, s_name, s_birth from Student;

mysql> select s_id, s_name, s_birth from Student;
+------+--------+------------+
| s_id | s_name | s_birth    |
+------+--------+------------+
| 01   | 赵雷   | 1990-01-01 |
| 02   | 钱电   | 1990-12-21 |
| 03   | 孙风   | 1990-05-20 |
| 04   | 李云   | 1990-08-06 |
| 05   | 周梅   | 1991-12-01 |
| 06   | 吴兰   | 1992-03-01 |
| 07   | 郑竹   | 1989-07-01 |
| 08   | 王菊   | 1990-01-20 |
+------+--------+------------+
8 rows in set (0.00 sec)
```

##### 使用as别名多字段查询

注意：此操作只是将查询结果列名别名作为显示结果。

```mysql
select s_id, s_name, s_birth as shengri from Student;

mysql> select s_id, s_name, s_birth as shengri from Student;
+------+--------+------------+
| s_id | s_name | shengri    |
+------+--------+------------+
| 01   | 赵雷   | 1990-01-01 |
| 02   | 钱电   | 1990-12-21 |
| 03   | 孙风   | 1990-05-20 |
| 04   | 李云   | 1990-08-06 |
| 05   | 周梅   | 1991-12-01 |
| 06   | 吴兰   | 1992-03-01 |
| 07   | 郑竹   | 1989-07-01 |
| 08   | 王菊   | 1990-01-20 |
+------+--------+------------+
8 rows in set (0.00 sec)


select s_id, s_name, s_birth 'sheng ri' from Student;

mysql> select s_id, s_name, s_birth 'sheng ri' from Student;
+------+--------+------------+
| s_id | s_name | sheng ri   |
+------+--------+------------+
| 01   | 赵雷   | 1990-01-01 |
| 02   | 钱电   | 1990-12-21 |
| 03   | 孙风   | 1990-05-20 |
| 04   | 李云   | 1990-08-06 |
| 05   | 周梅   | 1991-12-01 |
| 06   | 吴兰   | 1992-03-01 |
| 07   | 郑竹   | 1989-07-01 |
| 08   | 王菊   | 1990-01-20 |
+------+--------+------------+
8 rows in set (0.00 sec)
```

##### 查询不重复的记录

有时候需要将表中的记录去掉重复后显示出来，可以用 distint 关键字来实现：

注意：只能在所有字段之前使用。

```mysql
select ename, hiredate, sal, deptno from emp;

mysql> select * from emp;
+-------+------------+---------+--------+
| ename | hiredate   | sal     | deptno |
+-------+------------+---------+--------+
| zzx1  | 2000-01-01 | 2000.00 |      1 |
| lisa  | 2003-02-01 | 4000.00 |      2 |
| dony  | 2004-03-01 | 1000.00 |      1 |
| dept5 | 2005-04-01 |    5.00 |      2 |
| dept6 | NULL       |    6.00 |   NULL |
+-------+------------+---------+--------+
5 rows in set (0.00 sec)

select distinct deptno from emp;

mysql> select distinct deptno from emp;
+--------+
| deptno |
+--------+
|      1 |
|      2 |
|   NULL |
+--------+
3 rows in set (0.00 sec)

select count(distinct deptno) as ecount from emp;

mysql> select count(distinct deptno) as ecount from emp;
+--------+
| ecount |
+--------+
|      2 |
+--------+
1 row in set (0.00 sec)
```

##### 条件查询



```mysql
select
	字段1，字段2，子段3....
from
	表名
where
	条件；
```

##### 条件

‘=’ 等于

‘<>’或‘!=’不等于

‘<’ 小于

‘<=’小于等于

‘>’ 大于

‘>=’大于等于



使用 where 关键字可以来实现这样的操作。

例如1：，需要查询所有 deptno 为 1 的记录： ‘=’ 等于

```mysql
select * from emp where deptno=1;

mysql> select * from emp;
+-------+------------+---------+--------+
| ename | hiredate   | sal     | deptno |
+-------+------------+---------+--------+
| zzx1  | 2000-01-01 | 2000.00 |      1 |
| lisa  | 2003-02-01 | 4000.00 |      2 |
| dony  | 2004-03-01 | 1000.00 |      1 |
| dept5 | 2005-04-01 |    5.00 |      2 |
| dept6 | NULL       |    6.00 |   NULL |
+-------+------------+---------+--------+
5 rows in set (0.00 sec)

mysql> select deptno from emp where deptno=1;
+--------+
| deptno |
+--------+
|      1 |
|      1 |
+--------+
2 rows in set (0.00 sec)
```

例如2：查询不等于 1995-12-01 的数据 ‘<>’或‘!=’不等于

```mysql
方法一：
select emp_no,title,from_date,to_date from titles where to_date!='1995-12-01' limit 10;

方法二：
select emp_no,title,from_date,to_date from titles where to_date<>'1995-12-01' limit 10;


mysql> select emp_no,title,from_date,to_date from titles where to_date!='1995-12-01' limit 10;
+--------+--------------------+------------+------------+
| emp_no | title              | from_date  | to_date    |
+--------+--------------------+------------+------------+
|  10001 | Senior Engineer    | 1986-06-26 | 9999-01-01 |
|  10002 | Staff              | 1996-08-03 | 9999-01-01 |
|  10003 | Senior Engineer    | 1995-12-03 | 9999-01-01 |
|  10004 | Senior Engineer    | 1995-12-01 | 9999-01-01 |
|  10005 | Senior Staff       | 1996-09-12 | 9999-01-01 |
|  10005 | Staff              | 1989-09-12 | 1996-09-12 |
|  10006 | Senior Engineer    | 1990-08-05 | 9999-01-01 |
|  10007 | Senior Staff       | 1996-02-11 | 9999-01-01 |
|  10007 | Staff              | 1989-02-10 | 1996-02-11 |
|  10008 | Assistant Engineer | 1998-03-11 | 2000-07-31 |
+--------+--------------------+------------+------------+
10 rows in set (0.00 sec)
```

例如3：找出薪资小于 60000 的 ‘<’ 小于

```mysql
select emp_no,salary,from_date,to_date from salaries where salary < 60000 limit 10;

mysql> select emp_no,salary,from_date,to_date from salaries where salary < 60000 limit 10;
+--------+--------+------------+------------+
| emp_no | salary | from_date  | to_date    |
+--------+--------+------------+------------+
|  10003 |  40006 | 1995-12-03 | 1996-12-02 |
|  10003 |  43616 | 1996-12-02 | 1997-12-02 |
|  10003 |  43466 | 1997-12-02 | 1998-12-02 |
|  10003 |  43636 | 1998-12-02 | 1999-12-02 |
|  10003 |  43478 | 1999-12-02 | 2000-12-01 |
|  10003 |  43699 | 2000-12-01 | 2001-12-01 |
|  10003 |  43311 | 2001-12-01 | 9999-01-01 |
|  10004 |  40054 | 1986-12-01 | 1987-12-01 |
|  10004 |  42283 | 1987-12-01 | 1988-11-30 |
|  10004 |  42542 | 1988-11-30 | 1989-11-30 |
+--------+--------+------------+------------+
10 rows in set (0.00 sec)
```

例如4：查找 emp_no 编号 10003 的 salary 那些 

```mysql
select emp_no,salary, from_date, to_date from salaries where emp_no = 10003 limit 10;

mysql> select emp_no,salary, from_date, to_date from salaries where emp_no = 10003 limit 10;
+--------+--------+------------+------------+
| emp_no | salary | from_date  | to_date    |
+--------+--------+------------+------------+
|  10003 |  40006 | 1995-12-03 | 1996-12-02 |
|  10003 |  43616 | 1996-12-02 | 1997-12-02 |
|  10003 |  43466 | 1997-12-02 | 1998-12-02 |
|  10003 |  43636 | 1998-12-02 | 1999-12-02 |
|  10003 |  43478 | 1999-12-02 | 2000-12-01 |
|  10003 |  43699 | 2000-12-01 | 2001-12-01 |
|  10003 |  43311 | 2001-12-01 | 9999-01-01 |
+--------+--------+------------+------------+
7 rows in set (0.00 sec)
```

 例如5：查找一个区间的薪资大于等于 40000  小于等于 70000  and 或者 between ... and

```mysql
方法一：
select emp_no,salary, from_date, to_date from salaries where salary >= 40000 and salary <= 70000 limit 10;

方法二：
select emp_no,salary, from_date, to_date from salaries where salary between 40000 and 70000 limit 10;

mysql> select emp_no,salary, from_date, to_date from salaries where salary >= 40000 and salary <= 70000 limit 10;
+--------+--------+------------+------------+
| emp_no | salary | from_date  | to_date    |
+--------+--------+------------+------------+
|  10001 |  60117 | 1986-06-26 | 1987-06-26 |
|  10001 |  62102 | 1987-06-26 | 1988-06-25 |
|  10001 |  66074 | 1988-06-25 | 1989-06-25 |
|  10001 |  66596 | 1989-06-25 | 1990-06-25 |
|  10001 |  66961 | 1990-06-25 | 1991-06-25 |
|  10002 |  65828 | 1996-08-03 | 1997-08-03 |
|  10002 |  65909 | 1997-08-03 | 1998-08-03 |
|  10002 |  67534 | 1998-08-03 | 1999-08-03 |
|  10002 |  69366 | 1999-08-03 | 2000-08-02 |
|  10003 |  40006 | 1995-12-03 | 1996-12-02 |
+--------+--------+------------+------------+
10 rows in set (0.00 sec)
```

以上的例子中， where 后面的条件是一个字段的‘=’比较，除了‘=’外，还可以使用 >,<,>=,<= != 等比较运算符；多个条件之间还可以使用 or，and 等逻辑运算符进行多条件联合查询。

以下是一个使用多字段条件查询的例子：

```mysql
select sal, deptno from emp where deptno=1 and sal<3000;

mysql> select sal, deptno from emp where deptno=1 and sal<3000;
+---------+--------+
| sal     | deptno |
+---------+--------+
| 2000.00 |      1 |
| 1000.00 |      1 |
+---------+--------+
2 rows in set (0.00 sec)
```

##### 查询指定显示条数

###### 扩展

可以使用关键字 limit 来实现，limit 语法如下：

```mysql
SELECT ……[LIMIT offset_start,row_count]
```

其中 offset_start 表示记录的起始偏移量，row_count 表示显示的行数。

1、sqlserver 数据库

```mysql
select top 10 * from table_name;
```

2、db2 数据库

```mysql
select * from table_name ferch first 10 rows only;
```

3、Oracle 数据库

```mysql
select * from table_name where rownum <= 20;
```

4、mysql 数据库

```mysql
select * from table_name limit 10;
```

5、lnformix 数据库

```mysql
select first 10 * from table_name;
```

6、Teradata 数据仓库

```mysql
select * from table_name sample 10;
```



例如：使用 limit 进行指定显示行数；

```mysql
select * from titles limit 5;

mysql> select * from titles limit 5;
+--------+-----------------+------------+------------+
| emp_no | title           | from_date  | to_date    |
+--------+-----------------+------------+------------+
|  10001 | Senior Engineer | 1986-06-26 | 9999-01-01 |
|  10002 | Staff           | 1996-08-03 | 9999-01-01 |
|  10003 | Senior Engineer | 1995-12-03 | 9999-01-01 |
|  10004 | Engineer        | 1986-12-01 | 1995-12-01 |
|  10004 | Senior Engineer | 1995-12-01 | 9999-01-01 |
+--------+-----------------+------------+------------+
5 rows in set (0.00 sec)

mysql> select emp_no, title, title, from_date, to_date from titles where to_date='1995-12-01' limit 10;

+--------+----------+----------+------------+------------+
| emp_no | title    | title    | from_date  | to_date    |
+--------+----------+----------+------------+------------+
|  10004 | Engineer | Engineer | 1986-12-01 | 1995-12-01 |
|  19397 | Staff    | Staff    | 1987-12-01 | 1995-12-01 |
|  20731 | Engineer | Engineer | 1990-12-01 | 1995-12-01 |
|  25692 | Staff    | Staff    | 1987-12-01 | 1995-12-01 |
|  28320 | Engineer | Engineer | 1989-12-01 | 1995-12-01 |
|  29888 | Engineer | Engineer | 1988-11-30 | 1995-12-01 |
|  33435 | Engineer | Engineer | 1987-12-01 | 1995-12-01 |
|  40537 | Staff    | Staff    | 1988-11-30 | 1995-12-01 |
|  48317 | Staff    | Staff    | 1986-12-01 | 1995-12-01 |
|  48487 | Engineer | Engineer | 1989-12-01 | 1995-12-01 |
+--------+----------+----------+------------+------------+
10 rows in set (0.01 sec)
```

例如6： 查询为空的（null） 使用 is null；

```mysql
select emp_no, title, title, from_date, to_date from titles where to_date is null limit 10;

```

例如7： 查询不为空的（null） 使用 is not null；

```mysql
select emp_no, title, title, from_date, to_date from titles where to_date is not null limit 10;

mysql> select emp_no, title, title, from_date, to_date from titles where to_date is not null limit 10;
+--------+-----------------+-----------------+------------+------------+
| emp_no | title           | title           | from_date  | to_date    |
+--------+-----------------+-----------------+------------+------------+
|  10001 | Senior Engineer | Senior Engineer | 1986-06-26 | 9999-01-01 |
|  10002 | Staff           | Staff           | 1996-08-03 | 9999-01-01 |
|  10003 | Senior Engineer | Senior Engineer | 1995-12-03 | 9999-01-01 |
|  10004 | Engineer        | Engineer        | 1986-12-01 | 1995-12-01 |
|  10004 | Senior Engineer | Senior Engineer | 1995-12-01 | 9999-01-01 |
|  10005 | Senior Staff    | Senior Staff    | 1996-09-12 | 9999-01-01 |
|  10005 | Staff           | Staff           | 1989-09-12 | 1996-09-12 |
|  10006 | Senior Engineer | Senior Engineer | 1990-08-05 | 9999-01-01 |
|  10007 | Senior Staff    | Senior Staff    | 1996-02-11 | 9999-01-01 |
|  10007 | Staff           | Staff           | 1989-02-10 | 1996-02-11 |
+--------+-----------------+-----------------+------------+------------+
10 rows in set (0.00 sec)
```

例如8：查找薪资等于 40000 又等于 70000 的，使用 or 或者 进行限定；

```mysql
select emp_no,birth_date,first_name,last_name,gender,hire_date from employees where last_name='Hofting' or last_name='Gomatam' limit 10;

mysql> select emp_no,birth_date,first_name,last_name,gender,hire_date from employees where last_name='Hofting' or last_name='Gomatam' limit 10;
+--------+------------+------------+-----------+--------+------------+
| emp_no | birth_date | first_name | last_name | gender | hire_date  |
+--------+------------+------------+-----------+--------+------------+
|  10090 | 1961-05-30 | Kendra     | Hofting   | M      | 1986-03-14 |
|  10091 | 1955-10-04 | Amabile    | Gomatam   | M      | 1992-11-18 |
|  11558 | 1959-06-20 | Sungwon    | Hofting   | M      | 1996-09-18 |
|  11662 | 1963-04-25 | Mokhtar    | Hofting   | M      | 1985-10-05 |
|  12259 | 1960-03-19 | Juichirou  | Hofting   | F      | 1998-05-26 |
|  13160 | 1958-05-09 | Shigeo     | Gomatam   | F      | 1994-05-12 |
|  13264 | 1956-09-02 | Oguz       | Hofting   | M      | 1986-08-23 |
|  14160 | 1960-09-29 | Shaowen    | Hofting   | M      | 1987-08-21 |
|  14733 | 1962-09-23 | Adam       | Hofting   | F      | 1993-01-23 |
|  15781 | 1956-01-10 | Rafail     | Gomatam   | M      | 1986-08-31 |
+--------+------------+------------+-----------+--------+------------+
10 rows in set (0.01 sec)
```

例如9：查询 salary 大于 30000 并且编号为 10001 或 10020 的； 使用 and 和 or 进行限定。

注意：同时使用 and 和 or 要考虑优先级 and 的优先级比 or 的优先级要高，所以得使用小括号限定优先级顺序“()”。

```mysql
select emp_no,salary,from_date,to_date from salaries where salary > 30000 and (emp_no='10040' or emp_no='10020') limit 10;

mysql> select emp_no,salary,from_date,to_date from salaries where salary > 30000 and (emp_no='10040' or emp_no='10020') limit 10;
+--------+--------+------------+------------+
| emp_no | salary | from_date  | to_date    |
+--------+--------+------------+------------+
|  10020 |  40000 | 1997-12-30 | 1998-12-30 |
|  10020 |  40647 | 1998-12-30 | 1999-12-30 |
|  10020 |  43800 | 1999-12-30 | 2000-12-29 |
|  10020 |  44927 | 2000-12-29 | 2001-12-29 |
|  10020 |  47017 | 2001-12-29 | 9999-01-01 |
+--------+--------+------------+------------+
10 rows in set (0.00 sec)
```

例如10：找出first_name 中 Lucien 和 Basil；使用 or 或者 not in 条件限定。

注意：使用 in 不代表是一个区间而是一个特性的值。

```mysql
例1：使用 or 进行限定
select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name = 'Lucien' or first_name = 'Basil' limit 10;

mysql> select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name = 'Lucien' or first_name = 'Basil' limit 10;
+--------+------------+------------+-------------+--------+------------+
| emp_no | birth_date | first_name | last_name   | gender | hire_date  |
+--------+------------+------------+-------------+--------+------------+
|  10046 | 1960-07-23 | Lucien     | Rosenbaum   | M      | 1992-06-20 |
|  10049 | 1961-04-24 | Basil      | Tramer      | F      | 1992-05-04 |
|  10258 | 1955-12-12 | Basil      | Ishibashi   | F      | 1985-05-17 |
|  10301 | 1962-08-26 | Lucien     | Staudhammer | M      | 1988-05-23 |
|  10597 | 1961-05-07 | Lucien     | Schaad      | F      | 1990-04-01 |
|  11933 | 1953-08-15 | Basil      | Erman       | M      | 1987-06-13 |
|  12004 | 1962-02-11 | Lucien     | Schlenzig   | F      | 1986-10-13 |
|  12793 | 1963-07-08 | Basil      | Covnot      | F      | 1989-11-11 |
|  14193 | 1964-02-23 | Lucien     | Kornyak     | F      | 1994-11-01 |
|  15638 | 1952-07-21 | Basil      | Perez       | M      | 1992-09-04 |
+--------+------------+------------+-------------+--------+------------+
10 rows in set (0.00 sec)

例2：使用 not in 进行限定
select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name in('Lucien', 'Basil') limit 10;

mysql> select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name in('Lucien', 'Basil') limit 10;
+--------+------------+------------+-------------+--------+------------+
| emp_no | birth_date | first_name | last_name   | gender | hire_date  |
+--------+------------+------------+-------------+--------+------------+
|  10046 | 1960-07-23 | Lucien     | Rosenbaum   | M      | 1992-06-20 |
|  10049 | 1961-04-24 | Basil      | Tramer      | F      | 1992-05-04 |
|  10258 | 1955-12-12 | Basil      | Ishibashi   | F      | 1985-05-17 |
|  10301 | 1962-08-26 | Lucien     | Staudhammer | M      | 1988-05-23 |
|  10597 | 1961-05-07 | Lucien     | Schaad      | F      | 1990-04-01 |
+--------+------------+------------+-------------+--------+------------+
10 rows in set (0.01 sec)
```

例如10：格式化数字使用  format(字段，'格式')

```mysql
mysql> select emp_no, format(salary,'$999.999') as salary from salaries limit 5;
+--------+--------+
| emp_no | salary |
+--------+--------+
|  10001 | 60,117 |
|  10001 | 62,102 |
|  10001 | 66,074 |
|  10001 | 66,596 |
|  10001 | 66,961 |
+--------+--------+
5 rows in set, 5 warnings (0.00 sec)
```

例如11：格式化字符

str_to_date: 将字符串 varchar 类型转换为 date 类型。

date_format: 将 date 类型转换成具有一定格式的 varchar 字符串类型。

语法格式：

```mysql
str_to_date('字符串日期','日期格式')

日期格式： %Y = 年, %m = 月, %d = 日, %h = 时, %i = 分, %s = 秒
```







###### 模糊查询

like 称为模糊查询，支持 % 或 下划线匹配，下划线，一个下划线只匹配一个字符。

% 匹配任意个字符（“%”是一个特殊的符号，“_”也是一个特殊符号）。

例如：找出名字里带有 “e” 的 使用 like 'e'。

```mysql
例1：找出名字里带有 “e” 的 使用 like 'e'。

select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name like '%e%' limit 10;

mysql> select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name like '%e%' limit 10;
+--------+------------+------------+-----------+--------+------------+
| emp_no | birth_date | first_name | last_name | gender | hire_date  |
+--------+------------+------------+-----------+--------+------------+
|  10001 | 1953-09-02 | Georgi     | Facello   | M      | 1986-06-26 |
|  10002 | 1964-06-02 | Bezalel    | Simmel    | F      | 1985-11-21 |
|  10006 | 1953-04-20 | Anneke     | Preusig   | F      | 1989-06-02 |
|  10007 | 1957-05-23 | Tzvetan    | Zielinski | F      | 1989-02-10 |
|  10010 | 1963-06-01 | Duangkaew  | Piveteau  | F      | 1989-08-24 |
+--------+------------+------------+-----------+--------+------------+
10 rows in set (0.00 sec)

例2：找出名字以 n 结尾的。
select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name like '%n' limit 10;

mysql> select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name like '%n' limit 10;
+--------+------------+------------+------------+--------+------------+
| emp_no | birth_date | first_name | last_name  | gender | hire_date  |
+--------+------------+------------+------------+--------+------------+
|  10004 | 1954-05-01 | Chirstian  | Koblick    | M      | 1986-12-01 |
|  10007 | 1957-05-23 | Tzvetan    | Zielinski  | F      | 1989-02-10 |
|  10019 | 1953-01-23 | Lillian    | Haddadi    | M      | 1999-04-30 |
|  10023 | 1953-09-29 | Bojan      | Montemayor | F      | 1989-12-17 |
|  10031 | 1959-01-27 | Karsten    | Joslin     | M      | 1991-09-01 |
+--------+------------+------------+------------+--------+------------+
10 rows in set (0.00 sec)

例3：找出名字以 k 开始的。
select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name like 'k%' limit 10;

mysql> select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name like 'k%' limit 10;
+--------+------------+------------+-------------+--------+------------+
| emp_no | birth_date | first_name | last_name   | gender | hire_date  |
+--------+------------+------------+-------------+--------+------------+
|  10005 | 1955-01-21 | Kyoichi    | Maliniak    | M      | 1989-09-12 |
|  10016 | 1961-05-02 | Kazuhito   | Cappelletti | M      | 1995-01-27 |
|  10018 | 1954-06-19 | Kazuhide   | Peha        | F      | 1987-04-03 |
|  10031 | 1959-01-27 | Karsten    | Joslin      | M      | 1991-09-01 |
|  10066 | 1952-11-13 | Kwee       | Schusler    | M      | 1986-02-26 |
+--------+------------+------------+-------------+--------+------------+
10 rows in set (0.00 sec)

例4：找出选定字母的，如找出第三个字母是 a 的。
select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name like '__a%' limit 10;

mysql> select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name like '__a%' limit 10;
+--------+------------+------------+-----------+--------+------------+
| emp_no | birth_date | first_name | last_name | gender | hire_date  |
+--------+------------+------------+-----------+--------+------------+
|  10010 | 1963-06-01 | Duangkaew  | Piveteau  | F      | 1989-08-24 |
|  10022 | 1952-07-08 | Shahaf     | Famili    | M      | 1995-08-22 |
|  10025 | 1958-10-31 | Prasadram  | Heyers    | M      | 1987-08-17 |
|  10035 | 1953-02-08 | Alain      | Chappelet | M      | 1988-09-05 |
|  10036 | 1959-08-10 | Adamantios | Portugali | M      | 1992-01-03 |
+--------+------------+------------+-----------+--------+------------+
10 rows in set (0.00 sec)
```

例如：找出名字中带有 下划线的 “_” 使用转义字符 “\”；

```mysql
select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name like '%\_%' limit 10;

mysql> select emp_no,birth_date, first_name,last_name,gender,hire_date from employees where first_name like '%\_%' limit 10;
Empty set (0.15 sec)
```

#### 5.排序

例如1：按照 工资薪金进行排序 

```mysql
默认是升序排序！！！ 

select emp_no,salary,from_date,to_date from salaries order by salary limit 10;

指定升序操作 asc ！！！
select emp_no,salary,from_date,to_date from salaries order by salary asc limit 10;

mysql> select emp_no,salary,from_date,to_date from salaries order by salary limit 10;
+--------+--------+------------+------------+
| emp_no | salary | from_date  | to_date    |
+--------+--------+------------+------------+
| 253406 |  38623 | 2002-02-20 | 9999-01-01 |
|  49239 |  38735 | 1996-09-17 | 1997-09-17 |
| 281546 |  38786 | 1996-11-13 | 1997-06-26 |
|  15830 |  38812 | 2001-03-12 | 2002-03-12 |
|  64198 |  38836 | 1989-10-20 | 1990-10-20 |
+--------+--------+------------+------------+
10 rows in set (0.90 sec)

指定降序 order by 字段 desc; ！！！

select emp_no,salary,from_date,to_date from salaries order by salary desc limit 10;

mysql> select emp_no,salary,from_date,to_date from salaries order by salary desc limit 10;
+--------+--------+------------+------------+
| emp_no | salary | from_date  | to_date    |
+--------+--------+------------+------------+
|  43624 | 158220 | 2002-03-22 | 9999-01-01 |
|  43624 | 157821 | 2001-03-22 | 2002-03-22 |
| 254466 | 156286 | 2001-08-04 | 9999-01-01 |
|  47978 | 155709 | 2002-07-14 | 9999-01-01 |
| 253939 | 155513 | 2002-04-11 | 9999-01-01 |
+--------+--------+------------+------------+
10 rows in set (0.64 sec)
```

例如2：多字段排序，当一列数据有相同的时候，利用另一列的数据进行排序。

```mysql
select emp_no,salary,from_date,to_date from salaries order by salary asc,emp_no asc limit 10;

mysql> select emp_no,salary,from_date,to_date from salaries order by salary asc,emp_no asc limit 10;

+--------+--------+------------+------------+
| emp_no | salary | from_date  | to_date    |
+--------+--------+------------+------------+
| 253406 |  38623 | 2002-02-20 | 9999-01-01 |
|  49239 |  38735 | 1996-09-17 | 1997-09-17 |
| 281546 |  38786 | 1996-11-13 | 1997-06-26 |
|  15830 |  38812 | 2001-03-12 | 2002-03-12 |
|  64198 |  38836 | 1989-10-20 | 1990-10-20 |
+--------+--------+------------+------------+
10 rows in set (0.65 sec)
```

例如3：根据字段位置也可以排序 order by 2  “2”代表的是第二列数据进行排序。

```mysql
select emp_no,salary,from_date,to_date from salaries order by 2 limit 10;

mysql> select emp_no,salary,from_date,to_date from salaries order by 2 limit 10;
+--------+--------+------------+------------+
| emp_no | salary | from_date  | to_date    |
+--------+--------+------------+------------+
| 253406 |  38623 | 2002-02-20 | 9999-01-01 |
|  49239 |  38735 | 1996-09-17 | 1997-09-17 |
| 281546 |  38786 | 1996-11-13 | 1997-06-26 |
|  15830 |  38812 | 2001-03-12 | 2002-03-12 |
|  64198 |  38836 | 1989-10-20 | 1990-10-20 |
+--------+--------+------------+------------+
10 rows in set (0.65 sec)
```

例如：找出薪资在 30000 到 50000 之间的员工信息，按照薪资降序排列。

```mysql
select emp_no,salary,from_date,to_date from salaries where salary between 30000 and 50000 order by salary desc limit 10;

mysql> select emp_no,salary,from_date,to_date from salaries where salary between 30000 and 50000 order by salary desc limit 10;
+--------+--------+------------+------------+
| emp_no | salary | from_date  | to_date    |
+--------+--------+------------+------------+
|  34734 |  50000 | 1993-07-18 | 1994-07-18 |
|  11201 |  50000 | 1996-10-30 | 1997-10-30 |
|  18578 |  50000 | 1993-08-12 | 1994-08-12 |
|  40785 |  50000 | 1999-09-04 | 1999-10-14 |
|  39116 |  50000 | 2002-07-20 | 9999-01-01 |
+--------+--------+------------+------------+
10 rows in set (0.58 sec)
```

#### 6.聚合

很多情况下，需要进行一些聚合操作，这个时候就要用到 sql 的聚合操作。

聚合操作的语法格式如下：

```mysql
SELECT [field1,field2,……fieldn] fun_name
FROM tablename
[WHERE where_contition]
[GROUP BY field1,field2,……fieldn
[WITH ROLLUP]]
[HAVING where_contition]
```

对其参数进行以下说明：

- fun_name 表示要做的聚合操作，也就是聚合操作，常用的有 sum（求和）、count(*)（记录数）、max（最大值）、min（最小值）、avg（平均值）。注意：使用会自动忽略 null
- group by 关键字表示要进行分类聚合的字段，比如要按照部分分类的统计员工数量，部门就该写在 group by 后面。
- with rollup 是可选语法，表明是否对==分类聚合==的结果进行再汇总。
- having 关键字表示对分类后的结果再进行条件的过滤。
- round 关键字用于指定显示小数

注意：having 和 where 的区别在于 having 是对聚合后的结果进行条件过滤，而 where 是在聚合前就对记录进行过滤，如果逻辑允许，可以尽可能用 where 先过滤记录，这样因为结果集减小，将对聚合的效率大大提高，最后再根据逻辑看是否用 having 进行再过滤。

例如1：要 salaries 表中 emp_no 字段的总数

```mysql
select count(1) from salaries;

mysql> select count(1) from salaries;
+----------+
| count(1) |
+----------+
|  2844047 |
+----------+
1 row in set (0.04 sec)
```

例如2：在此基础上，要统计个部门的人数：

```mysql
select emp_no, count(1) from salaries group by emp_no limit 10;

mysql> select emp_no, count(1) from salaries group by emp_no limit 10;
+--------+----------+
| emp_no | count(1) |
+--------+----------+
|  10001 |       17 |
|  10002 |        6 |
|  10003 |        7 |
|  10004 |       16 |
+--------+----------+
10 rows in set (0.00 sec)
```

例如3：更细一些，既要统计各部门人数，又要统计总人数： with rollup

```mysql
select emp_no,count(1) from salaries group by emp_no with rollup limit 5;

mysql> select emp_no,count(1) from salaries group by emp_no with rollup limit 5;
+--------+----------+
| emp_no | count(1) |
+--------+----------+
|  10001 |       17 |
|  10002 |        6 |
|  10003 |        7 |
|  10004 |       16 |
|  10005 |       13 |
+--------+----------+
10 rows in set (0.00 sec)
```

例如4：统计人数大于 5 人的部门： having  后跟再过滤

```mysql
select emp_no, count(1) from salaries group by emp_no having count(1) > 5 limit 5;

mysql> select emp_no, count(1) from salaries group by emp_no having count(1) > 5 limit 5;
+--------+----------+
| emp_no | count(1) |
+--------+----------+
|  10001 |       17 |
|  10002 |        6 |
|  10003 |        7 |
|  10004 |       16 |
|  10005 |       13 |
+--------+----------+
10 rows in set (0.00 sec)
```

例如5：最后统计公司所有员工的新书总额、最高和最低薪水：

```mysql
select sum(salary) as esum,max(salary) as emax,min(salary) as emin, round(avg(salary),2) as eavg, count(salary) as ecount from salaries;

mysql> select sum(salary) as esum,max(salary) as emax,min(salary) as emin, round(avg(salary),2) as eavg, count(salary) as ecount from salaries;
+--------------+--------+-------+----------+---------+
| esum         | emax   | emin  | eavg     | ecount  |
+--------------+--------+-------+----------+---------+
| 181480757419 | 158220 | 38623 | 63810.74 | 2844047 |
+--------------+--------+-------+----------+---------+
1 row in set (0.67 sec)
```

例如6：分组函数要使用到 where 查询之后要先进行分组，才能使用分组函数。

执行顺序语法：

```mysql
select
	...
from
	...
where
	...
group by
	...
order by
	...
	
执行顺序是： from -> where -> group by -> select -> order by 
```

例如7：找出 emp_no 薪资总和以及最大值

```mysql
select emp_no, sum(salary) as esum , max(salary) as emax  from salaries group by emp_no limit 5;

mysql> select emp_no, sum(salary) as esum , max(salary) as emax  from salaries group by emp_no limit 5;
+--------+---------+-------+
| emp_no | esum    | emax  |
+--------+---------+-------+
|  10001 | 1281612 | 88958 |
|  10002 |  413127 | 72527 |
|  10003 |  301212 | 43699 |
|  10004 |  904196 | 74057 |
|  10005 | 1134585 | 94692 |
+--------+---------+-------+
5 rows in set (0.00 sec)
```

 例如8：假如 要查每个部门，不同的工作岗位 薪资的最大值 可以这样写

```mysql
select 部门字段，岗位字段， max(薪资字段) from 表名 group by 岗位字段，部门字段 ;
```



例如9：使用having来找出部门最高薪资，但是要按照部门编号分组，求每一次最大值

方法一：

```mysql
select emp_no, max(salary) as emax  from salaries group by emp_no  having max(salary) > 50000 limit 5;

mysql> select emp_no, max(salary) as emax  from salaries group by emp_no  having max(salary) > 50000 limit 5;
+--------+-------+
| emp_no | emax  |
+--------+-------+
|  10001 | 88958 |
|  10002 | 72527 |
|  10004 | 74057 |
|  10005 | 94692 |
|  10006 | 60098 |
+--------+-------+
5 rows in set (0.04 sec)
```

方法二：

```mysql
select emp_no, max(salary) as emax  from salaries  where salary > 50000 group by emp_no limit 5;

mysql> select emp_no, max(salary) as emax  from salaries  where salary > 50000 group by emp_no limit 5;
+--------+-------+
| emp_no | emax  |
+--------+-------+
|  10001 | 88958 |
|  10002 | 72527 |
|  10004 | 74057 |
|  10005 | 94692 |
|  10006 | 60098 |
+--------+-------+
5 rows in set (0.01 sec)
```

例如10：找出每个部分平均薪资，要求显示平均薪资高于  使用having 进行过滤

```mysql
select emp_no, round(avg(salary), 2) as eavg from salaries group by emp_no having avg(salary) > 50000 limit 5;

mysql> select emp_no, round(avg(salary), 2) as eavg from salaries group by emp_no having avg(salary) > 50000
+--------+----------+
| emp_no | eavg     |
+--------+----------+
|  10001 | 75388.94 |
|  10002 | 68854.50 |
|  10004 | 56512.25 |
|  10005 | 87275.77 |
|  10006 | 50514.92 |
+--------+----------+
5 rows in set (0.00 sec)
```





##### 函数解释说明

1. 单行处理函数的特点：一个输入对应一个输出。
2. 多行处理函数相对应的是：多行处理函数。（多个处理函数特点：多个输入，对应1个输出！）。

##### 常见的函数有哪些

- lower 转换成小写；
- upper 转换成大写；
- substr 取子串（substr （被截取的字符串，起始下标，截取的长度））；
- concat 函数进行字符串拼接；
- length 取长度；
- trim 取空格；
- str_to_date 将字符串转换成日期；
- date_format 格式化日期；
- round 四舍五入；
- rand() 生成随机数；
- ifnull 可以将 null 转换成一个具体值；
- case..when..then..when..then..else..end 函数 例如 if else 语句

1. lower 转换成“小”写

```mysql
mysql> select first_name from employees limit 5;
+------------+
| first_name |
+------------+
| Georgi     |
| Bezalel    |
| Parto      |
| Chirstian  |
| Kyoichi    |
+------------+
10 rows in set (0.00 sec)

mysql> select lower(first_name) as name from employees limit 5;
+-----------+
| name      |
+-----------+
| georgi    |
| bezalel   |
| parto     |
| chirstian |
| kyoichi   |
+-----------+
10 rows in set (0.00 sec)
```

2. upper 转换成“大”写；

```mysql
mysql> select first_name as ename from employees limit 5;
+-----------+
| ename     |
+-----------+
| Georgi    |
| Bezalel   |
| Parto     |
| Chirstian |
| Kyoichi   |
+-----------+
10 rows in set (0.00 sec)

mysql> select upper(first_name) as ename from employees limit 5;
+-----------+
| ename     |
+-----------+
| GEORGI    |
| BEZALEL   |
| PARTO     |
| CHIRSTIAN |
| KYOICHI   |
+-----------+
10 rows in set (0.00 sec)
```

3. substr 取子串（substr （被截取的字符串，起始下标，截取的长度））；

```mysql
select substr(first_name, 1, 1) as ename from employees limit 5;

mysql> select substr(first_name, 1, 1) as ename from employees limit 5;
+-------+
| ename |
+-------+
| G     |
| B     |
| P     |
| C     |
| K     |
+-------+
5 rows in set (0.00 sec)
```

注意：起始下标从 1 开始，没有从 0 开始。

例如：找出员工名字第一个字母是 A 的员工信息？

```mysql
第一种方法：模糊查询
select first_name as ename from employees where first_name like 'A%' limit 5;

mysql> select first_name as ename from employees where first_name like 'A%' limit 5;
+------------+
| ename      |
+------------+
| Anneke     |
| Arif       |
| Alain      |
| Adamantios |
| Alejandro  |
+------------+
5 rows in set (0.00 sec)

第二种方法：substr 函数
select first_name as name from employees where substr(first_name, 1, 1) = 'A' limit 5;

mysql> select first_name as name from employees where substr(first_name, 1, 1) = 'A' limit 5;
+------------+
| name       |
+------------+
| Anneke     |
| Arif       |
| Alain      |
| Adamantios |
| Alejandro  |
+------------+
5 rows in set (0.00 sec)
```

4. concat 函数进行字符串拼接；

```mysql
select concat(emp_no, first_name) as name from employees limit 5;

mysql> select concat(emp_no, first_name) as name from employees limit 5;
+----------------+
| name           |
+----------------+
| 10001Georgi    |
| 10002Bezalel   |
| 10003Parto     |
| 10004Chirstian |
| 10005Kyoichi   |
+----------------+
5 rows in set (0.00 sec)
```

5. length 取长度

```mysql
select first_name,length(first_name) as name from employees limit 5;

mysql> select first_name,length(first_name) as name from employees limit 5;
+------------+------+
| first_name | name |
+------------+------+
| Georgi     |    6 |
| Bezalel    |    7 |
| Parto      |    5 |
| Chirstian  |    9 |
| Kyoichi    |    7 |
+------------+------+
5 rows in set (0.00 sec)
```

6. 名字字段首字母大写

```mysql
select upper(substr(first_name, 1, 1)) as name from employees limit 5;

select substr(first_name, 2, length(first_name)) as name from employees limit 5;

select concat(upper(substr(first_name, 1, 1)),substr(first_name, 2, length(first_name))) as result from employees limit 5;

mysql> select concat(upper(substr(first_name, 1, 1)),substr(first_name, 2, length(first_name))) as result from employees limit 5;
+-----------+
| result    |
+-----------+
| Georgi    |
| Bezalel   |
| Parto     |
| Chirstian |
| Kyoichi   |
+-----------+
5 rows in set (0.00 sec)
```

7. trim 去空格

```mysql
select first_name from employees where first_name = '   Parto' limit 5;

mysql> select first_name from employees where first_name = '   Parto' limit 5;
Empty set (0.06 sec)

select first_name from employees where first_name =  trim('   Parto') limit 5;

mysql> select first_name from employees where first_name =  trim('   Parto') limit 5;
+------------+
| first_name |
+------------+
| Parto      |
| Parto      |
| Parto      |
| Parto      |
| Parto      |
+------------+
5 rows in set (0.00 sec)
```

8. round 四舍五入；

```mysql
select round(salary, 2) as salary from salaries limit 5;

mysql> select round(salary, 2) as salary from salaries limit 5;
+--------+
| salary |
+--------+
|  60117 |
|  62102 |
|  66074 |
|  66596 |
|  66961 |
+--------+
5 rows in set (0.01 sec)
```

9. rand 生成随机数 生成 100 以内的随机数

```mysql
select round(rand() * 100, 0) as sun from employees limit 5;

mysql> select round(rand() * 100, 0) as sun from employees limit 5;
+-----+
| sun |
+-----+
|   5 |
|  12 |
|  46 |
|  94 |
|  30 |
+-----+
5 rows in set (0.00 sec)
```

10. ifnull 可以将 null 转换成一个具体值；

```mysql
select emp_no, emp_no + ifnull(salary, 0) as sname from salaries limit 5;

mysql> select emp_no, emp_no + ifnull(salary, 0) as sname from salaries limit 5;
+--------+-------+
| emp_no | sname |
+--------+-------+
|  10001 | 70118 |
|  10001 | 72103 |
|  10001 | 76075 |
|  10001 | 76597 |
|  10001 | 76962 |
+--------+-------+
5 rows in set (0.00 sec)
```

11. case..when..then..when..then..else..end 函数 例如 if else 语句

```mysql
select emp_no,first_name, (case first_name when 'Georgi' then emp_no * 104 when 'Parto' then emp_no * 204 else emp_no end) as ename from employees where limit 5;

mysql> select emp_no,first_name, (case first_name when 'Georgi' then emp_no * 104 when 'Parto' then emp_no * 204 else emp_no end) as ename from employees limit 5;
+--------+------------+---------+
| emp_no | first_name | ename   |
+--------+------------+---------+
|  10001 | Georgi     | 1040104 |
|  10002 | Bezalel    |   10002 |
|  10003 | Parto      | 2040612 |
|  10004 | Chirstian  |   10004 |
|  10005 | Kyoichi    |   10005 |
+--------+------------+---------+
5 rows in set (0.00 sec)
```

#### 7.表连接

查找字段 emp_no 和 dept_no 匹配的 dept_name 的字段名称

```mysql
select 
	e.emp_no,d.dept_no, d.dept_name 
from 
	departments d,dept_emp e
where 
	d.dept_no = e.dept_no limit 5;
	
mysql> select
no,d.dep    -> e.emp_no,d.dept_no, d.dept_name
    -> from
    -> departments d,dept_emp e
    -> where
    -> d.dept_no = e.dept_no limit 5;
+--------+---------+------------------+
| emp_no | dept_no | dept_name        |
+--------+---------+------------------+
|  10011 | d009    | Customer Service |
|  10038 | d009    | Customer Service |
|  10049 | d009    | Customer Service |
|  10060 | d009    | Customer Service |
|  10088 | d009    | Customer Service |
+--------+---------+------------------+
10 rows in set (0.00 sec)
```

使用 join on 来优化查询  也可以使用 inner join on 来实现内连接 （可读性也好！！）

```mysql
select 
	e.emp_no,d.dept_no, d.dept_name 
from 
	departments d
join
	dept_emp e
on 
	d.dept_no = e.dept_no limit 5;
	
mysql> select
    -> e.emp_no,d.dept_no, d.dept_name
    -> from
    -> departments d
    -> join
    -> dept_emp e
    -> on
    -> d.dept_no = e.dept_no limit 5;
+--------+---------+------------------+
| emp_no | dept_no | dept_name        |
+--------+---------+------------------+
|  10011 | d009    | Customer Service |
|  10038 | d009    | Customer Service |
|  10049 | d009    | Customer Service |
|  10060 | d009    | Customer Service |
|  10088 | d009    | Customer Service |
+--------+---------+------------------+
5 rows in set (0.02 sec)
```

##### 区间查询

```mysql
select 
	s.emp_no, s.salary, d.grade
from 
	salaries s
join 
	salgrade d
on
	s.salary between d.losal and d.hisal 
limit 5;

+--------+--------+-------+
| emp_no | salary | grade |
+--------+--------+-------+
|  10001 |  60117 |     6 |
|  10001 |  62102 |     6 |
|  10001 |  66074 |     6 |
|  10001 |  66596 |     6 |
|  10001 |  66961 |     6 |
+--------+--------+-------+
5 rows in set (0.00 sec)

```



##### 外连接

使用（right outer）将右边的作为主表；其中 outer 是可以省略的

使用 right join 实现外连接，作用是显示右边字段的所有数据。未匹配的也将显示出来（右外连接）

right 表示join 关键字右边的表看成主表，主要是为了将这张表的数据全部查询出来，捎带着关联查询左边的表。

```mysql
select 
	e.emp_no,d.dept_no, d.dept_name 
from 
	dept_emp e
right join
	departments d
on 
	d.dept_no = e.dept_no limit 5;
	
+--------+---------+-----------+
| emp_no | dept_no | dept_name |
+--------+---------+-----------+
|  10017 | d001    | Marketing |
|  10055 | d001    | Marketing |
|  10058 | d001    | Marketing |
|  10108 | d001    | Marketing |
|  10140 | d001    | Marketing |
+--------+---------+-----------+
5 rows in set (0.00 sec)
```

使用（left）将左边的表作为主表

```mysql
select 
	e.emp_no,d.dept_no, d.dept_name 
from 
	dept_emp e
left join
	departments d
on 
	d.dept_no = e.dept_no limit 5;
	
+--------+---------+-----------+
| emp_no | dept_no | dept_name |
+--------+---------+-----------+
|  10017 | d001    | Marketing |
|  10055 | d001    | Marketing |
|  10058 | d001    | Marketing |
|  10108 | d001    | Marketing |
|  10140 | d001    | Marketing |
+--------+---------+-----------+
5 rows in set (0.00 sec)
```

##### 两张表以上的链接查询

语法格式是：

```mysql
select 
	...
from 
	a
join
	b
on
	a 和 b 的链接条件
join
	c
on 
	a 和 c 的链接条件
join 
	d
on 
 	a 和 d 的链接条件
```

例如：

三个表的链接的查询

```mysql
select 
	t.title,s.emp_no, s.salary, d.grade
from 
	salaries s
join 
	salgrade d
on
	s.salary between d.losal and d.hisal 
join
	titles t
on
	t.emp_no = s.emp_no
limit 5;

+-----------------+--------+--------+-------+
| title           | emp_no | salary | grade |
+-----------------+--------+--------+-------+
| Senior Engineer |  10001 |  60117 |     6 |
| Senior Engineer |  10001 |  62102 |     6 |
| Senior Engineer |  10001 |  66074 |     6 |
| Senior Engineer |  10001 |  66596 |     6 |
| Senior Engineer |  10001 |  66961 |     6 |
+-----------------+--------+--------+-------+
5 rows in set (0.00 sec)
```

案例： 找出每个员工的部门名称以及工资等级。

要求：显示员工名，部门名，薪资，薪资等级。

```mysql
select 
	dept_emp.emp_no,titles.title,departme.dept_name,salaries.salary,salgrade.grade
from 
	titles
join
	salaries
on
	titles.emp_no = salaries.emp_no
join
	dept_emp
on
	titles.emp_no = dept_emp.emp_no
join
	departme
on
	departme.dept_no = dept_emp.dept_no
join
	salgrade
on
	salaries.salary between salgrade.losal and salgrade.hisal
limit 10;

+--------+-----------------+-------------+--------+-------+
| emp_no | title           | dept_name   | salary | grade |
+--------+-----------------+-------------+--------+-------+
|  10001 | Senior Engineer | Development |  80013 |     8 |
|  10001 | Senior Engineer | Development |  81025 |     8 |
|  10001 | Senior Engineer | Development |  81097 |     8 |
|  10001 | Senior Engineer | Development |  84917 |     8 |
|  10001 | Senior Engineer | Development |  85112 |     8 |
+--------+-----------------+-------------+--------+-------+
5 rows in set (0.00 sec)
```

#### 8.子查询

##### 什么是子查询？

select 语句中嵌套 select 语句，被嵌套的 select 语句称为子查询。

##### 子查询都可以出现在哪里呢？

```mysql
select 
	...(select).
from 
	...(select).
where
	...(select).
```

案例1：利用子查询找出最低薪资以外的人员和薪资(where 条件中)

```mysql
select
	titles.emp_no, salaries.salary
from
	salaries
join 
	titles 
on
	titles.emp_no = salaries.emp_no
where
	salaries.salary > (select min(salary) from salaries)
limit 5;

+--------+--------+
| emp_no | salary |
+--------+--------+
|  10001 |  60117 |
|  10001 |  62102 |
|  10001 |  66074 |
|  10001 |  66596 |
|  10001 |  66961 |
+--------+--------+
5 rows in set (0.42 sec)
```

案例2：找出每个岗位的平均薪资的薪资等级（from 条件中）

第一步：找出每个岗位的平均薪资

```mysql
select emp_no, round(avg(salary),2) as eavg from salaries group by emp_no limit 5;

+--------+----------+
| emp_no | eavg     |
+--------+----------+
|  10001 | 71867.33 |
|  10002 | 68854.50 |
|  10003 | 43030.29 |
|  10004 | 56512.25 |
|  10005 | 87275.77 |
+--------+----------+
5 rows in set (0.00 sec)
```

第二步：进行最终表连接的查询

```mysql
select 
	t.*, salgrade.grade
from
	(select emp_no, round(avg(salary),2) as eavg from salaries group by emp_no) t
join
	salgrade
on
	t.eavg between salgrade.losal and salgrade.hisal
limit 5;

+--------+----------+-------+
| emp_no | eavg     | grade |
+--------+----------+-------+
|  10001 | 71867.33 |     7 |
|  10002 | 68854.50 |     6 |
|  10003 | 43030.29 |     4 |
|  10004 | 56512.25 |     5 |
|  10005 | 87275.77 |     8 |
+--------+----------+-------+
5 rows in set (0.65 sec)
```

案例3：找出每个员工的部门名称，要求显示员工名（select 条件中）

注意：对于 select 后面的子查询来说，这个子查询只能一次返回 1 条结果，多于 1 条，就报错！！！

```mysql
select 
	d.emp_no, (select t.dept_name from departme t where d.dept_no = t.dept_no) as name
from 
	dept_emp d;
limit 10;

+--------+-----------+
| emp_no | name       |
+--------+-----------+
|  10017 | Marketing |
|  10055 | Marketing |
|  10058 | Marketing |
|  10108 | Marketing |
|  10140 | Marketing |
+--------+-----------+
5 rows in set (0.00 sec)
```

#### 9.表记录合并

将两个表的数据按照一定的查询条件查询出来，将结果合并（加法）到一起显示出来，这个时候，就需要使用 union 和  union all 关键字来实现这样的功能，具体语法如下：

```mysql
SELECT * FROM t1
UNION|UNION ALL
SELECT * FROM t2
……
UNION|UNION ALL
SELECT * FROM tn;
```

UNION 和 UNION ALL 的主要区别是 UNION ALL 是把结果集直接合并在一起，而 UNION 是将 UNION ALL 后的结果进行一次 DISTINCT，去除重复记录后的结果。

- union 可以去重
- union all 去不了重

案例1：查出成员编号和薪资

```mysql
select emp_no, title from titles where title = 'Staff' 
union
select emp_no, title from titles where title = 'Engineer' 
limit 5;

+--------+-------+
| emp_no | title |
+--------+-------+
|  10002 | Staff |
|  10005 | Staff |
|  10007 | Staff |
|  10011 | Staff |
|  10016 | Staff |
+--------+-------+
5 rows in set (0.00 sec)
```

#### 10.分页显示

每页显示 pageSize 条记录

查询公式：第 pageNo 页： limit (pageNO - 1) * pageSize, pageSize;

#### 11快速复制表

```mysql
mysql> create table emp2 as select * from emp;
Query OK, 5 rows affected (0.04 sec)
Records: 5  Duplicates: 0  Warnings: 0

insert into emp2 select * from emp;


mysql> show tables;
+-----------------+
| Tables_in_test1 |
+-----------------+
| emp             |
| emp2            |
+-----------------+
2 rows in set (0.00 sec)

mysql> select * from emp;
+-------+------------+---------+--------+
| ename | hiredate   | sal     | deptno |
+-------+------------+---------+--------+
| zzx1  | 2000-01-01 | 2000.00 |      1 |
| lisa  | 2003-02-01 | 4000.00 |      2 |
| dony  | 2004-03-01 | 1000.00 |      1 |
| dept5 | 2005-04-01 |    5.00 |      2 |
| dept6 | NULL       |    6.00 |   NULL |
+-------+------------+---------+--------+
5 rows in set (0.00 sec)

mysql> select * from emp2;
+-------+------------+---------+--------+
| ename | hiredate   | sal     | deptno |
+-------+------------+---------+--------+
| zzx1  | 2000-01-01 | 2000.00 |      1 |
| lisa  | 2003-02-01 | 4000.00 |      2 |
| dony  | 2004-03-01 | 1000.00 |      1 |
| dept5 | 2005-04-01 |    5.00 |      2 |
| dept6 | NULL       |    6.00 |   NULL |
+-------+------------+---------+--------+
5 rows in set (0.00 sec)
```





