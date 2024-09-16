#### 画布

##### 描述

 canvas 标签用于绘制图像（通过脚本，通常是 JavaScript）。
不过，canvas>元素本身并没有绘制能力（它仅仅是图形的容器） - 您必须使用脚本来完成实际的绘图任务。
getContext() 方法可返回一个对象，该对象提供了用于在画布上绘图的方法和属性。

##### 颜色、样式和阴影

```html
fillStyle   //设置或返回用于填充绘画的颜色，渐变或模式。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
    var c=document.getElementById("myCanvas");
    var ctx=c.getContext("2d");
    ctx.fillStyle="#FF0000";
    ctx.fillRect(20,20,150,100);
</script>
```

##### 边框的颜色、渐变或模式

```html
strokeStyle //设置或返回用于边框的颜色、渐变或模式。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
    var c=document.getElementById("myCanvas");
    var ctx=c.getContext("2d");
    ctx.strokeStyle="#FF0000";
    ctx.strokeRect(20,20,150,100);
</scrip>
```

##### 阴影的颜色

```html
shadowColor //设置或返回用于阴影的颜色。
<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
    var c=document.getElementById("myCanvas");
    var ctx=c.getContext("2d");
    ctx.shadowBlur=20;
    ctx.fillStyle="red";
    ctx.shadowColor="black";
    ctx.fillRect(20,20,100,80);
    ctx.shadowColor="blue";
    ctx.fillRect(140,20,100,80);
</script>
```

##### 模糊级别

```html
shadowBlur  //设置或返回用于阴影的模糊级别

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
    var c=document.getElementById("myCanvas");
    var ctx=c.getContext("2d");
    ctx.shadowBlur=20;
    ctx.shadowColor="black";
    ctx.fillStyle="red";
    ctx.fillRect(20,20,100,80);
</script>
```

##### 水平距离

```html
shadowOffsetX   //设置返回阴影与形状的水平距离。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
    var c=document.getElementById("myCanvas");
    var ctx=c.getContext("2d");
    ctx.shadowBlur=10;
    ctx.shadowOffsetX=20;
    ctx.shadowColor="black";
    ctx.fillStyle="red";
    ctx.fillRect(20,20,100,80);
</script>
```

##### 垂直距离

```html
shadowOffsetY   //设置或返回阴影与形状的垂直距离。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
    var c=document.getElementById("myCanvas");
    var ctx=c.getContext("2d");
    ctx.shadowBlur=10;
    ctx.shadowOffsetY=20;
    ctx.shadowColor="black";
    ctx.fillStyle="red";
    ctx.fillRect(20,20,100,80);
</script>
```

##### 线性渐变

```html
createLinearGradient()  //创建线性渐变（用在画布内容上）。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
var grd=ctx.createLinearGradient(0,0,170,0);
grd.addColorStop(0,"black");
grd.addColorStop(1,"white");
ctx.fillStyle=grd;
ctx.fillRect(20,20,150,100);
</script>
```

###### 颜色和停止位置

```html
addColorStop()  //规定渐变对象中的颜色和停止位置

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
var grd=ctx.createLinearGradient(0,0,170,0);
grd.addColorStop(0,"black");
grd.addColorStop(1,"white");
ctx.fillStyle=grd;
ctx.fillRect(20,20,150,100);
</script>
```

#### 线条样式

##### 结束端点样式

```html
lineCap //设置或返回线条的结束端点样式。

<p>三种不同的结束线:</p>
<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.lineWidth=10;
ctx.lineCap="butt";
ctx.moveTo(20,20);
ctx.lineTo(200,20);
ctx.stroke();
ctx.beginPath();
ctx.lineCap="round";
ctx.moveTo(20,40);
ctx.lineTo(200,40);
ctx.stroke();
ctx.beginPath();
ctx.lineCap="square";
ctx.moveTo(20,60);
ctx.lineTo(200,60);
ctx.stroke();
</script>
```

