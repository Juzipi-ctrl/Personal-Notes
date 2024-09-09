# Redis

## Nosql概述

#### 什么是 NoSql

> Nosql

Nosql = Not Only SQL （不仅仅是 SQL）

关系型数据库：表格，行，列

> Nosql 特点

解耦！

1、方便扩展（数据之间没有关系，很好扩展！）

2、大数据量性能（Redis 一秒写 8 万次，读取 11 万次，Nosql 的缓存记录级，是一种细粒度的缓存，性能会比较高！）

3、数据类型是多样型的！（不需要事先设计数据库！随取随用！）

4、传统 RDBMS 和 Nosql

```shell
传统的 RDBMS 
- 结构化组织
- SQL
- 数据和关系都存在单独的表中
- 操作，数据定义语言
- 严格的一致性
- 基础的事务操作
- 。。。。
```

```shell
Nosql
- 不仅仅是数据
- 没有固定的查询语言
- 键值对存储，列存储，文档存储，图形数据库
- 最终一致性
- CAP 定理 和 BASE 
- 高性能	高可用		高可扩
```

#### NoSQL 的四大分类

**kv键值对：**

- 新浪：Redis
- 美团：Redis + Tair
- 阿里、百度：Redis + memecache

**文档型数据库（bson格式和json一样）：**

- MongoDB （一般必须要掌握）
  - MongoDB 是一个基于分布式文件存储的数据库，c++编写，主要用来处理大量的文！
  - MongoDB 是一个介于关系型数据库和非关系型数据库中间的产品！MongoDB 是非关系型数据库中功能最丰富，最像关系型数据库！
- ConthDB

**列存储数据库**

- HBase
- 分布式文件系统

## Redis 入门

### 概述

> Redis 是什么

Redis（`R`emote `D`ictonary `S`erver），即远程字典服务

> Redis 能干嘛？

1、内存存储、持久化，内存中是断电即失、所以说持久化很重要（rdb，aof）

2、效率高，可以用于高速缓存

3、发布订阅系统

4、地图信息分析

5、计时器，计数器



> 特性

1、多样的数据类型

2、持久化

3、集群

4、事务

### Linux 安装

