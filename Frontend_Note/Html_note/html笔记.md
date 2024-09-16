# html简介

#### 实例解析

![1664427303619](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1664427303619.png)

```html 
<!DOCTYPE html>	声明为 HTML5 的文档
    <html> 元素是 THML 页面的根元素
        <head> 元素包含了文档的元，（meta）数据，如<mete charset="utf-8"></mete>定义网页的编码格式为 utf-8
            <title></title> 定义了文档的标题
            <body> 元素包含了可见的页面内容
                <h1>元素定义了一个标题
                    <P> 定义了一个
                        
                    </P>
                </h1>
            </body>
        </head>
</html>
</!doctype>
```

##### 标题

```c++
<h1> </h1>
```

##### 段落

```c++
<P> </P>
```

##### 链接

```html
<a href="www.caibai.club">这是个链接</a>

<a href="http://www.runoob.com/" target="_blank">访问菜鸟教程!</a>
<p>如果你将 target 属性设置为 &quot;_blank&quot;, 链接将在新窗口打开。</p>
```

##### 图像

```html
<img src="图片路径" alt="图像的替代文字" title="鼠标悬停提示文字" width="宽" height="高" />
```

#### 属性

```php+HTML
class 为html元素定义一个或多个类名（class name）（类名从样式文件引入）
id  定义元素的唯一 id
style	规定元素的行内样式（lnline style）
litle	描述了元素的额外信息（作为工具条使用）
```



#### 格式化标签

##### 水平线

```html
<hr>	定义水平线
```

##### 换行

```html
<br>	定义换行
```

##### 粗体

```html
<b>	</b> 定义粗体文本
```

##### 着重

```html
<em>	</em>定义着重文字
```

##### 斜体

```html
<i>	</i> 定义斜体字
```

##### 小号字

```html
<small>	</small> 定义小号字
```

##### 重语气

```html
<strong>	</strong> 定义加重语气
```

##### 下标字

```html
<sub>	</sub> 定义下标字
```

##### 上标字

```html
<sub>	</sub> 定义上标字
```

##### 插入字

```html
<ins>	</ins> 定义插入字
```

##### 删除字

```html
<del>	</del> 定义删除字
```



#### 输出标签

##### 代码

```html
<coode>	</coode> 定义计算机代码
<code>一段电脑代码 print("Hello World")</code>
```

##### 键盘码

```html
<kbd>	</kbd> 定义键盘码
<kbd>键盘输入</kbd>
```

##### 代码样本

```html
<samp>	</samp> 定义计算机代码样本
<samp>计算机样本</samp>
```

##### 变量

```html
<var>	</var> 定义变量
<var>变量</var>
```

##### 格式文本

```html
<pre>	</pre> 定义预格式文本
<pre>
此例演示如何使用 pre 标签
对空行和 空格
进行控制
</pre>
```

#### 引文，引用，及标签定义

##### 缩写

```html
<abbr>	</abbr> 定义缩写
The<abbr title="World Health Organization">WHO</abbr> was founded in 1948.
```

##### 地址

```html
<address>	</address> 定义地址
<address>
Written by <a href="mailto:webmaster@example.com">Jon Doe</a>.<br> 
Visit us at:<br>
Example.com<br>
Box 564, Disneyland<br>
USA
</address>
```

##### 文字方向

```html
<bdo>	</bdo> 定义文字方向
<p>该段落文字从左到右显示。</p>  
<p><bdo dir="rtl">该段落文字从右到左显示。</bdo></p>
```

##### 长引用

```html
<blockquote> 定义长的引用
    
</blockquote>
<blockquote cite="http://www.worldwildlife.org/who/index.html">
For 50 years, WWF has been protecting the future of nature. The world's leading conservation organization, WWF works in 100 countries and is supported by 1.2 million members in the United States and close to 5 million globally.
</blockquote>
```

##### 短引用

```html
<q>	</q> 定义短引用语
<p>WWF's goal is to:
<q>Build a future where people live in harmony with nature.</q>
We hope they succeed.</p>
```

##### 引用、引证

```html
<cite>	</cite> 定义引用、引证
<p><cite>The Scream</cite> by Edward Munch. Painted in 1893.</p>
```

##### 定义项目

```html
<dfn>	</dfn> 定义一个定义项目
<dfn>定义项目</dfn>
```

