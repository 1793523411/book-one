# jQuery操作DOM
## 为什么要使用jQuery操作DOM
对比JS操作DOM和jQuery操作DOM


```
//原生js
//        window.onload = function () {
//            var btn = document.getElementsByTagName("button")[0];
//            var divArr = document.getElementsByTagName("div");
//
//            btn.onclick = function () {
//                for(var i=0;i<divArr.length;i++){
//                    divArr[i].style.display = "block";
//                    divArr[i].innerHTML = "明日中秋！";
//                }
//            }
//        }

        //jquery版
        $(document).ready(function () {
            //获取元素
            var jQbtn = $("button");//根据标签名获取元素
            var jQdiv = $("div");//根据标签名获取元素
            //绑定事件
            jQbtn.click(function () {
                //事件驱动程序
//                jQdiv.show(1000);//显示盒子。
//                jQdiv.html("tomorrow中秋！");//设置内容
                jQdiv.show(1000).html(1111);
                //1.链式编程。  2.隐式迭代。

            });//事件绑定是通过方法绑定的。


        });
```



使用jQuery的方式来操作DOM更加的简介，方便，统一的调用方式方便我们学习，降低来我们的学习成本。
## 重点内容
样式和类操作
jQuery动画
节点操作

### 样式操作 
#### 样式属性操作  .css()
作用：设置或获取元素的样式属性值
1 设置样式属性操作：
a设置单个样式：


```
// 第一个参数表示：样式属性名称
// 第二个参数表示：样式属性值
$(selector).css(“color”, “red”);
```


b设置多个样式：（也可以设置单个）


```
// 参数为 {}（对象）
$(selector).css({“color”: “red”, “font-size”: “30px”});
```



2获取样式属性操作：


```
// 参数表示要获取的 样式属性名称
$(selector).css(“font-size”);
```


此时，会返回”font-size”样式属性对应的值。
### 类操作
添加类样式：


```
(addClass) 为指定元素添加类className
$(selector).addClass(“liItem”);
```


注意：此处类名不带点，所有类操作的方法类名都不带点
移除类样式：
`removeClass(className)` 为指定元素移除类 className


```
$(selector).removeClass(“liItem”);
```


`$(selector).removeClass();` 不指定参数，表示移除被选中元素的所有类

判断有没有类样式：
`hasClass(calssName)` 判断指定元素是否包含类 className


```
$(selector).hasClass(“liItem”);
```


此时，会返回true或false

切换类样式：


```
toggleClass(className) 为指定元素切换类 className，该元素有类则移除，没有指定类则添加。
$(selector).toggleClass(“liItem”);
```



注意点：
操作类样式的时候，所有的类名，都不带点（.）
经验：
1 操作的样式非常少，那么可以通过.css()这个 方法来操作
2 操作的样式很多，那么要通过使用类的方式来操作
3 如果考虑以后维护方便（把CSS从js中分离出来）的话，推荐使用类的方式来操作。类比CSS书写位置（把css从html中分离出来）

前面内容特色总结：简约、“粗暴”、干净利落、直截了当


## Query动画是什么？
jQuery提供的一组网页中常见的动画效果，这些动画是标准的、有规律的效果；同时还提供给我们了自定义动画的功能。
### 隐藏显示动画
1 show方法
作用：让匹配的元素展示出来



```
// 用法一：
// 参数为数值类型，表示：执行动画时长
/* 单位为：毫秒（ms），参数2000即2秒钟显示完毕 */
$(selector).show(2000);

// 用法二：
// 参数为字符串类型，是jQuery预设的值，共有三个，分别是：slow、normal、fast
/* 跟用法一的对应关系为： */
/* slow：600ms、normal：400ms、fast：200ms */
$(selector).show(“slow”);

// 用法三：
// 参数一可以是数值类型或者字符串类型
// 参数二表示：动画执行完后立即执行的回调函数
$(selector).show(2000, function() {});

// 用法四：
// 不带参数，作用等同于 css(“display”, ”block”)
/* 注意：此时没有动画效果 */
$(selector).show();
```



注意：
jQuery预设的三组动画效果的语法几乎一致：参数可以有两个，第一个是动画的执行时长，第二个是动画执行完成后的回调函数。
第一个参数是：可以是指定字符或者毫秒数

2 hide方法
作用：让匹配元素隐藏掉
用法参考show方法
$(selector).hide(1000); // 1000表示什么？
$(selector).hide(“slow”);
$(selector).hide(1000, function(){});
$(selector).hide();

