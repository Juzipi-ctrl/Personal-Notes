# Schema语法

## （1）元素定义

Schema 和 DTD 一样，都可以定义 XML 文档中的元素。在 Schema 文档中，元素定义的语法格式如下所示：

```xml
<xs:element name = "xxx" type = "yyy" />
```

以上的语法格式中，element 用于声明一个元素，xxx 指的是元素的名称，yyy 指的是元素的数据类。在 XMLSchema 中有很多内建的数据类型，其中最常用的有以下几种：

- xs::string ：表示字符串类型
- xs::decimal ：表示小数类型
- xs::integer：表示整数类型
- xs::boolean：表示布尔类型
- xs::date：表示日期类型
- xs::time：表示时间类型

了解元素的定义方式，一个XML的示例代码，具体如下：

```xml
<lastname>Smith</lastname>
<age>28</age>
<dateborn>1980-03-27</dateborn>
```

以上xml示例中，定义了3个元素，这三个元素对应的 Schema 定义如下所示：

```xml
<xs::element name = "lastname" type = "xs:string" />
<xs::element name = "age" type = "xs:integer" />
<xs::element nmme = "dateborn" type = "xs:date" />
```

## （2）属性的定义

在 Schema 文档中，属性定义的语法格式如下所示：

```xml
<xs:attribute name = "xxx" type = "yyy" />
```

以上语法格式中，xxx 指的是属性名称，yyy 指的是属性的数据类型。其中，属性的常用数据类型与元素相同，都使用的事 XML Schema 中内建的数据类型。

了解属性的定义方式，以一个简单 xml 的例子，具体以下所示：

```xml
<lastname lang = "EN">Smith</lastname>
```

以上的这段 xml 中，属性的名称是 lang ，属性值的类型时字符类型，因此，对应的 Schema 定义方式如下：

```xml
<xs:attribute name = "lang" type = "xs:string" />
```

## （3）简单类型

在 xml Schema 文档中，只包含字符数据的元素都是简单类型的。简单类型使用 xs:simpleType 元素来定义。如果想对现有元素内容的类型进行限制，则需要使用 xs:restriction 元素。以下通过几种情况进行限定：

### 1） xs:minlnclusive 和 xs:maxlnclusive 元素对值的限定

例如一个区间为 18~58 之间的表示：

```xml
<xs:element name="age">
    <xs:simpleType>  <!--类型标记-->
        <xs:restriction base="xs:integer">
            <xs:minInclusive value="18"></xs:minInclusive>  <!--范围设置-->
            <xs:maxInclusive value="58"></xs:maxInclusive>
        </xs:restriction>
    </xs:simpleType>
</xs:element>
```

以上示例中，元素 age 的属性时 integer,通过 xs:minlnclusive 和 xs:maxlnclusive 元素限制了。

### 2） xs::enumeration 元素对一组值的限定

如果希望将 xml 元素的内容限制为一组可接收的值，可以使用枚举约束（Enumeration Constraint),例如，要限定一个元素名为 Car 的元素，可接收的值只有 Audi, Golf, BMW ,具体示例如下：

```xml
<xs:element name="car">
<xs:simpleType>  <!--类型标记-->
    <xs:restriction base="xs:integer">
        <xs:enumeration value="Audi"></xs:enumeration>  <!--可允许接收-->
        <xs:enumeration value="Golf"></xs:enumeration>
        <xs:enumeration value="BMW"></xs:enumeration>
    </xs:restriction>
</xs:simpleType>
</xs:element>
```

### 3）xs:pattern 元素对一系列值的限定

如果希望把xml元素的内容限定定义为一系列可使用的数字或字母，可以使用模式约束（Pattern Constraint）。例如，要定义一个带有限定的元素“letter”，要求可接受的值只能是字母 a~z 其中一个，具体如下：

```xml
<xs:element name="letter">
<xs:simpleType>  <!--类型标记-->
    <xs:restriction base="xs:integer"> 
      <xs:pattern value = "[a-z]" />  <!--约束-->
    </xs:restriction>
</xs:simpleType>
</xs:element>
```

### 4）xs:restriction 元素对空白字符限定

在xml文档中，空白字符比较特殊，如果需要对空白字符（Whitespase Characters）进行处理，可以使用 whiteSpace 元素。WhiteSpace 元素中3个属性值可以设定，分别是 preserve, replace 和 collapse 。其中， preserve 表示不对元素中的任何空白字符进行处理，replace 表示移除所有的空白字符，collapse 表示将所有的空白字符缩减为一个单一字符。接下来，以 preserve 为例，进行限定，具体如下：