#### html“base“元素

base 元素描述了基本的链接/链接目标，该函数作为 THML文档中所有的链接标签的默认链接:

```html
<head>
<base href="http://www.runoob.com/images/" target="_blank">
</head>
```

#### html“link“元素

link	标签定义了文档与外部资源之间的关系

link	标签通常用于链接到样式表：

```html
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

#### html“style“元素

style	标签定义了HTML文档的样式文件引导地址。

style	元素中你也可以直接添加样式来渲染HTML文档：

```html
<head>
<style type="text/css">
body {
    background-color:yellow;
}
p {
    color:blue
}
</style>
</head>
```

#### html“meta“元素

meta标签描述了一些基本的元数据。

<meta> 标签提供了元数据.元数据也不显示在页面上，但会被浏览器解析。

META 元素通常用于指定网页的描述，关键词，文件的最后修改时间，作者，和其他元数据。

元数据可以使用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他Web服务。

<meta> 一般放置于 <head> 区域

##### 使用实例

为搜索引擎定义关键词:

```html
<meta name="keywords" content="HTML, CSS, XML, XHTML, JavaScript">
```

为网页定义描述内容:

```html
<meta name="description" content="免费 Web & 编程 教程">
```

定义网页作者:

```html
<meta name="author" content="Runoob">
```

每30秒钟刷新当前页面:

```html
<meta http-equiv="refresh" content="30">
```

#### 图像标签（<img）和源属性（src）

在 HTML 中，图像由<img> 标签定义。

<img> 是空标签，意思是说，它只包含属性，并且没有闭合标签。

要在页面上显示图像，你需要使用源属性（src）。src 指 "source"。源属性的值是图像的 URL 地址。

**定义图像的语法是：**

```html
<img src="url" alt="some_text">  
```

URL 值存储图像的位置。

##### 图像ait属性

alt 属性用来为图像定义一串预备的可替换的文本。

替换文本属性的值是用户定义的。

```html
<img src="boat.gif" alt="Big Boat">
```

在浏览器无法载入图像时，替换文本属性告诉读者她们失去的信息。此时，浏览器将显示这个替代性的文本而不是图像。为页面上的图像都加上替换文本属性是个好习惯，这样有助于更好的显示信息，并且对于那些使用纯文本浏览器的人来说是非常有用的。

#### 设置图像的高度与宽度

height（高度） 与 width（宽度）属性用于设置图像的高度与宽度。

属性值默认单位为像素:

```html
<img src="pulpit.jpg" alt="Pulpit rock" width="304" height="228">
```

**提示:** 指定图像的高度和宽度是一个很好的习惯。如果图像指定了高度宽度，页面加载时就会保留指定的尺寸。如果没有指定图片的大小，加载页面时有可能会破坏HTML页面的整体布局。

##### 图像地图

```html
<map>	</map>	定义图像地图
<map name="planetmap">
  <area shape="rect" coords="0,0,82,126" alt="Sun" href="sun.htm">
  <area shape="circle" coords="90,58,3" alt="Mercury" href="mercur.htm">
  <area shape="circle" coords="124,58,8" alt="Venus" href="venus.htm">
</map>
```

##### 可点击区域

```html
<area>	定义图像地图中的可点击区域
 <area shape="rect" coords="0,0,82,126" alt="Sun" href="sun.htm">
 <area shape="circle" coords="90,58,3" alt="Mercury" href="mercur.htm">
 <area shape="circle" coords="124,58,8" alt="Venus" href="venus.htm">
```

#### 表格

 表格由 “table” 标签来定义。每个表格均有若干“行“（由 “tr”标签定义），每行被分割为若干单元格（由 “td”标签定义）。字母 td 指表格数据（table data），即数据单元格的内容。 

```html
<h4>一列:</h4>
<table border="1">
  <tr>
    <td>100</td>
  </tr>
</table>
 
<h4>一行三列:</h4>
<table border="1">
  <tr>
    <td>100</td>
    <td>200</td>
    <td>300</td>
  </tr>
</table>
 
<h4>两行三列:</h4>
<table border="1">
  <tr>
    <td>100</td>
    <td>200</td>
    <td>300</td>
  </tr>
  <tr>
    <td>400</td>
    <td>500</td>
    <td>600</td>
  </tr>
