# 三大家族
## offset家族
### 三大家族和一个事件对象
三大家族（offset/scroll/client）
事件对象/event   （事件被触动时，鼠标和键盘的状态）（通过属性控制）
### Offset家族简介
offset这个单词本身是--偏移，补偿，位移的意思。
js中有一套方便的获取元素尺寸的办法就是offset家族；


```
offsetWidth和offsetHight 以及offsetLeft和offsetTop以及offsetParent
共同组成了offset家族。
```


#### offsetWidth和offsetHight （检测盒子自身宽高+padding+border）
这两个属性，他们绑定在了所有的节点元素上。获取之后，只要调用这两个属性，我们就能够获取元素节点的宽和高。
offset宽/高  =  盒子自身的宽/高 + padding +border；
offsetWidth = width+padding+border；
offsetHeight = Height+padding+border；
#### offsetLeft和offsetTop  （检测距离父盒子有定位的左/上面的距离）
返回距离上级盒子（带有定位）左边s的位置
如果父级都没有定位则以body为准
offsetLeft 从父亲的padding 开始算,父亲的border 不算。
在父盒子有定位的情况下，offsetLeft == style.left(去掉px)
#### offsetParent   （检测父系盒子中带有定位的父盒子节点）
1、返回改对象的父级 （带有定位）
如果当前元素的父级元素没有进行CSS定位	（position为absolute或	relative，fixed），	offsetParent为body。
2、如果当前元素的父级元素中有CSS定位	（position为absolute或	relative，fixed），	offsetParent取最近的那个父级元素。
### offsetLeft和style.left区别

一、最大区别在于offsetLeft可以返回没有定位盒子的距离左侧的位置。 
而 style.left不可以
二、offsetTop 返回的是数字，而 style.top 返回的是字符串，除了数字外还带有单位：px。
三、offsetTop 只读，而 style.top 可读写。（只读是获取值，可写是赋值）
四、如果没有给 HTML 元素指定过 top 样式，则style.top 返回的是空字符串。

style.left在=的左边和右边还不一样。（左边的时候是属性，右边的时候是值）



## scroll家族
### Scroll家族组成
#### ScrollWidth和scrollHeight（不包括border）
检测盒子的宽高。（调用者：节点元素。属性。）
盒子内容的宽高。（如果有内容超出了，显示内容的高度）
IE567可以比盒子小。 IE8+火狐谷歌不能比盒子小
#### scrollTop和scrollLeft
网页，被浏览器遮挡的头部和左边部分。
被卷去的头部和左边部分。
#### 他有兼容性问题
一、未声明 DTD（谷歌只认识他）


```
document.body.scrollTop
```


二、已经声明DTD（IE678只认识他）
   `document.documentElement.scrollTop`
三、火狐/谷歌/ie9+以上支持的
   `window.pageYOffset`
#### 兼容写法


```
var aaa = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0;

var aaa = document.documentElement.scrollTop + document.body.scrollTop;
```



### 获取title、body、head、html标签


```
document.title --- 文档标题；
document.head --- 文档的头标签
document.body --- 文档的body标签；
document.documentElement --- 这个很重要
```


它表示文档的html标签， 也就是说，基本结构当中的html标签并不是通过document.html 去访问的，而是document.documentElement 。
### Json
Json是一种和数组类似的数据类型。
不同的是：数组中的元素是单一的。
而json中的元素，是以键值对的形式出现的。（key: value）
#### 定义方法
var  json  =  { key1：value1,key2：value2,key3：value3...  };
数组是通过索引值获取数组中的元素的，而json是通过key获取元素的。
#### 获取内容
JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式，我们称之为JavaScript对象表示法。使用JSON进行数据传输的优势之一。表示方法为键值对，key：value。
var myjson={k1:v1,k2:v2,k3:v3...}
获取方式：v1 == myjson.k1  v2 == myjson.k2
Json一般就是被当做一个配置单用；
#### Json的遍历（了解）
用的是新的语法方法：for ... In ....
 
## 判断页面有没有DTD
document.compatMode === "BackCompat"
BackCompat  未声明
CSS1Compat  已经声明
注意大小写



## client家族
### 主要成员
1、clientWidth	获取网页可视区域宽度（两种用法）
   clientHeight	获取网页可视区域高度（两种用法）
调用者不同，意义不同：
盒子调用：指盒子本身。
body/html调用：		可视区域大小。	
2、clientX       鼠标距离可视区域左侧距离（event调用）
   clientY       鼠标距离可视区域上侧距离（event调用）
3、clientTop/clientLeft 		盒子的border宽高
### 三大家族区别（三大家族总结）
#### Width和height
clientWidth  = width  + padding
clientHeight  = height + padding
offsetWidth  = width  + padding + border
offsetHeight  = height + padding + border
scrollWidth   = 内容宽度（不包含border）
scrollHeight  = 内容高度（不包含border）
#### top和left


```
offsetTop/offsetLeft ：
		调用者：任意元素。(盒子为主)
		嘛作用：距离父系盒子中带有定位的距离。
scrollTop/scrollLeft:(盒子也可以调用，必须有滚动条)
		调用者：document.body.scrollTop/.....(window)
		嘛作用：浏览器无法显示的部分（被卷去的部分）。
clientY/clientX:（clientTop/clientLeft 值的是border）
		调用者：event.clientX(event)
		嘛作用：鼠标距离浏览器可视区域的距离（左、上）。
```


### client家族特殊用法之:检浏览器宽/高度(可视区域)
 
### Onresize事件
只要浏览器的大小改变，哪怕1像素，都会触动这个事件。
### 事件总结
区分：
	

```
1.window.onscroll        	屏幕滑动
2.window.onresize      	浏览器大小变化
3.window.onload	         页面加载完毕
4.div.onmousemove    		鼠标在盒子上移动
（注意：不是盒子移动！！！）
  5.onmouseup/onmousedown  ==  onclick
```


### 获得屏幕宽高
window.screen.width
分辨率是屏幕图像的精密度，指显示器所能显示的像素有多少。
我们的电脑一般：
横向1280个像素点，
纵向960个像素点。
我们看电影的时候是满屏和半屏的，就是这。
