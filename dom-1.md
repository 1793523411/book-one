## 事件
### 概述

JS是以事件驱动为核心的一门语言。
### 事件三要素

事件源、事件、事件驱动程序。
三句话：获取事件源、绑定事件、书写事件驱动程序。
获取事件源：document.getElementById(“box”);
绑定事件：  box.onclick = function(){ 程序 };
书写事件驱动程序：以后要学习的关于DOM的操作。

## DOM概述
### 解析过程
HTML加载完毕，渲染引擎会在内存中把HTML文档，生成一个DOM树，getElementById是获取内中DOM上的元素节点。然后操作的时候修改的是该元素的属性。
### DOM   (文档对象模型)
document是文档对象模型的一部分。
DOM是一个复合的数据类型。
 
**DOM的数据结构（树状）**
 
### HTML的组成部分为节点（ Node ）
在HTML当中一切都是节点……
由结构图中我们可以看到，整个文档就是一个文档节点。
每一个HMTL标签都是一个元素节点（标签）。
标签中的文字则是文字节点。（文本）
标签的属性是属性节点。（属性）
### DOM节点的获得
操作节点，必须首先找到该元素。有三种方法来做这件事：
通过 id 找到 HTML 元素


```
document.getElementById("demo");
```


通过标签名找到 HTML 元素


```
document.getElementsByTagName("div");
```


通过类名找到 HTML 元素


```
document.getElementsByClassName("a");
```


通过类名查找 HTML 元素在 IE 5,6,7,8 中无效
标签=document.getElementById("demo"); 通过ID获得标签
他的返回值是一个标签，可以直接使用。获得属性值，设置属性。
标签数组= document.getElementsByTagName("div"); 通过标签名获得标签数组
标签数组= document.getElementsByClassName("a");通过类名获得标签数组
他们两个的返回值是标签数组，习惯性是遍历之后再使用。
特殊情况：数组中的值只有1个。      
       

```
document.getElementsByTagName("div")[0];取数组中第一个元素
             document.getElementsByClassName("a")[0];取数组中第一个元素
```


### DOM 访问关系（节点的获得）
节点的访问关系，是以属性的方式存在的。
DOM的节点并不是孤立的，因此可以通过DOM节点之间的相对关系对它们进行访问。
#### 父节点  （ parentNode ）   
调用者就是节点。一个节点只有一个父节点。调用方式就是节点.parentNode.
案例：
1.通过子盒子设置父盒子的背景色。
2.关闭二维码
#### 兄弟节点
`Sibling`就是兄弟的意思。
`Next：`下一个的意思。
`Previous:`前一个的意思。
`nextSibling：`调用者是节点。IE678中指下一个元素节点（标签）。在火狐谷歌IE9+以后都指的是下一个节点（包括空文档和换行节点）。
`nextElementSibling：`在火狐谷歌IE9都指的是下一个元素节点。
总结：在IE678中用nextSibling，在火狐谷歌IE9+以后用nextElementSibling
下一个兄弟节点=节点.nextElementSibling || 节点.nextSibling

`previousSibling：`调用者是节点。IE678中指前一个元素节点（标签）。在火狐谷歌IE9+以后都指的是前一个节点（包括空文档和换行节点）。
`previousElementSibling：`在火狐谷歌IE9都指的是前一个元素节点。
总结：在IE678中用previousSibling，在火狐谷歌IE9+以后用previousElementSibling。
下一个兄弟节点=节点.previousElementSibling|| 节点.previousSibling
#### 单个子节点
`firstChild：`调用者是父节点。IE678中指第一个子元素节点（标签）。在火狐谷歌IE9+以后都指的是第一个节点（包括空文档和换行节点）。
`firstElementChild:`在火狐谷歌IE9都指的第一个元素节点。
第一个子节点=父节点.firstElementChild || 父节点.firstChild
`lastChild:`调用者是父节点。IE678中指最后一个子元素节点（标签）。在火狐谷歌IE9+以后都指的是最后一个节点（包括空文档和换行节点）。
`lastElementChild：`在火狐谷歌IE9都指的最后一个元素节点。
第一个子节点=父节点.lastElementChild|| 父节点.lastChild
#### 所有子节点
`childNodes：`它是标准属性，它返回指定元素的子元素集合，包括HTML节点，所有属性，文本节点   （他还是W3C的亲儿子 ）
火狐 谷歌等高本版会把换行也看做是子节点