</table>
```

##### 表格

```html
<table>	定义表格
    
</table>

<table border="1">
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
  <tr>
    <td>February</td>
    <td>$80</td>
  </tr>
</table>
```

##### 表头

```html
<th>	</th>	定义表格的表头

<table border="1">
<tr>
<th>Month</th>
<th>Savings</th>
</tr>
<tr>
<td>January</td>
<td>$100</td>
</tr>
</table>
```

##### 表格的行

```html
<tr>	</tr>	定义表格的行

<table border="1">
<tr>
<th>Month</th>
<th>Savings</th>
</tr>
<tr>
<td>January</td>
<td>$100</td>
</tr>
</table>
```

##### 表格单元

```html
<td>	</td>	定义表格单元

<table border="1">
<tr>
<th>Month</th>
<th>Savings</th>
</tr>
<tr>
<td>January</td>
<td>$100</td>
</tr>
</table>
```

##### 表格标题

```html
<caption>	</caption> 定义表格标题

<table border="1">
  <caption>Monthly savings</caption>
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
</table>
```

##### 表格的列的组

```html
<colgroup>	</colgroup>	定义表格列的组

<table border="1">
  <colgroup>
    <col span="2" style="background-color:red">
    <col style="background-color:yellow">
  </colgroup>
  <tr>
    <th>ISBN</th>
    <th>Title</th>
    <th>Price</th>
  </tr>
  <tr>
    <td>3476896</td>
    <td>My first HTML</td>
    <td>$53</td>
  </tr>
</table>
```

##### 表格的列的属性

```html
<col>	定义用于表格列的属性

  <colgroup>
    <col span="2" style="background-color:red">
    <col style="background-color:yellow">
  </colgroup>
```

##### 表格的页眉

```html
<thead>	</thead>	定义表格的页眉

<table border="1">
  <thead>
    <tr>
      <th>Month</th>
      <th>Savings</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Sum</td>
      <td>$180</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>January</td>
      <td>$100</td>
    </tr>
    <tr>
      <td>February</td>
      <td>$80</td>
    </tr>
  </tbody>
</table>
```

##### 表格的主体

```html
<tbody>	</tbody>	定义表格的主体

thead {color:green;}
tbody {color:blue;}
tfoot {color:red;}
```

##### 定义表格的页脚

```html
<tfoot>	</tfoot>	定义表格的页脚
thead {color:green;}
tbody {color:blue;}
tfoot {color:red;}
```

#### 列表标签

##### 有序列表

```html
<ol>	定义有序列表
    
</ol>
<ol>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ol>
 
<ol start="50">
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ol>
```

##### 无序列表

```html
<ul>	定义无序列表
    
</ul>
<ul>
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
</ul>
```

##### 列表页

```html
<li>	</li>	定义列表页
<ol>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ol>

<ul>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ul>
```

##### 列表

```html
<dl>	</dl> 定义列表
<dl>
  <dt>Coffee</dt>
    <dd>Black hot drink</dd>
  <dt>Milk</dt>
    <dd>White cold drink</dd>
</dl>
```

##### 列表项目

```html
<dt>	</dt> 自定义列表项目
<dl>
  <dt>Coffee</dt>
    <dd>Black hot drink</dd>
  <dt>Milk</dt>
    <dd>White cold drink</dd>
</dl>
```

##### 列表项的描述

```html
<dd>	</dd> 定义自定列表项的描述
<dl>
  <dt>Coffee</dt>
    <dd>Black hot drink</dd>
  <dt>Milk</dt>
    <dd>White cold drink</dd>
</dl>
```

#### 分组标签

##### 块级

```html
<div> 	定义了文档的区域，块级（block-level）
    
</div>
<div style="color:#0000FF">
  <h3>这是一个在 div 元素中的标题。</h3>
  <p>这是一个在 div 元素中的文本。</p>
</div>
```

##### 内联元素

```html
<span>	</span>	用来组合文档中的行内元素，内联元素（liline）
<p>我的母亲有 <span style="color:blue">蓝色</span> 的眼睛。</p>
```

#### 表单

表单是一个包含表单元元素的区域。

表单元素是允许用户在表单中输入内容，比如：文本域（textarea）、下拉列表（select）、单选框（radio-buttons）、复选框（chackbox）等等。

我们可以使用 “form” 标签来创建表单：

```html
<form>
    input 元素
