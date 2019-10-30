## css预处理器

CSS 预处理器是一种语言，用来为 CSS 增加一些编程的的特性，无需考虑浏览器的兼容性问题，并且你可以在 CSS 中使用变量、简单的程序逻辑、函数等等在编程语言中的一些基本技巧，可以让你的 CSS 更简洁，适应性更强，代码更直观等诸多好处。

常见的CSS预处理器有：LESS、SASS、Stylus等

其使用方法大致相同，我们在这里以LESS

## less

### 安装

1、安装Nodejs环境 Node Package Manager (验证 node -v npm -v)

2、打开控制台（cmd），执行`npm install -g less (验证 lessc -v)`

3、执行` npm install -g less-plugin-clean-css`

4、命令行编译 `lessc path/xxx.less path/xxx.css`

更多less[看官网](http://lesscss.cn/#download-options)

##  浏览器中使用

我们可以引入一个less.js文件，实现实时的解析，而不必每次修改都要编译，最后完成所有开发任务后，再通过编辑器编译成css文件。

1、[下载](https://raw.github.com/less/less.js/v2.5.3/dist/less.min.js)然后引入less.js

2、引入xx.less文件，如：

`<link rel="stylesheet/less" type="text/css" href="styles.less" />`

注意：rel属性必须指定成stylesheet/less，并且styles.less要先于less.js引入。

必须以服务器方式访问，可以放到study目录下，或者webstrom自带服务器功能