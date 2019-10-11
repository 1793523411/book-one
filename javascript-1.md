## 先介绍一下JavaScript的故事吧！

* Javascript的历史来源
  94年网景公司   研发出世界上第一款浏览器。
  95年 sun公司   java语言诞生
  网景公司和sun合作。
  Java+script   ===> javascript

* W3c规范
结构标准        html
表现标准		  css
行为标准	     js 
   
* JavaScript和ECMAScript的关系
    ECMAScript是一种由Ecma国际前身为欧洲计算机制造商协会,英文名称是European Computer Manufacturers Association，制定的标准。
JavaScript是由公司开发而成的，公司开发而成的一定是有一些问题，不便于其他的公司拓展和使用。所以欧洲的这个ECMA的组织，牵头制定JavaScript的标准，取名为ECMAScript。
简单来说ECMAScript不是一门语言，而是一个标准。符合这个标准的比较常见的有：JavaScript、Action Script（Flash中用的语言）。就是说，你JavaScript学完了，Flash中的程序也会写了。
ECMAScript在2015年6月，发布了ECMAScript 6版本，语言的能力更强。但是，浏览器的厂商不能那么快的去追上这个标准。这些新的特性，我们就业班的深入，也会给大家介绍。
* 今天的JavaScript：承担更多责任
   2003年之前，JavaScript被认为“牛皮鲜”，用来制作页面上的广告，弹窗、漂浮的广告。什么东西让人烦，什么东西就是JavaScript开发的。所以浏览器就推出了屏蔽广告功能。
2004年JavaScript命运开始改变了，那一年谷歌公司，开始带头使用Ajax技术了，Ajax技术就是JavaScript的一个应用。并且，那时候人们逐渐开始提升用户体验了。
  
* 2010年的时候，人们更加了解HTML5技术了，HTML5推出了一个东西叫做Canvas（画布），工程师可以在Canvas上进行游戏制作，利用的就是JavaScript。
        
* 2011年，Node.js诞生，使JavaScript能够开发服务器程序了。

* 今天，JavaScript工程师是绝对的吃香，能够和iOS、Android工程师比肩，毫不逊色的。
现在，公司都流行WebApp，就是用网页技术开发手机应用。什么意思呢？手机系统有iOS、安卓、windows phone。那么公司比如说开发一个“携程网”APP，就需要招聘三队人马，比如iOS工程师10人，安卓工程师10人，windows工程师10人。共30人，工资开销大。并且，如果要改版，要改3个版本。所以，现在公司，都用web技术，用html+css+javascript技术来开发app。好处是不用招聘那么多工程师，只需要几个前端开发工程师即可。并且也易于迭代，就是网页一改变，所有的终端都变了。
## js介绍
js是一款运行在客户端的网页编程语言。
* 组成部分
  * ecmascript   js标准 
  * dom        通过js操作网页元素
  * bom        通过api操作浏览器
* 特点
  * 简单易用
  * 解释执行
* 编译执行  java  c#  转化为.dll可执行文件==>电脑读取.dll可执行文件

  * 基于对象
  * 面向过程
* 作用
 * 表单验证
 * 轮播特效
 * 开发游戏
 
## JS作用
1．验证表单（以前的网速慢）
2．页面特效（PC端的网页效果）
3．移动端（移动web和app）
4．异步和服务器交互（AJAX）
5．服务端开发（nodejs）

## 浏览器工作原理
 

## 弱类型脚本语言（解释型语言，解析执行与编译执行）
* 解析执行与编译执行
编译执行：把代码编译成CPU认识的语言(文件)，然后整体的执行。
解析执行：一行一行解析，解析一行执行一行。
* 弱类型脚本语言
脚本语言是：弥补编译语言的不足而存在的，作为补充语言，不用编译。
弱类型语言：简单理解定义一个变量，可以有多种数据类型。（var temp）

## 组成（前端标准和JS组成）
### 前端标准（HTML/CSS/JS）
JavaScript、HTML、CSS各自的作用
HTML							提供网页上显示的内容（结构）
CSS								美化网页（样式）
JavaScript（JS）				控制网页行为（行为）
设计原则：
结构、样式、行为---分离！

### JS组成


```
JS  =  ECMAScript  +  DOM  +  BOM + 高级
```



ECMAScript（前身为欧洲计算机制造商协会）
JavaScript的语法规范
DOM（Document Object Model 的简称）
JavaScript操作网页上元素的API
BOM（Browser Object Model 的简称）
JavaScript操作浏览器部分功能的API
## 输出语句
一、console.log(“内容”)在控制台打印输出内容
二、alert(“内容”)弹窗显示内容
三、document.write(“内容”)在页面书写内容
## 引入方式
* 内嵌式（学习期间用）
* 外链式（实际开发）
注释问题：单行，多行，方法注释等..... 快捷键：ctrl+/ 和ctrl+shift+/

## 变量

### 命名规则
驼峰命名规则：getElementById/matherAndFather/aaaOrBbbAndCcc
遵从规则：
1.变量命名必须以字母或是下标符号”_”或者”$”为开头。
2.变量名长度不能超过255个字符。
3.变量名中不允许使用空格，首个字不能为数字。
4.不用使用脚本语言中保留的关键字及保留符号作为变量名。
5.变量名区分大小写。(javascript是区分大小写的语言)
6.汉语可以作为变量名。但是不建议使用！！！（low）

### 变量使用
#### 定义赋值和定义后在赋值


```
var  age = 19;		
var age ;     age = 19
不建议使用：var age = “张三”; 	    age = 19;    跨类型。
```