```
nodeType==1时才是元素节点(标签)
      nodeType  ==  1  表示的是元素节点   记住   元素就是标签
      nodeType  ==  2  表示是属性节点   
      nodeType  ==  3  是文本节点   
```


子节点数组 = 父节点.childNodes;   获取所有节点。
`children：`非标准属性，它返回指定元素的子元素集合。
但它只返回HTML节点，甚至不返回文本节点，虽然不是标准的DOM属性，但它和innerHTML方法一样，得到了几乎所有浏览器的支持。
children在IE6/7/8中包含注释节点 
在IE678中，注释节点不要写在里面。
子节点数组 = 父节点.children;   用的最多。
#### 知识补充
节点自己.parentNode.children[index];随意得到兄弟节点。

作为了解内容：


```
function siblings(elm) {
		var a = [];
		var p = elm.parentNode.children;
		for(var i =0,pl= p.length;i<pl;i++) {
			if(p[i] !== elm) a.push(p[i]);
		}
		return a;
}
```


定义一个函数。必须传递自己。定义一个数组，获得自己的父亲，在获得自己父亲的所有儿子（包括自己）。遍历所哟与的儿子，只要不是自己就放进数组中。
#### 要明白两个属性（！！！重点！！！）
parentNode   和  children  这两个属性。
### DOM节点操作 （！！！！！重点！！！！！）
节点的访问关系都是属性。节点的操作都是函数或者方法。
#### 创建节点
使用方法是这样的document.createElement();
新的标签（节点） = document.createElement(“标签名”);
#### 插入节点（使用节点）
使用方法： 父节点.appendChild();
父节点.appendChild(新节点); 父节点的最后插入一个新节点

使用方法：父节点.insertBefore(要插入的节点，参考节点)；
父节点.insertBefore(新节点,参考节点)在参考节点前插入;
如果参考节点为null，那么他将在节点最后插入一个节点。
#### 删除节点   
用法：用父节点删除子节点。
父节点.removeChild（子节点）；必须制定要删除的子节点
节点自己删除自己：
不知道父级的情况下，可以这么写：node.parentNode.removeChild(node)
#### 复制节点 （    oldNode.cloneNode（true）  ）
想要复制的节点调用这个函数cloneNode()，得到一个新节点。 方法内部可以传参，入股是true，深层复制，如果是false，只复制节点本身。
新节点=要复制的节点.cloneNode(参数) ; 参数可选复制节点
用于复制节点， 接受一个布尔值参数， true 表示深复制（复制节点及其所有子节点）， false 表示浅复制（复制节点本身，不复制子节点）
#### 节点属性（节点.属性）
获取：getAttribute(名称)
设置：setAttribute(名称, 值)
删除：removeAttribute(名称)
注意：IE6、7不支持。
调用者：节点。   有参数。   没有返回值。
每一个方法意义不同。
## DOM详解（属性操作）
### DOM元素
DOM就是html文档的模型抽象。数据以树的形式在内存中排列。
节点就是DOM的组成。是一个对象，有属性和方法。获取方式有很多种。
节点分为元素节点（标签），文本节点，属性节点。
区分方法：nodeType: 1是标签,2是属性,3是文本

**value和innerHTML和innerText和textContent
1.老版本的火狐不支持innerText，支持textContent
2.p不能嵌套p。h1不能嵌套h1。a连接内部不能嵌套a连接**

###DOM案例
* 显示二维码
* 禁用文本框和获取失去焦点输入事件。
* 表单处理。Input取值赋值和select选水果。   
* 验证账号密码，高亮显示。
* 全选反选
#### 属性获取修改和删除（属性绑定）
* teb栏。（排他思想）（简单写法和兼容写法）
1.点亮盒子。
（第三种体验双重for循环，第一种打印三角形，第二种冒泡排序）
2.弹出索引值。
3.属性绑定。
4.两个for循环变一个
* 自定义属性（兼容写法）
1.直接绑定属性：不会再标签中显示（没有的属性）；
2.标签中的自定义属性，不能box.aaa获取
（火狐谷歌IE9+）(IE678可以获取)
3.get/setAttribute（）；可以
#### 节点关系。（父节点、兄弟节点、子节点、所有子节点）
1.子节点。（京东头）
2.nodeType/nodeName/nodeValue:    
元素/属性/文本    123/标签:属性名:#text/null:属性值:内容
3.childNodes实现各行变色index = 0;
4.父节点/所有子节点/兄弟节点

