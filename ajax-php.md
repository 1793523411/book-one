# PHP基础

## 服务端web开发
在讲解什么是服务端开发之前,让我们先思考几个问题

* 网站访问:
当我们做好了.html的网站,如何让别人(朋友,用户)可以访问到呢?

使用U盘拷贝,QQ发送文件等直接将文件共享的方式?---不灵活
将网站放在服务器上,让用户通过网址访问?---绝大多数网站的做法
* 网站内容更新:

如果用户每次访问我们的网站看到的内容都是一样的,在最初的新鲜劲过去以后估计就再也不想访问我们的网站了o(╯□╰)o,那么如何去更新网站的内容呢?

当有内容,图片,或者界面需要更新是,直接修改.html文件?---费时费力
通过某种手段,当有新的消息,自动的完成网站的更新?---动态网站
* 如何实现网站动态化

网站的本质,其实就是一堆按照某种规则排列的字符串而已,如果我们可以通过某种方式,让电脑动态生成这些字符串,是不是就实现了网站的动态化?

想要让电脑干事情,可以通过编程语言来实现.
编程语言的编写位置为服务器,因为用户是问服务器要网站的
在服务器,通过编程语言让用户访问的网站动态化叫做:服务端web开发
 *可选开发方式: 虽然基本上所有可以返回字符串的编程语言都能够实现这个功能,目前市场主流开发语言有:Java,PHP,ASP.Net,Ruby,Python,Erlang等.虽然可以选择的开发语言有很多种,但是本质都是一样的:

当用户访问网站了,根据`某些逻辑`,生成对应的`HTML,CSS,JS`代码给用户
## PHP简介
PHP在众多的编程语言中,是比较容易上手,结合我们搭建的WAMP环境就能够开始学习了

PHP代码执行方式: 服务端web编程写好的代码,需要通过浏览器访问服务器,在服务器端执行,然后返回给用户结果,如果直接使用浏览器打开,就会解析为文本
phpSteps.gif-128.5kB

### PHP常见语法
注,这里只列举常用的PHP语法,更为详细的语法教程可以查阅w3cschool_PHP教程

文件定义,注释: PHP文件以.php结尾,代码的编写位置在<?php 写在这里?>.注释的写法跟js一致



```
<?php
  //这是单行注释
  /*
      这是多行注释
  */
?>
```


### PHP变量规则:

变量以$符号开头，其后是变量的名称
变量名称必须以字母或下划线开头
变量名称不能以数字开头
变量名称只能包含字母数字字符和下划线（A-z、0-9 以及_）
变量名称对大小写敏感


```
// 变量以`$`符号开头，其后是变量的名称
// 变量名称必须以字母或下划线开头
$a;
$b;
$a1;
$_abc;

// 变量名称不能以数字开头
// 变量名称只能包含字母数字字符和下划线（`A-z`、`0-9` 以及` _`）
// 下面这些是错误的变量定义
$1;
$哈哈;
$^&*;

//变量名称对大小写敏感（`$y` 与`$Y` 是两个不同的变量）
// 下面定义的两个变量是不同的,大写,小写x
$x;
$X;
```


### 数据类型 
PHP支持的数据类型包括:字符串,整数,浮点数,布尔,数组,对象,NULLL(注:由于对象中可以使用函数,故对象的语法在下文中会提及)
定义字符串时需要注意:
单引号:`` 内部的内容只是作为字符串
双引号:"" 如果内部是PHP的变量,那么会将该变量的值解析
字符串连接:不同于JavaScript,PHP中使用.进行连接


```
// 字符串
$str = '123';

// 字符串连接
$str2 = '123'.'哈哈哈';

// 字符串

// 整数
$numA = 1; //正数
$numB = -2;//负数

// 浮点数
$x = 1.1;

// 布尔
$a = true;
$b = false;

// 数组
$arr = array('123',123)
```


### 运算符 
PHP中的运算符跟JavaScript中的基本一致,用法也基本一致

算数运算符: +,-,/,*,%
赋值运算符: x = y,x += y,x -= y 注:这里列举的并不完全,更为详细的PHP运算符教程请查阅w3cschool_PHP运算符


```
<?php 
$x=10; 
$y=6;
echo ($x + $y); // 输出 16
echo ($x - $y); // 输出 4
echo ($x * $y); // 输出 60
echo ($x / $y); // 输出 1.6666666666667
echo ($x % $y); // 输出 4
?>
```


### 函数: 
PHP虽然系统内建了一些函数,但是这不影响我们定义自己的. 函数的作用就是在代码中可以重复使用的语法块,页面加载的时候不会执行,只有在被调用的时候才会执行


