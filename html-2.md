### web存储

随着互联网的快速发展，基于网页的应用越来越普遍，同时也变的越来越复杂，为了满足各种各样的需求，会经常性在本地存储大量的数据，传统方式我们以document.cookie来进行存储的，但是由于其存储大小只有4k左右，并且解析也相当的复杂，给开发带来诸多不便，HTML5规范则提出解决方案

Storage 存储

```
window.sessionStorage(浏览器存储)
```

```
window.localStorage（本地存储）
```

\(向本地保存数据,有可能在浏览器内存里面，有可能在硬盘上面.\)

##### 特性

1、设置、读取方便  
2、容量较大，sessionStorage约5M、localStorage约20M  
3、只能存储字符串，可以将对象JSON.stringify\(\) 编码后存储

##### window.sessionStorage

1、生命周期为关闭浏览器窗口  
2、在同一个窗口下数据可以共享

##### window.localStorage

1、永久生效，除非手动删除  
2、可以多窗口共享

##### 方法详解

setItem\(key, value\) 设置存储内容  
getItem\(key\) 读取存储内容  
removeItem\(key\) 删除键值为key的存储内容  
clear\(\) 清空所有存储内容  
key\(n\) 以索引值来获取存储内容

案例：记住用户名

##### 其它

WebSQL、IndexDB  
已经被w3c 放弃了..  
生命周期差异，存储空间差异  
WebSQL、IndexDB

sessionStorage

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    <input type="text" />
    <button>sesssionStorage存储</button>
    <button>sesssionStorage获取</button>
    <button>sesssionStorage更新</button>
    <button>sesssionStorage删除</button>
    <button>sesssionStorage清除</button>
    <script>

        //在h5中提供两种web存储方式

        // sessionStorage  session（会话，会议） 5M  当窗口关闭是数据销毁  内存
        // localStorage    20M 永久生效 ，除非手动删除  清理垃圾  硬盘上

        var txt=document.querySelector('input');

        var btns=document.querySelectorAll('button');
//        sessionStorage存储数据
        btns[0].onclick=function(){
            window.sessionStorage.setItem('userName',txt.value);
            window.sessionStorage.setItem('pwd','123456');
            window.sessionStorage.setItem('age',18);
        }

//        sessionStorage获取数据
        btns[1].onclick=function(){
          txt.value= window.sessionStorage.getItem('userName');
        }

//        sessionStorage更新数据
        btns[2].onclick=function(){
            window.sessionStorage.setItem('userName',txt.value);
        }

//        sessionStorage删除数据
        btns[3].onclick=function(){
            window.sessionStorage.removeItem('userName');
        }

        //        sessionStorage清空数据
        btns[4].onclick=function(){
            window.sessionStorage.clear();
        }
    </script>
</body>
</html>
```

localStorage

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    <input type="text" />
    <button>localStorage存储</button>
    <button>localStorage获取</button>
    <button>localStorage更新</button>
    <button>localStorage删除</button>
    <button>localStorage清除</button>

    <script>

        /*
        *  localStorage
        *  数据存在硬盘上
        *  永久生效
        *  20M
        * */

        var  txt=document.querySelector('input');
        var btns=document.querySelectorAll('button');

//        localStorage存储数据
        btns[0].onclick=function(){
            window.localStorage.setItem('userName',txt.value);
        }

//        localStorage存储数据
        btns[1].onclick=function(){
           txt.value= window.localStorage.getItem('userName');
        }

        btns[3].onclick=function(){
            window.localStorage.removeItem('userName');
        }

    </script>
</body>
</html>
```

### 地理定位

在HTML规范中，增加了获取用户地理信息的API，这样使得我们可以基于用户位置开发互联网应用，即基于位置服务 \(Location Base Service\)  
1、IP地址  
2、三维坐标  
    GPS（Global Positioning System，全球定位系统）  
  目前世界上在用或在建的第2代全球卫星导航系统（GNSS）有：1.美国 Global Positioning System （全球定位系统） 简称GPS；.2.苏联/俄罗斯 GLOBAL NAVIGATION SATELLITE SYSTEM （全球卫星导航系统）简称GLONASS（格洛纳斯）；3.欧盟（欧洲是不准确的说法，包括中国在内的诸多国家也参与其中）Galileo satellite navigation system（伽利略卫星导航系统） 简称GALILEO（伽利略）；4.中国 BeiDou\(COMPASS\) Navigation Satellite System（北斗卫星导航系统）简称 BDS ；5.日本 Quasi-Zenith Satellite System （准天顶卫星系统） 简称QZSS ；印度 India Regional Navigation Satellite System（印度区域卫星导航系统）简称IRNSS；以上6个系统中国都能使用。  
    Wi-Fi  
    手机信号  
3、用户自定义数据  
如下图对不同获取方式的优缺点进行了比较，浏览器会自动以最优方式去获取用户地理信息。  
![](/assets/1.png)