</form>
```

##### 表单输入元素

多数情况下被用到的表单标签是输入标签“input”。

输入类型是由“tupe”属性定义。

##### 文本域(text Fields)

文本通过“input type=”text”“ 标签类设定，当用户在表单中输入键字字母，数字等内容时，就会用到文本域。

```html
<form>
    First name: <input type="text" name="firstname"><br>
	Last name: <input type="text" name="lastname">
</form>
```

##### 密码字段

密码字段通过标签 “input type=”password”“来定义：

```html
<form>
	Password: <input type="password" name="pwd">
</form>
```

##### 单选按钮（Radio Buttons）

“input type=”radio”“标签定义了表单的单选框选项：

```html
<form action="">
<input type="radio" name="sex" value="male">男<br>
<input type="radio" name="sex" value="female">女
</form>
```

##### 复选框（Checkboxes）

“input type=”checkbox”“定义了复选框。

复选框可以选取一个或多个选项：

```html
<form>
<input type="checkbox" name="vehicle" value="Bike">我喜欢自行车<br>
<input type="checkbox" name="vehicle" value="Car">我喜欢小汽车
</form>
```

##### 提交按钮（Submit）

“input type=”submit”“定义了提交按钮。

当用户单击确认按钮时，表单的内容会被传送到服务器。表单的动作属性“action”定义了服务的文件名。

“action” 属性会对接受到用户输入数据进行相关的处理：

```html
<form name="input" action="html_form_action.php" method="get">
Username: <input type="text" name="user">
<input type="submit" value="Submit">
</form>
```

- **post**：指的是 HTTP POST 方法，表单数据会包含在表单体内然后发送给服务器，用于提交敏感数据，如用户名与密码等。
- **get**：默认值，指的是 HTTP GET 方法，表单数据会附加在 **action** 属性的 URL 中，并以 **?**作为分隔符，一般用于不敏感信息，如分页等。例如：https://www.runoob.com/?page=1，这里的 page=1 就是 get 方法提交的数据。

```html
<!-- 以下表单使用 GET 请求发送数据到当前的 URL，method 默认位 GET。 -->
<form>
  <label>Name:
    <input name="submitted-name" autocomplete="name">
  </label>
  <button>Save</button>
</form>

<!-- 以下表单使用 POST 请求发送数据到当前的 URL。 -->
<form method="post">
  <label>Name:
    <input name="submitted-name" autocomplete="name">
  </label>
  <button>Save</button>
</form>

<!-- 表单使用 fieldset, legend, 和 label 标签 -->
<form method="post">
  <fieldset>
    <legend>Title</legend>
    <label><input type="radio" name="radio"> Select me</label>
  </fieldset>
</form>
```

#### 表单标签

##### 输入表单

```html
<form> 定义用户输入的表单
    
</form>
<form action="demo_form.php" method="get">
  First name: <input type="text" name="fname"><br>
  Last name: <input type="text" name="lname"><br>
  <input type="submit" value="提交">
</form>
```

##### 输入域

```html
<input>	定义输入域
<form action="demo-form.php">
First name: <input type="text" name="FirstName" value="Mickey"><br>
Last name: <input type="text" name="LastName" value="Mouse"><br>
<input type="submit" value="提交">
</form>
```

##### 文本域

```html
<textarea>	</textarea> 定义文本域（一个多行的输入控件）
<textarea rows="10" cols="30">
我是一个文本框。
</textarea>
```

##### 输入标题

```html
<label>	</label> 定义了<input> 元素的标签，一般为输入标签
<form action="demo_form.php">
  <label for="male">Male</label>
  <input type="radio" name="sex" id="male" value="male"><br>
  <label for="female">Female</label>
  <input type="radio" name="sex" id="female" value="female"><br><br>
  <input type="submit" value="提交">
</form>
```

##### 表单元素

```html
<fieldset> 	定义了一组相关的表单元素，并使用外框包含起来
    
</fieldset>
<form>
  <fieldset>
    <legend>Personalia:</legend>
    Name: <input type="text"><br>
    Email: <input type="text"><br>
    Date of birth: <input type="text">
  </fieldset>
</form>
```

##### 元素标题

```html
<legend>	定义了<fieldset>元素标题
    
