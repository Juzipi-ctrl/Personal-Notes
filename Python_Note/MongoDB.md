## Python MongoDB

MongoDB 是目前最流行的 nosql 数据库之一，使用的数据库类型 bson （类似 json）



### pymongo

Python 要连接 MongoDB 需要 MongoDB 驱动，这里使用 pymongo 驱动来连接。

#### pip 安装

pip 是一个通用的 Python 包管理工具，提供了对 Python 包的查找，下载，安装，卸载的功能。

1. 安装 pymongo：

```shell
$ python3 -m pip3 install pymongo
```

也可以指定安装的版本：

```python
$ python3 -m pip3 install pymongo==3.5.1
```

更新 pymongo 命令：

```python
$ python3 -m pip3 install --upgrade pymongo
```



### easy_install 安装

旧版的 Python 可以使用 easy_install 来安装，easy_install 也是 Python 包管理工具。

```python
$ python -m easy_install pymongo
```

更新 pymongo 命令：

```python
$ python -m easy_install -U pymongo
```

### 测试 pymongo

可以创建一个测试文件，代码如下：

```python
#!/usr/bin/python3
 
import pymongo
```

执行以上代码文件，如果没有出现报错，表示安装成功。



## 创建数据库

### 创建一个数据库

创建数据库需要使用 MongoClient 对象，并且指定连接的 URL 地址和要创建的数据库名。

如下实例中，我们创建的数据库 runoobdb :

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
```

> **注意:** 在 MongoDB 中，数据库只有在内容插入后才会创建! 就是说，数据库创建后要创建集合(数据表)并插入一个文档(记录)，数据库才会真正创建。

### 判断数据库是否已存在

我们可以读取 MongoDB 中的所有数据库，并判断指定的数据库是否存在：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient('mongodb://localhost:27017/')
 
dblist = myclient.list_database_names()
# dblist = myclient.database_names() 
if "runoobdb" in dblist:
  print("数据库已存在！")
```

> **注意：**database_names 在最新版本的 Python 中已废弃，Python3.7+ 之后的版本改为了 list_database_names()。

------

## 创建集合

MongoDB 中的集合类似 SQL 的表。

### 创建一个集合

MongoDB 使用数据库对象来创建集合，实例如下：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
 
mycol = mydb["sites"]
```

> **注意:** 在 MongoDB 中，集合只有在内容插入后才会创建! 就是说，创建集合(数据表)后要再插入一个文档(记录)，集合才会真正创建。

### 判断集合是否已存在

我们可以读取 MongoDB 数据库中的所有集合，并判断指定的集合是否存在：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient('mongodb://localhost:27017/')
 
mydb = myclient['runoobdb']
 
collist = mydb. list_collection_names()
# collist = mydb.collection_names()
if "sites" in collist:   # 判断 sites 集合是否存在
  print("集合已存在！")
```

> **注意：**collection_names 在最新版本的 Python 中已废弃，Python3.7+ 之后的版本改为了 list_collection_names()。



## 增、删、改、查

### 增加

#### 插入集合

集合中插入文档使用 **insert_one()** 方法，该方法的第一参数是字典 **name => value** 对。

以下实例向 **sites** 集合中插入文档：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
mydict = { "name": "RUNOOB", "alexa": "10000", "url": "https://www.runoob.com" }
 
x = mycol.insert_one(mydict) 
print(x)
print(x)

'''
<pymongo.results.InsertOneResult object at 0x10a34b288>
'''
```



#### 返回 _id 字段

**insert_one()** 方法返回 **InsertOneResult** 对象，该对象包含 **inserted_id** 属性，它是插入文档的 **id** 值。

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient('mongodb://localhost:27017/')
mydb = myclient['runoobdb']
mycol = mydb["sites"]
 
mydict = { "name": "Google", "alexa": "1", "url": "https://www.google.com" }
 
x = mycol.insert_one(mydict)
 
print(x.inserted_id)

'''
5b2369cac315325f3698a1cf
'''
```

如果我们在插入文档时没有指定 **_id**，MongoDB 会为每个文档添加一个唯一的 **id**。



#### 插入多个文档

集合中插入多个文档使用 **insert_many()** 方法，该方法的第一参数是字典列表。

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
mylist = [
  { "name": "Taobao", "alexa": "100", "url": "https://www.taobao.com" },
  { "name": "QQ", "alexa": "101", "url": "https://www.qq.com" },
  { "name": "Facebook", "alexa": "10", "url": "https://www.facebook.com" },
  { "name": "知乎", "alexa": "103", "url": "https://www.zhihu.com" },
  { "name": "Github", "alexa": "109", "url": "https://www.github.com" }
]
 
x = mycol.insert_many(mylist)
 
# 输出插入的所有文档对应的 _id 值
print(x.inserted_ids)