### style属性设置和获取（$方法的封装）
（style是一个对象，不能获取内嵌和外链）
* 样式少的时候使用
* style是对象
* 值是字符串，没有设置值是“”；
* 命名规则，驼峰命名。和css不一样
* 设置了类样式不能获取。（只和行内式交互，和内嵌和外链无关）
* box.style.cssText = “字符串形式的样式”；

###　BOM简介


```
	1.open/alert/confirm
	2.close
	3.setTimeOut/setInterval
	4.location
	5.onload
	6.navigator

```


## 内置对象
### Date
案例：日历、倒计时
### String/Number/Boolean
#### 给索引查字符(charAt/charCodeAt)
1 charAt，获取相应位置字符（参数： 字符位置）
注释：字符串中第一个字符的下标是 0。如果参数 index 不在 0 与 string.length 之间，该方法将返回一个空字符串。
2 charCodeAt获取相应位置字符编码（参数： 字符位置）
charAt()方法和charCodeAt()方法用于选取字符串中某一位置上的单个字符
区别：charCodeAt()方法，它并不返回指定位置上的字符本身，而是返回该字符在Unicode字符集中的编码值。如果该位置没有字符，返回值为NaN.
字符/字符编码 = Str.charAt/charCodeAt(索引值);
#### 给字符查索引（indexOf/lastIndexOf）
1 indexOf，从前向后索引字符串位置（参数： 索引字符串）
从前面寻找第一个符合元素的位置
2 lastIndexOf，从后向前索引字符串位置（参数：索引字符串）
从后面寻找第一个符合元素的位置
找不到则返回 -1
索引值 = str.indexOf/lastIndexOf(想要查询的字符);
#### url 编码和解码
URI (Uniform ResourceIdentifiers,通用资源标识符)进行编码，以便发送给浏览器。有效的URI中不能包含某些字符，例如空格。而这URI编码方法就可以对URI进行编码，它们用特殊的UTF-8编码替换所有无效的字符，从而让浏览器能够接受和理解。
encodeURIComponent() 函数可把字符串作为 URI 组件进行编码
decodeURIComponent() 函数可把字符串作为 URI 组件进行解码
#### 字符串的链接
新字符串 = str1.concat(str2)； 链接两个字符串
#### 字符串的截取
* slice，截取字符串（参数：1，截取位置【必须】，2终结点）
3字符串 = str.slice（索引1，索引2); 两个参数都是索引值。
(1).（2,5）  正常包左不包右。
(2). ( 2 )   	从指定的索引位置剪到最后。
(3).（-3）   从倒数第几个剪到最后.
(4).（5,2）  前面的大，后面的小，空。

* substr，截取字符串（参数：1，截取位置【必须】，2截取长度）
	字符串 = str.substr（参数1，参数2); 1索引值,2长度。
		第一个参数为从索引位置取值，第二个参数返回字符长度。
(1).（2,4）    从索引值为2的字符开始，截取4个字符。
(2).（1）     一个值，从指定位置到最后。
(3).（-3）    从倒数第几个剪到最后.
(4). 不包括前大后小的情况。
* substring 同slice
字符串 = str.substring（参数1，参数2); 两个参数都是索引值。
  不同1：参数智能调转位置。
  不同2：参数负值，将全部获取字符串。
（1）.（2,5）    正常包左不包右。
(2).   ( 2 )      从指定的索引位置剪到最后。
(3).  （-3）    获取全部字符串.
(4).  （5,2）   前面的大，后面的小，不是空。（2,5）
#### 特殊方法简介


```
trim()     //只能去除字符串前后的空白
replace()  //替换   str.replace(/aaa/gi,“bbb”);
split()    //字符串变数组
```


* Math
Math.abs();       取绝对值
Math.floor();      向下取整
Math.ceil();       向上取整
Math.round();     四舍五入取整
Math.random();   随机数0-1
* addEventListenner（兼容绑定、移除、原理）
1.使用方法
2.实现原理
3.兼容性。
5.移除事件
	

```
		1.bnt.onclick = null;
		2.btn.removeEventListener(...);
		3.btn.detachEvent(...);(attachEvent)
```

	

