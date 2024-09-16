## python3 JSON数据解析’

JSON（JavaScript object notation） 是一种轻量的数据交换格式。

python3 中可以使用 json 模块来对 json 数据进行编码解码，它包含了两个函数：

- **json.dumps():** 对数据进行编码。
- **json.loads():** 对数据进行解码。



### python编码为json类型转换对应表：

在 json 的编解码过程中，Python 的原始类型与 json 类型会相互转换，具体的转化对照如下：

| Python                               | JSON   |
| ------------------------------------ | ------ |
| dict                                 | object |
| list, tuple                          | array  |
| str                                  | string |
| int,float,int- & float0derived Enums | number |
| True                                 | true   |
| False                                | false  |
| None                                 | null   |



### JSON解码为Python类型转换对应表：

| JSON         | Python |
| ------------ | ------ |
| object       | dict   |
| arrar        | list   |
| string       | str    |
| number(int)  | int    |
| number(real) | float  |
| true         | True   |
| false        | False  |
| null         | None   |



### json.dumps 与 json.loads 实例

以下实例演示了 Python 数据结构转换为 json：

```python
#!/usr/bin/python3
 
import json
 
# Python 字典类型转换为 JSON 对象
data = {
    'no' : 1,
    'name' : 'Runoob',
    'url' : 'https://www.runoob.com'
}
 
json_str = json.dumps(data)
print ("Python 原始数据：", repr(data))
print ("JSON 对象：", json_str)

'''
Python 原始数据： {'no': 1, 'name': 'Runoob', 'url': 'https://www.runoob.com'}
JSON 对象： {"no": 1, "name": "Runoob", "url": "https://www.runoob.com"}
'''
```

通过输出的结果可以看出，简单类型通过编码后更其原始的repr() 输出结果非常相似。

接着以上实例，可以将一个 json 编码的字符串转回一个 Python 数据结构：

```python
#!/usr/bin/python3
 
import json
 
# Python 字典类型转换为 JSON 对象
data1 = {
    'no' : 1,
    'name' : 'Runoob',
    'url' : 'http://www.runoob.com'
}
 
json_str = json.dumps(data1)
print ("Python 原始数据：", repr(data1))
print ("JSON 对象：", json_str)
 
# 将 JSON 对象转换为 Python 字典
data2 = json.loads(json_str)
print ("data2['name']: ", data2['name'])
print ("data2['url']: ", data2['url'])

'''
Python 原始数据： {'name': 'Runoob', 'no': 1, 'url': 'http://www.runoob.com'}
JSON 对象： {"name": "Runoob", "no": 1, "url": "http://www.runoob.com"}
data2['name']:  Runoob
data2['url']:  http://www.runoob.com
'''
```

要处理的是文件而不是字符串，可以使用 **json.dump()**和 **json.load()**来编码和解码 JSON 数据。例如：

```python
# 写入 JSON 数据
with open('data.json', 'w') as f:
    json.dump(data, f)
 
# 读取数据
with open('data.json', 'r') as f:
    data = json.load(f)
```