##### 拐角类型

```html
lineJoin    //设置或返回两条线相交，所创建的拐角类型。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.lineWidth=10;
ctx.lineJoin="round";
ctx.moveTo(20,20);
ctx.lineTo(100,50);
ctx.lineTo(20,100);
ctx.stroke();
</script>
```

#### 线条宽度

```html
lineWidth   //设置或返回当前的线条宽度

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.lineWidth=10;
ctx.strokeRect(20,20,80,100);
</script>
```

#### 斜接长度

```html
miterLimit  //设置或返回最大斜接长度

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<p>试图设置　miterLimit 4(然后,斜接长度将超过斜接限制),当行满足它将显示为　lineJoin =“bevel”。</p>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.lineWidth=10;
ctx.lineJoin="miter";
ctx.miterLimit=5;
ctx.moveTo(20,20);
ctx.lineTo(50,27);
ctx.lineTo(20,34);
ctx.stroke();
</script>
```

#### 矩形

##### 创建矩形

```html
roct()  //创建矩形

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.rect(20,20,150,100);
ctx.stroke();
</script> 
```

##### 填充的矩形

```html
fillRect()  //绘制被填充的矩形

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillRect(20,20,150,100);
</script>
```

##### 绘制矩形（无填充）

```html
<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.strokeRect(20,20,150,100);
</script>
```

##### 指定像素

```html
<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="red";
ctx.fillRect(0,0,300,150);
ctx.clearRect(20,20,100,50);
</script>
```

#### 路径

##### 绘制

```html
fill()  //绘制当前绘图（路径）。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.rect(20,20,150,100);
ctx.fillStyle="red";
ctx.fill();
</script> 
```

##### 绘制已定义

```html
stroke()    //绘制已定义的路径。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.moveTo(20,20);
ctx.lineTo(20,100);
ctx.lineTo(70,100);
ctx.strokeStyle="red";
ctx.stroke();
</script> 
```

##### 起始一条路径

```html
beginPath() //起始一条路径，或重置当前路径。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();              
ctx.lineWidth="5";
ctx.strokeStyle="green";  // 绿色路径
ctx.moveTo(0,75);
ctx.lineTo(250,75);
ctx.stroke();  // 画 
ctx.beginPath();
ctx.strokeStyle="purple";  // 紫色的路径
ctx.moveTo(50,0);
ctx.lineTo(150,130);            
ctx.stroke();  // 画
</script>
```

##### 指定点

```html
moveTo()  //把路径移动到画布的指定点，不创建线条。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.moveTo(0,0);
ctx.lineTo(300,150);
ctx.stroke();
</script>
```

##### 起点路径

```html
clossPath() //创建从当前点回到起始点的路径。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.moveTo(20,20);
ctx.lineTo(20,100);
ctx.lineTo(70,100);
ctx.closePath();
ctx.stroke();
</script>
```

##### 创建定点线条

``` html
lineTo() //添加一个新点，然后在画布中创建从该点指定的线条。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.moveTo(0,0);
ctx.lineTo(300,150);
ctx.stroke();
</script>
```

##### 任意形状和尺寸的区域

``` html
clip()  //从原始画布剪切任意形状和尺寸的区域

<span>没有进行clip():</span>
<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
// 画一个矩形
ctx.rect(50,20,200,120);
ctx.stroke();
// 画一个红色矩形
ctx.fillStyle="red";
ctx.fillRect(0,0,150,100);
</script>

<span>有进行clip():</span>
<canvas id="myCanvas2" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas2");
var ctx=c.getContext("2d");
//剪切一个矩形区域
ctx.rect(50,20,200,120);
ctx.stroke();
ctx.clip();
//剪切之后画一个矩形
ctx.fillStyle="red";
ctx.fillRect(0,0,150,100);
</script> 
```

##### 二次贝塞尔曲线

