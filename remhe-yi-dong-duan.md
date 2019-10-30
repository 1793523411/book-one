## rem适配

1、设置`<meta name="viewport" content="width=device-width, initial-scale=1">`

2. 设置页面元素宽度单位为 rem 或 em

注：此方案比较灵活，我们的案例将采用这种方案

### 关于em和rem

em 相对长度单位，其参照当前元素字号大小，如果当前元素未设置字号则会继承其祖先元素字号大小 例如 .box {font-size: 16px;} 则 1em = 16px .box {font-size: 32px;} 则 1em = 32px，0.5em = 16px 

```css
html {
			font-size: 16px;
		}

		body {
			padding: 0;
			margin: 0;
			background-color: #F7F7F7;
			font-size: 62.5%;
			/*10 / 16 = 0.625*/
		}

		/*em 是一个相对长度单位，参照的是当前元素的字号的px长度*/
		
		.box {
			font-size: 16px;
		}

		span {
			display: block;
			width: 20em;
			height: 20em;
			background: pink;
			font-size: 12px;
		}
		
		/**/
```

rem 相对长度单位，其参照根元素(html)字号大小 例如 html {font-size: 16px;} 则 1rem = 16px html {font-size: 32px;} 则 1rem = 32px，0.5rem = 16px;  注：所有浏览器默认字号都是16px（某些安卓手机可以调置系统字号后，浏览器默认字号会受影响）

```css
	body {
			padding: 0;
			margin: 0;
			background-color: #F7F7F7;
		}
	
		/*rem也是一个相对的长度单位，参照的是html根元素的字号*/

		/*rem使用比较灵活*/
		
		.box {
			width: 10rem;
			height: 10rem;
			background-color: pink;
			font-size: 20px;
		}
```

## 媒体查询

设备终端的多样化，直接导致了网页的运行环境变的越来越复杂，为了能够保证我们的网页可以适应多个终端，不得不专门为某些特定的设备设计不同的展示风格，要实现这个目标的前提是必须有能力了解当前网页是运行什么终端设备，通过媒体查询可以做到这一点

### 媒体类型

可以通过媒体类型对不同的设备指定不同的样式，一般我们使用screen

| 值     | 描述                             |
| ------ | -------------------------------- |
| all    | 用于所有设备                     |
| print  | 用于打印机，打印预览             |
| screen | 用于电脑屏幕，平板设备，智能手机 |



### 媒体特性

略

### 关键字

1、and 可以将多个媒体特性连接到一起，相当于“且”的意思。

2、not 排除某个媒体类型，相当于“非”的意思，可以省略。

3、only指定某个特定的媒体类型，可以省略。

### 引入方式

1、link方法，见代码示例

`<link href="./3-1.css" media="only screen and (max-width: 320px)">`

2、@media方法（写在CSS里），见代码示例

### 常用特性

1、width / height 完全等于layout viewport，见代码示例3-3.html

2、max-width / max-height 小于等于layout viewport，见代码示例3-4.html

3、min-width / min-height 大于等于layout viewport，见代码示例3-5.html

4、device-width / device-height 完全等于ideal viewport，见代码示例3-6.html

5、orientation: portrait | landscape 肖像/全景模式，见代码示例3-7.html

[.....还有其它](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Media_queries)

```css
<!-- <meta name="viewport" content="width=device-width"> -->
	<style>
		/*width height max-width max-height 检测视口宽度*/
		/*@media only screen and (max-width: 980px) {
			html {
				background-color: pink;
			}
		}*/

		@media only screen and (device-width: 320px) {
			body {
				background-color: pink;
			}
		}
```

```css
body {
			padding: 0;
			margin: 0
		}

		/* orientation: portrait | landscape */
		/* 横/坚屏 */
		
		/* 肖像（坚屏）模式 */
		@media only screen and (orientation: portrait) {
			body {
				background-color: blue;
			}
		}
		
		/* 全景（横屏）模式 */
		@media screen and (orientation: landscape) {
			body {
				background-color: red;
			}
		}
```