'''
[ObjectId('5b236aa9c315325f5236bbb6'), ObjectId('5b236aa9c315325f5236bbb7'), ObjectId('5b236aa9c315325f5236bbb8'), ObjectId('5b236aa9c315325f5236bbb9'), ObjectId('5b236aa9c315325f5236bbba')]
'''
```

**insert_many()** 方法返回 **InsertManyResult** 对象，该对象包含 **inserted_ids** 属性，该属性保存着所有插入文档的 **id** 值。



#### 插入指定 _id 的多个文档

也可以自己指定 id 插入，以下实例在 **site2** 集合中插入数据 **id** 为指定的：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["site2"]
 
mylist = [
  { "_id": 1, "name": "RUNOOB", "cn_name": "教程"},
  { "_id": 2, "name": "Google", "address": "Google 搜索"},
  { "_id": 3, "name": "Facebook", "address": "脸书"},
  { "_id": 4, "name": "Taobao", "address": "淘宝"},
  { "_id": 5, "name": "Zhihu", "address": "知乎"}
]
 
x = mycol.insert_many(mylist)
 
# 输出插入的所有文档对应的 _id 值
print(x.inserted_ids)

'''
[1, 2, 3, 4, 5]
'''
```







### 删除

#### 删除数据

以使用 **delete_one()** 方法来删除一个文档，该方法第一个参数为查询对象，指定要删除哪些数据。

实例删除 name 字段值为 "Taobao" 的文档：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
myquery = { "name": "Taobao" }
 
mycol.delete_one(myquery)
 
# 删除后输出
for x in mycol.find():
  print(x)
```



#### 删除多个文档

可以使用 **delete_many()** 方法来删除多个文档，该方法第一个参数为查询对象，指定要删除哪些数据。

删除所有 name 字段中以 F 开头的文档:

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
myquery = { "name": {"$regex": "^F"} }
 
x = mycol.delete_many(myquery)
 
print(x.deleted_count, "个文档已删除")
```

#### 删除集合中的所有文档

**delete_many()** 方法如果传入的是一个空的查询对象，则会删除集合中的所有文档：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
x = mycol.delete_many({})
 
print(x.deleted_count, "个文档已删除")
```



#### 删除集合

以使用 **drop()** 方法来删除一个集合。

以下实例删除了 customers 集合：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
mycol.drop()
```

如果删除成功 drop() 返回 true，如果删除失败(集合不存在)则返回 false。

我们使用以下命令在终端查看集合是否已删除：

```python
> use runoobdb
switched to db runoobdb
> show tables;
```

### 修改

#### 修改文档

可以在 MongoDB 中使用 **update_one()** 方法修改文档中的记录。该方法第一个参数为查询的条件，第二个参数为要修改的字段。

如果查找到的匹配数据多于一条，则只会修改第一条。

实例将 alexa 字段的值 10000 改为 12345:

```python
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
myquery = { "alexa": "10000" }
newvalues = { "$set": { "alexa": "12345" } }
 
mycol.update_one(myquery, newvalues)
 
# 输出修改后的  "sites"  集合
for x in mycol.find():
  print(x)
```

**update_one()** 方法只能修匹配到的第一条记录，如果要修改所有匹配到的记录，可以使用 **update_many()**。

以下实例将查找所有以 **F** 开头的 **name** 字段，并将匹配到所有记录的 **alexa** 字段修改为 **123**：

```python
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
myquery = { "name": { "$regex": "^F" } }
newvalues = { "$set": { "alexa": "123" } }
 
x = mycol.update_many(myquery, newvalues)
 
print(x.modified_count, "文档已修改")
```



### 查询

#### 查询文档

MongoDB 中使用了 find 和 find_one 方法来查询集合中的数据，它类似于 SQL 中的 SELECT 语句。

#### 查询一条数据

可以使用 **find_one()** 方法来查询集合中的一条数据。

查询 **sites** 文档中的第一条数据：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
x = mycol.find_one()
 
print(x)

'''
{'_id': ObjectId('5b23696ac315325f269f28d1'), 'name': 'RUNOOB', 'alexa': '10000', 'url': 'https://www.runoob.com'}
'''
```



#### 查询集合中所有数据

**find()** 方法可以查询集合中的所有数据，类似 SQL 中的 **SELECT \*** 操作。

以下实例查找 **sites** 集合中的所有数据：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
for x in mycol.find():
  print(x)
```



#### 查询指定字段的数据

可以使用 find() 方法来查询指定字段的数据，将要返回的字段对应值设置为 1。

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
for x in mycol.find({},{ "_id": 0, "name": 1, "alexa": 1 }):
  print(x)

