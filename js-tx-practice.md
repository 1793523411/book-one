[点](https://github.com/1793523411/TencentWeb)
## 轮播图
### 滑动焦点图


```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        .box {
            width: 490px;
            height: 170px;
            padding: 5px;
            border: 1px solid #ccc;
            margin: 100px auto;
        }
        .inner {
            width: 490px;
            height: 170px;
            position: relative;
            overflow: hidden;
        }
        ul {
            width: 500%;
            list-style: none;
            position: absolute;
            left: 0;
        }
        li {
            float: left;
        }
        .square {
            position: absolute;
            bottom: 10px;
            right: 10px;
        }
        span {
            display: inline-block;
            width: 16px;
            height: 16px;
            background-color: #fff;
            text-align: center;
            margin: 3px;
            border: 1px solid #ccc;
            line-height: 16px;
            cursor: pointer;
         }
         .current {
             background-color: #000;
             color: #fff;
         }

    </style>
    <script>
        window.onload =function (){
            var inner = document.getElementById("inner");
            var imgWidth = inner.offsetWidth;
            var ul = inner.children[0];
            var spanArr = inner.children[1].children;
            for(var i =0;i<spanArr.length;i++){
                spanArr[i].index = i;
                spanArr[i].onmouseover = function(){
                    for(var j=0;j<spanArr.length;j++){
                        spanArr[j].className = "";
                    }
                    this.className = "current";
                    animate(ul,-this.index*imgWidth)
                }
            }
            function animate(ele,target) {
                clearInterval(ele.timer);
                var speed = target>ele.offsetLeft?10:-10;
                ele.timer = setInterval(function(){
                    var val = target - ele.offsetLeft;
                    ele.style.left = ele.offsetLeft + speed +"px";
                    if(Math.abs(val)<Math.abs(speed)){
                        ele.style.left = target + "px";
                        clearInterval(ele.timer);
                    }                
                 },10)
            }

        }
    </script>
</head>
<body>
    <div class="box">
<div class="inner" id="inner">
    <ul>
        <li><img src="images/01.jpg" alt=""></li>
        <li><img src="images/02.jpg" alt=""></li>
        <li><img src="images/03.jpg" alt=""></li>
        <li><img src="images/04.jpg" alt=""></li>
        <li><img src="images/05.jpg" alt=""></li>
    </ul>

<div class="square">
    <span class=current>1</span>
    <span>2</span>
    <span>3</span>
    <span>4</span>
    <span>5</span>
</div>
</div>

    </div>
</body>
</html>
```


### 带定时器的滑动轮播图


```
<!doctype html>
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
	<title>无标题文档</title>
	<style type="text/css">
		body,ul,ol,li,img{margin:0;padding:0;list-style:none;}
		#box{width:490px;height:170px;padding:5px;
			position: relative;border:1px solid #ccc;margin:100px auto 0;overflow:hidden;}
		.ad{width:490px;height:170px;overflow:hidden;position:relative;}
		#box img{width:490px;}
		.ad ol{position:absolute;right:10px;bottom:10px;}
		.ad ol li{width:20px;height:20px;line-height:20px;border:1px solid #ccc;text-align:center;background:#fff;float:left;margin-right:10px;cursor:pointer;_display:inline;}
		.ad ol li.current{background:yellow;}
		.ad ul li{float:left;}
		.ad ul{ position:absolute; top:0; width:2940px;}
		.ad ul li.current{display:block;}
		#arr {display: none;}
		#arr span{ width:40px; height:40px; position:absolute; left:5px; top:50%; margin-top:-20px; background:#000; cursor:pointer; line-height:40px; text-align:center; font-weight:bold; font-family:'黑体'; font-size:30px; color:#fff; opacity:0.3; border:1px solid #fff;}
		#arr #right{right:5px; left:auto;}
	</style>
</head>
<body>
<div id="box" class="all">
	<div class="ad">
		<ul id="imgs">
			<li><img src="images/1.jpg" /></li>
			<li><img src="images/2.jpg" /></li>
			<li><img src="images/3.jpg" /></li>
			<li><img src="images/4.jpg" /></li>
			<li><img src="images/5.jpg" /></li>
		</ul>
	</div>
	<div id="arr">
		<span id="left"><</span>
		<span id="right">></span>
	</div>
</div>


<script>
	//需求：鼠标放到盒子上，显示左右切换的图片。点击左则按钮图片(ul)向右移动，相反的按钮向左移动。
	//思路：获取两个按钮，点击左侧按钮移动ul向右走(每次只走一张)(计数器从0开始)。
	//如何移动盒子。利用计数器模拟index值，点右侧自增，点左侧自减。
	//步骤：
	//1.鼠标放上去显示移开以藏
	//2.点击右侧盒子图片向做移动并用计数器模拟index值。
	//3，点击左侧盒子，同理。

	//1.鼠标放上去显示移开以藏
	var box = document.getElementById("box");
	var imgWidth = box.children[0].offsetWidth;
	var ul = box.children[0].children[0];
	var boxLeftRight = box.children[1];
	var btnArr = boxLeftRight.children;

	//鼠标放上去显示，移开隐藏
	box.onmouseover = function () {
		boxLeftRight.style.display = "block";
	}
	box.onmouseout = function () {
		boxLeftRight.style.display = "none";
	}

	//2.点击右侧盒子图片向做移动并用计数器模拟index值。
	//定义计数器
	var index = 0;

	btnArr[1].onclick = function () {
		index++;
		//我们要对index的值进行约束。index的值必须在[0,4]
		if(index>ul.children.length-1){
			index = ul.children.length-1;
			alert("到头了！");
		}
		//点击盒子以后移动图片（ul，和目标位置）
		animate(ul,-index*imgWidth);
	}

	//3，点击左侧盒子，同理。
	btnArr[0].onclick = function () {
		index--;
		if(index<0){
			index = 0;
			alert("第一张！");
		}
		//点击盒子以后移动图片（ul，和目标位置）
		animate(ul,-index*imgWidth);
	}


	function animate(ele,target){
		clearInterval(ele.timer);
		var speed = target>ele.offsetLeft?10:-10;
		ele.timer = setInterval(function () {
			var val = target - ele.offsetLeft;
			ele.style.left = ele.offsetLeft + speed + "px";
			if(Math.abs(val)<Math.abs(speed)){
				ele.style.left = target + "px";
				clearInterval(ele.timer);
			}
		},10)
	}
</script>

</body>
</html>


```


### 带定时器的无缝轮播图


```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style type="text/css">
        *{ padding:0; margin:0; list-style:none; border:0;}
        .all{
            width:500px;
            height:200px;
            padding:7px;
            border:1px solid #ccc;
            margin:100px auto;
            position:relative;
        }
        .screen{
            width:500px;
            height:200px;
            overflow:hidden;
            position:relative;
        }
        .screen li{ width:500px; height:200px; overflow:hidden; float:left;}
        .screen ul{ position:absolute; left:0; top:0px; width:3000px;}
        .all ol{ position:absolute; right:10px; bottom:10px; line-height:20px; text-align:center;}
        .all ol li{ float:left; width:20px; height:20px; background:#fff; border:1px solid #ccc; margin-left:10px; cursor:pointer;}
        .all ol li.current{ background:yellow;}

        #arr {display: none;}
        #arr span{ width:40px; height:40px; position:absolute; left:5px; top:50%; margin-top:-20px; background:#000; cursor:pointer; line-height:40px; text-align:center; font-weight:bold; font-family:'黑体'; font-size:30px; color:#fff; opacity:0.3; border:1px solid #fff;}
        #arr #right{right:5px; left:auto;}
    </style>
    <script>
        window.onload = function() {
            var all = document.getElementById("all");
            var screen = all.firstElementChild || all.firstChild;
            var imgWidth = screen.offsetWidth;
            var ul = screen.firstElementChild || screen.firstChild;
            var ol = screen.children[1];
            var div = screen.lastElementChild || screen.lastChild;
            var spanArr = div.children;

            var ulNewLi = ul.children[0].cloneNode(true);
            ul.appendChild(ulNewLi);
            for (var i = 0; i < ul.children.length - 1; i++) {
                var olNewLi = document.createElement("li");
                olNewLi.innerHTML = i + 1;
                ol.appendChild(olNewLi)
            }
            var olLiArr = ol.children;
            olLiArr[0].className = "current";
            for (var i = 0; i < olLiArr.length; i++) {
                olLiArr[i].index = i;
                olLiArr[i].onmouseover = function () {
                    for (var j = 0; j < olLiArr.length; j++) {
                        olLiArr[j].className = "";
                    }
                    this.className = "current";
                    key = square = this.index;
                    animate(ul, -this.index * imgWidth);
                }
            }
            var timer = setInterval(autoPlay, 1000);

            var key = 0;
            var square = 0;

            function autoPlay() {
                key++;
                if (key > olLiArr.length) {
                    ul.style.left = 0;
                    key = 1;
                }
                animate(ul, -key * imgWidth);
                square++;
                if (square > olLiArr.length - 1) {
                    square = 0;
                }
                for (var i = 0; i < olLiArr.length; i++) {
                    olLiArr[i].className = "";
                }
                olLiArr[square].className = "current";
            }

            all.onmouseover = function () {
                div.style.display = "black";
                clearInterval(timer);
            }
            all.onmouseout = function () {
                div.style.display = "none";
                timer = setInterval(autoPlay, 1000);
            }
            spanArr[0].onclick = function () {
                key--;
                if (key < 0) {
                    ul.style.left = -imgWidth * (olLiArr.length) + "px";
                    key = olLiArr.length - 1;
                }
                animate(ul, -key*imgWidth);
                square--;
                if (square < 0) {
                    square = olLiArr.length-1;
                }
                for (var i = 0; i < olLiArr.length; i++) {
                    olLiArr[i].className = "";
                }
                olLiArr[square].className = "current";
        }
            spanArr[1].onclick = function(){
            autoPlay();
        }


        function animate(ele,target){
            clearInterval(ele.timer);
            var speed = target>ele.offsetLeft?10:-10;
            ele.timer = setInterval(function () {
                var val = target - ele.offsetLeft;
                ele.style.left = ele.offsetLeft + speed + "px";
                if(Math.abs(val)<Math.abs(speed)){
                    ele.style.left = target + "px";
                    clearInterval(ele.timer);
                }
            },10)
        }
 }

    </script>
</head>
<body>
    <div class="all" id='all'>
        <div class="screen" id="screen">
            <ul id="ul">
                <li><img src="images/1.jpg" width="500" height="200" /></li>
                <li><img src="images/2.jpg" width="500" height="200" /></li>
                <li><img src="images/3.jpg" width="500" height="200" /></li>
                <li><img src="images/4.jpg" width="500" height="200" /></li>
                <li><img src="images/5.jpg" width="500" height="200" /></li>
            </ul>
            <ol>
    
            </ol>
            <div id="arr">
                <span id="left"><</span>
                <span id="right">></span>
        </div>
    </div>
</body>
</html>
```


### 旋转木马
* 旋转木马
原理：我们先定义一个数组，数组中的元素是json；json中的元素是属性。
点击一个按钮，按顺序更换数组中元素的位置。
（如果我们想完成旋转木马，只需要更换数组中元素的位置）
步骤：
1.我们必须让页面加载的时候把所有的属性加载出来，让我看看。（核心）
2.鼠标放到大盒子上显示对应的左右切换按钮，移开隐藏
3.获取两个按钮。对他们进行事件绑定。对他们进行判断。
4.如果是左侧的按钮执行一套程序，如果是右侧的按钮执行另一套程序。
5.绑定按钮的函数，一个是正转，一个是反转。（传参确定）
6.调换相应的数组对应的元素。（先删除谁，在怎么添加）
* 正转反转的问题
最开始是：12345；我想让他变成：23451
把1删除，在最后添加1；
在数组json中，删除第一个元素，添加到最末尾。（正转）
在数组json中，删除最后一个元素，添加到第一位。（反转）
* 函数节流
定义一个变量，只有函数执行完毕在去执行下一个。



```
@charset "UTF-8";
/*初始化  reset*/
blockquote,body,button,dd,dl,dt,fieldset,form,h1,h2,h3,h4,h5,h6,hr,input,legend,li,ol,p,pre,td,textarea,th,ul{margin:0;padding:0}
body,button,input,select,textarea{font:12px/1.5 "Microsoft YaHei", "微软雅黑", SimSun, "宋体", sans-serif;color: #666;}
ol,ul{list-style:none}
a{text-decoration:none}
fieldset,img{border:0;vertical-align:top;}
a,input,button,select,textarea{outline:none;}
a,button{cursor:pointer;}

.wrap{
    width:1200px;
    margin:10px auto;
}
.slide {
    height:500px;
    position: relative;
}
.slide li{
    position: absolute;
    left:200px;
    top:0;
}
.slide li img{
    width:100%;
}
.arrow{
    opacity: 0;
}
.prev,.next{
    width:76px;
    height:112px;
    position: absolute;
    top:50%;
    margin-top:-56px;
    background: url(../images/prev.png) no-repeat;
    z-index: 99;
}
.next{
    right:0;
    background-image: url(../images/next.png);
}


```



```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>旋转木马轮播图</title>
    <link rel="stylesheet" href="css/css.css"/>
    <script src="js/jquery1.0.0.1.js"></script>
    <script src="js/js.js"></script>
</head>
<body>

    <div class="wrap" id="wrap">
       <div class="slide" id="slide">
           <ul>
               <!--五张图片-->
               <li><a href="#"><img src="images/slidepic1.jpg" alt=""/></a></li>
               <li><a href="#"><img src="images/slidepic2.jpg" alt=""/></a></li>
               <li><a href="#"><img src="images/slidepic3.jpg" alt=""/></a></li>
               <li><a href="#"><img src="images/slidepic4.jpg" alt=""/></a></li>
               <li><a href="#"><img src="images/slidepic5.jpg" alt=""/></a></li>
           </ul>
           <!--左右切换按钮-->
           <div class="arrow" id="arrow">
               <a href="javascript:;" class="prev"></a>
               <a href="javascript:;" class="next"></a>
           </div>
       </div>
    </div>


</body>
</html>
```



```
/**
 * Created by Lenovo on 2016/9/13.
 */
window.onload = function () {
    //需求：点击足有按钮实现旋转木马。
        //原理：点击右侧按钮，让3号盒子的样式赋值给2号盒子，然后2->1,1->5,5->4,4->3。。。
        //左侧同理。
    //步骤：
    //1.鼠标放到轮播图上，两侧的按钮显示，移开隐藏。
    //2.让页面加载出所有的盒子的样式。
    //3.把两侧按钮绑定事件。(调用同一个方法，只有一个参数，true为正向旋转，false为反向旋转)
    //4.书写函数。
        // (操作数组。正向旋转：删除数组中第一个样式，添加到数组中的最后一位)
        // (操作数组。反向旋转：删除数组中最后一个样式，添加到数组中的第一位)


    var json = [
        {   //  1
            width:400,
            top:70,
            left:50,
            opacity:20,
            z:2
        },
        {  // 2
            width:600,
            top:120,
            left:0,
            opacity:80,
            z:3
        },
        {   // 3
            width:800,
            top:100,
            left:200,
            opacity:100,
            z:4
        },
        {  // 4
            width:600,
            top:120,
            left:600,
            opacity:80,
            z:3
        },
        {   //5
            width:400,
            top:70,
            left:750,
            opacity:20,
            z:2
        }
    ];

    //0.获取元素
    var slide = document.getElementById("slide");
    var liArr = slide.getElementsByTagName("li");
    var arrow = slide.children[1];
    var arrowChildren = arrow.children;
    //设置一个开闭原则变量，点击以后修改这个值。
    var flag = true;



    //1.鼠标放到轮播图上，两侧的按钮显示，移开隐藏。
    slide.onmouseenter = function () {
        //arrow.style.opacity = 1;
        animate(arrow,{"opacity":100});
    }
    slide.onmouseleave = function () {
        //arrow.style.opacity = 1;
        animate(arrow,{"opacity":0});
    }

    //2.让页面加载出所有的盒子的样式。
    //for(var i=0;i<liArr.length;i++){
    //    //利用animate()框架让指定的属性，缓慢运动到指定位置。
    //    animate(liArr[i],{
    //        "width":json[i].width,  //第一个li，必须对应第一个数组元素中的第一个的指定属性
    //        "top":json[i].top,
    //        "left":json[i].left,
    //        "opacity":json[i].opacity,
    //        "zIndex":json[i].z
    //    });
    //    //liArr[i].style.width = json[i].width+"px";
    //    //liArr[i].style.top = json[i].top+"px";
    //    //liArr[i].style.left = json[i].left+"px";
    //    //liArr[i].style.opacity = json[i].opacity/100;
    //    //liArr[i].style.zIndex = json[i].z;
    //}


    move();
    //3.把两侧按钮绑定事件。(调用同一个方法，只有一个参数，true为正向旋转，false为反向旋转)
    //arrowChildren[0].
    //arrowChildren[1].
    //利用for...in...绑定事件。绑定后利用元素的className属性知道是前一个还是后一个，然后调用函数。
    for(var k in arrowChildren){
        arrowChildren[k].onclick = function () {
            if(this.className === "prev"){
                if(flag === true){
                    flag = false;
                    move(true);
                    //点击一次立刻修改为false，这样儿别人就不能在点击。（点击也不执行move()）
                }
            }else{
                if(flag){
                    flag = false;
                    move(false);
                }
            }
        }
    }

    //4.书写函数。
    // (操作数组。正向旋转：删除数组中第一个样式，添加到数组中的最后一位)
    // (操作数组。反向旋转：删除数组中最后一个样式，添加到数组中的第一位)
    function move(bool){
        //判断：如果等于undefined,那么就不执行这两个if语句
        //if(bool === true || bool === false){
        if(bool !== undefined){
            if(bool){
                // (操作数组。反向旋转：删除数组中最后一个元素，添加到数组中的第一位)
                //json.push();//在最后添加
                //json.pop();//删除最后一位
                //json.unshift();//在最前面添加
                //json.shift();//删除第一位

                //var ele = json.pop();
                //json.unshift(ele);
                json.unshift(json.pop());
            }else{
                // (操作数组。正向旋转：删除数组中第一个元素，添加到数组中的最后一位)
                //var ele = json.shift();
                //json.push(ele);
                json.push(json.shift());
            }
        }
        //在次为页面上的所有li赋值属性，利用缓动框架
        for(var i=0;i<liArr.length;i++){
            //利用animate()框架让指定的属性，缓慢运动到指定位置。
            animate(liArr[i],{
                "width":json[i].width,  //第一个li，必须对应第一个数组元素中的第一个的指定属性
                "top":json[i].top,
                "left":json[i].left,
                "opacity":json[i].opacity,
                "zIndex":json[i].z
            }, function () {
                //回调函数，所有程序执行完毕，在初始化flag的值为true
                flag = true;
            });
        }
    }

}
```



```

```



```
/**
 * Created by Lenovo on 2016/9/11.
 */
function show(ele){
    ele.style.display = "block";
}

/**
 * 获取元素样式兼容写法
 * @param ele
 * @param attr
 * @returns {*}
 */
function getStyle(ele,attr){
    if(window.getComputedStyle){
        return window.getComputedStyle(ele,null)[attr];
    }
    return ele.currentStyle[attr];
}

//参数变为3个
//参数变为3个
function animate(ele,json,fn){
    //先清定时器
    clearInterval(ele.timer);
    ele.timer = setInterval(function () {
        //开闭原则
        var bool = true;


        //遍历属性和值，分别单独处理json
        //attr == k(键)    target == json[k](值)
        for(var k in json){
            //四部
            var leader;
            //判断如果属性为opacity的时候特殊获取值
            if(k === "opacity"){
                leader = getStyle(ele,k)*100 || 1;
            }else{
                leader = parseInt(getStyle(ele,k)) || 0;
            }

            //1.获取步长
            var step = (json[k] - leader)/10;
            //2.二次加工步长
            step = step>0?Math.ceil(step):Math.floor(step);
            leader = leader + step;
            //3.赋值
            //特殊情况特殊赋值
            if(k === "opacity"){
                ele.style[k] = leader/100;
                //兼容IE678
                ele.style.filter = "alpha(opacity="+leader+")";
                //如果是层级，一次行赋值成功，不需要缓动赋值
                //为什么？需求！
            }else if(k === "zIndex"){
                ele.style.zIndex = json[k];
            }else{
                ele.style[k] = leader + "px";
            }
            //4.清除定时器
            //判断: 目标值和当前值的差大于步长，就不能跳出循环
            //不考虑小数的情况：目标位置和当前位置不相等，就不能清除清除定时器。
            if(json[k] !== leader){
                bool = false;
            }
        }

        console.log(1);
        //只有所有的属性都到了指定位置，bool值才不会变成false；
        if(bool){
            clearInterval(ele.timer);
            //所有程序执行完毕了，现在可以执行回调函数了
            //只有传递了回调函数，才能执行
            if(fn){
                fn();
            }
        }
    },25);
}



//获取屏幕可视区域的宽高
function client(){
    if(window.innerHeight !== undefined){
        return {
            "width": window.innerWidth,
            "height": window.innerHeight
        }
    }else if(document.compatMode === "CSS1Compat"){
        return {
            "width": document.documentElement.clientWidth,
            "height": document.documentElement.clientHeight
        }
    }else{
        return {
            "width": document.body.clientWidth,
            "height": document.body.clientHeight
        }
    }
}
```



### 渐隐渐现轮播图


```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <style type="text/css">
        *{
            margin:0;
            padding:0;
            list-style: none;
        }
        #box{
            position:relative;
            width:400px;
            height:300px;
        }
        img{
            position:absolute;
            width:400px;
            height:300px;
        }
        #imgId1{
            opacity:1;
        }
        #imgId2{
            opacity:0;
        }
        #imgId3{
            opacity:0;
        }
        #imgId4{
            opacity:0;
        }
        #imgId5{
            opacity:0;
        }
        ul{
            position:absolute;
            right:20px;
            bottom:10px;
            height:40px;
        }
        li{
            float:left;
            margin-left:10px;
            width:20px;
            height:20px;
            border-radius:50%;
            background-color:orange;
        }
        #leftArrow{
            position: absolute;
            left:0px;
            top:50%;
        }
        #rightArrow{
            position: absolute;
            right:0px;
            top:50%;
        }
    </style>
</head>
<body style="height:1000px;">
<div id="box">
    <img src="images/1.jpg" id="imgId1">
    <img src="images/2.jpg" id="imgId2">
    <img src="images/3.jpg" id="imgId3">
    <img src="images/4.jpg" id="imgId4">
    <img src="images/5.jpg" id="imgId5">
    <ul id="btns">
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
    <div id="leftArrow" style="font-size: 50px">＜</div>
    <div id="rightArrow" style="font-size: 50px">＞</div>
</div>

</body>
</html>

<script type="text/javascript" src="jquery-1.11.1.min.js"></script>
<script type="text/javascript">

    var arr=["timg1.jpg","timg2.jpg","timg3.jpg","timg4.jpg","timg5.jpg"];
    var ord = 0;//代表当前图片的序号，从0开始。
    var myTimer = null;

    function  initUI() {
        $("#box li:first").css({"backgroundColor":"red"});
    }

    function  initEvent() {
        $("#box").mouseenter(function () {
            stopPlay();
        });

        $("#box").mouseleave(function () {
            autoPlay();
        });

        $("#box li").click(function () {
            goImg($("#box li").index(this));
        });

        $("#leftArrow").click(function () {
            let transord =ord-1;
            transord = transord<0?arr.length-1:transord;
            goImg(transord);
        });

        $("#rightArrow").click(function () {
            let transord =ord+1;
            transord = transord>arr.length-1?0:transord;
            goImg(transord);
        });
    }

    //1、自动播放
    function autoPlay() {
        myTimer = setInterval(function () {
            //一、改变数据
            // 1、记录当前序号（淡出的图片序号）
            let outOrd = ord;
            //2、改变要显示的图片的序号（淡出图片序号加一）
            ord++;
            if(ord>arr.length-1){
                ord=0;
            }
            //二、改变外观
            let $img = $("#box img");
            //1、淡入淡出效果
            //让一张(outOrd)淡出 当前消失
            $img.eq(outOrd).animate({"opacity":0},2000);
            //让一张(ord)淡入下一张图片显示
            $img.eq(ord).animate({"opacity":1},2000);
            //2、改变豆豆的颜色；
            $("#box li").eq(ord).css({"backgroundColor":"red"}).siblings().css({"backgroundColor":"orange"});
        },3000);
    }

    //2、停止播放
    function stopPlay() {
        window.clearInterval(myTimer);
    }

    //3、跳转到指定的图片
    function  goImg(transOrd) {
        //一、改变数据
        // 1、记录当前序号（淡出的图片序号）
        let outOrd = ord;
        //2、改变要显示的图片的序号（传入的图片序号）
        ord=transOrd;
        if(ord>arr.length-1){
            ord=0;
        }
        //二、改变外观
        let $img = $("#box img");
        //1、淡入淡出效果
        //让一张(outOrd)淡出 当前消失
        $img.eq(outOrd).animate({"opacity":0},2000);
        //让一张(ord)淡入下一张图片显示
        $img.eq(ord).animate({"opacity":1},2000);
        //2、改变豆豆的颜色；
        $("#box li").eq(ord).css({"backgroundColor":"red"}).siblings().css({"backgroundColor":"orange"});
    }

    $(function () {
        //1、初始化界面
        initUI();
        //2、绑定事件
        initEvent();
        //3、自动播放
        autoPlay();
    });

</script>
```
### 3D切割轮播图


```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        *{
            margin: 0;
            padding: 0;
            list-style: none;
        }

        .view{
            width: 560px;
            height: 300px;
            border: 1px solid #000;
            margin:100px auto;
            position: relative;
        }

        .view ul li{
            width: 112px;
            height:300px;
            float: left;
            position: relative;

            /* 让里面的子盒子保持3d 效果*/

            transform-style:preserve-3d;
            transition:all 1s;

            transform:rotateX(-45deg) rotateY(-27deg);
        }

        .view li span{
            position: absolute;
            width: 100%;
            height: 100%;
        }

        .view li span:nth-child(1){
            transform:translateZ(150px);
            background-image: url(images/1.jpg);

        }

        .view li span:nth-child(2){
            transform:rotateX(90deg) translateZ(150px);


            background-image: url(images/2.jpg);
        }

        .view li span:nth-child(3){
            transform:rotateX(180deg) translateZ(150px);
            background-image: url(images/3.jpg);
        }

        .view li span:nth-child(4){
            transform:rotateX(-90deg) translateZ(150px);
            background-image: url(images/4.jpg);
        }

        .view li:nth-child(1) span{

        }

        .view li:nth-child(2) span{
            background-position: -112px 0;
        }
        .view li:nth-child(3) span{
            background-position: -224px 0;
        }
        .view li:nth-child(4) span{
            background-position: -336px 0;
        }
        .view li:nth-child(5) span{
            background-position: -448px 0;
        }


        /*左右按钮*/

        .view .prev,.view .next{
            position: absolute;
            width: 80px;
            height: 80px;
            background-color: rgba(255,255,255,0.5);
            text-align: center;
            line-height: 80px;
            font-size:50px;
            color:red;
            left:0;
            top:50%;
            /*margin-top:-40px;*/
            transform:translateY(-50%);
            text-decoration: none;
        }

        .view .next{
            left:auto;
            right:0;
        }

    </style>
</head>
<body>
<div class="view">
    <ul>
        <li>
            <span>1</span>
            <span>2</span>
            <span>3</span>
            <span>4</span>
        </li>
        <li>
            <span>1</span>
            <span>2</span>
            <span>3</span>
            <span>4</span>
        </li>
        <li>
            <span>1</span>
            <span>2</span>
            <span>3</span>
            <span>4</span>
        </li>
        <li>
            <span>1</span>
            <span>2</span>
            <span>3</span>
            <span>4</span>
        </li>
        <li>
            <span>1</span>
            <span>2</span>
            <span>3</span>
            <span>4</span>
        </li>
    </ul>
    <a href="javascript:;" class="prev">&lt;</a>
    <a href="javascript:;" class="next">&gt;</a>
</div>
<script src="js/jquery.min.js"></script>
<script>
$(function(){
    //    基本思路
    //    定义变量 记录当前播放的index
           var index=0;

        var isTransitionEnd=true;

    //    当左箭头被点击是
        $('.prev').click(function(){

            if(isTransitionEnd){
                index++;
                //选择 90deg
                var r=90*index;
                isTransitionEnd=false;
                $('li').css('transform','rotateX('+r+'deg)');

                $('li').each(function(index,item){
//                 设置动画的延迟间隔0.25秒
                    $(item).css('transition-delay',index*0.25+'s');
                });
            }
        });
// 下一张
    $('.next').click(function(){
//        如果上次过渡结束 ，执行下一次
        if(isTransitionEnd){
            //        索引值减小
            index--;
            //       选择 90deg
            var r=90*index;
            isTransitionEnd=false;

            $('li').css('transform','rotateX('+r+'deg)');

            $('li').each(function(index,item){
//                 设置动画的延迟间隔0.25秒
                $(item).css('transition-delay',index*0.25+'s');
            });

        }

    });
//    只有最会一个li过渡结束才算 轮播图过渡结束
    $('li').eq(4).on('webkitTransitionEnd',function(){
        isTransitionEnd=true;
    })

})

</script>
</body>
</html>
```


