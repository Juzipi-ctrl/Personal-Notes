# Css

1、css 是什么

2、css 怎么用

3、css 选择器（重点+难点）

4、美化网页（文字、阴影、超链接、列表、渐变。。。）

5、盒子模型

6、浮动

7、定位

8、网页动画（特效效果）

## 什么是 css

cascading style sheet 层叠级样式表

css：表现层（美化网页）

字体、颜色、边距、高度、宽度、背景，定位

## 快速入门

```html
<!-- 样式标签 -->
<style></style>
```

## css 的导入方式

链接式 html

```html
<!-- 链接式 -->
<link rel="stylesheet" href="ur     l">  
```

导入式

```html
<!-- 导入式 -->
<style>
    @import url("url")
</style>
```

## 选择器

1、标签选择器

2、类选择器

3、id 选择器

## 层次选择器

1、后代选择器

```css
body p {
    background: red;
}
```

2、子选择器

```css
body>p {
    background:#3cbda6;
}
```

3、相邻选择器

```css
.active + p {
    background: #a13d30;
}
```

4、通用选择器

```css
.active~p {
    background: #02ff00;
}
```



## 结构类选择器

```css
/* ul 的第一个子元素 */
            ul li:first-child{
                background: #02ff00;
            }

            /* ul 的最后一个子元素 */
            ul li:last-child{
                background: #ff4832;
            }

            /* 选中 p1 d定位到父元素，选择当前的第一个元素   顺序
                选择当前 p 元素的父级元素，选中父级元素的第一个，并且是当前元素才生效
            */
            p:nth-child(1){
                background: #2700ff;
            }

            /* 选中父元素下的 p 元素的第二个。类型 */
            p:nth-of-type(2){
                background:yellow;
            }

/* 连接 a 特效 */
        a:hover{
            background:#a24fff;
        }

```

## 圆角边框

```css
 div{
            width: 100px;
            height: 100px;
            margin: 30px;
            border: 10px solid red;
            border-radius: 0 100% 0 0;
            transform: rotate(45deg);
        }
```

## 阴影

```css
.container{
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .container img{
            width: 300px;
            height: 300px;
            border-radius: 100%;
            box-shadow: 10px 10px 100px yellowgreen;
        }
```

## 浮动

**display 和 浮动**

```css
<!-- 
        block   块元素
        inline  行内元素
        inline-block   行内块元素
    -->
    <style>
        div{
            width: 100px;
            height: 100px;
            border: 1px solid red;
            display: inline;
        }
        span{
            width: 100px;
            height: 100px;
            border: 1px solid red;
            display: inline-block;
        }
    </style>

```

## 定位

### 1、相对定位

```html
<style>
        div{
            margin: 10px;
            padding: 5px;
            font-size: 22px;
            line-height: 25px;
        }
        .father{
            border: 5px solid #666;
            padding: 0%;
        }
        #first{
            background-color: coral;
            border: 5px dashed red;
            /* 相对定位 */
            position: relative;  
            top: -20px;
            left: 20px; 
        }
        #sercond{
            background-color: aquamarine;
            border: 5px dashed rgb(0, 255, 0);
        }
        #third{
            background-color: greenyellow;
            border: 5px dashed rgb(0, 170, 255);
            position: relative;
            bottom: -10px;
            right: 20px;
        }
        
    </style>

</head>
<body>
    

    <div class="father">
        <div id="first">第一个盒子</div>
        <div id="sercond">第二个盒子</div>
        <div id="third">第三个盒子</div>
    </div>
    

</body>
```

相对定位：position: relative; 

相对于原来的位置，进行指定的偏移，相对定位的话，它任然在标准文档流中！

```css
top: -20px;
left: 20px; 
bottom: -10px;
right: 20px;
```



### 2、绝对定位

定位：基于什么定位

```css
.father {
                border: 5px solid #666;
                padding: 0%;
                position: relative;  
            }

            #first {
                background-color: coral;
                border: 5px dashed red;
            }

            #sercond {
                background-color: aquamarine;
                border: 5px dashed rgb(0, 255, 0);
                position: absolute;   /* 绝对定位 */
                left: 40px;
                right: 600px;
            }
```



### 3、固定定位

```css
<style>
        body{
            height: 1000px;
        }
        /* 绝对定位 */
        div:nth-of-type(1){
            width: 100px;
            height: 100px;
            background:red;
            position: absolute;
            right: 200px;
            bottom: 200px;
        }
        /* 固定定位  fixed */
        div:nth-of-type(2){
            width: 50px;
            height: 50px;
            background: violet;
            position: fixed;
            right: 0;
            bottom: 500px;
        }
    </style>
```



### 4、z-index



