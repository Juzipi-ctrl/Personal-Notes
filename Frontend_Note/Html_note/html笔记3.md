# SVG矢量图形

    * html5 支持内联SVG
    * html3 <svg> 元素是 SVG 图形的容器
    * svg 有多种绘制路径、框、园、文本和图形图像的方法。

## 什么是svg

    * svg 指可伸缩矢量图形（scalable vector graphice）
    * svg 用于定义用于网络的基于矢量的图形
    * svg 使用 XML 格式定义图形
    * svg 图像在放大或改变吗尺寸的情况下其图形质量不会有损失
    * svg 是万维网联盟的标准

## svg优势

与其他图形格式相比（比如jpeg和gif），使用svg的优势在于：
    1. svg 图像可通过文本编辑器类创建和修改。
    2. svg 图像可被搜索、索引、脚本化或压缩。
    3. svg 是可伸缩的。
    4. svg 图像可在任何的分辨率下被高质量地打印。
    5. svg 可在图像质量不下降的情况下被放大。

## 把 svg 直接嵌入 HTML 页面

### svg 圆形

    ```html
        <svg xmlns="http://www.w3.org/2000/svg" version="1.1">
        <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red" />
        </svg> 
    ```

### SVG五角星

    ```html
        <svg xmlns="http://www.w3.org/2000/svg" version="1.1" height="190">
        <polygon points="100,10 40,180 190,60 10,60 160,180"
        style="fill:lime;stroke:purple;stroke-width:5;fill-rule:evenodd;"/>
        </svg>
    ```

### SVG 与 Canvas两者间的区别

    SVG 是一种使用 XML 描述 2D 图形的语言。
    
    Canvas 通过 JavaScript 来绘制 2D 图形。
    
    SVG 基于 XML，这意味着 SVG DOM 中的每个元素都是可用的。您可以为某个元素附加 JavaScript 事件处理器。
    
    在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。
    
    Canvas 是逐像素进行渲染的。在 canvas 中，一旦图形被绘制完成，它就不会继续得到浏览器的关注。如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。

## MathML

    html5 可以在文档中使用 MathML 元素，对应的标签是 <math></math>。
    MathML 是数学标记语言，是一种基于 XML（标准通用的标记语言的子集）的标准，用来互联网上书写数学符号和公式的置标语言。

### MathML实例

    ```html
         <math xmlns="http://www.w3.org/1998/Math/MathML">
         <mrow>
            <msup><mi>a</mi><mn>2</mn></msup>
            <mo>+</mo>
            <msup><mi>b</mi><mn>2</mn></msup>
            <mo>=</mo>
            <msup><mi>c</mi><mn>2</mn></msup>
         </mrow>
      </math>
    ```

#### 使用第三方库

    ```html
        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="UTF-8">
            <title></title>
            <script type="text/javascript" src="https://static.runoob.com/assets/js/mathml/mspace.js"></script>
        </head>
            
        <body>
            
            <math xmlns="http://www.w3.org/1998/Math/MathML">
    
                <mrow>
                    <msup><mi>a</mi><mn>2</mn></msup>
                    <mo>+</mo>
                                    
                    <msup><mi>b</mi><mn>2</mn></msup>
                    <mo>=</mo>
                                    
                    <msup><mi>c</mi><mn>2</mn></msup>
                </mrow>
                       
            </math>
        </body>
        </html>
    ```

### 添加运算符

    ```html
        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="UTF-8">
            <title>菜鸟教程(runoob.com)</title>
        </head>
            
        <body>
            
            <math xmlns="http://www.w3.org/1998/Math/MathML">
                    
                <mrow>                
                    <mrow>
                                    
                    <msup>
                        <mi>x</mi>
                        <mn>2</mn>
                    </msup>
                                            
                    <mo>+</mo>
                                            
                    <mrow>
                        <mn>4</mn>
                        <mo>⁢</mo>
                        <mi>x</mi>
                    </mrow>
                                            
                    <mo>+</mo>
                    <mn>4</mn>
                                            
                    </mrow>
                                    
                    <mo>=</mo>
                    <mn>0</mn>
                                        
                </mrow>
            </math>
                    
        </body>
        </html>
    ```

#### 用第三方库

    ```html
        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="UTF-8">
            <title></title>
            <script type="text/javascript" src="https://static.runoob.com/assets/js/mathml/mspace.js"></script>
        </head>
            
        <body>
            
            <math xmlns="http://www.w3.org/1998/Math/MathML">
                    
                <mrow>                
                    <mrow>
                                    
                    <msup>
                        <mi>x</mi>
                        <mn>2</mn>
                    </msup>
                                            
                    <mo>+</mo>
                                            
                    <mrow>
                        <mn>4</mn>
                        <mi>x</mi>
                    </mrow>
                                            
                    <mo>+</mo>
                    <mn>4</mn>
                                            
                    </mrow>
                                    
                    <mo>=</mo>
                    <mn>0</mn>
                                        
                </mrow>
            </math>
                    
        </body>
        </html>
    ```

