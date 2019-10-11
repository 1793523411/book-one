# 京东案例（无js）
## 搭建项目环境     (结构样式行为分离)
一、HTML		 核心文件     index.html
二、CSS       控制样式     
a）base.css(基础样式)       b）global.css(全局样式)
三、Image      放图片的文件夹
四、JS		    音频视频.....
## 站点
站点 == 项目 == 项目文件夹 == （根目录）

## 引入图标
一、下载
        

```
京东：www.jd.com/favicon.ico           能下载京东图标
        所有：网站名（带www.）/favicon.ico    下载所有网站的图标
```


二、引入


```
<link rel="shortcut icon" href="favicon.ico"/>
```




```
网站名：bitbug.net      
  <link rel="shortcut icon" href=" /favicon.ico" />     绿色部分删掉
```


## 小知识
font :  加粗  字号/行高  格式；    行高如果不写，默认为0；

u   ins     下划线
i   em      倾斜
s   del      删除线

font-weight:  normal;         加粗变正常
font-style:  normal;           倾斜变正常
text-decoration: none;         下划线删除线变正常
outline-style: none;           去除蓝色外边框
resize:  none;               禁止文本框拖拽
## 权限问题

|选择器|权限|
|:---:|:--:|
|div|1|
|.box .site-nav|10|
|#box|100|
|`<div style="width:..">`|1000|
|!important|1/0|





 
## 盒子稳定性
一、只给宽高的盒子（宽/高度剩余法）
二、给padding的盒子
三、给margin的盒子
## 量取盒子高度
fireworks
 
## 模拟鼠标


```
cursor: pointer;           鼠标变成小手
cursor: move;            鼠标变成四角箭头
cursor: text;             鼠标变成工形插入条光标
cursor: default;           鼠标变成小白
```


## 文字居中问题


```
1.text-align: center;
2.padding-left/padding-right;
3.定位、margin.......
```



## 圆角矩形


```
border-radius: 宽/高一半；
border-radius: 50%；
border-radius: 0.3em；
border-radius: 左上角  右上角  右下角  左下角；
```


 
## 清除浮动
问题：父盒子高度为0，子盒子不占位置，子盒子不会撑开父盒子。
（下面的标准流盒子，会跑到父盒子中的子盒子下面。）
处理办法：清除浮动。（清除子盒子因为浮动，对父子造成的影响）
使用方法：谁出问题给谁加一个clearfix类名。



清除浮动方法：
* clear: both;
 
* overflow: hidden;  
 
* 单伪元素标签法


```
.clearfix:after {
content: “”;
height: 0;
visibility: hidden;
overflow: hidden;
dispaly: block;
clear: both;
}
.clearfix {
zoom: 1;/*IE678*/
}
```


* 双伪元素标签法


```
.clearfix:before,  .clearfix:after {
content: “”;
display: table;
}
.clearfix:after {
clear: both;
}
.clearfix {
zoom: 1;/*IE678*/
}
```


## 层级
简单概述：谁高。
使用：
一、必须有定位。（除去static）
二、用z-index来控制层级数。
## 小知识（浮动的盒子相互影响）
浮动的盒子千万不要让他超出父盒子。
超出父盒子的部分会影响下面盒子中的浮动的子盒子。
## 什么时候用margin和padding（不考虑宽高）
1.需要使用背景图的时候必须用padding。
2.会出现外边距合并或者margin塌陷的时候用padding。
3.行内元素上下只能设置padding，不能设置margin。（行内高16px）
4.看border，如果是a连接，看能不能让字体变色，或者显示小手。
5.看需求。
## 隐藏盒子问题


```
1.overflow：hidden;			隐藏盒子超出的部分。
2.display: none;				隐藏盒子，而且不占位置。(用的最多)
3.visibility: hidden;			隐藏盒子，而且占位置。
4.opacity: 0;					隐藏盒子，而且占位置。
5.Position/top/left/...-999px 隐藏盒子，而且占位置。
```


## 浮动的盒子问题
浮动的盒子比标准流盒子高，但是能够遮挡住标准流盒子，遮挡不住里面的图片和文字。

## JS关闭a链接的跳转


```
<a href="javascript:;">1111111111</a>
<a href="javascript:void(0)">1111</a>
```


## 权重问题
left比right，权重高。有left又有right的时候，执行left的值。
top比bottom，权重高。有top又有bottom的时候，执行top的值。
## 半透明
opacity：0.4；   优点方便。缺点：里面的内容也会半透明。
C3的技术来解决半透明：
background: rgba(0,0,0,0.3);
background: rgba(0,0,0, .3);
## 定位问题
relative不能给行内元素设置宽高
定位中，两个定位不能给行内元素设置宽高。
Static和relative。另外两个可以。


## 层级问题  （谁高）
总结：标准流盒子，低于浮动的盒子，浮动的盒子又低于定位的盒子。
定位高于浮动，浮动高于标准流。（高低和占不占位置无关）
（除去static之外）。
用法：
* 必须有定位。（除去static之外）。
* 给定z-index的值为层级的值。（不给默认为0）
（层级为0的盒子，也比标准流和浮动高。）
（层级为负数的盒子，比标准流和浮动低。）
（层级不取小数）
（层级一样，后面的盒子比前面的层级高。）
（浮动或者标准流的盒子，后面的盒子比前面的层级高。）

定位中：abselute是不占位置的，relative是站位的的。而层级的高低，是和占不占位置没有关系的。