```html
quadraticCurveTo()      //创建二次贝尔赛曲线。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.moveTo(20,20);
ctx.quadraticCurveTo(20,100,200,20);
ctx.stroke();
</script> 
```

###### 1定义和用法

quadraticCurveTo() 方法通过使用表示二次贝塞尔曲线的指定控制点，向当前路径添加一个点。

二次贝塞尔曲线需要两个点。
第一个点是用于二次贝塞尔计算中的控制点，第二个点是曲线的结束点。
曲线的开始点是当前路径中最后一个点。如果路径不存在，那么请使用 beginPath() 和 moveTo() 方法来定义开始点。

二次贝塞尔曲线

开始点：moveTo(20,20)
控制点：quadraticCurveTo(20,100,200,20)
结束点：quadraticCurveTo(20,100,200,20)

##### 三次贝尔赛曲线

```html
bezierCurveTo()     //创建三次贝尔赛曲线

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.moveTo(20,20);
ctx.bezierCurveTo(20,100,200,100,200,20);
ctx.stroke();
</script> 
```

###### 2定义和用法

bezierCurveTo() 方法通过使用表示三次贝塞尔曲线的指定控制点，向当前路径添加一个点。

三次贝塞尔曲线需要三个点。前两个点是用于三次贝塞尔计算中的控制点，第三个点是曲线的结束点。
曲线的开始点是当前路径中最后一个点。如果路径不存在，那么请使用 beginPath() 和 moveTo() 方法来定义开始点。

三次贝塞尔曲线

开始点：moveTo(20,20)
控制点 1：bezierCurveTo(20,100,200,100,200,20)
控制点 2：bezierCurveTo(20,100,200,100,200,20)
结束点：bezierCurveTo(20,100,200,100,200,20)

##### 弧或曲线

```html
arc()       //创建弧或曲线（用于创建原形或部分圆）

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.arc(100,75,50,0,2*Math.PI);
ctx.stroke();
</script> 
```

###### 3定义和用法

arc() 方法创建弧/曲线（用于创建圆或部分圆）。

提示：如需通过 arc() 来创建圆，请把起始角设置为 0，结束角设置为 2*Math.PI。

提示：请使用 stroke() 或 fill() 方法在画布上绘制实际的弧。

An arc

中心：arc(100,75,50,0*Math.PI,1.5*Math.PI)

起始角：arc(100,75,50,0,1.5*Math.PI)

结束角：arc(100,75,50,0*Math.PI,1.5*Math.PI)

##### 切线之间的弧或曲线

```html
arcTo()     //创建两切线之间的弧或曲线

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();     
ctx.moveTo(20,20);             //创建一个起点
ctx.lineTo(100,20);            // 创建一个水平线
ctx.arcTo(150,20,150,70,50);   // 创建一个弧
ctx.lineTo(150,120);           // 继续垂直线
ctx.stroke();                  //绘画
</script> 
```

##### 指定点位

```html
lsPointlnPath()     //如果指定的点位于当前路径中，则返回true，否则返回false。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.rect(20,20,150,100);
if (ctx.isPointInPath(20,50))
{
    ctx.stroke();
};
</script> 
```

#### 转换

##### 缩放

```html
scale()     //缩放当前绘图至更大或更小。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.strokeRect(5,5,25,15);
ctx.scale(2,2);
ctx.strokeRect(5,5,25,15);
</script> 
```

##### 旋转

```html
rotale()    //旋转当前绘图

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.rotate(20*Math.PI/180);
ctx.fillRect(50,20,100,50);
</script>
```

##### 映射画布位置

```html
translate()     //重新映射画布上的（0，0）位置。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillRect(10,10,100,50);
ctx.translate(70,70);
ctx.fillRect(10,10,100,50);
</script>
```

##### 替换矩阵

