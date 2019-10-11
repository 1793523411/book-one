 # css书写，表签元素，三大特性，修饰，伪类
 
 ## 样式表书写位置
 
* 内嵌式写法


```
<head>
<style type=”text/css”>
样式表写法
</style>
</head>
```


* 外链式写法


```
写在head里，<link rel=”stylesheet” href=”1.css”>
```


 
* 行内样式表
 `class="color:red;..."`

### 三种写法特点:
* 内嵌式写法，样式只作用于当前文件，没有真正实现结构表现分离。
* 外链式写法，作用范围是当前站点，谁调用谁生效，范围广，真正实现结构表现分离。
* 行内样式表，作用范围仅限于当前标签，范围小，结构表现混在一起。  （不推荐使用）
## 标签分类(显示方式)
### 块元素
典型代表,Div,h1-h6,p,ul,li  <br>
 特点: 
 独占一行
 可以设置宽高
 嵌套（包含）下，子块元素宽度（没有定义情况下）和父块元素宽度默认一致。
### 行内元素
典型代表 span  ,a,  ,strong , em,  del,  ins
特点：★在一行上显示
      ★不能直接设置宽高
      ★元素的宽和高就是内容撑开的宽高。
### 行内块元素(内联元素)
典型代表  input  img
特点：★在一行上显示
      ★可以设置宽高      

### 块元素、行内元素
* 块元素转行内元素
display:inline;
 
* 行内元素转块元素
display:block;
 
* 块和行内元素转行内块元素
display:inline-block;
 

## css三大特性
### 层叠性
当多个样式作用于同一个（同一类）标签时，样式发生了冲突，总是执行后边的代码(后边代码层叠前边的代码)。和标签调用选择器的顺序没有关系。
 

### 继承性
   继承性发生的前提是包含（嵌套关系）
   ★文字颜色可以继承
   ★文字大小可以继承
   ★字体可以继续
   ★字体粗细可以继承
   ★文字风格可以继承
   ★行高可以继承
   总结：文字的所有属性都可以继承。
* 特殊情况：
h系列不能继承文字大小。
a标签不能继承文字颜色。
５.3	优先级
 默认样式<标签选择器<类选择器<id选择器<行内样式<!important  
         0         1          10     100      1000      1000以上
       
### 优先级特点
★继承的权重为0
★权重会叠加
 ## 链接伪类
a:link{属性:值;}  a{属性:值}效果是一样的。
a:link{属性:值;}       链接默认状态	 
a:visited{属性:值;}     链接访问之后的状态 
a:hover{属性:值;}      鼠标放到链接上显示的状态  	a:active{属性:值;}      链接激活的状态
  ：focus{属性:值；}     获取焦点
 
## 修饰
### 文本


```
text-decoration: none  |   underline   |     line-through
```


###背景属性
`background-color `    背景颜色
`background-image `   背景图片
`Background-repeat`    repeat(默认)  |  no-repeat |   repeat-x   |  `repeat-y `    背景平铺
`Background-position  left  |  right  |  center  |  top  | bottom`  ### 背景定位
 
* 方位值只写一个的时候，另外一个值默认居中。
 
* 写2个方位值的时候，顺序没有要求。
 
* 写2个具体值的时候，第一个值代表水平方向，第二个值代表垂直方向。
#### Background-attachment   背景是否滚动   scroll  |  fixed
### 背景属性连写
 
* 连写的时候没有顺序要求，url为必写项。