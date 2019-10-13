# Ajax概念及基本使用

**同步&异步**
## 先上概念

* 同步:必须等待前面的任务完成,才能继续后面的任务

* 异步:不受当前任务的影响

举个例子:

同步:我们在银行排队时,只有等到你了,才能够去处理业务.


异步:我们在排队的时候,玩手机是没有任何影响的(不建议做低头族哦)


* 异步更新网站
当我们访问一个普通的网站时,当浏览器加载完:HTML,CSS,JS以后网站的内容就固定了.如果网站内容发生更改必须刷新页面才能够看到更新的内容

* 网站内容更新:
常规的网站内容更新,必须通过刷新显示新内容

想像一下
你正用手机看着微博

手机网速很慢

内容看完了,点击加载更多按钮

页面重新刷新 o(╯□╰)o

* 异步更新
实际情况是:我们在访问新浪微博时,当你看到一大半了,会自动帮我们加载更多的微博,同时页面并没有刷新

php_weibo.gif-4765.5kB

## Ajax概念
当我们正在排队的时候,可以通过手机去干一些其他的事情.

在浏览器中,我们也能够不刷新页面,通过ajax的方式去获取一些新的内容,类似网页有微博,朋友圈,邮箱等

单词解释:
Asynchronous Javascript And XML（异步JavaScript和XML）,他并不是凭空出现的新技术,而是对于现有技术的结合:核心是js对象XMLHttpRequest

XMLHttpRequest
ajax使用的依旧是HTTP请求,那么让我们来回忆一下一个完整的HTTP请求需要什么

请求的网址,方法get/post

提交请求内容数据,请求主体等

接收响应回来的内容

###  五步使用法:

建立XMLHTTPRequest对象

#### 注册回调函数

当服务器回应我们了,我们想要执行什么逻辑
使用open方法设置和服务器端交互的基本信息

设置提交的网址,数据,post提交的一些额外内容
设置发送的数据，开始和服务器端交互

发送数据
更新界面

在注册的回调函数中,获取返回的数据,更新界面
示例代码:GET

get的数据,直接在请求的url中添加即可

```
<script type="text/javascript">

    // 创建XMLHttpRequest 对象

    var xml = new XMLHttpRequest();

    // 设置跟服务端交互的信息

    xml.open('get','01.ajax.php?name=fox');

    xml.send(null);    // get请求这里写null即可

    // 接收服务器反馈

    xhr.onreadystatechange = function () {

        // 这步为判断服务器是否正确响应

        if (xhr.readyState == 4 && xhr.status == 200) {

            // 打印响应内容

            alert(xml.responseText);

        } 

    };

</script>
    
```
    
```
示例代码:POST

<script type="text/javascript">

    // 异步对象

    var xhr = new XMLHttpRequest();



    // 设置属性

    xhr.open('post', '02.post.php' );



    // 如果想要使用post提交数据,必须添加

    xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");



    // 将数据通过send方法传递

    xhr.send('name=fox&age=18');



    // 发送并接受返回值

    xhr.onreadystatechange = function () {

    // 这步为判断服务器是否正确响应

    if (xhr.readyState == 4 && xhr.status == 200) {

           alert(xhr.responseText);

         } 

    };

</script>
```


### XMLHttpRequest_API讲解
#### 创建XMLHttpRequest对象(兼容性写法)
* 新版本浏览器:



```
var xml=new XMLHttpRequest();
（IE5 和 IE6）

var xml=new ActiveXObject("Microsoft.XMLHTTP");
```


* 考虑兼容性创建Ajax对象



```
 var request ;

 if(XMLHttpRequest){

    // 新式浏览器写法

    request = new XMLHttpRequest();

 }else{

    //IE5,IE6写法

    new ActiveXObject("Microsoft.XMLHTTP");

 }
```

#### 发送请求:
|方法|	描述|
|:---:|:---:|
|open(method,url,async)	|规定请求的类型、URL 以及是否异步处理请求。method：请求的类型；GET 或 POSTurl：文件在服务器上的位置async：true（异步）或 false（同步）
|send(string)|	将请求发送到服务器。string：仅用于 POST 请求
### POST请求注意点:
如果想要像form表单提交数据那样使用POST请求,需要使用XMLHttpRequest对象的setRequestHeader()方法 来添加 HTTP 头。然后在 send() 方法中添加想要发送的数据：




```
xmlhttp.open("POST","ajax_test.php",true);

xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");

xmlhttp.send("fname=Bill&lname=Gates");
```


### onreadystatechange事件
当服务器给予我们反馈时,我们需要实现一些逻辑

|属性|	描述|
|:---:|:---:|
|onreadystatechange|	存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。
|readyState|	存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。0: 请求未初始化1: 服务器连接已建立2: 请求已接收3: 请求处理中4: 请求已完成，且响应已就绪
|status|	200: "OK"404: 未找到页面

### 服务器响应内容
如果响应的是普通字符串,使用responseText,如果响应的是XML,使用responseXML

|属性|	描述|
|:---:|:---:|
|responseText|	获得字符串形式的响应数据。
|responseXML|	获得 XML 形式的响应数据。