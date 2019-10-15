# Node.js-3

## 知识点

* Express
* 基于文件做一套 CRUD

* jQuery 的 each 和 原生的 JavaScript 方法 forEach

* 301 和 302 的区别

* 模块中导出单个成员和导出多个成员的方式
  * `module.exports = xxx`
  * 通过多次：`exports.xxx = xxx`
  * 导出多个也可以：`moudle.exports = {多个成员}`
* module.exports 和 exports 的区别
  * exports 只是 module.exports 的一个引用而已，目的只是为了简化写法
  * 每个模块最终 return 的是 module.exports
* require 方法加载规则
  * 优先从缓存加载
  * 核心模块
  * 路径形式的模块
    * `./xxx`
    * `../xxxx`
    * `/xxxx` / 在这里表示的是磁盘根路径
    * `c:/xxx`
  * 第三方模块
    * 第三方模块的标识就是第三方模块的名称（不可能有第三方模块和核心模块的名字一致）
    * npm
      * 开发人员可以把写好的框架、库发布到 npm 上
      * 使用者在使用的时候就可以很方便的通过 npm 来下载
    * 使用方式：`var 名字 = require('npm install 的那个包名')`
    * node\_modules
    * node\_modules/express
    * node\_modules/express/package.json
    * node\_modules/express/package.json main
    * 如果 package.json 或者 package.json main 不成立，则查找备选项：index.js
    * 如果以上条件都不成立，则继续进入上一级目录中的 node\_modules 按照上面的规则继续查找
    * 如果直到当前文件模块所属磁盘根目录都找不到，最后报错：`can not find module xxx`
* package.json 包描述文件
  * 就是产品的说明书
  * `dependencies` 属性，用来保存项目的第三方包依赖项信息
  * 所以建议每个项目都要有且只有一个 package.json \(存放在项目的根目录\)
  * 我们可以通过 `npm init [--yes]` 来生成 package.json 文件
  * 同样的，为了保存依赖项信息，我们每次安装第三方包的时候都要加上：`--save` 选项。
* npm 常用命令
  * install
  * uninstall
* Express 基本使用

* 文件路径中的 `/` 和模块标识中的 `/`

* nodemon

* Express
  * art-template 模板引擎的配置
  * body-parser 解析表单 POST 请求体
* 技术只是一种解决问题的手段、工具而已
  * 第三方的东西，不要纠结
  * 先以解决问题为主
* 详解了 express 静态服务 API
  * app.use\('/public/', express.static\('./public'\)\)
* crud

## 目标

* 文件路径中的 `/` 和模块标识中的 `/`
* Express 中配置使用 art-template 模板引擎
* Express 中配置使用 body-parser
* Express 中配置处理静态资源
* CRUD 案例中单独提取路由模块