```html
transform()     //替换绘图的当前矩阵。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="yellow";
ctx.fillRect(0,0,250,100)
ctx.transform(1,0.5,-0.5,1,30,10);
ctx.fillStyle="red";
ctx.fillRect(0,0,250,100);
ctx.transform(1,0.5,-0.5,1,30,10);
ctx.fillStyle="blue";
ctx.fillRect(0,0,250,100);
</script>
```

##### 转换单位矩阵

```html
setTransform()      //将当前转换重置为单位矩阵。然后云心 transtorm()。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;"></canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="yellow";
ctx.fillRect(0,0,250,100)
ctx.setTransform(1,0.5,-0.5,1,30,10);
ctx.fillStyle="red";
ctx.fillRect(0,0,250,100);
ctx.setTransform(1,0.5,-0.5,1,30,10);
ctx.fillStyle="blue";
ctx.fillRect(0,0,250,100);
</script>
```

#### 文本

##### 字体属性

```html
font()      //设置或返回文本的当前字体属性。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">。</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.font="40px Arial";
ctx.fillText("Hello World",10,50);
</script>
```

#### 对齐方式

```html
texAlign()      //设置或返回文本内容的当前对齐方式。

<canvas id="myCanvas" width="300" height="200" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
//在位置150创建一个红色线
ctx.strokeStyle="red";
ctx.moveTo(150,20);
ctx.lineTo(150,170);
ctx.stroke();
ctx.font="15px Arial";    
// 表明不同 TextAlign 值
ctx.textAlign="start";      
ctx.fillText("textAlign=start",150,60);        
ctx.textAlign="end";      
ctx.fillText("textAlign=end",150,80);                  
ctx.textAlign="left";      
ctx.fillText("textAlign=left",150,100);
ctx.textAlign="center";     
ctx.fillText("textAlign=center",150,120);              
ctx.textAlign="right";      
ctx.fillText("textAlign=right",150,140);
</script>
```

##### 绘制当前文本基线

```html
texBaseline()       //设置或返回绘制文本时使用的当前文本基线。

<canvas id="myCanvas" width="400" height="200" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
//在Y = 100画一条红线
ctx.strokeStyle="red";
ctx.moveTo(5,100);
ctx.lineTo(395,100);
ctx.stroke();
ctx.font="20px Arial"
//每个在y = 100的单词有不同的 textbaseline 值
ctx.textBaseline="top"; 
ctx.fillText("Top",5,100); 
ctx.textBaseline="bottom"; 
ctx.fillText("Bottom",50,100); 
ctx.textBaseline="middle"; 
ctx.fillText("Middle",120,100); 
ctx.textBaseline="alphabetic"; 
ctx.fillText("Alphabetic",190,100); 
ctx.textBaseline="hanging"; 
ctx.fillText("Hanging",290,100); 
</script>
```

##### 填充文本

```html
fillText()      //在画布上绘制“被填充的”文本。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.font="20px Georgia";
ctx.fillText("Hello World!",10,50);
ctx.font="30px Verdana";
// 创建一个渐变
var gradient=ctx.createLinearGradient(0,0,c.width,0);
gradient.addColorStop("0","magenta");
gradient.addColorStop("0.5","blue");
gradient.addColorStop("1.0","red");
// 填充一个渐变
ctx.fillStyle=gradient;
ctx.fillText("Big smile!",10,90);
```

##### 绘制文本（无填充）

```html
strokeText()        //在画布上绘制文本（无填充）

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.font="20px Georgia";
ctx.strokeText("Hello World!",10,50);
ctx.font="30px Verdana";
// 创建一个渐变
var gradient=ctx.createLinearGradient(0,0,c.width,0);
gradient.addColorStop("0","magenta");
gradient.addColorStop("0.5","blue");
gradient.addColorStop("1.0","red");
// 填充一个渐变
ctx.strokeStyle=gradient;
ctx.strokeText("Big smile!",10,90);
</script>
```

##### 文本宽度

