## viewport

手机拥有了浏览器的初期,人们并没有专门为移动设备设计页面,造成的直接结果就是,访问的页面是直接将电脑页面进行缩放,操作起来有诸多不便,viewport就是用来解决这个问题的

### viewport的概念
移动设备上,用来显示网页的区域.
如果把移动设备的浏览器(也有可能是app中的webview) ,当做相框的话
viewport就相当于相框中的画,可能会比相框小,可能会比相框大,如果刚好一样大,那就皆大欢喜.
修改viewport
我们可以通过meta标签去修改viewport的值 ,防止滚动条出现,提升用户体验

### 移动web常见设置


```
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
```


该属性最早是苹果公司在Safari中推出用来解决移动设备的viewport问题的.后来被各大安卓以及浏览器厂商效仿,所以说这个属性真的是非常有用的
可选值
* width:
 * 设置layout viewport 的宽度，为一个正整数，或字符串"width-device"
* initial-scale:
 * 设置页面的初始缩放值，为一个数字，可以带小数
* minimum-scale:
 * 允许用户的最小缩放值，为一个数字，可以带小数
* maximum-scale:
 * 允许用户的最大缩放值，为一个数字，可以带小数
* height:
 * 设置layout viewport 的高度，这个属性对我们并不重要，很少使用
* user-scalable:
 * 是否允许用户进行缩放，值为"no"或"yes", no 代表不允许，yes代表允许


## 移动web注意细节样式

移动端开发不同于桌面端开发,需要注意一些细节

### 点击高亮效果
在移动端浏览器会遇见点击出现高亮的效果，在某项项目是不需要这个默认的效果的。那么我们通常会把这个点击的颜色设置成透明。

css代码


```
-webkit-tap-highlight-color:transparent;/*清除点击高亮效果*/
```


盒子模型
通过css3的新属性box-sizing我们能够让盒子有限顾及自己的尺寸而不是内容,避免出现多余的滚动条

css代码


```
/*设置宽度以边框开始计算*/
-webkit-box-sizing: border-box;/*webkit内核兼容性写法*/
box-sizing: border-box;
```


#### Input默认样式清除
在移动设备的浏览器中input标签一般会有默认的样式,通过**border=none,outline=none**无法去除,比如立体效果,3d效果等等,我们需要添加下列样式

css代码


```
/*在移动端清除浏览器默认样式*/
-webkit-appearance: none;
```


最小宽度和最大的宽度
考虑到移动设备在大尺寸的的屏幕不会过度缩放 失去清晰度,在小尺寸的屏幕中不会出现布局错乱的问题

css代码
注 下列代码取值不是固定的,根据实际情况需要进行调整


```
max-width: 640px;  /*在行业当中的移动端的设计图一般使用的是640px*/
min-width: 300px;  /*在移动设备当中现在最小的尺寸320px*/
```


结构伪类选择器
`nth-child()`如果有多个不同兄弟节点获取的时候,索引需要特殊计算,我们可以限定在某一个类型上,语法如下



```
E:first-of-type匹配同类型中的第一个元素E。
E:last-of-type匹配同类型中的最后一个元素E。
E:nth-of-type(n) 匹配同类型中的第n个元素E。
```



## touch事件

移动端使用的是touch事件,但是并不能直接通过ontouch等语法访问,需要使用`addEventListener`进行绑定

可选事件

```
touchstart:手指触摸时触发
touchmove:手指在屏幕上滑动时连续触发
touchend:当手指离开屏幕时触发。
touchcancel:系统停止跟踪触摸时候会触发。(这个事件使用较少,了解即可)
```

事件参数中 能够获取移动的一些属性

```
dom.addEventListener('touchstart',function(e){
    console.log(e.targetTouches); //目标元素的所有当前触摸
    console.log(e.changedTouches);//最新更改的所有触摸
    console.log(e.touches);//所有的触摸
})
```

