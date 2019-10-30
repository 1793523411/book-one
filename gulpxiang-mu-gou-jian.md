# gulp项目构建
多个开发者共同开发一个项目，每位开发者负责不同的模块，这就会造成一个完整的项目实际上是由许多的“代码版段”组成的；
使用less、sass等一些预处理程序，降低CSS的维护成本，最终需要将这些预处理程序进行解析；
合并css、javascript，压缩html、css、javascript、images可以加速网页打开速度，提升性能；
这一系列的任务完全靠手动完成几乎是不可能的，借助构建工具可以轻松实现。
所谓构建工具是指通过简单配置就可以帮我们实现合并、压缩、校验、预处理等一系列任务的软件工具。
常见的构建工具包括：Grunt、Gulp、F.I.S（百度出品）、webpack
## Gulp
Gulp是基于Nodejs开发的一个构建工具，借助gulp插件可以实现不同的构建任务，以其简洁的配置和卓越的性能成为目前主流的构建工具。
全局安装 `npm install -g gulp`

### Gulp基础
1、本地安装gulp 
进入项目根目录执行`npm install gulp --save-dev`（添加--save-dev会在package.json记录依赖关系）。
2、任务清单
在项目根目录中创建`gulpfile.js`（这是一个配置文件）

```javascript
var gulp = require('gulp');
gulp.task('default',function(){
    //定义任务
})
```



3、定义任务
在`gulpfile.js`定义构建任务，如压缩、合并，Gulp自身并不执行任何任务，是通过调用具体插件来完成的。
以编译LESS为例，安装`npm install gulp-less`，如下图定义任务

```javascript
var gulp = require('gulp'),
    less = require('gulp-less');
gulp.task('less',function(){
    return gulp,src('./public.less/*.less')
    	.pipe(less())
    	.pipe(gulp.desk('./public/css'));
});
```



4、执行任务
输入命令 gulp less

```shell
gulp less
```



这样我们的LESS文件便会编译成CSS了。
### Gulp工作原理

通过不同的插件实现构建任务，Gulp只是按着配置文件调用执行了这些插件。
### Gulp API
Gulp是基于NodeJS的，通过require可以引入一个NodeJS的包（模块），其作用类似于浏览器中的script标签引入资源，被引入的包存放在node_modules目录下。
引入gulp包（模块）后返回一个对象，习惯赋值给变量gulp，通过该对象提供的方法（API）完成任务的配置。
1、gulp.task() 定义各种不同的任务，如下图有两个参数

```javascript
gulp.task('less',function(){
    //定义人物
})
```



不同任务间存在依赖关系时，可以指定依赖，如下

```javascript
gulp.task('less',['依赖一'],['依赖二'],['依赖三'],function(){
    
})
```



2、gulp.src() 需要构建资源的路径，字符串或数组（可以正则方式书写）

```javascript
gulp.task('less',function(){
    gulp.src('./public/less/**/*.js')
});
```



2、gulp.pipe() 管道，将需要构建的资源“输送”给插件。

```javascript
gulp.task('less',function(){
    gulp.src('./public/less/**/*.js')
    	.pipe(less())
});
```



3、gulp.dest() 构建任务完成后资源存放的路径（会自动创建）

```javascript
gulp.task('less',function(){
    gulp.src('./public/less/**/*.js')
    	.pipe(less())
    	.pipe(gulp.desk('./public/css'));
});
```



4、gulp.watch() 
### 常用Gulp插件(官网还有更多)

```
gulp-less 编译LESS文件
gulp-autoprefixer 添加CSS私有前缀
gulp-cssmin 压缩CSS
gulp-rname重命名
gulp-imagemin 图片压缩
gulp-uglify 压缩Javascript
gulp-concat 合并
gulp-htmlmin 压缩HTML
gulp-rev 添加版本号
gulp-rev-collector 内容替换
gulp-useref 文件合并，文件删除
gulp-if 条件判断
```

## 完整的一个项目构建

```javascript

var gulp = require('gulp'),
	
	less = require('gulp-less'),

	cssmin = require('gulp-cssmin'),

	autoprefixer = require('gulp-autoprefixer'),

	rev = require('gulp-rev'),

	imagemin = require('gulp-imagemin'),

	useref = require('gulp-useref'),

	gulpif = require('gulp-if'),

	uglify = require('gulp-uglify'),

	rename = require('gulp-rename'),

	revCollector = require('gulp-rev-collector');

// gulp 对象，提供了若干方法

// 处理css
gulp.task('css', function () {

	return gulp.src('./public/less/main.less')
		.pipe(less())
		.pipe(cssmin())
		.pipe(autoprefixer())
		.pipe(rev())
		.pipe(gulp.dest('./release/public/css'))
		.pipe(rev.manifest())
		.pipe(rename('css-manifest.json'))
		.pipe(gulp.dest('./release/rev'));

});

// 处理图片
gulp.task('image', function () {

	return gulp.src(['./public/images/**/*', './uploads/*'], {base: './'})
		.pipe(imagemin())
		.pipe(rev())
		.pipe(gulp.dest('./release'))
		.pipe(rev.manifest())
		.pipe(rename('image-manifest.json'))
		.pipe(gulp.dest('./release/rev'));

});

// 处理js
gulp.task('useref', function () {

	return gulp.src('./index.html')
		.pipe(useref())
		.pipe(gulpif('*.js', uglify()))
		.pipe(gulpif('*.js', rev()))
		.pipe(gulp.dest('./release'))
		.pipe(rev.manifest())
		.pipe(rename('js-manifest.json'))
		.pipe(gulp.dest('./release/rev'));

});

// 其它
gulp.task('other', function () {

	return gulp.src(['./api/*', './public/fonts/*', './public/libs/*', './views/*.html'], {base: './'})//base:确定以哪个为基础路径
		.pipe(gulp.dest('./release'));

});

// 替换
gulp.task('rev', ['css', 'image', 'useref'], function () {

	gulp.src(['./release/rev/*.json', './release/index.html'])
		.pipe(revCollector())
		.pipe(gulp.dest('./release'));

});
//return用来解决依赖关系的执行时间问题
gulp.task('default', ['rev', 'other']);

// gulp.task('default', function () {
// 	console.log('默认');
// })

// gulp.task('demo', ['css', 'image'], function () {
// 	console.log(11);
// });
```