</legend>
  <fieldset>
    <legend>Personalia:</legend>
    Name: <input type="text"><br>
    Email: <input type="text"><br>
    Date of birth: <input type="text">
  </fieldset>    
```

##### 选项列表

```html
<select>	定义下拉选项列表
    
</select>
<select>
    <option value="volvo">Volvo</option>
    <option value="saab">Saab</option>
    <option value="mercedes">Mercedes</option>
    <option value="audi">Audi</option>
</select>
```

##### 选项组

```html
<optgroup>	</optgroup> 定义选项组
<select>
  <optgroup label="Swedish Cars">
    <option value="volvo">Volvo</option>
    <option value="saab">Saab</option>
  </optgroup>
  <optgroup label="German Cars">
    <option value="mercedes">Mercedes</option>
    <option value="audi">Audi</option>
  </optgroup>
</select>
```

##### 下拉列表

```html
<option>	</option> 定义下拉列表中的选项
<optgroup label="Swedish Cars">
    <option value="volvo">Volvo</option>
    <option value="saab">Saab</option>
  </optgroup>
```

##### 点击按钮

```html
<button>	定义一个点击按钮
    
</button>
<button type="button">点我!</button>
```

##### 控件选项列表

```html
<datalist>	</datalist>	指定一个预先定义的输入控件选项列表
<input list="browsers">
<datalist id="browsers">
  <option value="Internet Explorer">
  <option value="Firefox">
  <option value="Chrome">
  <option value="Opera">
  <option value="Safari">
</datalist>
```

##### 密钥生成器字段

```html
<keygen>	定义了表单的密钥对生成器字段
 <form action="demo_keygen.php" method="get">
  用户名: <input type="text" name="usr_name">
  加密: <keygen name="security">
  <input type="submit">
</form>
```

#####   计算结果

```html
<output>	</output>定义一个计算结果
<form oninput="x.value=parseInt(a.value)+parseInt(b.value)">0
<input type="range" id="a" value="50">100
+<input type="number" id="b" value="50">
=<output name="x" for="a b"></output>
</form>
```

#### 框架

iframe语法：

```html
<iframe src="URL">
    
</iframe>
```

该URL指向不同的网页。

##### 高度与宽度

height和width属性用来定义iframe标签的高度与宽度。

属性默认以像素为单位，但是可以指定其按比例显示（如：“80%”）

```html
<iframe loading="lazy" src="demo_iframe.htm" width="200" height="200"></iframe>
```

##### 移除边框

frameborder 属性用于定义iframe表示是否显示边框。

设置属性值为 "0" 移除iframe的边框:

```html
<iframe src="demo_iframe.htm" frameborder="0"></iframe>
```

##### 链接页面

iframe 可以显示一个目标链接的页面

目标链接的属性必须使用 iframe 的属性，如下实例:

```html
<iframe src="demo_iframe.htm" name="iframe_a"></iframe>
<p><a href="https://www.runoob.com" target="iframe_a" rel="noopener">RUNOOB.COM</a></p>
```

##### 脚本

##### “script “标签

<script> 标签用于定义客户端脚本，比如 JavaScript。

<script> 元素既可包含脚本语句，也可通过 src 属性指向外部脚本文件。

JavaScript 最常用于图片操作、表单验证以及内容动态更新。

```html
<script>
document.write("Hello World!");
</script>
```

##### “noscript”标签

<noscript> 标签提供无法使用脚本时的替代内容，比方在浏览器禁用脚本时，或浏览器不支持客户端脚本时。

<noscript>元素可包含普通 HTML 页面的 body 元素中能够找到的所有元素。

```html
<script>
document.write("Hello World!")
</script>
```

#### 新元素

##### “canvas” 新元素

```html
<canvas>	</canvas>标签定义图形，比如图表和其他图像。该标签基于JavaScript的绘图API
```

#### 新多媒体元素

##### 音频

```html
<audio>	</audio>定义音频内容
<audio controls>
  <source src="horse.ogg" type="audio/ogg">
  <source src="horse.mp3" type="audio/mpeg">
  您的浏览器不支持 audio 元素。
</audio>
```

##### 视频

```html
<video>	</video>定义视频（video或者movie）
<video width="320" height="240" controls>
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.ogg" type="video/ogg">
    您的浏览器不支持 video 标签。