### 矩阵

    ```html
        <math xmlns="http://www.w3.org/1998/Math/MathML">
               
         <mrow>
            <mi>A</mi>
            <mo>=</mo>
                       
            <mfenced open="[" close="]">
                       
               <mtable>
                  <mtr>
                     <mtd><mi>x</mi></mtd>
                     <mtd><mi>y</mi></mtd>
                  </mtr>
                                       
                  <mtr>
                     <mtd><mi>z</mi></mtd>
                     <mtd><mi>w</mi></mtd>
                  </mtr>
               </mtable>
               
            </mfenced>
         </mrow>
      </math>
    ```

#### 第三方库

    ```html
        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="UTF-8">
            <title></title>
            <script type="text/javascript" src="https://static.runoob.com/assets/js/mathml/mspace.js"></script>
        </head>
            
        <body>
            <math xmlns="http://www.w3.org/1998/Math/MathML">
                    
                <mrow>
                    <mi>A</mi>
                    <mo>=</mo>
                            
                    <mfenced open="[" close="]">
                            
                    <mtable>
                        <mtr>
                            <mtd><mi>x</mi></mtd>
                            <mtd><mi>y</mi></mtd>
                        </mtr>
                                            
                        <mtr>
                            <mtd><mi>z</mi></mtd>
                            <mtd><mi>w</mi></mtd>
                        </mtr>
                    </mtable>
                    
                    </mfenced>
                </mrow>
            </math>
            
        </body>
        </html>
    ```

## 拖放

    拖放是一种常见的特性，即抓取对象以后拖到另一个位置。
    在html5中，拖放是标准的一部分，任何元素都能够拖放。

### 拖放实例

    ```html
        <!DOCTYPE HTML>
        <html>
        <head>
        <meta charset="utf-8"> 
        <title></title>
        <style type="text/css">
        #div1 {width:350px;height:70px;padding:10px;border:1px solid #aaaaaa;}
        </style>
        <script>
        function allowDrop(ev)
        {
            ev.preventDefault();
        }
        
        function drag(ev)
        {
            ev.dataTransfer.setData("Text",ev.target.id);
        }
        
        function drop(ev)
        {
            ev.preventDefault();
            var data=ev.dataTransfer.getData("Text");
            ev.target.appendChild(document.getElementById(data));
        }
        </script>
        </head>
        <body>
        
        <p>拖动图片到矩形框中:</p>
        
        <div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
        <br>
        <img decoding="async" loading="lazy" id="drag1" src="/images/logo.png" draggable="true" ondragstart="drag(event)" width="336" height="69">
        
        </body>
        </html>
    ```

#### 解释

##### 设置元素为可拖放

    首先，为了使元素可拖动，把 draggable 属性设置为 true ：
    
    ```html
    <img draggable="true">
    ```
    
    拖动什么 - ondragstart 和 setData()
    然后，规定当元素被拖动时，会发生什么。
    
    在上面的例子中，ondragstart 属性调用了一个函数，drag(event)，它规定了被拖动的数据。
    
    dataTransfer.setData() 方法设置被拖数据的数据类型和值：
    
    ```JavaScript
    function drag(ev)
    {
        ev.dataTransfer.setData("Text",ev.target.id);
    }
    ```
    Text 是一个 DOMString 表示要添加到 drag object 的拖动数据的类型。值是可拖动元素的 id ("drag1")。

##### 放到何处 - ondragover

    ondragover 事件规定在何处放置被拖动的数据。
    默认地，无法将数据/元素放置到其他元素中。如果需要设置允许放置，我们必须阻止对元素的默认处理方式。
    这要通过调用 ondragover 事件的 event.preventDefault() 方法：
    
    ```JavaScript
    event.preventDefault()
    ```

##### 进行放置 - ondrop

    当放置被拖数据时，会发生 drop 事件。
    在上面的例子中，ondrop 属性调用了一个函数，drop(event)：
    
    ```JavaScript
    function drop(ev)
    {
        ev.preventDefault();
        var data=ev.dataTransfer.getData("Text");
        ev.target.appendChild(document.getElementById(data));
    }
    ```

##### 代码解释

    调用 preventDefault() 来避免浏览器对数据的默认处理（drop 事件的默认行为是以链接形式打开）
    通过 dataTransfer.getData("Text") 方法获得被拖的数据。该方法将返回在 setData() 方法中设置为相同类型的任何数据。
    被拖数据是被拖元素的 id ("drag1")
    把被拖元素追加到放置元素（目标元素）中