地址[在 Linux 上安装 Redis |雷迪斯](https://redis.io/docs/getting-started/installation/install-redis-on-linux/)

1、下载安装包！

2、解压Redis的安装包！ 程序/opt

![image-20230620224628415](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230620224628415.png)

3、进入解压后的文件，可以看到Redis的配置文件

![image-20230620225635942](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230620225635942.png)

4、基本的环境安装

```shell
yum install gcc-c++

make

make install
```

![image-20230620230050108](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230620230050108.png)

![image-20230620230352634](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230620230352634.png)

![image-20230620230436960](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230620230436960.png)

5、Redis的默认安装路径 `usr/local/bin`

![image-20230620230718166](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230620230718166.png)

6、将Redis配置文件。复制到当前目录下，方便日后使用

![image-20230620231032676](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230620231032676.png)

7、Redis默认不是后台启动，修改配置文件

![image-20230620231308917](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230620231308917.png)

8、启动Redis 服务

启动：redis-server valueconfig/redis.conf

![image-20230620232121609](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230620232121609.png)

查看：ps -ef | grep redis

![image-20230620231638341](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230620231638341.png)

9、测试连接：redis-cli -p 6379

![image-20230620232306479](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230620232306479.png)

10、关闭Redis 服务：shutdown

![image-20230620233124913](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230620233124913.png)

## 测试性能

**redis-benchmark**是一个压力测试工具！

Redis 性能测试工具参数如下所示：

| 选项 | 描述                                       | 默认值    |
| ---- | ------------------------------------------ | --------- |
| -h   | 指定服务器主机名                           | 127.0.0.1 |
| -p   | 指定服务器端口                             | 6379      |
| -s   | 指定服务器 socket                          |           |
| -c   | 指定并发连接数                             | 50        |
| -n   | 指定请求数                                 | 10000     |
| -d   | 以字节的形式指定 SET/GET 值的数据大小      | 3         |
| -k   | 1 = keep alive 0 = reconnect               | 1         |
| -r   | SET/GET/INCR 使用随机 key，SADD 使用随机值 |           |
| -p   | 通过管道传输 <nupreq> 请求                 | 1         |
| -q   | 强制退出 redis。仅显示 query/sec 值        |           |
| -csv | 以 CSV 格式输出                            |           |
| -i   | 生成循环，永久执行测试                     |           |
| -t   | 仅运行以逗号分隔的测试命令列表             |           |
| l    | idle 模式。仅打开 N 个 idle 连接并等待。   |           |

简单测试

```bash
# 测试： 100 哥个并发连接 100000 请求
redis-benchark -h localhost -p 6379 -c 100 -n 100000
```



![image-20230613224324404](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230613224324404.png)

## 基础的知识

Redis 默认有16个数据库

![image-20230613233613271](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230613233613271.png)

默认使用的是第0个数据库

可以使使用 select 进行切换数据！

```bash
127.0.0.1:6379> select 3 		# 切换数据库
OK
127.0.0.1:6379[3]> dbsize		# 查看 DB 大小！
(integer) 0

127.0.0.1:6379[3]> set name value		# 创建数据
OK
127.0.0.1:6379[3]> dbsize
(integer) 1
127.0.0.1:6379[3]> get name
"value"

127.0.0.1:6379[3]> keys *		# 查看所有的 key
1) "name"
```

清空当前数据库`flushdb`

清空全部数据库的内容`flushall`

```bash
127.0.0.1:6379[3]> flushdb
OK
127.0.0.1:6379[3]> keys *
(empty list or set)
```

## 五大类型

### Redis-key

```shell
127.0.0.1:6379> set name value
OK
127.0.0.1:6379> exists name		# 判断当前的key是否存在
(integer) 1
127.0.0.1:6379> move name 1		# 移除当前的 key
(integer) 1
127.0.0.1:6379> keys *
1) "counter:__rand_int__"
2) "mylist"
3) "key:__rand_int__"
127.0.0.1:6379>

127.0.0.1:6379> expire name 10		# 设置key的过期时间，单位是秒
(integer) 0
127.0.0.1:6379> ttl name		# 查看当前可以的剩余时间
(integer) -2
```

### string

```bash
127.0.0.1:6379> set key1 v1		# 设置值
OK
127.0.0.1:6379> get key1		# 获得值
"v1"
127.0.0.1:6379> keys *			# 获得所有的key
1) "counter:__rand_int__"
2) "mylist"
3) "key1"
4) "key:__rand_int__"
127.0.0.1:6379> exists keys		# 判断某一个 key 是否存在
(integer) 0
127.0.0.1:6379> exists key1
(integer) 1
127.0.0.1:6379> append key1 "hello"		# 追加字符串，如果当前key不存在，就相当于setkey
(integer) 7
127.0.0.1:6379> get key1
"v1hello"
127.0.0.1:6379> strlen key1			# 获取字符串长度
(integer) 7

###########################################################################

# 步长
127.0.0.1:6379> set views 0		# 初始化浏览量为 0
OK
127.0.0.1:6379> get views
"0"
127.0.0.1:6379> incr views		# 自增1 
(integer) 1
127.0.0.1:6379> incr views
(integer) 2
127.0.0.1:6379> decr views		# 自减1
(integer) 1
127.0.0.1:6379> decr views
(integer) 0
127.0.0.1:6379> decr views
(integer) -1
127.0.0.1:6379> get views
"-1"
127.0.0.1:6379> incrby views 10		# 可以设置步长
(integer) 9
127.0.0.1:6379> incrby views 10
(integer) 19
127.0.0.1:6379>

###########################################################################

# 字符串范围
127.0.0.1:6379> set key1 "hello,value123"		# 设置key1 的值
OK
127.0.0.1:6379> get key1
"hello,value123"
127.0.0.1:6379> getrange key1 0 3		# 截取字符串  [0,3]
"hell"
127.0.0.1:6379> getrange key1 0 -1		# 获取全部字符串 和 get key 是一样的
"hello,value123"

###########################################################################

# 替换
127.0.0.1:6379> set key2 abcd
OK
127.0.0.1:6379> get key2
"abcd"
127.0.0.1:6379> setrange key2 1 xx		# 指定位置开始的字符串
(integer) 4
127.0.0.1:6379> get key2
"axxd"

###########################################################################
# setex (set with expire)		# 设置过期时间
# setnx (set if not exist)		# 不存在再设置（在分布式锁中会常常使用！）

127.0.0.1:6379> setex key3 30 "hello"		# 设置key3的值为 hello ，30 秒后过期
OK
127.0.0.1:6379> ttl key3
(integer) 25
127.0.0.1:6379> get key3
"hello"
127.0.0.1:6379> setnx mykey "redis"			# 如果 kykey 不存在，创建mykey
(integer) 1
127.0.0.1:6379> keys *
1) "key1"
2) "key2"
3) "mykey"
127.0.0.1:6379> ttl key3
(integer) -2
127.0.0.1:6379> setnx mykey "MongoDB"		# 如果mykey存在，创建失败！
(integer) 0
127.0.0.1:6379> get mykey
"redis"

###########################################################################

127.0.0.1:6379> mset k1 v1 k2 v2 k3 v3		# 同时设置多个值
OK
127.0.0.1:6379> keys *
1) "k1"
2) "k2"
3) "k3"
127.0.0.1:6379> mget k1 k2 k3		# 同时获取多个值
1) "v1"
2) "v2"
3) "v3"
127.0.0.1:6379> msetnx k1 v1 k4 v4		# msetnx 是一个原子操作，要么一起成功，要么一起失败！
(integer) 0
127.0.0.1:6379> get k4
(nil)


# 对象
set user:1 {name:value123,age:3}  # 设置一个 user:1 对象 只为 json 字符串保存一个对象！

# 这里的 key 是一个巧妙的设计：user:{id}:{filed}， 如此设计在 Redis 中是完全 OK 了！

127.0.0.1:6379> mset user:1:name value123 user:1:age 2
OK
127.0.0.1:6379> mget user:1:name user:1:age
1) "value123"
2) "2"

###########################################################################
getset # 先 get 然后在 set

127.0.0.1:6379> getset dp redis		# 如果不存在值，则返回 nil
(nil)
127.0.0.1:6379> get dp
"redis"
127.0.0.1:6379> getset dp moredis		# 如果存在值，获取原来的值，并设置新的值
"redis"
127.0.0.1:6379> get dp
"moredis"
```

数据结构是相同的。

### list

在 Redis 里面，可以把list 完成、栈、队列、阻塞队列！

所哟命令都是以 ‘l’开头的

```shell
127.0.0.1:6379> lpush list one		# 将一个值或者多个值，插入到列表头部（左）
(integer) 1
127.0.0.1:6379> lpush list two
(integer) 2
127.0.0.1:6379> lpush list three
(integer) 3
127.0.0.1:6379> lrange list 0 -1		# 获取区间值
1) "three"
2) "two"
3) "one"
127.0.0.1:6379> lrange list 0 1
1) "three"
2) "two"

###########################################################################

127.0.0.1:6379> rpush list rigdis		# 将一个值或者多个值，插入到列表头部（右）
(integer) 4
127.0.0.1:6379> lrange list 0 -1
1) "three"
2) "two"
3) "one"
4) "rigdis"

###########################################################################

127.0.0.1:6379> lrange list 0 -1
1) "three"
2) "two"
3) "one"
4) "rigdis"
127.0.0.1:6379> lpop list		# 移除list一个元素（左）
"three"
127.0.0.1:6379> rpop list		# 移除list一个元素（右）
"rigdis"
127.0.0.1:6379> lrange list 0 -1
1) "two"
2) "one"

###########################################################################

127.0.0.1:6379> lrange list 0 -1
1) "two"
2) "one"
127.0.0.1:6379> lindex list 1		# 通过下标获得 list 中的某一个值！
"one"
127.0.0.1:6379> lindex list 0
"two"

###########################################################################

127.0.0.1:6379> llen list		# 返回列表的长度
(integer) 2

###########################################################################

# 移除指定的值
127.0.0.1:6379> lrem list 1 one    # 移除指定的值 数字：移除几个
(integer) 1

###########################################################################

127.0.0.1:6379> lrange mylist 0 -1
1) "hello"
2) "hello1"
3) "hello2"
4) "hello3"
127.0.0.1:6379> ltrim mylist 1 2		# 通过下标截取指定长度
OK
127.0.0.1:6379> lrange mylist 0 -1
1) "hello1"
2) "hello2"

###########################################################################

127.0.0.1:6379> lrange lylist 0 -1
1) "hello"
2) "hello1"
3) "hello2"
127.0.0.1:6379> rpoplpush lylist mylist  # 移除列表的最后一个元素，将它移动到新的列表中
"hello2"
127.0.0.1:6379> lrange lylist 0 -1		# 查看旧表
1) "hello"
2) "hello1"
127.0.0.1:6379> lrange mylist 0 -1		# 查看新表
1) "hello2"

###########################################################################

127.0.0.1:6379> exists mylist		# 判断这个列表是否存在
(integer) 1
127.0.0.1:6379> lrange mylist 0 0
1) "hello2"
127.0.0.1:6379> lset mylist 0 item		# 如果存在，更新或替换当前下标的值，更新操作
OK
127.0.0.1:6379> lrange mylist 0 0
1) "item"

###########################################################################

127.0.0.1:6379> rpush mylist "hello" "world"
(integer) 2 
127.0.0.1:6379> linsert mylist before world "other"  		# 将某个具体的Value插入到其中某个元素的前面或者后面
(integer) 3
127.0.0.1:6379> lrange mylist 0 -1
1) "hello"
2) "other"
3) "world"

127.0.0.1:6379> linsert mylist after world "new"
(integer) 4
127.0.0.1:6379> lrange mylist 0 -1
1) "hello"
2) "other"
3) "world"
4) "new"
```

### set（集合）

```shell
127.0.0.1:6379> sadd myset "hello"		# set 集合中添加元素
(integer) 1
127.0.0.1:6379> sadd myset "value123" "lockevalue"
(integer) 2
127.0.0.1:6379> smembers myset			# 查看指定set的所有值
1) "hello"
2) "lockevalue"
3) "value123"
127.0.0.1:6379> sismember myset hello		# 判断某一个值是否在 set 集合当中！
(integer) 1

###########################################################################

127.0.0.1:6379> scard myset		# 统计元素个数
(integer) 3

###########################################################################

127.0.0.1:6379> srem myset hello		# 移除set集合中指定的元素
(integer) 1
127.0.0.1:6379> scard myset
(integer) 2
127.0.0.1:6379> smembers myset
1) "lockevalue"
2) "value123"

###########################################################################

127.0.0.1:6379> smembers myset
1) "lockevalue"
2) "value123"
127.0.0.1:6379> SRANDMEMBER myset		# 随机抽选出一个元素
"value123"

###########################################################################

127.0.0.1:6379> SMEMBERS myset
1) "lockevalue"
2) "value123"
127.0.0.1:6379> spop myset			# 随机删除一些 set 集合中的元素
"lockevalue"
127.0.0.1:6379> SMEMBERS myset
1) "value123"

###########################################################################

127.0.0.1:6379> sadd myset "hello" "world" "value123" "set2"
(integer) 4
127.0.0.1:6379> smove myset myset2 "hello"		# 将一个指定的值，移动到另外一个 set 集合！
(integer) 1
127.0.0.1:6379> SMEMBERS myset
1) "set2"
2) "world"
3) "value123"
127.0.0.1:6379> SMEMBERS myset2
1) "hello"

###########################################################################

数字集合类：
	- 差集 SDIFF
	- 交集 SINTER
	- 并集 SUNION
	
127.0.0.1:6379> sadd key1 "a" "b" "c" "d" "e"
(integer) 5
127.0.0.1:6379> sadd key2 "a" "f" "d" "h" "i"
(integer) 5
127.0.0.1:6379> SDIFF key1 key2			# 差集
1) "e"
2) "b"
3) "c"
127.0.0.1:6379> SINTER key1 key2		# 交集
1) "d"
2) "a"
127.0.0.1:6379> SUNION key1 key2		# 并集
1) "d"
2) "b"
3) "i"
4) "a"
5) "h"
6) "f"
7) "e"
8) "c"


```

### Hash

Map 集合，KeyMap集合！

```shell
127.0.0.1:6379> hset myhash field1 value123		# set 一个具体 key-value
(integer) 1
127.0.0.1:6379> hget myhash field1			# 获取一个字段值
"value123"
127.0.0.1:6379> hmset myhash field1 hello field2 world		# set 多个 key-value
OK
127.0.0.1:6379> hmget myhash field1 field2			# 获取多个字段值
1) "hello"
2) "world"
127.0.0.1:6379> hgetall myhash			# 获取全部数据
1) "field1"
2) "hello"
3) "field2"
4) "world"

127.0.0.1:6379> hdel myhash field1		# 删除 hash 指定 key 字段！对应的value的值也就消失了
(integer) 1
127.0.0.1:6379> hgetall myhash
1) "field2"
2) "world"

###########################################################################

127.0.0.1:6379> hgetall myhash
1) "field2"
2) "world"
3) "field1"
4) "hello"
127.0.0.1:6379> hlen myhash			# 获取 hash 表的字段数量
(integer) 2

###########################################################################

127.0.0.1:6379> hexists myhash field1		# 判断 hash 中指定字段是否存在！
(integer) 1

###########################################################################

127.0.0.1:6379> hkeys myhash		# 只获取所有 field
1) "field2"
2) "field1"
127.0.0.1:6379> hvals myhash		# 只获得所有 value
1) "world"
2) "hello"

###########################################################################

127.0.0.1:6379> hset myhash field3 5		# 指定增量
(integer) 1
127.0.0.1:6379> HINCRBY myhash field3 1
(integer) 6
127.0.0.1:6379> HINCRBY myhash field3 -1
(integer) 5
127.0.0.1:6379> hsetnx myhash field4 hello		# 如果不存在则可以设置
(integer) 1
```

hash 变更的数据 user name age，尤其是用户信息之类的，经常变动的信息！hash 更适合于对象的存储，string 更加适合字符串存储！

### zset（有序集合）

在 set 的基础上，增加了一个值，set k1 v1， zst k1 score1 v1

```shell
127.0.0.1:6379> zadd myset 1 one		# 添加一个值
(integer) 1
127.0.0.1:6379> zadd myset 2 two 3 three		# 添加多个值
(integer) 2
127.0.0.1:6379> zrange myset 0 -1
1) "one"
2) "two"
3) "three"

###########################################################################

# 排序实现
127.0.0.1:6379> zadd salary 2500 xiaohong 5000 zhangsan 500 value123		# 添加三个用户
(integer) 3
127.0.0.1:6379> ZRANGEBYSCORE salary -inf +inf		# 升序排列
1) "value123"
2) "xiaohong"
3) "zhangsan"
127.0.0.1:6379> ZREVRANGE salary 0 -1		# 降序排列
1) "zhangsan"
2) "value123"
127.0.0.1:6379> ZRANGEBYSCORE salary -inf +inf withscores		# 显示全部的用户并且附带成绩
1) "value123"
2) "500"
3) "xiaohong"
4) "2500"
5) "zhangsan"
6) "5000"
127.0.0.1:6379> ZRANGEBYSCORE salary -inf 2500 withscores		# 显示工资小于 2500 员工的降序排列！
1) "value123"
2) "500"
3) "xiaohong"
4) "2500"

###########################################################################

# 移除rem中的元素
127.0.0.1:6379> zrange salary 0 -1
1) "value123"
2) "xiaohong"
3) "zhangsan"
127.0.0.1:6379> zrem salary xiaohong		# 移除指定元素
(integer) 1
127.0.0.1:6379> zrange salary 0 -1
1) "value123"
2) "zhangsan"
127.0.0.1:6379> ZCARD salary		# 获取有序集合中的个数
(integer) 2

###########################################################################

# 区间获取
127.0.0.1:6379> zadd myset 1 hello 2 world 3 value123
(integer) 3
127.0.0.1:6379> ZCOUNT myset 1 3		# 区间获取
(integer) 3
127.0.0.1:6379> zcount myset 1 2
(integer) 2
```

## 三种特殊数据类型

### geospatial 地理位置

#### geoadd 添加地理位置

```shell
# geoadd 添加地理位置
# 参数 key 值（经度，纬度，名称）
# 有效的经度从 -180度到180度。
# 有效的纬度从 -85.05112878 度到 85.05112878 度。

127.0.0.1:6379> geoadd china:city 116.40 39.90 beijing 121.47 31.23 shanghai 106.50 29.53 chongqing 114.05 22.52 shengzhen 120.16 30.24 hangzhou 108.96 34.26 xian
(integer) 6
```

#### geopos 查询

```shell
# geopos 查询 
127.0.0.1:6379> GEOPOS china:city beijing		# 获取指定城市的经度和维度
1) 1) "116.39999896287918"
   2) "39.900000091670925"
127.0.0.1:6379> GEOPOS china:city beijing chongqing
1) 1) "116.39999896287918"
   2) "39.900000091670925"
2) 1) "106.49999767541885"
   2) "29.529999579006592"
```

#### geodist 之间距离

单位：

- **m 表示单位为米。**
- **km 表示为千米。**
- **mi表示单位为英里。**
- **ft 表示单位为英尺。**

```shell
127.0.0.1:6379> geodist china:city beijing shanghai km  # 查看上海到北京的直线距离
"1067.3788"
127.0.0.1:6379> geodist china:city beijing chongqing km
"1464.0708"
```

#### georadius 范围查找

```shell
# georadius 以给定的经度为中心，找出某一半径内的元素
127.0.0.1:6379> GEORADIUS china:city 110 30 800 km		# 以 110 30 为点，半径 800km 为查找范围
1) "chongqing"
2) "xian"
127.0.0.1:6379> GEORADIUS china:city 100 30 800 km withdist		# 显示到中间距离的位置
1) 1) "chongqing"
   2) "629.6756"
127.0.0.1:6379> GEORADIUS china:city 110 30 800 km withcoord  # 显示用户的位置信息
1) 1) "chongqing"
   2) 1) "106.49999767541885"
      2) "29.529999579006592"
2) 1) "xian"
   2) 1) "108.96000176668167"
      2) "34.2599996441893"
127.0.0.1:6379>  GEORADIUS china:city 110 30 800 km withcoord count 2		# 筛选出指定结果
1) 1) "chongqing"
   2) 1) "106.49999767541885"
      2) "29.529999579006592"
2) 1) "xian"
   2) 1) "108.96000176668167"
      2) "34.2599996441893"
127.0.0.1:6379>  GEORADIUS china:city 110 30 800 km withcoord count 1
1) 1) "chongqing"
   2) 1) "106.49999767541885"
      2) "29.529999579006592"
```

#### GEORADIUSBYMEMBER 找出指定位置周围

```shell
# 找出位于指定元素周围的其他元素！

chongqing 114.05 22.127.0.0.1:6379> GEORADIUSBYMEMBER china:city beijing 1000 km
1) "beijing"
2) "xian"
```

#### geohash 命令

```shell
# 该命令将返回11个字符串的 geohash 字符串！
# 二维的经纬度转换为 一维的字符串！如果两个字符串越接近，那么则距离越近！
127.0.0.1:6379> geohash china:city beijing chongqing
1) "wx4fbxxfke0"
2) "wm5xzrybty0"
```

> geo 底层的实现原理其实就是 zset ！ 可以使用 zset 命令来操作 geo！

 ```shell
127.0.0.1:6379> zrange china:city 0 -1			# 查看地图中全部的元素
1) "chongqing"
2) "xian"
3) "shengzhen"
4) "hangzhou"
5) "shanghai"
6) "beijing"
127.0.0.1:6379> zrem china:city beijing			# 移除元素
(integer) 1
127.0.0.1:6379> zrange china:city 0 -1
1) "chongqing"
2) "xian"
3) "shengzhen"
4) "hangzhou"
5) "shanghai"
 ```

### hyperloglog

hyperloglog 基数统计的算法！

**网页的uv（一个人访问一个网站多次，但是还是算作一个人）**

> 测试使用

```shell
127.0.0.1:6379> PFADD mykey a b c d e f g h i j		# 创建第一组元素 mykey
(integer) 1
127.0.0.1:6379> PFCOUNT mykey		# 统计 mykey 元素的基数数量
(integer) 10
127.0.0.1:6379> PFADD mykey2 i j z x c v b n m		# 创建第二组元素 mykey
(integer) 1
127.0.0.1:6379> PFMERGE mykey3 mykey mykey2			# 合并两组 mykey mykey2 => mykey3 并集
OK
127.0.0.1:6379> PFCOUNT mykey3		# 再次查看
(integer) 15
```

如果允许容错，就可以使用 huperloglog！！

### Bitmap

> 位存储

bitmap 位图，数据结构！ 都是操作二进制位来进行记录，就只有 0 和 1 两个状态1

```shell
127.0.0.1:6379> setbit sign 0 1		# 存储
(integer) 0
127.0.0.1:6379> getbit sign 0		# 读取
(integer) 1

# 统计操作

127.0.0.1:6379> bitcount sign		# 统计记录操作
(integer) 1
```

## 事务

Redis 事务本质：一组命令的集合！ 一个事务中所有的命令都会被序列化，在事务执行过程的中，会按照顺序执行！

一次性，顺序性，排他性！ 执行一些列的命令

`Redis 事务没有隔离级别的概念！`

所有的命令在事务中，并没有直接被执行！只有发起执行命令的时候才会执行！ exec

**Redis 单条命令保存原子性的，但是事务不保证原子性！**

Redis 的事务：

- 开启事务（multi）
- 命令入队（....）
- 执行事务（exec）

> 正常执行事务！

```shell
127.0.0.1:6379> multi		# 开启事务
OK
# 命令入队
127.0.0.1:6379> set k1 v1
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> get k2
QUEUED
127.0.0.1:6379> set k3 v3
QUEUED
127.0.0.1:6379> exec	# 执行事务
1) OK
2) OK
3) "v2"
4) OK
```

> 放弃事务

```shell
127.0.0.1:6379> multi		# 开启事务
OK
127.0.0.1:6379> set k1 v1
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> set k4 v4
QUEUED
127.0.0.1:6379> discard		# 取消事务
OK
127.0.0.1:6379> get k4
(nil)
```

> 监控！ watch

**悲观锁：**

- 很悲观，认为什么时候都会出现问题，无论做什么都会加锁！

**乐观锁：**

- 很乐观，认为什么时候都不会出问题，所以不会上锁！更新数据的时候去判断一下，在此间是否有人修改过这个数据。
- 获取 version
- 更新的时候比较 version

> Redis 测监视测试

```shell
127.0.0.1:6379> set money 100
OK
127.0.0.1:6379> set out 0
OK
127.0.0.1:6379> watch money		# 监视 money 对象
OK
127.0.0.1:6379> multi		# 事务正常结束，数据期间没有发生变动，这个时候就正常只执行成功！
OK
127.0.0.1:6379> decrby money 20
QUEUED
127.0.0.1:6379> incrby out 20
QUEUED
127.0.0.1:6379> exec
1) (integer) 80
2) (integer) 20
127.0.0.1:6379> unwatch		# 解锁
OK
```

## Redis.conf 详解

启动的时候，就通过配置文件来启动！

![image-20230618014339228](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230618014339228.png)

1、配置文件 unit 单位对大小写不敏感！

> 包含

![image-20230618014455633](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230618014455633.png)

> 网络

![image-20230618014608224](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230618014608224.png)

> 网络

```shell
bind 127.0.0.1		# 绑定的 ip
protected-mode yes		# 保护模式
port 6379		# 端口设置
```

> 通用 GENERAL

```shell
daemonize yes		# 以守护进程的方式运行，默认是 no，需要自己开启为 yes！
# 日志
# Specify the server verbosity level.
# This can be one of:
# debug (a lot of information, useful for development/testing)
# verbose (many rarely useful info, but not a mess like the debug level)
# notice (moderately verbose, what you want in production probably)
# warning (only very important / critical messages are logged)
loglevel notice
logfile ""		# 日志的文件位置名
databases 16	# 数据库的数量，默认是 16 个数据库
```

> 快照

持久化：在规定的时间内，执行了多少次操作，则会持久化到文件 .rdb.aof

Redis 是内存数据库，如果没有持久化，那么数据断电即失！

```shell
# 如果900s内，如果至少有 1 key 进行了修改，我及时进行持久化操作！
save 900 1
# 如果300s内，如果至少有 10 key 进行了修改，我及时进行持久化操作！
save 300 10
# 如果60s内，如果至少有 10000 key 进行了修改，我及时进行持久化操作！
save 60 10000

stop-writes-on-bgsave-error yes		# 持久化如果出错，是否还需要继续操作

rdbcompression yes	# 是否压缩 rdb 文件，需要消耗一些CPU资源！

rdbchecksum yes		# 保存 rdb 文件的时候，进行错误检查！、

dir ./		# rdb 文件保存的目录！
```

> REPLICATION





> SECURITY 安全

可以在这里设置 Redis 的密码，默认是没有密码！

```shell
127.0.0.1:6379> config get requirepass			# 获取 Redis 的密码
1) "requirepass"
2) ""
127.0.0.1:6379> config set requirepass "value123"		# 设置 Redis 的密码
OK
127.0.0.1:6379> ping
(error) NOAUTH Authentication required.
127.0.0.1:6379> config get requirepass
(error) NOAUTH Authentication required.
127.0.0.1:6379> auth value123		# 登录恢复使用
OK
127.0.0.1:6379> config get requirepass
1) "requirepass"
2) "value123"
127.0.0.1:6379>
```

> 限制 clients

```shell
maxclients 10000		# 设置最大客户端连接数量

maxmemory <bytes>		# Redis 配置的最大内存容量

maxmemory-policy noeviction		# 内存达到上限之后的处理策略
        1、volatile-lru：只对设置了过期时间的key进行LRU（默认值） 
        2、allkeys-lru ： 删除lru算法的key   
        3、volatile-random：随机删除即将过期key   
        4、allkeys-random：随机删除   
        5、volatile-ttl ： 删除即将过期的   
        6、noeviction ： 永不过期，返回错误
```

> APPEND ONLY MODE 模式 aof 配置

```shell
appendonly no	# 默认是不开启 aof 模式的，默认是使用 rdb 方式持久化的，在大部分所有的情况下，rdb 完全够用！
appendfilename "appendonly.aof"		# 持久化的文件配置

# appendfsync always		# 每次修改都会 sync 消耗性能
appendfsync everysec		# 没秒执行一次 sync 可能会丢失 ls 的数据
# appendfsync no			# 不执行 sync 这个时候操作系统自己同步数据，速度最快！
```

## Redis 持久化

Redis 是内存数据库，如果给你不将内存中的数据库状态保存到磁盘，那么一旦服务器进程退出，服务器中的数据库状态也会消失。所以 Redis 提供了持久化功能!

## RDB(Redis DateBase)

> 什么是RDB

![image-20230619114148247](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230619114148247.png)

在指定的时间间隔内将内存中的数据集快照写入磁盘，也就是讲的 Snapshot 快照，它恢复时将快照文件直接读到内存里。

Redis 会单独创建（fork）一个字进程来进行持久化，会先将数据写入到一个临时文件中，待持久化过程都结束了，再用这个临时问问价替换上次持久化的文件。整个过程中，主进程是不进行任何io操作的。这就确保了极高的性能。如果需要进行大规模数据的恢复，且对数据恢复的完整性不是非常敏感，那么 rdb 方式要比 aof 方式更加的高效。rdb 的缺点是最后一个持久化后的数据可能丢失。

==rdb 保存的文件是 dump.rdb==都是在配置文件中快照中进行配置的！

![image-20230619140044992](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230619140044992.png)

![image-20230619140219542](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230619140219542.png)



> 重写

aof 默认就是文件的无限追加，文件会越来越大！

![image-20230619151432220](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230619151432220.png)

如果 aof 文件大于 64m ，太大了！ fork 一个新的进程来讲文件进行重写！

> 优点和缺点

```shell
appendonly no	# 默认是不开启 aof 模式的，默认是使用 rdb 方式持久化的，在大部分所有的情况下，rdb 完全够用！
appendfilename "appendonly.aof"		# 持久化的文件配置

# appendfsync always		# 每次修改都会 sync 消耗性能
appendfsync everysec		# 没秒执行一次 sync 可能会丢失 ls 的数据
# appendfsync no			# 不执行 sync 这个时候操作系统自己同步数据，速度最快！
```

优点：

1. 每一次修改都同步，文件的完整性会更更加好！
2. 每秒同步一次，可能会丢失一秒的数据！
3. 从不同步，效率最高！

缺点：

1. 相对于数据文件来说，aof 远远大于 rdb，修复的速度也比 rdb 慢
2. aof 运行效率也要比 rdb 慢，所以 Redis 默认的配置就是 rdb 持久化！

## AOF（Append Only File）

将所有的命令都记下来，history ，恢复的时候就把这个文件全部都执行一遍！

![image-20230619215732095](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230619215732095.png)

以日志的形式来记录每个写操作，将 Redis 执行过程的所有指令记录下来（读操作不记录），只许追加文件但不可以改写文件，Redis 启动之初会读取该文件重新构建数据，换言之，Redis 启动的话就根据日志文件的内容将写指令从前到后执行一次以完成数据的恢复工作。

==Aof 保存的是 appendonly.aof 文件==

> append

![image-20230619220908566](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230619220908566.png)

> 修复工具

```shell
# 修复工具命令
redis-check-aof --fix appendonly.aof
```

## Redis 订阅发布

> 测试

订阅端：

```shell
127.0.0.1:6379> SUBSCRIBE value123		# 订阅一个频道
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "value123"
3) (integer) 1
# 等待读取推送的信息
1) "message"
2) "value123"
3) "hello,value"
1) "message"
2) "value123"
3) "hello,redis"
```

发送端：

```shell
127.0.0.1:6379> PUBLISH value123 "hello,value"			# 发送一个频道
(integer) 1
127.0.0.1:6379> publish value123 "hello,redis"
(integer) 1
```



## Redis 主从复制

主从复制，读写分离！ 80% 的情况下都是在进行读操作！减缓服务器的压力！ 架构中经常使用！ 一主二从！

### 环境配置

只配置从库

```shell
127.0.0.1:6379> info replication		# 查看当前库的信息
# Replication
role:master		# 角色 master
connected_slaves:0		# 没有从机
master_failover_state:no-failover
master_replid:405b664ff8851d128bf359423cdd490046d361d5
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0

```

复制3个配置文件，然后修改对应的信息

1、端口

2、pid 名字

3、log 文件名字

4、dump.rdb 名字

修改完毕之后，启动这3个Redis 服务器，可以通过进程信息查看！

![image-20230622170818229](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230622170818229.png)

### 一主二从

`默认情况下，每台Redis服务器都是主节点；`一般情况下只用配置从机就好了！

```shell
slaveof 主机名 端口号

# 从机中查看
127.0.0.1:6380> info replication
# Replication
role:slave
master_host:127.0.0.1
master_port:6379
master_link_status:up
master_last_io_seconds_ago:3
master_sync_in_progress:0
slave_read_repl_offset:14
slave_repl_offset:14
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:14d73947ebf5561ca9ea0f236751251fdcfcd6c3
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:14
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:14

# 主机中查看
127.0.0.1:6379> info replication
# Replication
role:master
connected_slaves:2
slave0:ip=127.0.0.1,port=6380,state=online,offset=378,lag=0
slave1:ip=127.0.0.1,port=6381,state=online,offset=378,lag=0
master_failover_state:no-failover
master_replid:14d73947ebf5561ca9ea0f236751251fdcfcd6c3
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:378
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:378

```

真实环境中配置因该是在配置文件中配置，这样的话是永久的，但是此时演示的是命令。

> 细节

主机可以写，从机不能写只能读，主机中的所有信息和数据，都会自动被从机保存！

主机写：

![image-20230622211806907](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230622211806907.png)

从机读：

![image-20230622211834512](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230622211834512.png)

测试：主机断开连接，从机依旧连接到主机的，但是没有写操作，这个时候，主机回来了，从机依旧可以直接获取到主机写的信息！

如果是使用命令行，来配置的主从，这个时候如果重启了，就会变回主机！只要变为从机，立马就会从主机中获取值！

> 复制原理

slave 启动成功连接到 master 后会发送一个 sync 同步命令

master 接到命令，启动后台的存盘进程，同时收集所有几首到的用于修改数据集命令，在后台进程执行完毕之后，``master 将传送整个数据文件到 slave ，并完成一次完全同步。`

全量复制：而 slave 服务在接收到数据库文件数据后，将器存盘加载到内存中。

增量复制：master 继续将新的所有收集的修改命令依次传给 slave，完成同步。

但是只要是重新连接 master ，一次完全同步（全量复制）将被自动执行! 我们的数据一定可以在从机中看到！

> 层层链路

上一个

![image-20230622214244708](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230622214244708.png)

这个时候也可以完成主从复制！

> 如果没有首节点，使用命令使得当前成为首节点！

```shell
slaveof no one 		# 当前设置为首节点 主机 其他从机 也可以连接 我这个新的主机
```

### 哨兵模式

> 测试

1、配置哨兵配置文件 sentinel.conf

```shell
# sentinel monitor 被监控的名称 host port 1
# 后面这个数字 1，代表主机挂了，slave 投票看让谁接替成为主机，票数最多的，就会成为主机！
sentinel monitor myredis 127.0.0.1 6379 1
```

2、启动哨兵

```shell
[root@localhost bin]# redis-sentinel valueconfig/sentinel.conf | lolcat

2736:X 22 Jun 2023 22:12:49.778 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
2736:X 22 Jun 2023 22:12:49.778 # Redis version=7.0.11, bits=64, commit=00000000, modified=0, pid=2736, just started
2736:X 22 Jun 2023 22:12:49.778 # Configuration loaded
2736:X 22 Jun 2023 22:12:49.778 * Increased maximum number of open files to 10032 (it was originally set to 1024).
2736:X 22 Jun 2023 22:12:49.778 * monotonic clock: POSIX clock_gettime
2736:X 22 Jun 2023 22:12:49.778 * Running mode=sentinel, port=26379.
2736:X 22 Jun 2023 22:12:49.778 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
2736:X 22 Jun 2023 22:12:49.781 * Sentinel new configuration saved on disk
2736:X 22 Jun 2023 22:12:49.781 # Sentinel ID is 3d76490b8cf8aa971787be5ccf16b0085ccef799
2736:X 22 Jun 2023 22:12:49.781 # +monitor master myredis 127.0.0.1 6379 quorum 1
2736:X 22 Jun 2023 22:12:49.783 * +slave slave 127.0.0.1:6380 127.0.0.1 6380 @ myredis 127.0.0.1 6379
2736:X 22 Jun 2023 22:12:49.785 * Sentinel new configuration saved on disk
2736:X 22 Jun 2023 22:12:49.785 * +slave slave 127.0.0.1:6381 127.0.0.1 6381 @ myredis 127.0.0.1 6379
2736:X 22 Jun 2023 22:12:49.786 * Sentinel new configuration saved on disk

```

如果master节点断开了，这个时候就会从从机中随机选择一个服务器！

![image-20230622222552589](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230622222552589.png)

如果主机回来了也只能当新主机的从机

![image-20230622223141046](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230622223141046.png)

![image-20230622223159427](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230622223159427.png)

> 哨兵模式的优点和缺点

优点：

1、哨兵集群，基于主从复制模式，所有的主从配置优点，它全有。

2、主从可以切换，故障可以转移，系统的可用性就会更好。

3、哨兵模式就是主从模式的升级，手动哦到自动，更加健壮。

缺点：

1、Redis 不好在线扩容，集群容器一旦到达上限，在线扩容就十分麻烦！

2、实现哨兵模式的配置其实是很麻烦的，里面有很多选择！

> 哨兵模式的全部配置

## 一、redis.conf 配置项说明如下：

1. Redis默认不是以守护进程的方式运行，可以通过该配置项修改，使用yes启用守护进程

   ```bash
   daemonize no
   ```

2. 当Redis以守护进程方式运行时，Redis默认会把pid写入/var/run/redis.pid文件，可以通过pidfile指定

   pidfile /var/run/redis.pid

3. 指定Redis监听端口，默认端口为6379，作者在自己的一篇博文中解释了为什么选用6379作为默认端口，因为6379在手机按键上MERZ对应的号码，而MERZ取自意大利歌女Alessia Merz的名字

   ```shell
   port 6379
   ```

4. 绑定的主机地址

   ```shell
   bind 127.0.0.1
   ```

5. 当客户端闲置多长时间后关闭连接，如果指定为0，表示关闭该功能

   ```
   timeout 300
   ```

6. 指定日志记录级别，Redis总共支持四个级别：debug、verbose、notice、warning，默认为verbose

   ```
   loglevel verbose
   ```

7. 日志记录方式，默认为标准输出，如果配置Redis为守护进程方式运行，而这里又配置为日志记录方式为标准输出，则日志将会发送给/dev/null

   ```shell
   logfile stdout
   ```

8. 设置数据库的数量，默认数据库为0，可以使用SELECT 命令在连接上指定数据库id

   ```shell
   databases 16
   ```

9. 指定在多长时间内，有多少次更新操作，就将数据同步到数据文件，可以多个条件配合

   ```
   save <seconds> <changes>
   ```

   Redis默认配置文件中提供了三个条件：

   ```shell
   save 900 1
   
   save 300 10
   
   save 60 10000
   ```

   分别表示900秒（15分钟）内有1个更改，300秒（5分钟）内有10个更改以及60秒内有10000个更改。

10. 指定存储至本地数据库时是否压缩数据，默认为yes，Redis采用LZF压缩，如果为了节省CPU时间，可以关闭该选项，但会导致数据库文件变的巨大

    ```shell
    rdbcompression yes
    ```

11. 指定本地数据库文件名，默认值为dump.rdb

    ```shell
    dbfilename dump.rdb
    ```

12. 指定本地数据库存放目录

    ```shell
    dir ./
    ```

13. 设置当本机为slav服务时，设置master服务的IP地址及端口，在Redis启动时，它会自动从master进行数据同步

    ```shell
    slaveof <masterip> <masterport>
    ```

14. 当master服务设置了密码保护时，slav服务连接master的密码

    ```shell
    masterauth <master-password>
    ```

15. 设置Redis连接密码，如果配置了连接密码，客户端在连接Redis时需要通过AUTH 命令提供密码，默认关闭

    ```shell
    requirepass foobared
    ```

16. 设置同一时间最大客户端连接数，默认无限制，Redis可以同时打开的客户端连接数为Redis进程可以打开的最大文件描述符数，如果设置 maxclients 0，表示不作限制。当客户端连接数到达限制时，Redis会关闭新的连接并向客户端返回max number of clients reached错误信息

    ```shell
    maxclients 128
    ```

17. 指定Redis最大内存限制，Redis在启动时会把数据加载到内存中，达到最大内存后，Redis会先尝试清除已到期或即将到期的Key，当此方法处理 后，仍然到达最大内存设置，将无法再进行写入操作，但仍然可以进行读取操作。Redis新的vm机制，会把Key存放内存，Value会存放在swap区

    ```shell
    maxmemory <bytes>
    ```

18. 指定是否在每次更新操作后进行日志记录，Redis在默认情况下是异步的把数据写入磁盘，如果不开启，可能会在断电时导致一段时间内的数据丢失。因为 redis本身同步数据文件是按上面save条件来同步的，所以有的数据会在一段时间内只存在于内存中。默认为no

    ```shell
    appendonly no
    ```

19. 指定更新日志文件名，默认为appendonly.aof

    ```shell
    appendfilename appendonly.aof
    ```

20. 指定更新日志条件，共有3个可选值：

    ```shell
    no：表示等操作系统进行数据缓存同步到磁盘（快）
    always：表示每次更新操作后手动调用fsync()将数据写到磁盘（慢，安全）  
    everysec：表示每秒同步一次（折衷，默认值）
    appendfsync everysec
    ```

21. 指定是否启用虚拟内存机制，默认值为no，简单的介绍一下，VM机制将数据分页存放，由Redis将访问量较少的页即冷数据swap到磁盘上，访问多的页面由磁盘自动换出到内存中（在后面的文章我会仔细分析Redis的VM机制）

    ```shell
    vm-enabled no
    ```

22. 虚拟内存文件路径，默认值为/tmp/redis.swap，不可多个Redis实例共享

    ```shell
    vm-swap-file /tmp/redis.swap
    ```

23. 将所有大于vm-max-memory的数据存入虚拟内存,无论vm-max-memory设置多小,所有索引数据都是内存存储的(Redis的索引数据 就是keys),也就是说,当vm-max-memory设置为0的时候,其实是所有value都存在于磁盘。默认值为0

    ```shell
    vm-max-memory 0
    ```

24. Redis swap文件分成了很多的page，一个对象可以保存在多个page上面，但一个page上不能被多个对象共享，vm-page-size是要根据存储的 数据大小来设定的，作者建议如果存储很多小对象，page大小最好设置为32或者64bytes；如果存储很大大对象，则可以使用更大的page，如果不 确定，就使用默认值

    ```shell
    vm-page-size 32
    ```

25. 设置swap文件中的page数量，由于页表（一种表示页面空闲或使用的bitmap）是在放在内存中的，，在磁盘上每8个pages将消耗1byte的内存。

    ```shell
    vm-pages 134217728
    ```

26. 设置访问swap文件的线程数,最好不要超过机器的核数,如果设置为0,那么所有对swap文件的操作都是串行的，可能会造成比较长时间的延迟。默认值为4

    ```shell
    vm-max-threads 4
    ```

27. 设置在向客户端应答时，是否把较小的包合并为一个包发送，默认为开启

    ```shell
    glueoutputbuf yes
    ```

28. 指定在超过一定的数量或者最大的元素超过某一临界值时，采用一种特殊的哈希算法

    ```shell
    hash-max-zipmap-entries 64
    ```

    hash-max-zipmap-value 512

29. 指定是否激活重置哈希，默认为开启（后面在介绍Redis的哈希算法时具体介绍）

    ```
    activerehashing yes
    ```

30. 指定包含其它的配置文件，可以在同一主机上多个Redis实例之间使用同一份配置文件，而同时各个实例又拥有自己的特定配置文件

    ```shell
    include /path/to/local.conf
    ```

## 二、redis-[sentinel](https://so.csdn.net/so/search?q=sentinel&spm=1001.2101.3001.7020).conf配置项说明如下：

1. sentinel监听端口，默认是26379，可以修改。

   ```shell
   port 26379
   ```

2. 告诉sentinel去监听地址为ip:port的一个master，这里的master-name可以自定义，quorum是一个数字，指明当有多少个sentinel认为一个master失效时，master才算真正失效。master-name只能包含英文字母，数字，和“.-_”这三个字符需要注意的是master-ip 要写真实的ip地址而不要用回环地址（127.0.0.1）。

   ```shell
   sentinel monitor <master-name> <ip> <redis-port> <quorum>
   配置示例：
   sentinel monitor mymaster xx.xx.xx.xx 6379 2
   ```

3. 设置连接master和slave时的密码，注意的是sentinel不能分别为master和slave设置不同的密码，因此master和slave的密码应该设置相同。

   ```shell
   sentinel auth-pass <master-name> <password>
   配置示例：
   sentinel auth-pass mymaster 0123passw0rd
   ```

4. 这个配置项指定了需要多少失效时间，一个master才会被这个sentinel主观地认为是不可用的。 单位是毫秒，默认为30秒

   ```shell
   sentinel down-after-milliseconds <master-name> <milliseconds> 
   配置示例：
   sentinel down-after-milliseconds mymaster 30000
   ```

5. 这个配置项指定了在发生failover主备切换时最多可以有多少个slave同时对新的master进行 同步，这个数字越小，完成failover所需的时间就越长，但是如果这个数字越大，就意味着越 多的slave因为replication而不可用。可以通过将这个值设为 1 来保证每次只有一个slave 处于不能处理命令请求的状态。

   ```shell
   sentinel parallel-syncs <master-name> <numslaves> 
   配置示例：
   sentinel parallel-syncs mymaster 1
   ```

6. 哨兵故障转移超时

   ```shell
   sentinel failover-timeout <master-name> <milliseconds>
   配置示例：
   sentinel failover-timeout mymaster1 20000
   
   **failover-timeout 可以用在以下这些方面**
   1、同一个sentinel对同一个master两次failover之间的间隔时间。
   2、 当一个slave从一个错误的master那里同步数据开始计算时间。直到slave被纠正为向正确的master那里同步数据时。
   3、 当想要取消一个正在进行的failover所需要的时间。  
   4、 当进行failover时，配置所有slaves指向新的master所需的最大时间。不过，即使过了这个超时，slaves依然会被正确配置为指向master，但是就不按parallel-syncs所配置的规则来了。
   ```

7. sentinel的notification-script和reconfig-script是用来配置当某一事件发生时所需要执行的脚本，可以通过脚本来通知管理员，例如当系统运行不正常时发邮件通知相关人员。对于脚本的运行结果有以下规则：

   ```shell
   若脚本执行后返回1，那么该脚本稍后将会被再次执行，重复次数目前默认为10
   
   若脚本执行后返回2，或者比2更高的一个返回值，脚本将不会重复执行。
   
   如果脚本在执行过程中由于收到系统中断信号被终止了，则同返回值为1时的行为相同。
   
   一个脚本的最大执行时间为60s，如果超过这个时间，脚本将会被一个SIGKILL信号终止，之后重新执行。
   ```

   **1)**.通知型脚本:当sentinel有任何警告级别的事件发生时（比如说redis实例的主观失效和客观失效等等），将会去调用这个脚本，这时这个脚本应该通过邮件，SMS等方式去通知系统管理员关于系统不正常运行的信息。调用该脚本时，将传给脚本两个参数，一个是事件的类型，一个是事件的描述。如果sentinel.conf配置文件中配置了这个脚本路径，那么必须保证这个脚本存在于这个路径，并且是可执行的，否则sentinel无法正常启动成功。

   ```shell
   sentinel notification-script <master-name> <script-path> 
   配置示例：
   sentinel notification-script mymaster /var/redis/notify.sh
   ```

   **2)**. 当一个master由于failover而发生改变时，这个脚本将会被调用，通知相关的客户端关于master地址已经发生改变的信息。以下参数将会在调用脚本时传给脚本:

   ```shell
   sentinel client-reconfig-script <master-name> <script-path> <master-name> <role> <state> <from-ip> <from-port> <to-ip> <to-port>、
   配置示例：
   sentinel client-reconfig-script mymaster /var/redis/reconfig.sh
   ```

   目前总是“failover”, 是“leader”或者“observer”中的一个。 参数 from-ip, from-port, to-ip, to-port是用来和旧的master和新的master(即旧的slave)通信的。这个脚本应该是通用的，能被多次调用，不是针对性的。





