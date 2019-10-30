## 解决npm被墙的问题

`npm`的存储包文件的服务器存储在国外，有时候会被墙

` https://npm.taobao.org/ `淘宝团队把`npm`在国外做了一个备份

安装淘宝`cnpm`

命令行下运行如下代码：

```
任意目录下执行均可
npm install --global cnpm
```

这时

```
npm install jquery  //--走国外
npm install jquery  //--通过淘宝的服务器下载
```

也可以执行以下命令安装cnpm

`npm install -g cnpm --registry=https://registry.npm.taobao.org`

## 不行安装cnpm还想用淘宝的服务器

```
npm install -jquery --registry=https://registry.npm.taobao.org`
```

但这样每次手动添加参数会很麻烦，所以我们可以把这个选项中加入到配置文件中

```
npm config set registry https://registry.npm.taobao.org 
```

经过了上面的配置后，以后所有的`npm install `都会通过淘宝的服务器下载下来

## nodejs 自动重启工具

开启服务时，每一次保存不用`Ctrl+c`,然后执行`node app.js`,没保存一次，

node自动重启一次

```
npm install -g nodemon
```

