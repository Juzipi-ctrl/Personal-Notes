## JSON 使用

### 把JSON文本转换为 JavaScript 对象

JSON最常见的用法之一，是从 web 服务器上读取 JSON 数据（作为文本或作为 HttpRequest），将JSON数据转换为 JavaScript 对象，然后在网页中使用数据。

### JSON 实例-来自字符串的对象

创建 JSON 语法的 JavaScript 字符串：

```json
var txt = '{ "sites" : [' +
'{ "name":"百度一下" , "url":"www.baidu.com" },' +
'{ "name":"google" , "url":"www.google.com" },' +
'{ "name":"微博" , "url":"www.weibo.com" } ]}';
```

由于 JSON 语法是  JavaScript 语法的子集，JavaScript 函数 eval() 可用于 JSON 文本转换为 JavaScript 对象。

eval() 函数使用的是 JavaScript 编辑器，可解析 JSON 文本，然后生成 JavaScript 对象。必须把文本包括在括号中，这样才能避免语法错误：

```json 
var obj = eval ("(" + txt + ")");
```

在网页中使用 JavaScript 对象：

```json
var txt = '{ "sites" : [' +
'{ "name":"百度一下" , "url":"www.baidu.com" },' +
'{ "name":"google" , "url":"www.google.com" },' +
'{ "name":"微博" , "url":"www.weibo.com" } ]}';
 
var obj = eval ("(" + txt + ")");
 
document.getElementById("name").innerHTML=obj.sites[0].name 
document.getElementById("url").innerHTML=obj.sites[0].url
```



### JSON 解析器

eval()  函数可编译并执行任何 JavaScript 代码。这里隐藏了一个潜在的安全问题。

使用 JSON 解析器将 JSON 转换为 JavaScript 对象是更安全的做法。JSON 解析器只能识别 JSON 文本，而不会编辑脚本。

在浏览器中，者提供了原生的 JSON 支持，而且 JSON 解析器的速度更快。









