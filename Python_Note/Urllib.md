## Python urllib

Python urllib 库用于操作网页 URL，并对网页的内容进行==抓取处理==。

本文主要介绍 Python3 的 urllib。

urllib 包 包含以下几个模块：

- **urllib.request** - 打开和读取 URL。
- **urllib.error** - 包含 urllib.request 抛出的异常。
- **urllib.parse** - 解析 URL。
- **urllib.robotparser** - 解析 robots.txt 文件。



## urllib.request

urllib.request 定义了一些打开 URL 的函数和类，包含授权验证、重定向、浏览器 cookies等。

urllib.request 可以模拟浏览器的一个请求发起过程。

可以使用 urllib.request 的 urlopen 方法来打开一个 URL，语法格式如下：

```python
urllib.request.urlopen(url, data=None, [timeout, ]*, cafile=None, capath=None, cadefault=False, context=None)
```

- **url**：url 地址。
- **data**：发送到服务器的其他数据对象，默认为 None。
- **timeout**：设置访问超时时间。
- **cafile 和 capath**：cafile 为 CA 证书， capath 为 CA 证书的路径，使用 HTTPS 需要用到。
- **cadefault**：已经被弃用。
- **context**：ssl.SSLContext类型，用来指定 SSL 设置。

实例如下：

```python
from urllib.request import urlopen

myURL = urlopen("https://www.****.com/")
print(myURL.read())
```

以上代码使用 urlopen 打开一个 URL，然后使用 read() 函数获取网页的 HTML 实体代码。

read() 是读取整个网页内容，可以指定读取的长度：

```python
from urllib.request import urlopen

myURL = urlopen("https://www.****.com/")
print(myURL.read(300))
```

除了 read() 函数外，还包含以下两个读取网页的函数：

- **readline()** - 读取文件的一行内容

```python
from urllib.request import urlopen

myURL = urlopen("https://www.****.com/")
print(myURL.readline()) #读取一行内容
```

- **readlines()** - 读取文件的全部内容，它会把读取的内容赋值给一个列表变量。

```python
from urllib.request import urlopen

myURL = urlopen("https://www.****.com/")
lines = myURL.readlines()
for line in lines:
    print(line) 
```

在对网页进行抓取时，经常需要判断网页是否可以正常访问，这里可以使用 getcode() 函数获取网页状态码，返回 200 说明网页正常，返回 404 说明网页不存在：

```python
import urllib.request

myURL1 = urllib.request.urlopen("https://www.****.com/")
print(myURL1.getcode())   # 200

try:
    myURL2 = urllib.request.urlopen("https://www.****.com")
except urllib.error.HTTPError as e:
    if e.code == 404:
        print(404)   # 404
```

如果要将抓取的网页保存到本地，可以使用 Python3 File write() 方法函数：

```python
from urllib.request import urlopen

myURL = urlopen("https://www.*****.com/")
f = open("runoob_urllib_test.html", "wb")
content = myURL.read()  # 读取网页内容
f.write(content)
f.close()
```



执行以上代码，在本地就会生成一个 runoob_ullib_test.html 文件，里面包含了 https://www.****.com/ 网页的内容。

URL 的编码与解码可以使用 **urllib.request.quote()** 与 **urllib.request.unquote()**方法：

```python
import urllib.request 

encode_url = urllib.request.quote("https://www.*****.com/")  # 编码
print(encode_url)

unencode_url = urllib.request.unquote(encode_url)    # 解码
print(unencode_url)
```



## 模拟头部信息

在抓取一般网页需要对 headers(网页头部信息)进行模拟，这时候需要使用到 urllib.request.Request 类：

```python
class urllib.request.Request(url, data=None, headers={}, origin_req_host=None, unverifiable=False, method=None)
```

参数说明：

- **url**：url 地址。
- **data**：发送到服务器的其他数据对象，默认为 None。
- **headers**：HTTP 请求的头部信息，字典格式。
- **origin_req_host**：请求的主机地址，IP 或域名。
- **unverifiable**：很少用这个参数，用于设置网页是否需要验证，默认是 False。
- **method**：请求方法， 如 GET、POST、DELETE、PUT等。

```python
import urllib.request
import urllib.parse

url = "https://www.****.com/?s="  # 搜索页面
keyword = "Python 教程"
key_code = urllib.request.quote(keyword)  # 对请求进行编码
url_all = url + key_code
header = {
    "User-Agent": "Mozilla/5.0 (X11; Fedora; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36"
}  # 头部信息
request = urllib.request.Request(url_all, headers=header)
reponse = urllib.request.urlopen(request).read()

fh = open("./urllib_test_runoob_search.html", "wb")  # 将文件写入到当前目录中
fh.write(reponse)
fh.close()

```

执行以上 Python 代码，会在当前目录生成 urllib_test_runoob_search.html 文件，打开 urllib_test_runoob_search.html 文件（可以使用浏览器打开）