</video>
```

##### 媒体资源

```html
<source>	定义多媒体资源（video）和（audio）
<audio controls>
    <source src="horse.ogg" type="audio/ogg">
    <source src="horse.mp3" type="audio/mpeg">
    您的浏览器不支持 audio 元素。
</audio>
```

##### 内容嵌入

```html
<embed>	定义嵌入的内容，比如插件。
1、嵌入图片：
	<embed type="image/jpg" src="https://static.runoob.com/images/runoob-logo.png" width="258" height="39">
2、嵌入HTML页面：
	<embed type="text/html" src="snippet.html" width="500" height="200">
3、嵌入视频：
	<embed type="video/webm" src="video.mp4" width="400" height="300">
```

##### 文本轨道

```html
<track>	为诸如“video”和“audio”元素之类的媒介规定外部文本轨道。
<video width="320" height="240" controls>
<video controls
       src="/video/php/friday.mp4">
    <track default
           kind="captions"
           srclang="en"
           src="/video/php/friday.vtt" />
</video>
</video>
```

#### 新表单元素

##### 选项表

```html
<datalist>	</datalist>定义选项列表。与input元素配合使用该元素，来定义input可能的值。
<input list="browsers">
<datalist id="browsers">
  <option value="Internet Explorer">
  <option value="Firefox">
  <option value="Chrome">
  <option value="Opera">
  <option value="Safari">
</datalist>
```

##### 秘钥生成器

```html
<keygen>	规定用于表单的秘钥对生成字段。
<form action="demo_keygen.asp" method="get">
  用户名: <input type="text" name="usr_name">
  加密: <keygen name="security">
  <input type="submit">
</form>
```

##### 类型输出

```html
<output>	</output>定义不同类型的输出，不如脚本的输出。
<form oninput="x.value=parseInt(a.value)+parseInt(b.value)">0
  <input type="range" id="a" value="50">100
  +<input type="number" id="b" value="50">
  =<output name="x" for="a b"></output>
```

#### 新的语义和结构元素

##### 独立区域

```html
<article>	</article>定义页面独立的内容区域。
<article>
  <h1>Internet Explorer 9</h1>
  <p> Windows Internet Explorer 9(缩写为 IE9 )在2011年3月14日21:00 发布。</p>
</article>
```

##### 侧面栏内容

```html
<aside>	</aside>定义页面的侧边内容。
<p>My family and I visited The Epcot center this summer.</p>
 
<aside>
  <h4>Epcot Center</h4>
  <p>The Epcot Center is a theme park in Disney World, Florida.</p>
</aside>
```

##### 脱离

```html
<bdi>	</bdi> 允许设置一段文本，使其脱离其父元素的文本方向设置。
<ul>
 <li>用户 <bdi>hrefs</bdi>: 60 分</li>
 <li>用户 <bdi>jdoe</bdi>: 80 分</li>
 <li>用户 <bdi>إيان</bdi>: 90 分</li>
</ul>
```

##### 命令按钮

```html
<command>	定义命令按钮，比如单选项按钮，复选项或按钮
<menu>
<command type="command" label="Save" onclick="save()">Save</command>
</menu>
```

##### 描述文档

```html
<details>	</details>用于描述文档或文档某个部分的细节。
<details>
<summary>Copyright 1999-2011.</summary>
<p> - by Refsnes Data. All Rights Reserved.</p>
<p>All content and graphics on this web site are the property of the company Refsnes Data.</p>
</details>
```

##### 对话框

```html
<dialog>	</dialog>定义对话框，比如提示框
<table border="1">
<tr>
  <th>January <dialog open>This is an open dialog window</dialog></th>
  <th>February</th>
  <th>March</th>
</tr>
<tr>
  <td>31</td>
  <td>28</td>
  <td>31</td>
</tr>
</table>
```

##### details元素标题

```html
<summary>	</summary>标题包含details元素的标题
<details>
  <summary>Epcot Center</summary>
  <p>Epcot is a theme park at Walt Disney World Resort featuring exciting attractions, international pavilions, award-winning fireworks and seasonal special events.</p>
</details>
```

##### 流内容

```html
<figure>	</figure>规定独立的流内容（图像，图标，照片，代码等等）。
<figure>
  <img src="img_pulpit.jpg" alt="The Pulpit Rock" width="304" height="228">
