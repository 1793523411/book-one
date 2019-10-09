_OK，现在我要正式开始我的web前端开发之旅了...._
# 引言
**&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp HTML作为一种标记语言，我觉得就跟Markdown一样，一学就会，当然H5引入了一些比较与意思的东西，我就是先学的HTML（不带数字5），然后在学的HTML5，接着我就总结一下我对HTML这门超文本标记语言的学习吧**
********
## 不带数字5的HTML

&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp先回顾一下自己都学了哪些东西在这个阶段，首先是基本的标签，属性，属性值，单标签，双标签，对网页上的内容租出改变，比如：文字大小，文字样式，插入一个水平线等等。我觉得在这个阶段学的最重要的，也就是在后面基本上一直用的，我也印象比较深的应该是这些内容：<br>
* 图片标签，基本上很重要吧，同样是最为比较吸引人的标签多媒体表亲，像音乐，视频，学的时候感觉很牛逼，但后面基本真的没怎么用过，包括后面好多针对图片做处理的css操作，而多媒体标签不能说没有，不如图片丰富，毕竟一个网站，图片（**图片资源，图标（不包括图标字体），logo**）还是相对较多的。<br>

* form表单，对这个东西，我去，真的是服了，开始学的时候是在表格之后学的，当时觉得表格有点东西，表单跟表格差不多，表格应该很有用，表单一般般，不是很重视，到后面，学Ajax，才知道form表单是多么重要，学nodejs更是了解了HTML的奥秘所在，在这还学历，表单控件（**H5有智能的表单控件**），锚点，列表等有些东西，还都挺有趣。<br>

* 还有一标签语义化，我觉得这个也挺重要的，当我自己在写一个HTML近700行，css近2000行，js500多行的网页的时候(**当然能力尚不足够，是仿腾讯视频的做的，[仓库网址](https://github.com/1793523411/TencentWeb)**)，我知道在HTML这必须分清自己写的标签代表的是什么元素，这个时候标签的语义化很有用，我是这么觉得，虽然基本所有标签都可以用div取代，但我真的不建议这么做（**包括超链接，插入图片，列表，表格，加上css,div无所不能，故HTML又叫div**），真的会把自己迷死的。
## HTML5
HTML5相比较HTML可有趣多了，也高级多了。（**广义上讲H5=html5+css+javascript**）<br>
首先新增了智能表单，可以取色支持自动提示，度量器等丰富的功能满足了许多需求，多媒体标签，对浏览器的兼容性更好，可以自己做自己喜欢的进度条，对标签语义化做的更好了，最重要的一点是做了Dom拓展，还有一些，拖拽，web存储，，地理定位，，网络状态，应用程序缓存等高级功能。

 ### DOM拓展
 

 
 #### 获取元素
获取单个元素

```
  var box1 = document.querySelector('.box3')
  box1.styel.background = 'red'
```
1、document.getElementsByClassName ('class') 通过类名获取元素，以类数组形式存在。
2、document.querySelector(‘div’) 通过CSS选择器获取元素，符合匹配条件的第1个元素。
3、document.querySelectorAll('selector') 通过CSS选择器获取元素，以类数组形式存在。<br>

 获取复合元素


```
//会获取所有复合条的 标签，返回的是一个数组， 参数：可以是任意 css选择器
     var divs= document.querySelectorAll('div.box');
        console.log(divs);

        for(var i=0;i<divs.length;i++){
            divs[i].style.background='red';
        }
```


 ####类名操作
 
1、Node.classList.add('class') 添加class
`` box1.classList.add('active'); ``
2、Node.classList.remove('class') 移除class
``  box1.classList.remove('active'); ``
3、Node.classList.toggle('class') 切换class，有则移除，无则添加


```
document.querySelector('button').onclick=function(){
            document.querySelector('.box3').classList.toggle('active');
        }
```


4、Node.classList.contains('class') 检测是否存在class
 

```
判断是否包含某个类名  返回结果 true/false
        var f=box1.classList.contains('active');
```


&nbspNode指一个有效的DOM节点，是一个通称。
&nbspH5的操作类名的方式跟jQuery一样好用
 #### 自定义属性
 
 在HTML5中我们可以自定义属性，其格式如下data-*=""，例如
data-info="我是自定义属性"，通过Node.dataset['info'] 我们便可以获取到自定义的属性值。
Node.dataset是以类对象形式存在的
当我们如下格式设置时，则需要以驼峰格式才能正确获取

 

```
<!-- 给标签添加自定义属性 必须以data-开头 -->
    <div class="box" title="盒子" data-my-name="zs"  data-content="我是一个div">div</div>
    自定义的属性 需要通过 dateset[]方式来获取 
    var box=document.querySelector('.box');
        console.log(box.dataset['content']);
         var num=100;
        num.index=10;
        box.index=100;
        box.dataset['content']='aaaa';
//        data-my-name="zs" 如何获取
        console.log(box.dataset['myName']);
```







 
 ### 拖拽
 **事件监听**
 拖拽元素
ondrag 		应用于拖拽元素，整个拖拽过程都会调用
ondragstart	应用于拖拽元素，当拖拽开始时调用
ondragleave	应用于拖拽元素，当鼠标离开拖拽元素时调用
ondragend	应用于拖拽元素，当拖拽结束时调用
目标元素
ondragenter	应用于目标元素，当拖拽元素进入时调用
ondragover	应用于目标元素，当停留在目标元素上时调用
ondrop		应用于目标元素，当在目标元素上松开鼠标时调用
ondragleave	应用于目标元素，当鼠标离开目标元素时调用

 #### 拖拽事件
 
 页面中设置了draggable="true"属性的元素


```
<script>
        var box=document.querySelector('.box');

//        绑定拖拽事件
//        拖拽开始
        box.ondragstart=function(){
            console.log('拖拽开始...');
        }
//      拖拽结束
        box.ondragend=function(){
            console.log('拖拽结束...');
        }
//        拖拽离开 :鼠标拖拽时离开被拖拽的元素是触发
        box.ondragleave=function(){
            console.log('拖拽离开了....');
        }

        box.ondrag=function(){
            console.log('拖拽....');
        }


    </script>

```

#### 拖拽-目标元素事件

页面中任何一个元素都可以成为目标元素


```
 var two=document.querySelector('.two');
        var one=document.querySelector('.one');

//        当被拖拽元素进入是触发
        two.ondragenter=function(){
            console.log('来了...');
        }

        // 当被拖拽元素离开时触发
        two.ondragleave=function(){
            console.log('走了...');
        }
        one.ondragstart=function(){
            console.log('拖拽开始...');
        }
        one.ondragend=function(){
            console.log('拖拽结束...');
        }
//      当 拖拽元素在 目标元素上是 连续触发
        two.ondragover=function(e){
//             阻止拖拽事件的默认行为；
            e.preventDefault();
            console.log('over...');
        }
```
   

 
