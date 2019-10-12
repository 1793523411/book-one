# 动画封装，事件，冒泡，事件委托
## 匀速动画


```
function animate(obj,target) {
        clearInterval(obj.timer)

        var speed = obj.offsetLeft < target ? 15 : -15;

        obj.timer = setInterval(function () {
            var result = target - obj.offsetLeft;

            obj.style.left = obj.offsetLeft + speed + "px";
            console.log(speed);
            if(Math.abs(result) <= 10 ){
                clearInterval(obj.timer);
                obj.style.left = target + "px";
            }

        },10);
    }
```



## 缓动动画
**缓动框架**
### 封装框架遇到的两个问题
原有的方法：div.style.width :这个方法比较固定，不能用变量或者字符串的形式更换属性，不方便我传值获取属性，和给属性赋值。
属性值的获取和属性的赋值
div.style["width"] = "5000px";
可以通过传字符串或者变量的方式获取和赋值属性。
缺点：他的操作完全是对行内式CSS来操作的。赋值的时候毫无问题。但是，获取值的时候有问题了。
1.12	获取任意类型的CSS样式的属性值
Div.style.width    
div.currentStyle.width
Window.getComputedStyle(div,null).width;
他们的公共使用变量或者字符串获取属性值的方法都是：去电属性和点，然后加上中括号和属性的字符串形式。
Div.style[“width”];
div.currentStyle[“width”];
Window.getComputedStyle(div,null)[“width”];

### 开闭原则
定义一个变量。数据可以修改。但是，只能修改成为两个值。
 
 

### 回调函数
程序执行完毕，在次执行的函数。
在函数中给指定的函数定义一个形参，然后程序执行到最后，调用这个形参后面加一个括号。


```
function animate(ele,target) {
                clearInterval(ele.timer);
                ele.timer = setInterval(function () {
                    var step = (target-ele.offsetLeft)/10;
                    step = step>0?Math.ceil(step):Math.floor(step);
                    ele.style.left = ele.offsetLeft + step + "px";
                    console.log(1);
                    if(Math.abs(target-ele.offsetLeft)<Math.abs(step)){
                        ele.style.left = target + "px";
                        clearInterval(ele.timer);
                    }
                },18);
            }
```



### 三个函数
都是在数轴上向上或者向下取整。
Math.ceil()    		向上取整
Math.floor()      	向下取整
Math.round();	   四舍五入
## 缓动动画原理


```
leader=leader+(target-leader)/10;
```


盒子位置 = 盒子本身位置+（目标位置-盒子本身位置）/ 10；
动画原理 = 盒子位置 + 步长（步长越来越小）。
体验缓动动画
 
分析为什么没有到达指定位置

|盒子本身位置|     目标位置|      步长 |        已经到达了的位置|
|:---:|:---:|:---:|:---:|
|0 						|400			|0						|0
|0						|400			|40						|40
|40						|400			|36						|76
|76						|400			|32.					|108.4
|.........|
|JS实际运算时会四舍五入取整，然后计算。|
|396(四舍五入获取)		|400	|		0.4			        |396.4|
|396(四舍五入获取)		|400	|		0.4			        |396.4|
|....
### offsetLeft和style.left的值的获取问题
获取盒子距离左侧具有定位的父盒子的距离（没有的body），四舍五入取整。
Style.left获取的是具体值。	（赋值的时候也是直接赋值）					
### 按例：筋斗云
鼠标悬停和鼠标移开不会影响初始化值，只有点击影响。而移开的情况下，span移动到计数器的位置。



```
<script>
        window.onload = function () {
            //需求1：鼠标放到哪个li上面，span对应移动到该li上。移开后，回到原位置。
            //需求2：鼠标点击那个li记录该li标签，移开的时候span回到该记录的li标签上。
            //步骤：
            //1.老三步
            //2.计数器


            //需求1：鼠标放到哪个li上面，span对应移动到该li上。移开后，回到原位置。
            //1.老三步
            var liArr = document.getElementsByTagName("li");
            var liWidth = liArr[0].offsetWidth;
            var span = document.getElementsByTagName("span")[0];
            //计数器
            var count = 0;


            //for循环绑定事件
            for(var i=0;i<liArr.length;i++){
                //自定义属性，然后绑定index属性为索引值
                liArr[i].index = i;
                //鼠标进入事件
                liArr[i].onmouseover = function () {
                    //让span运动到该li的索引值位置
                    //图片运动需要封装的方法
                    animate(span,this.index*liWidth);
                }
                //鼠标移开
                liArr[i].onmouseout = function () {
                    //让span运动到该li的索引值位置
                    //图片运动需要封装的方法
                    animate(span,count*liWidth);
                }
                //点击事件，记录功能
                liArr[i].onclick = function () {
                    //需要一个计数器，每次点击以后把所以只记录下来
                    //因为onmouseout事件要用到这个计数器，所以应该是一个全局变量
                    count = this.index;
                    animate(span,count*liWidth);
                }

            }

            //缓动动画封装
            function animate(ele,target) {
                clearInterval(ele.timer);
                ele.timer = setInterval(function () {
                    var step = (target-ele.offsetLeft)/10;
                    step = step>0?Math.ceil(step):Math.floor(step);
                    ele.style.left = ele.offsetLeft + step + "px";
                    console.log(1);
                    if(Math.abs(target-ele.offsetLeft)<Math.abs(step)){
                        ele.style.left = target + "px";
                        clearInterval(ele.timer);
                    }
                },18);
            }
        }
    </script>
```
## 事件对象（event）
再触发DOM上的某个事件时，会产生一个事件对象event，这个对象中包含着所有与事件有关的信息。所有浏览器都支持event对象，但支持的方式不同。
比如鼠标操作时候，会添加鼠标位置的相关信息到事件对象中。（类似Date）
普通浏览器支持 event（带参，任意参数）
ie 678 支持 window.event（无参，内置）
总结：他是一个事件中的内置对象。内部装了很多关于鼠标和事件本身的信息。

