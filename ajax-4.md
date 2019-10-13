## JQuery中的Ajax

### JQueryAjax使用
JQuery作为最受欢迎的js框架之一,常见的Ajax已经帮助我们封装好了,只需要调用即可,更为详细的api文档可以查阅:[w3cSchool_JQueryAjax](https://www.w3school.com.cn/jquery/jquery_ref_ajax.asp)

#### $.get()方法
使用get方法向服务器获取数据

参数列表
|参数|	描述|
|:---:|:---:|
|url	|必需。规定将请求发送的哪个 URL。|
|data	|可选。规定连同请求发送到服务器的数据。|
|success(response,status,xhr)	|可选。规定当请求成功时运行的函数。额外的参数：response - 包含来自请求的结果数据status - 包含请求的状态xhr - 包含 XMLHttpRequest 对象
|dataType	|可选。规定预计的服务器响应的数据类型。默认地，jQuery 将智能判断。可能的类型："xml""html""text""script""json""jsonp"

### 格式化表单$('form').serialize()
我们在向服务器提交数据时,如果使用的是Ajax需要手动将数据格式化`name=fox&age=18`类似这样的格式,JQuery已经帮助我封装好了一个格式化数据的方法

语法:`$(selector).serialize()` 直接可以将form中拥有name属性的表单元素的字,进行格式化

示例代码:



```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>测试jq_serialize方法</title>
  <script type="text/javascript" src="./files/jquery.min.js"></script>
  <script type="text/javascript">
      $(function(){
          $("#getFormInfo").on("click",function(){
              var info = $("#testForm").serialize()
              console.log(info);
          })
      })
  </script>
</head>
<body>
  <form id="testForm">
      <input type="text" placeholder="您的姓名" name="userName">
      <input type="text" placeholder="您的爱好" name="userHabbit">
      <input type="text" placeholder="您最喜爱的食物" name="userHabbit">
  </form>
  <input type="button" value="格式化表单数据" id="getFormInfo">
</body>
</html>
```
### $.post()方法
通过post的方式向服务器获取数据

参数列表:
|参数	|描述|
|:---:|:---:|
|url	|必需。规定把请求发送到哪个 URL。
|data|	可选。映射或字符串值。规定连同请求发送到服务器的数据。
|success(data, textStatus, jqXHR)	|可选。请求成功时执行的回调函数。
|dataType	|可选。规定预期的服务器响应的数据类型。默认执行智能判断（xml、json、script 或 html）。

示例代码:


```
$.post("01.post.php",data,function(backData){
    console.log(backData);
})
```


### $.ajax({}) 方法
$.ajax()方法相比于前面的方法,拥有更为自由的定制性,可以替换$.get(),$.post()方法

参数:

* 在w3cSchool_$.ajax_Api中,关于参数只有下列一个.实际使用中,传递的是一个对象
|参数	|描述
|:---:|:---|
|settings|	可选。用于配置 Ajax 请求的键值对集合。可以通过 $.ajaxSetup() 设置任何选项的默认值。

示例代码:

这里演示的是常用的属性


```
$.ajax({
        url:'01.php',//请求地址
        data:'name=fox&age=18',//发送的数据
        type:'GET',//请求的方式
        success:function (argument) {},// 请求成功执行的方法
        beforeSend:function (argument) {},// 在发送请求之前调用,可以做一些验证之类的处理
        error:function (argument) {console.log(argument);},//请求失败调用
    })
```

## 模版插件

### 模版引擎简介
我们在使用ajax请求数据时,返回的如果是一个JSON格式的字符串,我们需要将其包装到对应的HTML代码中,再添加到页面上,才能看到效果.那么这个包装得过程有没有简单的方法呢?

假设有如下数据(javascript中)


```
var obj = {
 name:"fox",
 age:18,
 skill:"卖萌"
};
```


希望包装为:



```
<ul>
  <li>姓名:fox</li>
  <li>年龄:18</li>
  <li>爱好:卖萌</li>
</ul>
```


定义模板,替换: 其间需要我们使用对象替换的位置为`<%= 属性名 %>`部分,如果可以读取模板->传入对象->完成替换->返回html代码 实现这样的步骤,那么就能够完成我们的模板操作了



```
<ul>
  <li>姓名:<%= name %></li>
  <li>年龄:<%= age %></li>
  <li>爱好:<%= skill %></li>
</ul>
```


模版插件原理
我们定义一段文本作为模板,读取文本,使用特殊的符号`<%= 属性名 %>`,通过正则表达式找到这些特殊的符号进行替换,是不是就实现了这样的效果呢?

定义正则表达式:
想要匹配<%= 属性名 %> 我们可以定义正则如下(javascript中)



```
/* 
JS中的RegExp对象:
    创建
        创建方法1: var reg = new RegExp("正则")
        创建方法2: var reg = /正则/;    推荐使用这种
    使用:
        reg.exec(string) 可以检测字符串
*/
/*
正则含义
    <%:以 <% 开始
    =\s* "="号之后有0个或多个空白字符
    ([^%>]+\S): 匹配除了%>以外的所有字符(至少1个)
    \s*:0个或多个空白字符
    %>:以%>结束
*/
    var reg = /<%=\s*([^%>]+\S)\s*%>/;
```


基本使用
定义好作为模板的文本
使用正则表达式进行匹配替换即可


```
// 定义文本
var str = '大家好，我叫<%= name %>，我今年<%= age %>，我的爱好为:<%= skill %>';
// 定义数据
var data = {
        name: 'itcast',
        age: 10,
        skill:'打篮球'
        };

        // 快速的创建方法,好处,直接使用 \ 即可 不需要考虑 转义
    var reg = /<%=\s*([^%>]+\S)\s*%>/;
    // 返回的是一个对象
    var match = null;

    // 使用  while循环 进行检查,知道没有匹配的内容
         while (match = reg.exec(str)){
            // 匹配到的字符串
            var mathString = match[0]
            // 子表达式匹配到的字符串
            var subString = match[1];
            // 打印文本内容
            console.log("循环中:"+str);
            // 替换字符串的内容
            var str = str.replace(mathString,data[subString]);
            match = reg.exec(str);

        }
    console.log("循环完毕:"+str);
```

### 常见的模板插件
BaiduTemplate(百度开发) ArtTemplate(腾讯开发) velocity.js(淘宝开发) Handlebars

#### ArtTemplate基本使用
模板引擎的用法大同小异,ArtTemplate由于性能优秀,这里我们演示ArtTemplate的用法

导入模板引擎: 将下载好的ArtTemplate导入到页面中
  `<script type="text/javascript" src = "./files/template-native.js"></script>`
定义模板:



```
<% %>这样的语法是定义逻辑表达式 <%=内容 %>这样的语法为输出表达式 注意:这路的模板type='text'如果写成javascript会执行

  <script type="text" id = "templ01">
        <ul>
            <li><%=name %></li>
            <li><%=age %></li>
            <li><%=skill %></li>
            <li><ul>favouriteFood
                <% for(var i = 0 ;i < favouriteFood.length;i++) {%>
                    <li><%=favouriteFood[i] %></li>
                <% } %>
                </ul>
            </li>
        </ul>
    </script>
```


读取模板,传入数据:

导入了模板引擎以后,我们可以使用template(模板id,数据);


```

    // 调用模板引擎的方法
    var backHtml = template("templ01",data);
    // 返回值就是填充好的内容
```


