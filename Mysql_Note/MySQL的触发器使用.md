## MySQL触发器

### 示例：

```mysql
create table tb_emp8(
    id int(11) primary key,
	name varchar(22) unique,
    deptId int(11) not null,
	salary float default 0,
constraint fk_emp_dept1 foreign key(deptId) references tb_dept1(id));

CREATE TABLE tb_emp6(
    id INT(11) PRIMARY KEY,
    name VARCHAR(25),
	deptId INT(11),salary FLOAT);

 CREATE TABLE tb_emp7(
     id INT(11) PRIMARY KEY,
     name VARCHAR(25),
     deptId INT(11),
 	salary FLOAT default 0);
```

### 为什么要使用触发器

触发器是被指定关联到一个表的数据库对象，当一个表的特定事件发生时，它将会被激活。主要用于保护表中的数据。MySQL所支持的触发器一共有三种：==insert触发器，update触发器，delete触发器==。

#### insert触发器

在insert语句执行之前或之后响应的触发器。应注意如下：

- 对于 AUTO_INCREMENT 列，NEW 在 INSERT 执行之前包含的值是0，在 INSERT 执行之后将包含新的自动生成值

#### update触发器

在update语句执行之前或之后响应的触发器。应注意如下：

- 在 update 触发器代码内，可引用一个名为 new （不区分大小写）的虚拟表来访问更新的值。
- 在 before update 触发器中，new 中的值可以被更新，即允许更改将要用于 update 语句中的值（只要具有对应的操作权限）
- old 的值全部是只读的，不能被更新
- 在 update 触发器代码内，可引用一个名为 old （不区分大小写）的虚拟表来访问 update 语句执行前的值。

#### delete触发器

在 delete 语句执行前或之后响应的触发器。应注意如下：

- old 的值全部都是只读的，不能被更新。
- 在 delete 触发器代码内，可引用一个名为 old （不区分大小写）的虚表来访问被删除的行。

### 创建触发器

#### 基本语法

```mysql
create trigger <触发器名> 
	trigger_time	<before | arter>
	trigger_event	<insert | update | delete>
	on <表名> for each row
	<触发器主体>
	
delimiter <??>  # 用于修改语句结束符

drop trigger trigger_name # 干掉已有的触发器

# 示例
/* 创建触发器存储表 */
create table if not exists `trigger_test` (
    `id` int not null AUTO_INCREMENT COMMENT "编号",
    `name` VARCHAR(20)  COMMENT "表名",
    `brand` DATETIME COMMENT "时间",
    PRIMARY KEY(`id`)
) 

/* 创建insert触发器 */
CREATE Trigger TRIGGER_inset AFTER INSERT 
on dept for each row
INSERT INTO trigger_test VALUES(null,concat(NEW.DNAME),now());

/* 插入一条数据 */
insert into dept values(22,"dmiter","akou");
```

#### 解释

1、创建触发器

```mysql
create trigger <触发器名> 
	trigger_time	<before | arter>
	trigger_event	<insert | update | delete>
	on <表名> for each row
	<触发器主体>
begin
    -- 触发器的操作语句
end;
```

2、在插入数据时触发触发器

```mysql
CREATE TRIGGER insert_trigger
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO log_table (message) VALUES ('New employee inserted');
END;
```

3、在更新数据时触发触发器

```mysql
CREATE TRIGGER update_trigger
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN
    IF NEW.salary > OLD.salary THEN
        INSERT INTO log_table (message) VALUES ('Employee salary increased');
    END IF;
END;
# new：新数据	old：旧数据   可以用于相比较  declare 创建变量
```

4、在删除数据时触发触发器

```mysql
CREATE TRIGGER delete_trigger
AFTER DELETE ON employees
FOR EACH ROW
BEGIN
    INSERT INTO log_table (message) VALUES ('Employee deleted');
END;
```





## 虚拟表

create view 语句用于在数据库中创建一个虚拟表，也称为视图（view）。视图是基于一个或多个数据库表的查询结果集，它本身不包含数据，而是根据查询定义的规则动态生成结果。