```xml
<xs:element name="address">
<xs:simpleType>  <!--类型标记-->
    <xs:restriction base="xs:integer">  
        <xs:restriction value="preserve" /> <!--空白字符限定-->
    </xs:restriction>
</xs:simpleType>
</xs:element>
```

上列示例中 address 元素内容的空白字符进行限定。在使用了 whiteSpace 限定时，将值设置为 “preserve”，表示这个 xml 处理器将不会处理该元素内容中的所有空白字符。

## （4）复杂类型

除简单类型之外的其他类型都是复杂类型，在定义复杂类型时，需要使用 xs:complexContent 元素来定义。复杂类型的元素可以包含子元素和属性，这样元素称为符合元素。在定义复合元素时，如果元素的开始标记和结束标记之间只包含字符数据内容，那么这样的内容是简易内容，需要使用 xs:simpleContent元素类定义。反之，元素的内容都是复杂内容，需要使用 xs:complexContent元素来定义。复合元素有4种基本类型：

### 1）空元素

这里的空元素指不包含内容，只包含属性的元素，具体示例如下：

```xml
<product prodid = "1234" />
```

以上元素定义中，没有定义元素 product 的内容，这时，空元素在 xml Schema 文档中对应的定义方式如下所示：

```xml
<xs:element name="car">
<xs:simpleType>  <!--类型标记-->
    <xs:restriction base="xs:integer">
       <xs:attribute name="prodid" type="xs:positiveInteger" /> <!--无内容只有属性元素-->
    </xs:restriction>
</xs:simpleType>
</xs:element>
```

### 2） 包含其他元素的元素

在 xml 文档中存在包含其他元素的元素，例如以下的示例代码：

```xml
<person>
    <firstname>John</firstname>
    <lastname>smith</lastname>
</person>
```

以上的示例中，元素 person 嵌套了两个元素，分别是 firstname 和 lastname。这时，在 Schema文档中对应的定义方式如下所示：

```xml
<xs:element name="person">
<xs:simpleType>  <!--类型标记-->
    <xs:restriction base="xs:integer">
        <xs:element name="firstname" type="xs:string" /> <!--包含元素的元素-->
        <xs:element name="lastname" type="xs:string"/>
    </xs:restriction>
</xs:simpleType>
</xs:element>
```

### 3）仅包含文本的元素

对于仅包含文本的复合元素，需要使用 simpleCountent 元素来添加内容。在使用简易内容时，必须在 simpleContent 元素内定义扩展或限定，这时，需要使用 extensino 或 restriction 元素来扩展或限制元素的基本简易类型。例如以下一个 xml 的简易例子，其中 "shoesize"仅包含文本，具体如下：

```xml
<shoesize country="france">35</shoesize>
```

在以上例子中，元素 shoesize 包含了属性以及元素内容，针对这种仅包含文本的元素，需要使用 extension 来对元素的类型进行扩展，在 Schema 文档中对应的定义方式如下：

```xml
<xs:element name="shoesize">
<xs:simpleType>  <!--类型标记-->
    <xs:simpleContent>
        <xs:extension base="xs:intege">
            <xs:attribute name="country" type="xs:string"></xs:attribute> <!--包含文本元素-->
        </xs:extension>
    </xs:simpleContent>
</xs:simpleType>
</xs:element>
```

### 4）包含元素和文本的元素

在 xml 文档中，某些元素经常需要包含文本以及其他元素，例如，以下的这段 xml 文档：

```xml
<letter>
    Dear Mr. <name>John Smith</name>.
    Your order <orderid>1032</orderid>
    will be shipped on <shipdate>2001-07-13</shipdate>.
</letter>
```

以上的这段xml文档，在 Schema 文档中对应的定义方式如下所示：

```xml
<xs:element name="letter">
<xs:simpleType mixed="true">  <!--类型标记-->
    <xs:sequence>
        <xs:element name="name" type="xs:string"></xs:element>
        <xs:element name="orderid" type="xs:positiveInteger"></xs:element>
        <xs:element name="shipdate" type="xs:date"></xs:element>
    </xs:sequence>
</xs:simpleType>
</xs:element>
```