```html
measureText()       //返回包含指定文本宽度的对象。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.font="30px Arial";
var txt="Hello World"
ctx.fillText("width:" + ctx.measureText(txt).width,10,50);
ctx.fillText(txt,10,100);
</script>
```

#### 图像绘制

##### 绘制图像、画布或视频

```html
drawlmage()     //向画布上绘制图像、画布或视频

<p>要使用的图片:</p>
<img id="scream" src="img_the_scream.jpg">
<p>画布:</p>
<canvas id="myCanvas" width="250" height="300" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
var img=document.getElementById("scream");
img.onload = function()
{
    ctx.drawImage(img,10,10);
}
```

#### 像素操作

##### 宽度

```JavaScript
width()     //返回 lmageData 对象的宽度。

alert("Width of imgData is: " + imgData.width);
```

##### 高度

```JavaScript
height()        //返回 lmageData 对象的高度。

alert("Height of imgData is: " + imgData.height);
```

##### 图像数据

```html
data()      //返回一个对象，其包含指定的 lmageData 对象的数据。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
var imgData=ctx.createImageData(100,100);
for (var i=0;i<imgData.data.length;i+=4)
{
    imgData.data[i+0]=255;
    imgData.data[i+1]=0;
    imgData.data[i+2]=0;
    imgData.data[i+3]=255;
}
ctx.putImageData(imgData,10,10);
</script>
```

##### 创建新的对象

```html
createImageData()       //创建新的、空白 lmageData 对象。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
您的浏览器不支持 HTML5 canvas 标签。
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
var imgData=ctx.createImageData(100,100);
for (var i=0;i<imgData.data.length;i+=4)
{
    imgData.data[i+0]=255;
    imgData.data[i+1]=0;
    imgData.data[i+2]=0;
    imgData.data[i+3]=255;
}
ctx.putImageData(imgData,10,10);
</script>
```

##### 返回对象

```html
getImageData()      //返回 ImgeData 对象，该对象为画布上指定的矩形复制像素数据。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="red";
ctx.fillRect(10,10,50,50);
function copy()
{
    var imgData=ctx.getImageData(10,10,50,50);
    ctx.putImageData(imgData,10,70);
}
</script>
<button onclick="copy()">复制</button>
```

##### 指定图像数据

```html
putImageData()      //把图像数据（从指定的 lmageData）放回画布上。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="red";
ctx.fillRect(10,10,50,50);
function copy()
{
    var imgData=ctx.getImageData(10,10,50,50);
    ctx.putImageData(imgData,10,70);
}
</script>
<button onclick="copy()">复制</button>
```

#### 合成

##### 返回当前 alpha 值

```html
globalAlpha()       //设置或返回绘图的当前  alpha 或透明值。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="red";
ctx.fillRect(20,20,75,50);
//转换透明度
ctx.globalAlpha=0.2;
ctx.fillStyle="blue"; 
ctx.fillRect(50,50,75,50); 
ctx.fillStyle="green"; 
ctx.fillRect(80,80,75,50);
</script>
```

##### 放回已有图像

```html
globalCompositeOperation()      //设置或返回新图像如何绘制到已有的图像上。

<canvas id="myCanvas" width="300" height="150" style="border:1px solid #d3d3d3;">
</canvas>
<script>
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="red";
ctx.fillRect(20,20,75,50);
ctx.fillStyle="blue";
ctx.globalCompositeOperation="source-over";
ctx.fillRect(50,50,75,50);
ctx.fillStyle="red";
ctx.fillRect(150,20,75,50);
ctx.fillStyle="blue";
ctx.globalCompositeOperation="destination-over";
ctx.fillRect(180,50,75,50);
</script>
```

#### 其他

##### 保存当前状态

```html
save()      //保存当前环境的状态。
save()      //保存当前环境的状态。
restore()   //返回之前保存过的路径状态和属性。
createEvent()
getContext() 
toDataURL()
```