</figure>
```

##### figure元素标题

```html
<figcaption>	</figcaption>定义figure元素的标题。
<figure>
  <img src="img_pulpit.jpg" alt="The Pulpit Rock" width="304" height="228">
  <figcaption>Fig1. - A view of the pulpit rock in Norway.</figcaption>
</figure>
```

#####  section 或 document 的页脚 

```html
<footer>	</footer>定义section 或 document 的页脚。
<footer>
  <p>Posted by: Hege Refsnes</p>
  <p><time pubdate datetime="2012-03-01"></time></p>
</footer>
```

##### 头部区域

```html
<header>	</header>定义文档的头部区域。
<article>
    <header>
        <h1>Internet Explorer 9</h1>
        <p><time pubdate datetime="2011-03-15"></time></p>
    </header>
    <p> Windows Internet Explorer 9(缩写为 IE9 )是在2011年3月14日21:00发布的</p>
</article>
```

##### 记号文本

```html
<mark>	</mark>定义带有记号的文本。
<p>Do not forget to buy <mark>milk</mark> today.</p>
```

##### 度量衡

```html
<meter>	</meter>定义度量衡。仅用于已知最大和最小的度量。
<meter value="2" min="0" max="10">2 out of 10</meter><br>
<meter value="0.6">60%</meter>
```

##### 导航链接

```html
<nav></nav>	定义导航链接的部分
<nav>
  <a href="/html/">HTML</a> 
  <a href="/css/">CSS</a> 
  <a href="/js/">JavaScript</a> 
  <a href="/jquery/">jQuery</a>
</nav>
```

##### 任务进度

```html
<progress>	</progress>定义任何类型的任务进度。
<progress value="22" max="100"></progress>
```

##### 注释

```html
<ruby>	</ruby>	定义ruby注释（中文注音或字符）
<ruby>
  汉 <rp>(</rp><rt>Han</rt><rp>)</rp>
  字 <rp>(</rp><rt>zi</rt><rp>)</rp>
</ruby>
```

##### 字符

```html
<rt></rt>	定义字符（中文注音或字符）的解释或发音。
<ruby>
  汉 <rp>(</rp><rt>Han</rt><rp>)</rp>
  字 <rp>(</rp><rt>zi</rt><rp>)</rp>
</ruby>
```

##### 注释使用

```html
<rp>	</rp>在ruby注释中使用，定义不支持ruby元素的浏览器所显示的内容。
<ruby>
  汉 <rp>(</rp><rt>Han</rt><rp>)</rp>
  字 <rp>(</rp><rt>zi</rt><rp>)</rp>
</ruby>
```

##### 区段

```html
<section>	</section>定义文档中的节（section、区段）。
<section>
<h1>WWF</h1>
<p>The World Wide Fund for Nature (WWF) is....</p>
</section>
```

##### 时间或日期

```html
<time>	</time>定义时间或日期。
<p>我们在每天早上 <time>9:00</time> 开始营业。</p>
 
<p>我在 <time datetime="2016-02-14">情人节</time> 有个约会。</p>
```

##### 添加换行符

```html
<wbr> 规定在文本的何处适合添加换行符。
<p>学习 AJAX ,您必须熟悉 <wbr>Http<wbr>Request 对象。</p>
```

#### canvas标签

canvas标签定义图形，比如图标和其他图像，必须使用脚本绘制图形。

##### 什么是cnanvas?

html5canvas元素用于图像的绘制，通过脚本（通常是JavaScript）来完成。

canvas 标签只是图像容器，必须使用脚本来绘制图形。

##### 画布

一个画布网页是一个矩形框，通过 canvas 元素来绘制。

例如：

```html
<canvas id="mycanvas" widch="200" height="100"></canvas>
```

注意：标签通常需要指定一个id属性（脚本中经常引用）,width和height属性定义的画布大小。

提示：可以在html页面中使用多个canvas元素。

##### 使用style属性类添加边框

```html
<canvas id="mycanvas" width="200" height="100"
        style="border:1px soild #000000"></canvas>