```
// 基础语法
function functionName() {
  这里写代码
}

// 无参数 无返回值的函数
function sayhi(){
    echo "Hello World";
}

// 有参数 无返回值的函数
function sayName($name){
    echo $name.'你好哦';
}
// 调用
sayName('小狐狸');

// 有参数,参数有默认值的函数
function sayFood($food='西兰花'){
    echo $food.'好好吃';
}
// 调用
sayFood('西葫芦');// 如果传入参数,就使用传入的参数
sayFood();// 如果不传入参数,直接使用默认值

// 有参数,有返回值的函数
function sum($a,$b){
    return $a+$b
}
sum(1,2);// 返回值为1+2 = 3
```


### 对象 
PHP中允许使用对象这种,自定义数据类型. 使用时必须先声明,实例化之后才能够使用

```
// 定义最基础的类
class Fox{

        public $name = 'itcast';
        public $age = 10;
}
$fox = new $fox;
// 对象属性取值
$name = $fox->name;
// 对象属性赋值
$fox->name = '小狐狸';

// 带构造函数的对象
class fox{
    // 私有属性,外部无法访问
    var $name = '小狐狸';
    // 定义方法 用来获取属性
    function Name(){
    return $this->name;
    }
    // 构造函数,可以传入参数
    function fox($name){
    $this->name = $name
    }
}
    // 定义了构造函数 需要使用构造函数初始化对象
    $fox = new fox('小狐狸');
    // 调用对象方法,获取对象名
    $foxName = $fox->Name();
```


### 内容输出:
echo:PHP语句直接使用即可,输出字符串 print_r():函数输出复杂数据类型,比如数组,对象 var_dump():函数输出详细信息，如对象、数组


```
$arr =array(1,2,'123');

echo'123'; 
// 结果为 123

print_r($arr);
// 结果为 Array ( [0] => 1 [1] => 2 [2] => 123 )

var_dump($arr);
/* 结果为 
    array
  0 => int 1
  1 => int 2
  2 => string '123' (length=3)
*/
```


### 循环语句: 这里只列举了foreach,for循环


```
// for 循环
for ($x=0; $x<=10; $x++) {
  echo "数字是：$x <br>";
} 

// foreach 循环
$colors = array("red","green","blue","yellow"); 
// 参数1为循环的对象,参数2会将对象的值挨个取出,直到最后
// 如果循环的是对象的话,输出的是对象属性的值
foreach ($colors as $value) {
  echo "$value <br>";
}
输出结果为
/*
red 
green 
blue 
yellow 
*/
header()函数 用来向客户端(浏览器)发送报头,如果出现中文无法显示,可以尝试在PHP代码顶部添加 如下代码
header("content-type:text/html; charset=utf-8");
```

### php中header()


浏览器访问http服务器,接收到响应时,会根据响应报文头的内容进行一些具体的操作,在php中,我们能够使用 header来设置这些内容

设置文本编码

设置编码格式为:utf-8


```
header('content-type:text/html; charset= utf-8');
```


设置页面跳转

设置跳转到百度首页


```
header('location:http://www.baidu.com');
```


设置页面间隔刷新


```
header('refresh:3; url=http://www.xiaomi.com');
```
## PHP表单

### PHP_GET数据获取
在PHP中,如果想要获取通过get方法提交的数据,可以通过$_GET对象来获取(虽然参数在地址栏中可以查看)

HTML代码: 下面就是一个简单的表单代码,将数据提交到01.php,使用get的方式


```
<form action="01.php" method="get" >
  <label for="">姓名:
      <input type="text" name= "userName"></label>
      <br/>
  <label for="">邮箱:
      <input type="text" name= "userEmail"></label>
      <br/>
      <input type="submit" name="">
</form>
```


PHP代码:



```
<?php 
    echo "<h1>GET_PAGE</h1>";
    echo 'userName:'.$_GET['userName'];
    echo '<br/>';
    echo 'userEmail:'.$_GET['userEmail'];
 ?>
php_get.gif-191.8kB

```


## PHP_POST数据获取
在PHP中,如果想要获取通过post方法提交的数据,可以通过$_POST对象来获取

HTML代码: 下面就是一个简单的表单代码,将数据提交到02.php,使用post的方式(注意:代码中的method改为post)



```
<form action="02.php" method="post" >
  <label for="">姓名:
      <input type="text" name= "userName"></label>
      <br/>
  <label for="">邮箱:
      <input type="text" name= "userEmail"></label>
      <br/>
      <input type="submit" name="">
</form>
```


PHP代码:



```
<?php 
    echo "<h1>POST_PAGE</h1>";
    echo 'userName:'.$_POST['userName'];
    echo '<br/>';
    echo 'userEmail:'.$_POST['userEmail'];
 ?>
php_post.gif-271.1kB

```


### POST&GET错误处理
当我们直接访问POST&GET页面时由于并没有传递任何数据,会因为$_GET或$_POST不存在对应的key而报错.