1.5.2	滑入滑出动画
1滑入动画效果（联想：生活中的卷帘门）
作用：让元素以下拉动画效果展示出来


```
$(selector).slideDown(speed,callback);
```



注意：省略参数或者传入不合法的字符串，那么则使用默认值：400毫秒（同样适用于fadeIn/slideDown/slideUp）


```
$(selector).slideDown();
```



2 滑出动画效果
作用：让元素以上拉动画效果隐藏起来


```
$(selector).slideUp(speed,callback);
```



3滑入滑出切换动画效果


```
$(selector).slideToggle(speed,callback);
```


参数等同与1.5.1 隐藏和显示
### 淡入淡出动画
1 淡入动画效果
作用：让元素以淡淡的进入视线的方式展示出来


```
$(selector).fadeIn(speed, callback);
```


2 淡出动画效果
作用：让元素以渐渐消失的方式隐藏起来


```
$(selector).fadeOut(1000);
```


3淡入淡出切换动画效果
作用：通过改变透明度，切换匹配元素的显示或隐藏状态


```
$(selector).fadeToggle('fast',function(){});
```


参数等同与1.5.1 隐藏和显示

4改变透明度到某个值
与淡入淡出的区别：淡入淡出只能控制元素的不透明度从 完全不透明 到完全透明；而fadeTo可以指定元素不透明度的具体值。并且时间参数是必需的！
作用：调节匹配元素的不透明度 


```
// 用法有别于其他动画效果
// 第一个参数表示：时长
// 第二个参数表示：不透明度值，取值范围：0-1
$(selector).fadeTo(1000, .5); //  0全透，1全不透

// 第一个参数为0，此时作用相当于：.css(“opacity”, .5);
$(selector).fadeTo(0, .5);
```



jQuery提供的动画使用方法总结：
 


有规律的体现：
jQuery提供的这几个动画效果控制的CSS属性包括：高度、宽度、不透明度。{height:400px; width:300px; opacity:.4;}
这三个CSS属性的共性是：属性值只有一个，并且这个值是数值（去掉单位后）。

### 自定义动画
注意：所有能够执行动画的属性必须只有一个数字类型的值。
比如：要改变字体大小，要使用：`fontSize（font-size）`，不要使用：font

