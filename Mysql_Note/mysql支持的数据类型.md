# 数据类型

## 数值类型

mysql 支持所有标准 sql 中的数值类型，其中包括严格数值类型，（integer,smallint,decimal和numeric），以及近似数值数据类型（float,real和double precision），并在此基础上做了扩展。扩展后增加了 tinyint,mediumint和bigint 这三种长度不同的整型，并添加了 bit 类型，用来存放位数据。

## 日期和时间类型

1. 如果要用来表示年月日，通常使用 date 来表示。
2. 如果要用来表示年月日时分秒，通常使用 datetime 来表示。
3. 如果要用来表示时分秒，通常使用 time 来表示。
4. 如果需要经常插入或者更新日期为当前系统时间，则通常使用 timestamp 来表示。timestamp 值返回后显示为“YYYY-MM-DD HH:MM:SS” 格式的字符串，显示宽度固定为 19 个字符。如果想要获得数字值，应在 timestamp 列添加 +0。
5. 如果只是表示年份，可以用 year 来表示，它比 date 占用更少的空间。year 有 2 位或 4 位格式的年，默认是 4 位格式。在 4 位格式中，允许的值是 1901~2155 和 0000。在 2 位格式中，允许的值是 70~69， 表示从 1970~2069年。MySQL 以 yyyy 格式显示 year 值。

```mysql
/* 创建一个 dtd 表分别以三种类型 创建表结构 */
CREATE Table dtd (d date, t TIME, dt datetime);

/* 查看表定义 */
desc dtd;

mysql> desc dtd;
+-------+----------+------+-----+---------+-------+
| Field | Type     | Null | Key | Default | Extra |
+-------+----------+------+-----+---------+-------+
| d     | date     | YES  |     | NULL    |       |
| t     | time     | YES  |     | NULL    |       |
| dt    | datetime | YES  |     | NULL    |       |
+-------+----------+------+-----+---------+-------+
3 rows in set (0.00 sec)

/* 使用 now() 函数插入当前日期 */
insert into dtd values(now(), now(), now());

/* 查看显示结果 */
select * from dtd;

mysql> select * from dtd;
+------------+----------+---------------------+
| d          | t        | dt                  |
+------------+----------+---------------------+
| 2023-08-31 | 23:27:45 | 2023-08-31 23:27:45 |
+------------+----------+---------------------+
1 row in set (0.00 sec)
```

