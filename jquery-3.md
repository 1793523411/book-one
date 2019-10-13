## jQuery事件机制
jQuery的事件机制，指的是：jQuery对JavaScript操作DOM事件的封装，包括了：事件绑定、事件解绑、事件触发。
### jQuery事件的发展历程（了解）
简单事件绑定 >> bind事件绑定 >> delegate事件绑定 >> on【重点】

简单事件绑定：


```
click(handler) 				单击事件
blur(handler) 				失去焦点事件
mouseenter(handler) 		鼠标进入事件
mouseleave(handler)			鼠标离开事件
dbclick(handler) 			双击事件
change(handler) 改变事件，如：文本框值改变，下来列表值改变等
focus(handler) 				获得焦点事件
keydown(handler) 			键盘按下事件
```


[其他参考](http://www.w3school.com.cn/jquery/jquery_ref_events.asp)

bind方式（不推荐，1.7以后的jQuery版本被on取代）
作用：给匹配到的元素直接绑定事件


```
// 绑定单击事件处理程序
第一个参数：事件类型
第二个参数：事件处理程序
$("p").bind("click mouseenter", function(e){
    //事件响应方法
});
```


比简单事件绑定方式的优势：
1．	可以同时绑定多个事件，比如：bind(“mouseenter  mouseleave”, function(){})
缺点：要绑定事件的元素必须存在文档中。

3 delegate方式（特点：性能高，支持动态创建的元素）
作用：给匹配到的元素绑定事件，对支持动态创建的元素有效


```
// 第一个参数：selector，要绑定事件的元素
// 第二个参数：事件类型
// 第三个参数：事件处理函数
$(".parentBox").delegate("p", "click", function(){
    //为 .parentBox下面的所有的p标签绑定事件
});
```


与前两种方式最大的优势：减少事件绑定次数提高效率，支持动态创建出来的元素绑定事件！

### on方式（最现代的方式，兼容zepto(移动端类似jQuery的一个库)，强烈建议使用的方式）（重点）
jQuery1.7版本后，jQuery用on统一了所有的事件处理的方法
作用：给匹配的元素绑定事件，包括了上面所有绑定事件方式的优点
语法：


```
// 第一个参数：events，绑定事件的名称可以是由空格分隔的多个事件（标准事件或者自定义事件）
// 第二个参数：selector, 执行事件的后代元素
// 第三个参数：data，传递给处理函数的数据，事件触发的时候通过event.data来使用
// 第四个参数：handler，事件处理函数
$(selector).on(events[,selector][,data],handler);

	// 表示给$(selector)绑定事件，当必须是它的内部元素span才能执行这个事件
$(selector).on( "click",“span”, function() {});

// 绑定多个事件
// 表示给$(selector)匹配的元素绑定单击和鼠标进入事件
$(selector).on(“click mouseenter”, function(){});
```



### 事件解绑
unbind() 方式
作用：解绑 bind方式绑定的事件


```
$(selector).unbind(); //解绑所有的事件
$(selector).unbind(“click”); //解绑指定的事件
```


undelegate() 方式
作用：解绑delegate方式绑定的事件


```
$( selector ).undelegate(); //解绑所有的delegate事件
$( selector).undelegate( “click” ); //解绑所有的click事件

off解绑on方式绑定的事件（重点）
// 解绑匹配元素的所有事件
$(selector).off();
// 解绑匹配元素的所有click事件
$(selector).off(“click”);
// 解绑所有代理的click事件，元素本身的事件不会被解绑 
$(selector).off( “click”, “**” ); 
```



### 事件触发
简单事件触发


```
$(selector).click(); //触发 click事件
```


trigger方法触发事件，触发浏览器行为


```
$(selector).trigger(“click”);
```


triggerHandler触发 事件响应方法，不触发浏览器行为
比如:文本框获得焦点的默认行为


```
$(selector).triggerHandler(“focus”);
```



### jQuery事件对象介绍


```
event.data 					传递给事件处理程序的额外数据
event.currentTarget 			等同于this，当前DOM对象
event.pageX 					鼠标相对于文档左部边缘的位置
event.target 					触发事件源，不一定===this
event.stopPropagation()；	阻止事件冒泡
event.preventDefault(); 	阻止默认行为
event.type 					事件类型：click，dbclick…
event.which 					鼠标的按键类型：左1 中2 右3
event.keyCode				键盘按键代码
案例：按键变色
```


## jQuery补充
### 链式编程
链式编程原理：return this;
通常情况下，只有设置操作才能把链式编程延续下去。因为获取操作的时候，会返回获取到的相应的值，无法返回 this。



```
end(); // 结束当前链最近的一次过滤操作，并且返回匹配元素之前的状态。
```


### 隐式迭代
隐式迭代的意思是：在方法的内部会为匹配到的所有元素进行循环遍历，执行相应的方法；而不用我们再进行循环，简化我们的操作，方便我们调用。
如果获取的是多元素的值，大部分情况下返回的是第一个元素的值。

### each方法
有了隐式迭代，为什么还要使用each函数遍历？
大部分情况下是不需要使用each方法的，因为jQuery的隐式迭代特性。
如果要对每个元素做不同的处理，这时候就用到了each方法

作用：遍历jQuery对象集合，为每个匹配的元素执行一个函数


```
// 参数一表示当前元素在所有匹配元素中的索引号
// 参数二表示当前元素（DOM对象）
$(selector).each(function(index,element){});
Element是一个 js对象，需要转换成jquery对象
```





### 多库共存
此处多库共存指的是：jQuery占用了$ 和jQuery这两个变量。当在同一个页面中引用了jQuery这个js库，并且引用的其他库（或者其他版本的jQuery库）中也用到了$或者jQuery这两个变量，那么，要保证每个库都能正常使用，这时候就有了多库共存的问题。



```
jQuery(function () {
            //打印版本号。
//            console.log($.fn.jquery);

            //让1.11.1放弃$的使用权
            $.noConflict();
            console.log($.fn.jquery);
            console.log(jQuery.fn.jquery);

            //放弃两个符号的使用权，同时定义一个新的使用权
//            var MrLv = $.noConflict(true);
//            console.log($.fn.jquery);
//            console.log(jQuery.fn.jquery);
//            console.log(MrLv.fn.jquery);
        })
```



```
// 模拟另外的库使用了 $ 这个变量
// 此时，就与jQuery库产生了冲突
var $ = { name : “ygj” };

解决方式：
// 作用：让jQuery释放对$的控制权，让其他库能够使用$符号，达到多库共存的目的。此后，只能使用jQuery来调用jQuery提供的方法
$.noConflict();  //true两个都交出来，返回值是新的调用方法
```


 

## jQuery插件机制
jQuery这个js库，虽然功能强大，但也不是面面俱到包含所有的功能。
jQuery是通过插件的方式，来扩展它的功能：
当你需要某个插件的时候，你可以“安装”到jQuery上面，然后，使用。
当你不再需要这个插件，那你就可以从jQuery上“卸载”它。
（联想：手机软件，安装的app就好比插件，用的时候安装上，不用的时候卸载掉）
### 第三方插件
jQuery.color.js
animate()自定义动画：不支持背景的动画效果
animate动画支持的属性列表
jQuery.lazyload.js
使用步骤：
1.	引入jQuery文件
2.	引入插件
3.	使用插件
1.7.2	制作插件

[如何创建jQuery插件](http://learn.jquery.com/plugins/basic-plugin-creation/)

全局jQuery函数扩展方法


```
$.pluginName = function() {};
```



jQuery对象扩展方法


```
$.fn. pluginName = function() {};

```



### jQueryUI
jQueryUI专指由jQuery官方维护的UI方向的插件。
[官方API](http://api.jqueryui.com/category/all/)
其他教程：jQueryUI教程
基本使用:
1.引入jQueryUI的样式文件
2.引入jQuery
3.引入jQueryUI的js文件
4.使用jQueryUI功能