[使用可以查看](http://lbsyun.baidu.com/index.php?title=jspopular3.0)

HTML5 Geolocation\(地理位置定位\)规范提供了一套保护用户隐私的机制。必须先得到用户明确许可，才能获取用户的位置信息

`navigator.getCurrentPosition\(successCallback, errorCallback, options\)`获取当前地理信息

`navigator.watchPosition\(successCallback, errorCallback, options\)`重复获取当前地理信息

1、当成功获取地理信息后，会调用succssCallback，并返回一个包含位置信息的对象position。Coords\(坐标\)

`position.coords.latitude`纬度

`position.coords.longitude`经度

2、当获取地理信息失败后，会调用errorCallback，并返回错误信息error

3、可选参数options对象可以调整位置信息数据收集方式

百度地图

### 网络状态

我们可以通过`window.onLine`来检测，用户当前的网络状况，返回一个布尔值  
   `window.online`用户网络连接时被调用  
   `window.offline`用户网络断开时被调用

```
<script>
    window.addEventListener('online',function(){
       alert('网络连接已建立！');
    });

    window.addEventListener('offline',function(){
        alert('网络连接已断开！');
    })
</script>
```

### 应用程序缓存

#### 优势

1、可配置需要缓存的资源  
2、网络无连接应用仍可用  
3、本地读取缓存资源，提升访问速度，增强用户体验  
4、减少请求，缓解服务器负担

#### 缓存清单

一个普通文本文件，其中列出了浏览器应缓存以供离线访问的资源，推荐使用.appcache为后缀名，添加MIME类型  
AddType text/cache-manifest .appcache  
例如我们创建了一个名为demo.appcache的文件，然后在需要应用缓存在页面的根元素\(html\)添加属性manifest="demo.appcache"，路径要保证正确。

#### manifest文件格式

1、顶行写CACHE MANIFEST  
2、CACHE: 换行 指定我们需要缓存的静态资源，如.css、image、js等  
3、NETWORK: 换行 指定需要在线访问的资源，可使用通配符  
4、FALLBACK: 当前页面无法访问时退回的页面\(回退;  后退\)  
 换行 当被缓存的文件找不到时的备用资源 可自行查阅资料

#### 其他

1、CACHE: 可以省略，这种情况下将需要缓存的资源写在CACHE MANIFEST  
2、可以指定多个CACHE: NETWORK: FALLBACK:，无顺序限制

CACHE:需要缓存那些资源.  
NETWORK:不需要缓存那些资源，必须在网络下面才能访问.  
FALLBACK:当访问不到某个资源时，自动由另外一个资源替换.  
CACHE MANIFEST

CACHE:  
   此部分是需要缓存的资源  
   1.jpg  
   js/jquery.min.js

NETWORK:  
   js/demo.js

```
# 可以使用 * 好替代
FALLBACK:
one.css two.css    会缓存two.css 当找不到one.css 会去找two.css 文件.
```

3、\#表示注释，只有当demo.appcache文件内容发生改变时或者手动清除缓存后，才会重新缓存。  
4、chrome 可以通过chrome://appcache-internals/工具和离线（offline）模式来调试管理应用缓存

![](/assets/2.png)

```
<<!DOCTYPE html>
<html manifest="01.appcache">
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<img src="https://pics4.baidu.com/feed/fc1f4134970a304eca032cbd7e46f883c8175cec.jpeg?token=f670fd861109be52106b566bfc5fae4e&s=7710798F5683BEB8103CADDB0300C093" alt=""/>
</body>
</html>
```

```
<!DOCTYPE html>
<html manifest="02.appcache">
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<img src="images/img1.jpg" alt=""/>
<img src="images/img2.jpg" alt=""/>
<img src="images/img3.jpg" alt=""/>
<img src="images/img4.jpg" alt=""/>
</body>
</html>
```

01.appcache文件

```
CACHE MANIFEST

# 注锟斤拷锟斤拷#锟斤拷头
#锟斤拷锟斤拷锟斤拷要锟斤拷锟斤拷锟斤拷募锟?
CACHE:
    https://pics4.baidu.com/feed/fc1f4134970a304eca032cbd7e46f883c8175cec.jpeg?token=f670fd861109be52106b566bfc5fae4e&s=7710798F5683BEB8103CADDB0300C093
```

02.appcache

```
CACHE MANIFEST

#要缓存的文件
CACHE:
    images/img1.jpg
    images/img2.jpg


#指定必须联网才能访问的文件
NETWORK:
     images/img3.jpg
     images/img4.jpg


#当前页面无法访问是回退的页面
FALLBACK:
    404.html
```

#### 全屏

HTML5规范允许用户自定义网页上任一元素全屏显示。  
 `requestFullscreen()` 开启全屏显示  
 `cancleFullscreen()` 关闭全屏显示  
不同浏览器需要添加前缀如：  
 `webkitRequestFullScreen、mozRequestFullScreen`  
 `webkitCancleFullScreen、mozCancleFullScreen`  
 通过`document.fullScreen`检测当前是否处于全屏  
 不同浏览器需要添加前缀  
    `document.webkitIsFullScreen、document.mozFullScreen`  
全屏伪类

```
:full-screen .box {}、:-webkit-full-screen {}、:moz-full-screen {}
var docElm = document.documentElement;
    if (docElm.requestFullscreen) {
       docElm.requestFullscreen();
    }
    else if (docElm.mozRequestFullScreen) {
       docElm.mozRequestFullScreen();
    }
    else if (docElm.webkitRequestFullScreen) {
       docElm.webkitRequestFullScreen();
    }
```



