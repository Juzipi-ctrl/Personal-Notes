# HTML

Hyper Text Markup Language

1、普通链接： 普通链接用于在网页上链接到其他页面或资源。它们可以是相对链接或绝对链接。

相对链接示例：

```html
<a href="about.html">关于我们</a>
```

绝对链接示例：

```html
<a href="https://www.example.com">示例网站</a>
```

2、链接： 锚链接用于在同一页面内导航到页面的不同部分。它们通常用于创建目录或跳转到页面的特定部分。

创建锚链接示例：

```html
<a href="#section1">跳转到第一部分</a>
```

在页面内部创建锚点示例：

```html
<h2 id="section1">第一部分</h2>
```

3、功能链接： 功能链接是一种特殊类型的链接，它们执行一些特定的功能而不是导航到其他页面或位置。例如，打开邮件客户端或拨打电话。

打开邮件客户端链接示例：

```html
<a href="mailto:example@example.com">发送电子邮件</a>
```

拨打电话链接示例：

```html
<a href="tel:1234567890">拨打电话</a>
```

这些只是HTML链接的基本用法示例。



## iframe

示例

```html
<iframe src="https://www.example.com"></iframe>
```



## form 表单

示例

```html
<form action="/submit" method="post">
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" required>

  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required>

  <input type="submit" value="Submit">
</form>
```

![image-20230624173555121](C:\Users\Value.DESKTOP-F8NSHR6\AppData\Roaming\Typora\typora-user-images\image-20230624173555121.png)