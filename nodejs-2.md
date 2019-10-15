# Node.js-2

## 第零部分

### 代码风格

```javascript
var foo = 'bar'
var foo ='bar'
var foo= 'bar'
var foo = "bar"

if (true) {
  console.log('hello') 
}

if (true) {
    console.log('hello') 
}

if (true ){
      console.log('hello') 
}
```

为了约定大家的代码风格，所以在社区中诞生了一些比较规范的代码风格规范：dnsajkndkjsabnjkdnjksandjknsajkdnjkasnjkdnjksandjknsajkdnjksajkdnas

- [JavaScript Standard Style](https://standardjs.com/)
- Airbnb JavaScript Style

### 渲染

- 代码风格
- 服务端渲染
  + 说白了就是在服务端使用模板引擎
  + 模板引擎最早诞生于服务端，后来才发展到了前端

- 服务端渲染和客户端渲染的区别
  + 客户端渲染不利于 SEO 搜索引擎优化
  + 服务端渲染是可以被爬虫抓取到的，客户端异步渲染是很难被爬虫抓取到的
  + 所以你会发现真正的网站既不是纯异步也不是纯服务端渲染出来的
  + 而是两者结合来做的
  + 例如京东的商品列表就采用的是服务端渲染，目的了为了 SEO 搜索引擎优化
  + 而它的商品评论列表为了用户体验，而且也不需要 SEO 优化，所以采用是客户端渲染



## 第一部分

- 模块系统
  + 核心模块
  + 第三方模块
  + 自己写的模块
  + 加载规则以及加载机制
  + 循环加载
- npm
- package.json
- Express
  + 第三方 Web 开发框架
  + 高度封装了 http 模块
  + 更加专注于业务，而非底层细节
- 增删改查
  + 使用文件来保存数据（锻炼异步编码）
- MongoDB
  + （所有方法都封装好了）

## 第二部分

- seo的资料，嘿嘿
  + 网站运营 SEO
  + SEO 运营专员
  + 百度、Google、搜狗、

- art-template与jQuery
  + art-template 和 jQuery 一毛钱关系都没有
  + each 是 art-template 的模板语法，专属的
  + `{{each 数组}}`
  + `<li>{{ $value }}</li>`
  + `{{/each}}` 这是 art-template 模板引擎支持的语法，只能在模板字符串中使用
  + $.each(数组, function)
  + $('div').each(function) 一般用于遍历 jQuery 选择器选择到的伪数组实例对象
  + forEach 是 EcmaScript 5 中的一个数组遍历函数，是 JavaScript 原生支持的遍历方法 可以遍历任何可以被遍历的成员
  + jQuery 的 each 方法和 forEach 几乎一致
  + 由于 forEach 是 EcmaScript 5 中的，所以低版本浏览器不支持

- 如果从a中调用b中的数据，又从b中调用a中的数据，执行a代码，为什么把b中的执行完后才会执行a，而不是在b调用a的时候a中的代码继续执行
  + a 加载了 b
    * 执行 b 中的代码
    * 同时得到 b 中导出的接口对象：exports
    * 执行 b 的过程中发现 b 也在 require a
    * b 就会反过来执行 a
    * a 中又加载 b
    * b 又反过来加载 a
    * 这就是循环加载
    * 如果你一旦出现了这种情况，说明你的思路有问题。
    * jQuery.js （可能不可能出现 jQuery 依赖了 main）
    * main.js 依赖了 jQuery
    * 这个问题是矛盾。
  + b 中也加载了 a
  + 
  + 网页中所有的路径其实都是 url 路径，不是文件路径

## 第三部分

- 网站开发模型
  + 黑盒子、哑巴
  + 写代码让它变得更智能
  + 按照你设计好的套路供用户使用

- 在 Node 中使用 art-template 模板引擎
  + 安装
  + 加载
  + template.render()
- 客户端渲染和服务端渲染的区别
  + 最少两次请求，发起 ajax 在客户端使用模板引擎渲染
  + 客户端拿到的就是服务端已经渲染好的
- 处理留言本案例首页数据列表渲染展示
- 处理留言本案例发表留言功能
  + 路径
  + 设计好的请求路径
  + $GET 直接或查询字符串数据
  + Node 中需要咱们自己动手来解析
    * url.parse()
  + /pinglun?name=jack&message=hello
  + split('?')
  + name=jack&message=hello
  + split('&')
  + name=jack message=hello
  + forEach()
  + name=jack.split('=')
  + 0 key
  + 1 value
- 掌握如何解析请求路径中的查询字符串
  + url.parse()
- 如何在 Node 中实现服务器重定向
  + header('location')
    * 301 永久重定向 浏览器会记住
      - a.com b.com
      - a 浏览器不会请求 a 了
      - 直接去跳到 b 了
    * 302 临时重定向 浏览器不记忆
      - a.com b.com
      - a.com 还会请求 a
      - a 告诉浏览器你往 b
- Node 中的 Console（REPL）使用

## 第四部分

- jQuery 的 each 和 原生的 JavaScript 方法 forEach
  + EcmaScript 5 提供的
    * 不兼容 IE 8
  + jQuery 的 each 由 jQuery 这个第三方库提供
    * jQuery 2 以下的版本是兼容 IE 8 的
    * 它的 each 方法主要用来遍历 jQuery 实例对象（伪数组）
    * 同时它也可以作为低版本浏览器中 forEach 替代品
    * jQuery 的实例对象不能使用 forEach 方法，如果想要使用必须转为数组才可以使用
    * `[].slice.call(jQuery实例对象)`
- 模块中导出多个成员和导出单个成员
- 301 和 302 状态码区别
  + 301 永久重定向，浏览器会记住
  + 302 临时重定向
- exports 和 module.exports 的区别
  + 每个模块中都有一个 module 对象
  + module 对象中有一个 exports 对象
  + 我们可以把需要导出的成员都挂载到 module.exports 接口对象中
  + 也就是：`moudle.exports.xxx = xxx` 的方式
  + 但是每次都 `moudle.exports.xxx = xxx` 很麻烦，点儿的太多了
  + 所以 Node 为了你方便，同时在每一个模块中都提供了一个成员叫：`exports`
  + `exports === module.exports` 结果为  `true`s
  + 所以对于：`moudle.exports.xxx = xxx` 的方式 完全可以：`expots.xxx = xxx`
  + 当一个模块需要导出单个成员的时候，这个时候必须使用：`module.exports = xxx` 的方式
  + 不要使用 `exports = xxx` 不管用
  + 因为每个模块最终向外 `return` 的是 `module.exports`
  + 而 `exports` 只是 `module.exports` 的一个引用
  + 所以即便你为 `exports = xx` 重新赋值，也不会影响 `module.exports`
  + 但是有一种赋值方式比较特殊：`exports = module.exports` 这个用来重新建立引用关系的
- Node 是一个比肩 Java、PHP 的一个平台
  + JavaScript 既能写前端也能写服务端

```javascript
moudle.exports = {
  a: 123
}

// 重新建立 exports 和 module.exports 之间的引用关系
exports = module.exports

exports.foo = 'bar'
```

```javascript
Array.prototype.mySlice = function () {
  var start = 0
  var end = this.length
  if (arguments.length === 1) {
    start = arguments[0]
  } else if (arguments.length === 2) {
    start = arguments[0]
    end = arguments[1]
  }
  var tmp = []
  for (var i = start; i < end; i++) {
    // fakeArr[0]
    // fakeArr[1]
    // fakeArr[2]
    tmp.push(this[i])
  }
  return tmp
}

var fakeArr = {
  0: 'abc',
  1: 'efg',
  2: 'haha',
  length: 3
}

// 所以你就得到了真正的数组。 
[].mySlice.call(fakeArr)
```

## 第五部分

- jQuery 的 each 和 原生的 JavaScript 方法 forEach
- 301 和 302 的区别
- 模块中导出单个成员和导出多个成员的方式
- module.exports 和 exports 的区别
- require 方法加载规则
  + 优先从缓存加载
  + 核心模块
  + 路径形式的模块
  + 第三方模块
    * node_modules
- package.json 包描述文件
  + dependencies 选项的作用
- npm 常用命令
- Express 基本使用