### 事件对象的获取（event的获取）
IE678中，window.event 
在火狐谷歌中，event或者，在事件绑定的函数中，加参，这个参数就是event.
  `Box.onclick = function (aaa){   aaa就是event     }`
### 兼容获取方式有两种：
不写参数直接使用event;
写参数，但是为`event....var event  = event || window.event;`(主要用这种)

## 冒泡
事件冒泡: 当一个元素上的事件被触发的时候，比如说鼠标点击了一个按钮，同样的事件将会在那个元素的所有祖先元素中被触发。这一过程被称为事件冒泡；这个事件从原始元素开始一直冒泡到DOM树的最上层。(BUG)
（本来应该一人做事一人当，结果，我做错了事情，你去告诉我妈）
什么是冒泡：子元素事件被触动，父盒子的同样的事件也会被触动。
取消冒泡就是取消这种机制。
### 阻止冒泡
w3c的方法是：（火狐、谷歌、IE11）
	event.stopPropagation()
IE10以下则是使用：event.cancelBubble = true
兼容代码如下：
  var event = event || window.event;
 if(event && event.stopPropagation){
            event.stopPropagation();
  }else{
            event.cancelBubble = true;
  }
### addEventListenner(参数1，参数2，参数3)
调用者是：事件源。			参数1：事件去掉on   参数2 ：调用的函数
参数3：可有可无。没有默认false.false情况下，支持冒泡。True支持捕获。

### 点击空白隐藏模态框
Document事件的绑定，无论绑定什么事件，只要事件被出发，传递过来的应该是指定的元素本身，而不是document。


```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        body,html {
            height: 100%;
            padding: 0;
            margin: 0;
        }
        .mask {
            width: 100%;
            height: 100%;
            position: fixed;
            top: 0;
            left: 0;
            display: none;
            background: rgba(0, 0, 0, 0.6);
        }
        .login {
            width: 400px;
            height: 300px;
            cursor: pointer;
            background-color: #fff;
            margin: 200px auto;
        }
    </style>
</head>
<body>
    <div class="mask">
        <div class="login" id="login"></div>
    </div>
    <a href="#">注册</a>
    <a href="#">登陆</a>
    <script src="jquery1.0.0.1.js"></script>
    <script>
        //需求：点击登录按钮，显示模态框。点击出去login以外的所有盒子隐藏模态框。
        //步骤：
        //1.给登录绑定事件
        //2.给document绑定事件，因为可以冒泡，只要判断，点击的不是login，那么隐藏模态框


        //1.给登录绑定事件
        var mask = document.getElementsByClassName("mask")[0];
        var a = document.getElementsByTagName("a")[1];

        a.onclick = function (event) {
            //显示模态框
            show(mask);

            //阻止冒泡
            event = event || window.event;
            if(event && event.stopPropagation){
                event.stopPropagation();
            }else{
                event.cancelBubble = true;
            }

        }

        //2.给document绑定事件，因为可以冒泡，只要判断，点击的不是login，那么隐藏模态框
        document.onclick = function (event) {
            //获取点击按钮后传递过来的值。
            event = event || window.event;

            //兼容获取事件触动时，被传递过来的对象
//            var aaa = event.target || event.srcElement;
            var aaa = event.target?event.target:event.srcElement;

            console.log(event.target);

            //判断目标值的ID是否等于login，如果等于不隐藏盒子，否则隐藏盒子。
            if(aaa.id !== "login"){
                mask.style.display = "none";
            }
        }


    </script>

</body>
</html>
```
## 事件委托

[**具体看我的CSDN博客有一篇关于这个的文章**
](https://blog.csdn.net/littleCucumber/article/details/100057756)