```

#####使用JavaScript来绘制图像

canvas元素本身是没有绘图能力的。所有的绘制工作必须在JavaScript内部完成：

```javascript
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="#FF0000";
ctx.fillRect(0,0,150,75);
```

##### 实例解析

首先，找到 canvas 元素：

```javascript
var c=document.getElementById("myCanvas");
```

然后，创建 cantext 对象：

```javascript
var ctx=c.getContext("2d");
```

getContext("2d") 对象是内建的HTML5对象，拥有多种绘制路径。矩形，图形，字符以及添加图像的方法。

下面两行代码绘制一个红色的矩形：

```javascript
ctx.fillStyle="#FF0000";
ctx.fillRect(0,0,150,75);
```

设置fillStyle属性可以是CSS颜色，渐变，或图案。fillStyle 默认设置是#000000（黑色）。

fillRect(*x,y,width,height*) 方法定义了矩形当前的填充方式。

##### canvas坐标

canvas 是一个二维网格。

canvas 的左上角坐标为 (0,0)

上面的 fillRect 方法拥有参数 (0,0,150,75)。

意思是：在画布上绘制 150x75 的矩形，从左上角开始 (0,0)。

##### canvas-路径

在canvas上画线，使用以下两种方法：

- moveTo(x, y) 定义线条开始坐标
- lineTo(x, y)定义线条结束坐标

绘制线条我们必须使用到“ink”的方法，就像 stroke()

```javascript
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.moveTo(0,0);
ctx.lineTo(200,100);
ctx.stroke();
```

#####  canvas绘制圆形

 在canvas中绘制圆形, 我们将使用以下方法 

```javascript
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.arc(95,50,40,0,2*Math.PI);
ctx.stroke()
```

 实际上我们在绘制圆形时使用了 "ink" 的方法, 比如 stroke() 或者 fill(). 

##### canvas-文本

使用 canvas 绘制文本，重要的属性和方法如下：

- font - 定义字体。
- fillText(text, x, y) - 在 canvas上绘制实心的文本。
- strkeText(text, x, y) - 在 canvas 上绘制空心的文本。

###### 使用 fillText();

```JavaScript
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.font="30px Arial";
ctx.fillText("Hello World",10,50);
```

###### 使用 strokeText();

```javascript
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.font="30px Arial";
ctx.strokeText("Hello World",10,50);
```

##### canvas - 渐变

渐变可以填充在矩形，原形，线条，文本等等，各种形状可以自己定义不同的颜色。

例如：一下不同的方式来设置 canvas 渐变：

- createLinearGradient(*x,y,x1,y1*) - 创建线条渐变。

- createRadialGradient(*x,y,r,x1,y1,r1*) - 创建一个径向/圆渐变。

  当使用渐变对象，必须使用两种或两种以上的停止颜色。

  addColorStop()方法指定颜色停止，参数使用坐标来描述，可以是0至1.

  使用渐变，设置fillStyle或strokeStyle的值为 渐变，然后绘制形状，如矩形，文本，或一条线。

  使用 createLinearGradient():

  ##### 线性渐变

  ```JavaScript
  var c=document.getElementById("myCanvas");
  var ctx=c.getContext("2d");
   
  // 创建渐变
  var grd=ctx.createLinearGradient(0,0,200,0);
  grd.addColorStop(0,"red");
  grd.addColorStop(1,"white");
   
  // 填充渐变
  ctx.fillStyle=grd;
  ctx.fillRect(10,10,150,80);
  ```

  ##### 径向或圆形渐变

  ```javascript
  var c=document.getElementById("myCanvas");
  var ctx=c.getContext("2d");
   
  // 创建渐变
  var grd=ctx.createRadialGradient(75,50,5,90,60,100);
  grd.addColorStop(0,"red");
  grd.addColorStop(1,"white");
   
  // 填充渐变
  ctx.fillStyle=grd;
  ctx.fillRect(10,10,150,80);
  ```

  ##### canvas - 图像

  把一副图像放置在画布上，使用以下方法：

  - drawImage(*image,x,y*)

  ```html
  <p>Image to use:</p>
  <img id="scream" src="img_the_scream.jpg" alt="The Scream" width="220" height="277"><p>Canvas:</p>
  <canvas id="myCanvas" width="250" height="300" style="border:1px solid #d3d3d3;">
  </canvas>
  
  <script>
  
  var c=document.getElementById("myCanvas");
  var ctx=c.getContext("2d");
  var img=document.getElementById("scream");
  
  img.onload = function() {
    ctx.drawImage(img,10,10);
  } 
  </script>
  ```
