# mysql

## 表的操作

1. 非空约束：NOT NULL，不允许某列的内容为空；
2.  设置列的默认值：DEFAULT；
3.  唯一约束：UNIQUE，该表中，该列的内容必须唯一；
4. 主键约束：PRIMARY KEY，非空且唯一；
5. 主键自增长：AUTO_INCREMENT，从1开始，步长为1；
6. 外键约束：FOREIGN KEY，A表中的外键列。A表中的外键列的值必须参照于B表中的某一列（B表主键）。

## sql 列的常用类型

```mysql
MySQL:           |         Java:	
INT              |         int		（最长） 数字中的整数型。
BIGINT           |         long		
FLOAT			 |		   单精度浮点型数据。
DOUBLE			 |		   双精度浮点型数据。
DECIMAL          |         BigDecimal
DATE/DATETIME    |         java.util.Date  短时间和长日期类型
VARCHAR          |         String

CLOB			 |			字符大对象，最多可以存储4g的字符串，存储一个说明。超过 255 个字符的都要采用 CLOB来存储。Character Large OBject: CLOB	

BLOB			 |			二进制大对象 Binary Large OBject 专门用来存储图片、声音、视频等等 往 BLOB 类型的字段上插入数据的时候，例如插入一个图片，视屏等，需要使用 io 流才行。
```

## 数据库操作

- 连接数据库语句

```mysql
mysql -u root -padmin;
```

- 查看数据库列表

```mysql
show databases;
```

- 创建数据库

```mysql
create database 数据库名称；
```

- 删除数据库

```mysql
drop database 数据库名称；
```

- 修改数据库（alter databese）

```mysql
// 修改数据库编码格式
alter database 数据库名称  charset= 编码格式；
```

- 查看当前数据库下所有数据表

```mysql
show tables;
```

## 建表语法

```
列名1  列的类型  [约束],
列名2  列的类型  [约束],
...
列名N  列的类型  [约束]
);
// 注意：最后一行没有逗号
```

#### 案例：

创建一个学生表？

有 学号，姓名，年龄，邮箱地址

```mysql
create table `student` (
    `id` int(3),
    `name` varchar(20),
    `age` varchar(20),
    `email` varchar(20),
    primary key(`id`)
)



C:\Program Files\mingw-w64\x86_64-8.1.0-posix-seh-rt_v6-rev0
```



## 创建表和字段

1. **学生表**
   Student(s_id,s_name,s_birth,s_sex) –学生编号,学生姓名, 出生年月,学生性别
2. **课程表**
   Course(c_id,c_name,t_id) – –课程编号, 课程名称, 教师编号
3. **教师表**
   Teacher(t_id,t_name) –教师编号,教师姓名
4. **成绩表**
   Score(s_id,c_id,s_score) –学生编号,课程编号,分数

## 学生表

```mysql
CREATE TABLE `Student`(
    `s_id` VARCHAR(20),
    `s_name` VARCHAR(20) NOT NULL DEFAULT '',
    `s_birth` VARCHAR(20) NOT NULL DEFAULT '',
    `s_sex` VARCHAR(10) NOT NULL DEFAULT '',
    PRIMARY KEY(`s_id`)
);
```

## 课程表

```mysql
CREATE TABLE `Course`(
    `c_id`  VARCHAR(20),
    `c_name` VARCHAR(20) NOT NULL DEFAULT '',
    `t_id` VARCHAR(20) NOT NULL,
    PRIMARY KEY(`c_id`)
);
```

## 教师表

```mysql
CREATE TABLE `Teacher`(
    `t_id` VARCHAR(20),
    `t_name` VARCHAR(20) NOT NULL DEFAULT '',
    PRIMARY KEY(`t_id`)
);
```

## 成绩表

```mysql
CREATE TABLE `Score`(
    `s_id` VARCHAR(20),
    `c_id`  VARCHAR(20),
    `s_score` INT(3),
    PRIMARY KEY(`s_id`,`c_id`)
);


create table 'salgrade' (
    'crade' int AUTO_INCREMENT,
    'losal' BIGINT,
    'hisal' BIGINT
);


CREATE TABLE `salgrade` (
	`grade` INT auto_increment NOT NULL,
	`losal` BIGINT NOT NULL,
	`hisal` BIGINT NOT NULL,
    PRIMARY KEY (`grade`)
)
ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


```

## 插入学生表数据

```mysql
insert into Student values('01' , '赵雷' , '1990-01-01' , '男');
insert into Student values('02' , '钱电' , '1990-12-21' , '男');
insert into Student values('03' , '孙风' , '1990-05-20' , '男');
insert into Student values('04' , '李云' , '1990-08-06' , '男');
insert into Student values('05' , '周梅' , '1991-12-01' , '女');
insert into Student values('06' , '吴兰' , '1992-03-01' , '女');
insert into Student values('07' , '郑竹' , '1989-07-01' , '女');
insert into Student values('08' , '王菊' , '1990-01-20' , '女');
```

## 课程表数据

```mysql
insert into Teacher values('01' , '张三');
insert into Teacher values('02' , '李四');
insert into Teacher values('03' , '王五');
```

## 教师表

```mysql
insert into Course values('01' , '语文' , '02');
insert into Course values('02' , '数学' , '01');
insert into Course values('03' , '英语' , '03');
```



## 成绩表数据

```MySQL
insert into Score values('01' , '01' , 80);
insert into Score values('01' , '02' , 90);
insert into Score values('01' , '03' , 99);
insert into Score values('02' , '01' , 70);
insert into Score values('02' , '02' , 60);
insert into Score values('02' , '03' , 80);
insert into Score values('03' , '01' , 80);
insert into Score values('03' , '02' , 80);
insert into Score values('03' , '03' , 80);
insert into Score values('04' , '01' , 50);
insert into Score values('04' , '02' , 30);
insert into Score values('04' , '03' , 20);
insert into Score values('05' , '01' , 76);
insert into Score values('05' , '02' , 87);
insert into Score values('06' , '01' , 31);
insert into Score values('06' , '03' , 34);
insert into Score values('07' , '02' , 89);
insert into Score values('07' , '03' , 98);
```

<font color="blue">hh</font>