[动画支持的属性](http://www.w3school.com.cn/jquery/effect_animate.asp)
	

作用：执行一组CSS属性的自定义动画


```
// 第一个参数表示：要执行动画的CSS属性（必选）
// 第二个参数表示：执行动画时长（可选）
// 第三个参数表示：动画执行完后立即执行的回调函数（可选）
$(selector).animate({params},speed,callback);
```



### 停止动画
stop()
作用：停止当前正在执行的动画
为什么要停止动画？
如果一个以上的动画方法在同一个元素上调用，那么对这个元素来说，后面的动画将被放到效果队列中。这样就形成了动画队列。（联想：排队进站）
动画队列里面的动画不会执行，直到第一个动画执行完成。


```
// 第一个参数表示后续动画是否要执行
（true:后续动画不执行  ;false:后续动画会执行）
// 第二个参数表示当前动画是否执行完
（true:立即执行完成当前动画  ;false:立即停止当前动画）
$(selector).stop(clearQueue,jumpToEnd);
```


都不给，默认false；
解释：
当调用stop()方法后，队列里面的下一个动画将会立即开始。但是，如果参数clearQueue被设置为true，那么队列面剩余的动画就被删除了，并且永远也不会执行。
如果参数jumpToEnd被设置为true，那么当前动画会停止，但是参与动画的每一个CSS属性将被立即设置为它们的目标值。比如：slideUp()方法，那么元素会立即隐藏掉。如果存在回调函数，那么回调函数也会立即执行。

注意：如果元素动画还没有执行完，此时调用sotp()方法，那么动画将会停止。并且动画没有执行完成，那么回调函数也不会被执行。

常用方式：


```
$(selector).stop();
```



## jQuery节点操作
### 动态创建元素


```
// $()函数的另外一个作用：动态创建元素
var $spanNode = $(“<span>我是一个span元素</span>”);
var node = $(“#box”).html（“<li>我是li</li>”）；
```


	
### 添加元素
在元素的最后一个子元素后面追加元素：
append()（重点）
作用：在被选元素内部的最后一个子元素（或内容）后面插入内容（存在或者创建出来的元素都可以）
如果是页面中存在的元素，那么调用append()后，会把这个元素放到相应的目标元素里面去；但是，原来的这个元素，就不存在了。
 如果是给多个目标追加元素，那么方法的内部会复制多份这个元素，然后追加到多个目标里面去。
常用参数：htmlString 或者 jQuery对象



```
// 在$(selector)中追加$node
$(selector).append($node);
// 在$(selector)中追加div元素，参数为htmlString
$(selector).append('<div></div>');
```



不常用操作：（用法跟append()方法基本一致）
1 appendTo()
作用：同append()，区别是：把$(selector)追加到node中去


```
$(selector).appendTo(node);
```



2 prepend()
作用：在元素的第一个子元素前面追加内容或节点


```
$(selector).prepend(node);
```



3 after()
作用：在被选元素之后，作为兄弟元素插入内容或节点


```
$(selector).after(node);
```



4 before()
作用：在被选元素之前，作为兄弟元素插入内容或节点


```
$(selector).before(node);
```


### html创建元素（推荐使用，重点）
作用：设置或返回所选元素的html内容（包括 HTML 标记）
设置内容的时候，如果是html标记，会动态创建元素，此时作用跟js里面的 innerHTML属性相同


```
// 动态创建元素
$(selector).html(‘<span>传智播客</span>’);
// 获取html内容
$(selector).html();
1.6.4	清空元素
// 清空指定元素的所有子元素（光杆司令）
// 没有参数
$(selector).empty();
$(selector).html(“”);
// “自杀” 把自己（包括所有内部元素）从文档中删除掉
$(selector).remove();

1.6.5	复制元素
作用：复制匹配的元素
// 复制$(selector)所匹配到的元素
// 返回值为复制的新元素
$(selector).clone();
```



总结：
推荐使用html(“<span></span>”)方法来创建元素或者html(“”)清空元素

### 操作form表单
#### 属性操作
设置属性：


```
// 第一个参数表示：要设置的属性名称
// 第二个参数表示：改属性名称对应的值
$(selector).attr(“title”, “hello”);
```



获取属性：


```
// 参数为：要获取的属性的名称，改操作会返回指定属性对应的值
$(selector).attr(“title”);
```


此时，返回指定属性的值

移除属性：


```
// 参数为：要移除的属性的名称
$(selector).removeAttr(“title”); 
```



注意：checked、selected、disabled要使用.prop()方法。
prop方法通常用来影响DOM元素的动态状态，而不是改变的HTML属性。例如：input和button的disabled特性，以及checkbox的checked特性。
[细节参考](http://api.jquery.com/prop/)

#### 值和内容
val()方法：
作用：设置或返回表单元素的值，例如：input,select,textarea的值


```
// 获取匹配元素的值，只匹配第一个元素
$(selector).val();
// 设置所有匹配到的元素的值
$(selector).val(“具体值”);
```



text() 方法:
作用：设置或获取匹配元素的文本内容


```
//获取操作不带参数（注意：这时候会把所有匹配到的元素内容拼接为一个字符串，不同于其他获取操作！）
$(selector).text();
//设置操作带参数，参数表示要设置的文本内容
$(selector).text(“我是内容”);
```



### 尺寸位置操作
#### 高度和宽度操作
高度操作height() ： 
作用：设置或获取匹配元素的高度值


```
//带参数表示设置高度
$(selector).height(200);
//不带参数获取高度
$(selector).height();
```


宽度操作width() ： 
作用：设置或获取匹配元素的宽度值


```
//带参数表示设置宽度
//不带参数获取宽度
$(selector).width(200);
```


css()获取高度和height获取高度的区别？
 
### 坐标值操作
offset() 
作用：获取或设置元素相对于文档的位置


```
// 无参数表示获取，返回值为：{left:num, top:num}，值是相对于document的位置
$(selector).offset();
// 有参数表示设置，参数推荐使用数值类型
$(selector).offset({left:100, top: 150});
```



注意点：设置offset后，如果元素没有定位(默认值：static)，则被修改为relative

position() 
作用：获取相对于其最近的具有定位的父元素的位置。


```
// 获取，返回值为对象：{left:num, top:num}
$(selector).position();
```


注意：只能获取，不能设置。

scrollTop() 
作用：获取或者设置元素垂直方向滚动的位置


```
// 无参数表示获取偏移
// 有参数表示设置偏移，参数为数值类型
$(selector).scrollTop(100);
```



scrollLeft() 
作用：获取或者设置元素水平方向滚动的位置


```
$(selector).scrollLeft(100);
```



对scrollTop的理解：
垂直滚动条位置 是可滚动区域 在 可视区域上方的 被隐藏区域的高度。
如果滚动条在最上方没有滚动 或者 当前元素没有出现滚动条，那么这个距离为0