处理方式1:
使用array_key_exists(key, 数组)函数来进行判断
参数1: 要检测的key字符串
参数2: 检验的数组
    

```
if(array_key_exists('name', $_GET)){
        //如果有数据 再去读取
    }else{
        // 反之 可以执行一些 其他的逻辑
    }
```


### PHP文件上传处理01_$_FILES对象
上传文件时html代码中需要进行如下设置:

在html表单中需要设置`enctype="multipart/form-data"`
只能post方式 PHP接收文件可以通过$_FILES来获取
HTML代码:



```
<form action="03.fileUpdate.php" method="post" enctype="multipart/form-data">
      <label for="">照片:
          <input type="file" name = "picture" multiple=""></label>
      <br/>
      <input type="submit" name="">
  </form>
```


PHP代码01 这部分代码测试$_FILES文件的具体内容



```
<?php  
  sleep(5);// 让服务器休息一会
  print_r($_FILES);
?>
php_post_file.gif-485.3kB
```



现象:

点击提交后,服务器没有立即出现反应,而是休息了一会sleep(5)
在wamp/tmp目录下面出现了一个.tmp文件
.tmp文件一会就被自动删除了
服务器返回的内容中,有文件的名字[name] => computer.png,以及上传文件保存的位置D:\wamp\tmp\php3D70.tmp
PHP文件上传处理02_文件保存
刚刚演示了$_FILES对象的作用,以及PHP接受上传文件时,会先保存在一个临时目录下,那么接下来我们就演示如何将临时目录下面的文件保存起来

HTML代码: 这部分的代码不需要改变



```
<form action="03.fileUpdate.php" method="post" enctype="multipart/form-data">
      <label for="">照片:
          <input type="file" name = "picture" multiple=""></label>
      <br/>
      <input type="submit" name="">
  </form>
```


PHP代码 move_uploaded_file()这个函数可以处理文件 w3cSchool_move_uploaded_file函数解释



```
Array ( [picture] => Array ( 
        [name] => computer.png 
        [type] => image/png 
        [tmp_name] => D:\wamp\tmp\php8913.tmp 
        [error] => 0 [size] => 5212 ) 
    )
```


其中我们需要通过picture(根据表单标签的name属性决定)获取临时文件名以及上传文件名



```
<?php  
    sleep(5);// 让服务器休息一会,方便我们查看上传的临时文件
    // 第一个参数是 规定要移动的文件
    // 第二个参数是 规定文件的新位置
    move_uploaded_file($_FILES['picture']['tmp_name'], './upload/'.$_FILES['picture']['name']);
 ?>
```
﻿## php保存上传文件


php中上传的文件,会先以临时文件的方式保存起来,我们将其移动到其他的位置即可

### $_FILE
在php中 能够通过$_FILE 获取上传的文件

浏览器端部分代码()
假定浏览器在form表单中如下标签
注1form提交数据需使用post提交
注2form提交数据时,需在form表单中添加enctype=multipart/form-data属性


```
<form action='xx.php' method='post' enctype='multipart/form-data'>
    <input type='file' name='icon'>
    <input type='submit'>
</form>
```


### 服务端代码


```
$_FILES用法跟$_GET,$_POST类似,都是关系型数组
#_FILE['key']:可以获取对应上传的文件,这里的key跟提交时的name相对应
#_FILE['key']['name'] 可以获取上传的文件名
#_FILE['key']['tmp_name']可以获取上传的文件保存的临时目录
<?php
// 可以打印 $_FILES的所有信息
print_r($_FILES);
?>
move_uploaded_file(移动文件)
```


上传的临时文件,一会就会被自动删除,我们需要将其移动到保存的位置


```
move_uploaded_file参数:
参数1:移动的文件
参数2:目标路径
move_uploaded_file($_FILES['photo']['tmp_name'], './images/test.jpg');

```
## php设置上传文件大小限制



在使用wamp过程中,如果想要修改上传的文件显示,需要如何设置呢?

### 修改php.ini
步骤

左键点击wamp
选择php
在弹出的窗口中选择php.ini
在打开的文件中进行修改(修改步骤如下)
修改完毕,保存并重启wamp
示意图 steps.gif-168.6kB

### 修改内容
使用文本编辑工具的搜索功能找到下列选项 进行修改

设置文件最大上传限制(值的大小可以根据需求修改)


```
file_uploads = On   ; 是否允许上传文件 On/Off 默认是On
upload_max_filesize = 32M       ; 上传文件的最大限制
post_max_size = 32M             ; 通过Post提交的最多数据
考虑网络传输快慢,这里修改一些参数
max_execution_time = 30000      ; 脚本最长的执行时间 单位为秒
max_input_time = 600            ; 接收提交的数据的时间限制 单位为秒
memory_limit = 1024M            ; 最大的内存消耗
```




![](/assets/PHP.png)
