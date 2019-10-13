# 同源以及跨域


同源
同源策略是浏览器的一种安全策略，所谓同源是指，域名，协议，端口完全相同。

|URL	|说明	|是否允许通信|
|:---:|:---:|:---:|
http://www.a.com/a.js
http://www.a.com/b.js	同一域名下	允许
http://www.a.com/lab/a.js
http://www.a.com/script/b.js	同一域名下不同文件夹	允许
http://www.a.com:8000/a.js
http://www.a.com/b.js	同一域名，不同端口	不允许
http://www.a.com/a.js
https://www.a.com/b.js	同一域名，不同协议	不允许
http://www.a.com/a.js
http://70.32.92.74/b.js	域名和域名对应ip	不允许
http://www.a.com/a.js
http://script.a.com/b.js	主域相同，子域不同	不允许
http://www.a.com/a.js
http://a.com/b.js	同一域名，不同二级域名（同上）	不允许（cookie这种情况下也不允许访问）
http://www.cnblogs.com/a.js
http://www.a.com/b.js	不同域名	不允许
## 跨域方案
顶级域名相同的可以通过`domain.name`来解决，即同时设置 domain.name = 顶级域名（如example.com）



```
document.domain + iframe

window.name + iframe

location.hash + iframe

window.postMessage()
```



## 浏览器中跨域请求方案

### JSONP
`JSON with Padding`其本质是利用了`<script src=""></script>`标签具有可跨域的特性，由服务端返回一个预先定义好的Javascript函数的调用，并且将服务器数据以该函数参数的形式传递过来，此方法需要前后端配合完成。

只能以GET方式请求

注意只能够通过get方法

服务端代码




```
<?php 

    // echo "alert('天气不错哦')";

    $callBack = $_GET['callback'];



    $arr = array(

        'name' =>'西兰花' ,

        'color' =>'red' 

         );

    echo $callBack."(".json_encode($arr).")";

```


?>
前端代码:注意,域名不同

核心是 通过script标签的src属性提交get请求



```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <title>Document</title>

    <script type="text/javascript">

        function fn(data){

            console.log(data);

        }

    </script>

    <script type="text/javascript" src='http://www.section02.com/seciton02_jsonP.php?callback=fn'></script>

</head>

<body>

    <h1>区域1的页面_jsonP演示</h1>

</body>

</html>
```


## jQuery 的$.ajax()
方法当中集成了JSONP的实现，可以非常方便的实现跨域数据的访问。

`dataType: 'jsonp'` 设置dataType值为jsonp即开启跨域访问

jsonp 可以指定服务端接收的参数的“key”值，默认为callback

jsonpCallback 可以指定相应的回调函数，默认自动生成

示例代码



```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <title>Document</title>

    <script type="text/javascript" src='jquery/jquery-3.0.0.min.js'></script>

</head>

<body>

<h1>区域1的页面</h1>

    <input type="button" name="" onclick='sendAjax()' value="jquery区域请求">

</body>

</html>

<script type="text/javascript">

    function sendAjax(){

        $.ajax({

            url:'http://www.section02.com/sectcion02_jqJsonp.php',

            type:'post',

            dataType: 'jsonp',

            data:{name:'itt'},

            success:function(data){

                console.log(data);

            }

        })

    }

</script>
```

