## Ajax数据传输_XML


XML简介
XML 指可扩展标记语言EXtensible Markup Language,他设计的时候是用来传递数据的,虽然格式跟HTML类似.

xml示例 下面是一个XML示例



```
<?xml version="1.0" encoding="UTF-8"?>
<singer>
<name>周杰伦</name>
<age>18</age>
<skill>途牛</skill>
</note>
```


xml是纯文本 XML是纯文本,这点跟HTML很像,所以我们可以用任何的文本编辑软件去打开编辑它

XML语法
虽然看起来跟HTML类似,但是XML的语法有些需要注意的,更为详细的可以查阅w3cschool_xml教程

XML声明 第一行是XML的声明,指定XML版本(1.0)以及使用的编码(UTF-8万国码)


```
<?xml version="1.0" encoding="UTF-8"?>
```


自定义标签 XML中没有默认的标签,所有的标签都是我们定义者自定义的



```
<!-- 下列标签都是被允许的 --> 
<fox></fox>
<name></name>
双标签 XML中没有但标签,都是双标签

<haha>标签内</haha>
根节点 XML中必须有一个根节点,所有的子节点都放置在根节点下

<root>
  <name></name>
</root>
XML属性 跟HTML一样,XML的标签里面也能够添加属性type = 'text',但是不建议这样用,而是使用标签的方式来表述内容(下半部分代码)
<!-- 使用属性配合标签表述信息 --> 
<person sex="female">
  <firstname>Anna</firstname>
  <lastname>Smith</lastname>
</person> 
<!-- 使用标签来表述信息 --> 
<person>
  <sex>female</sex>
  <firstname>Anna</firstname>
  <lastname>Smith</lastname>
</person>
```


### XML解析
因为XML就是标签,所以直接用解析Dom元素的方法解析即可

html代码


```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <person id='personXML'>
      <name>fox</name>
      <age>18</age>
      <skill>小花花</skill>
  </person>
</body>
</html>
获取方法
<script type="text/javascript">
    var xmlObj = document.getElementById("personXML");
    var name = xmlObj.getElementsByTagName('name')[0].innerHTML;

    console.log(name);
</script>
```


PHP中设置Header
在php中如果要使用xml传输数据,需要使用header()设置返回的内容为xml



```
header('content-type:text/xml;charset=utf-8');
```



## Ajax数据传输_JSON


JSON语法
JSON(JavaScript Object Notation),是ECMAScript的子集,作用是进行数据的交换,而且由于语法更为简洁,网络传输,以及机器解析都更为迅速.

### 语法规则:
数据在键值对中
数据由逗号分隔
花括号保存对象
方括号保存数组
数据类型:

下列内容 无论 键 值 都是用双引号包起来

数字（整数或浮点数）
字符串（在双引号中）
逻辑值（true 或 false）
数组（在方括号中）
对象（在花括号中）
null
示例代码 下部分代码看起来类似于定义JavaScript对象



```
// 基本对象
{
  "name":"fox",
  "age":"18",
  "sex":"true",
  "car":null
}
// 数组 
[
  {
      "name":"小小胡",
      "age":"1"
  },
  {
      "name":"小二胡",
      "age":"2"
  }
]
```


### JSON解析
接下来演示如何使用JavaScript和PHP对JSON进行解析

JavaScript 中
使用JSON对象

`JSON.parse()`方法:将JSON字符串转化为JavaScript对象
`JSON.stringify()`方法:将JavaScript对象,转化为JSON字符串
由于老式IE(8以下)浏览器中没有JSON对象,通过导入JSON2.js框架即可解决,框架获取地址为:JSON2.js_github地址



```
var Obj = {
  name:"fox",
  age:18,
  skill:"撩妹"
};

console.log(Obj);

// 将JavaScript对象格式化为JSON字符串
var jsonStr = JSON.stringify(Obj);

console.log(jsonStr);

// 将JSON字符串转化为JavaScript对象
var jsonObj = JSON.parse(jsonStr);
console.log(jsonObj);
使用eval()方法 使用eval()方法需要注意的是,需要将内容使用()括号包裹起来,如示例代码 ``javascript <script type="text/javascript"> var jsonStr ={

  "name":"fox",
  "age":18,
  "skill":"撩妹"
}`;

var jsonObj = eval('('+jsonStr+')'); console.log(jsonObj);

</script>
```





### PHP中

* **json_decode()**方法: 将`json`字符串转化为变量
* **json_encode()**方法: 将变量转化为`json`字符串

* **示例代码:**
php


```
<?php 
    header("Content-Type:text/html;charset=utf-8");
    // json字符串
    $jsonStr = '{"name":"itcast","age":54,"skill":"歌神"}';
    // 字符串转化为 php对象
      print_r(json_decode($jsonStr));

      echo "<br>";
      // php数组
      $arrayName = array('name' =>'littleFox' ,'age' => 13 );
      // php对象 转化为 json字符串
      print_r(json_encode($arrayName));
 ?>
```


* 输出结果为:
stdClass Object ( [name] => itcast [age] => 54 [skill] => 歌神 ) 
{"name":"littleFox","age":13}