'''
{'name': 'RUNOOB', 'alexa': '10000'}
{'name': 'Google', 'alexa': '1'}
{'name': 'Taobao', 'alexa': '100'}
{'name': 'QQ', 'alexa': '101'}
{'name': 'Facebook', 'alexa': '10'}
{'name': '知乎', 'alexa': '103'}
{'name': 'Github', 'alexa': '109'}
'''
```

除了 _id，不能在一个对象中同时指定 0 和 1，如果你设置了一个字段为 0，则其他都为 1，反之亦然。

以下实例除了 alexa 字段外，其他都返回：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
for x in mycol.find({},{ "alexa": 0 }):
  print(x)

'''
{'_id': ObjectId('5b23696ac315325f269f28d1'), 'name': 'RUNOOB', 'url': 'https://www.runoob.com'}
{'_id': ObjectId('5b2369cac315325f3698a1cf'), 'name': 'Google', 'url': 'https://www.google.com'}
{'_id': ObjectId('5b236aa9c315325f5236bbb6'), 'name': 'Taobao', 'url': 'https://www.taobao.com'}
{'_id': ObjectId('5b236aa9c315325f5236bbb7'), 'name': 'QQ', 'url': 'https://www.qq.com'}
{'_id': ObjectId('5b236aa9c315325f5236bbb8'), 'name': 'Facebook', 'url': 'https://www.facebook.com'}
{'_id': ObjectId('5b236aa9c315325f5236bbb9'), 'name': '知乎', 'url': 'https://www.zhihu.com'}
{'_id': ObjectId('5b236aa9c315325f5236bbba'), 'name': 'Github', 'url': 'https://www.github.com'}
'''
```

**以下代码同时指定了 0 和 1 则会报错**：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
for x in mycol.find({},{ "name": 1, "alexa": 0 }):
  print(x)

'''
错误内容大致为：
...
pymongo.errors.OperationFailure: Projection cannot have a mix of inclusion and exclusion.
...
'''
```



#### 根据指定条件查询

可以在 **find()** 中设置参数来过滤数据。

以下实例查找 name 字段为 "RUNOOB" 的数据：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
myquery = { "name": "RUNOOB" }
 
mydoc = mycol.find(myquery)
 
for x in mydoc:
  print(x)

'''
{'_id': ObjectId('5b23696ac315325f269f28d1'), 'name': 'RUNOOB', 'alexa': '10000', 'url': 'https://www.runoob.com'}
'''
```



#### 高级查询

查询的条件语句中，还可以使用修饰符。

以下实例用于读取 name 字段中第一个字母 ASCII 值大于 "H" 的数据，大于的修饰符条件为 **{"$gt": "H"}** :

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
myquery = { "name": { "$gt": "H" } }
 
mydoc = mycol.find(myquery)
 
for x in mydoc:
  print(x)

'''
{'_id': ObjectId('5b23696ac315325f269f28d1'), 'name': 'RUNOOB', 'alexa': '10000', 'url': 'https://www.runoob.com'}
{'_id': ObjectId('5b236aa9c315325f5236bbb6'), 'name': 'Taobao', 'alexa': '100', 'url': 'https://www.taobao.com'}
{'_id': ObjectId('5b236aa9c315325f5236bbb7'), 'name': 'QQ', 'alexa': '101', 'url': 'https://www.qq.com'}
{'_id': ObjectId('5b236aa9c315325f5236bbb9'), 'name': '知乎', 'alexa': '103', 'url': 'https://www.zhihu.com'}
'''
```



#### 使用正则表达式查询

还可以使用正则表达式作为修饰符。

正则表达式修饰符只用于搜索字符串的字段。

以下实例用于读取 name 字段中第一个字母为 "R" 的数据，正则表达式修饰符条件为 **{"$regex": "^R"}** :

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
myquery = { "name": { "$regex": "^R" } }
 
mydoc = mycol.find(myquery)
 
for x in mydoc:
  print(x)

'''
{'_id': ObjectId('5b23696ac315325f269f28d1'), 'name': 'RUNOOB', 'alexa': '10000', 'url': 'https://www.runoob.com'}
'''
```



#### 返回指定条数记录

要对查询结果设置指定条数的记录可以使用 **limit()** 方法，该方法只接受一个数字参数。

以下实例返回 3 条文档记录：

```python
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
myresult = mycol.find().limit(3)
 
# 输出结果
for x in myresult:
  print(x)

'''
{'_id': ObjectId('5b23696ac315325f269f28d1'), 'name': 'RUNOOB', 'alexa': '10000', 'url': 'https://www.runoob.com'}
{'_id': ObjectId('5b2369cac315325f3698a1cf'), 'name': 'Google', 'alexa': '1', 'url': 'https://www.google.com'}
{'_id': ObjectId('5b236aa9c315325f5236bbb6'), 'name': 'Taobao', 'alexa': '100', 'url': 'https://www.taobao.com'}
'''
```



### 数据排序

#### 排序

**sort()** 方法可以指定升序或降序排序。

**sort()** 方法第一个参数为要排序的字段，第二个字段指定排序规则，**1** 为升序，**-1** 为降序，默认为升序。

对字段 alexa 按升序排序：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
mydoc = mycol.find().sort("alexa")
for x in mydoc:
  print(x)
```



对字段 alexa 按降序排序：

```python
#!/usr/bin/python3
 
import pymongo
 
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["runoobdb"]
mycol = mydb["sites"]
 
mydoc = mycol.find().sort("alexa", -1)
 
for x in mydoc:
  print(x)
```