视图可以被当做一个虚拟表来使用，可以像访问表一样对其进行查询、插入、更新和删除操作。他提供了一种简化和抽象数据访问的方式，隐藏了底层表的细节，使得用户可以通过视图来获取所需的数据，而不必直接访问底层表。

### create view 语法的基本语法如下：

```mysql 
create view view_name as
select column1, column2,...
from table_name
where condition;

# 解析：
# view_name 是要创建的视图的名称；
# column1,column2,... 是视图中包含的列；
# table_name 是从那个表中获取数据；
# condition 是可选的筛选条件；
```

以下是一个示例，创建一个名为 cutomer_view 的视图，从 customers 表中选择 name 和 email 列：

```mysql
create view customer_view as
select name,emaio
from customers;
```

创建视图后，可以像查询表一样使用该视图，例如：

```mysql
select * from customer_view;

# 这将返回的 customer_view 视图中的所有行和列。
```

需要注意的是，视图只是一个虚拟表，不存储数据。每次查询视图时，都会根据定义的查询规则动态生成结果。因此，当底层表的数据发生变化时，查询视图的结果也会相应地更新。



## 聚集索引

create unique clustered 语句用于在数据库中创建一个唯一的聚集索引。聚集索引是一种特殊的索引类型，它决定了表中数据的物理存储顺序，并且每个索引键的值都是唯一的。

在 sql server中，聚集索引确定了表中数据行的物理存储顺序，并且表中只能有一个聚集索引。聚集索引的键值决定了数据行在磁盘上的物理存储位置，因此对于经常需要按照特定顺序访问数据的查询，使用聚集索引可以提高查询性能。

### create unique clustered 语句的基本语法如下：

```mysql
create unique clustered index index_name on table_name (column1, column2,...);

# 解析：
# index_name 是要创建的索引名称；
# table_name 是要创建索引的表名；
# (column1,column2,...) 是要包含在索引中的列。
```

以下是一个示例，创建一个名为 idx_customer_id 的唯一聚集索引，将 customers 表中的 customer_id 列作为索引键。

```mysql
CREATE UNIQUE CLUSTERED INDEX idx_customer_id
ON customers (customer_id);
```

创建唯一聚集索引后，可以通过索引键值快速定位和访问表中的数据。需要注意的是，创建聚集索引会对表的物理存储方式和产生影响，并且在创建索引时会对表中的数据进行排序，因此你可能会消耗较长的时间和资源。



## 分区函数

在 sql server 2008 中，可以使用以下语法创建分区函数：

```mysql
create partition function partition_function_name(paramter_data_type)
as range left | right 
for values(value1,value2,...,valuen);

# 解析：
# partition_function_name 是要创建的分区函数的名称；
# paramter_data_type 是分区函数的输入参数的数据类型；
# range left 和 right 是分区函数的类型；
# value1,value2,...,valuen 是用于定义分区边界的值。
```

以下是一个示例：

```mysql
CREATE PARTITION FUNCTION sales_date_range (DATE)
AS RANGE LEFT FOR 
VALUES ('2019-01-01', '2020-01-01', '2021-01-01');
```

这个示例创建了一个名为 sales_date_range 的分区函数，它接受一个 DATE 类型的参数。分区函数使用  range left 类型，并使用 '2019-01-01', '2020-01-01', '2021-01-01' 作为边界值。

请注意，创建分区函数需要具有适当的权限。



## 分区方案

在 SQLserver 2008 中，可以使用以下语句创建分区方案：

```mysql
create partition scheme partition_scheme_name
as partition partition_function_name
to (filegroup1, filegroup2, ..., filegroupN);

# 解析：
# partition_scheme_name 是要创建的分区方案名称；
# partition_function_name 是要与分区方案关联的分区函数的名称；
# filegroup1, filegroup2, ..., filegroupN 是要将分区映射到文件组的名称。
```

以下是一个示例：

```mysql
create partition scheme sales_partition_schmem 
as partition sales_data_range
to (sales_fg1, sales_fg2, sales_fg3, sales_fg4);
```

解析：这个示例创建了一个名为 sales_partition_schmem 的分区方案，它与名为 sales_data_range 的分区函数关联。分区方案分区映射到 sales_fg1, sales_fg2, sales_fg3, sales_fg4 这四个文件组。

