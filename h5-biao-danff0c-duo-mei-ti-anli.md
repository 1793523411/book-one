### 表单类型

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        form{
            width: 100%;
            /* 最大宽度*/
            max-width: 640px;
            /* 最小宽度*/
            min-width: 320px;
            margin:0 auto;
            font-family: "Microsoft Yahei";
            font-size: 20px;
        }

        input{
            display: block;
            width: 100%;
            height:30px;
            margin:10px 0;
        }
    </style>
</head>
<body>
    <!-- type：表单的类型-->
    <!--<input type="file" />-->
    <form action="">
        <fieldset>
            <legend>表单属性</legend>

            <label for="">
                email: <input type="email" name="email" id=""/>
            </label>

            <label for="">
                url: <input type="url" name="url" />
            </label>

            <label for="">
                number: <input type="number" name="number" step="3" />
            </label>

            <label for="">
                tel: <input type="tel" name="tel" />
            </label>

            <label for="">
                search: <input type="search" name="search" />
            </label>

            <label for="">
                range: <input type="range" name="range" value="100" min="0" max="300"/>
            </label>

            <label for="">
            color: <input type="color" name="color" />
            </label>

            <label for="">
                time: <input type="time" name="time" />
            </label>

            <label for="">
                date: <input type="date" name="date" />
            </label>

            <label for="">
                month: <input type="month" name="month" />
            </label>

            <label for="">
                week: <input type="week" name="week" />
            </label>




            <input type="submit" value="提交"/>
        </fieldset>
    </form>
</body>
</html>
```

### 下拉列表

```
 <select >
        <option>选项1</option>
        <option>选项1</option>
        <option>选项1</option>
        <option>选项1</option>
    </select>
    <br/><br/><br/>
    <!--  一个普通的输入框-->
    <input type="text" list="car" />

    <!--数据列表标签-->
    <datalist id="car">
        <option>宝马</option>
        <option>宝骏</option>
        <option>宝强</option>
        <option>宝宝</option>
        <option>奥迪</option>
        <option>奥迪奥</option>
        <option>迪奥</option>
    </datalist>
```

### 表单元素

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        form{
            width: 100%;
            /* 最大宽度*/
            max-width: 640px;
            /* 最小宽度*/
            min-width: 320px;
            margin:0 auto;
            font-family: "Microsoft Yahei";
            font-size: 20px;
        }

        input,meter,progress{
            display: block;
            width: 100%;
            height:30px;
            margin:10px 0;
        }
    </style>
</head>
<body>
    <form action="">
        <fieldset>
            <legend>表单元素</legend>
            <label>
                用户名：<input type="text" name="userName" />
            </label>

            <label>
                密码：<input type="password" name="pwd" />
            </label>
            <label >
                性别：<input type="text" name="sex" list="sex" />
            </label>

            <!-- 定义数据列表-->
            <datalist id="sex">
                <option >男</option>
                <option >女</option>
                <option >不祥</option>
            </datalist>

            <label for="">
                推荐人：<output>春哥</output>
            </label>
            <br/><br/>
            <label for="">
                加密类型： <keygen/>
            </label>
            <br/><br/>
            <label for="#">
                度量器：<meter value="80" max="100" min="0" low="30" high="80"></meter>
            </label>
            <!-- 进度条-->
            <progress value="40" max="100" min="0"></progress>
            <input type="submit" value="提交"/>
        </fieldset>
    </form>
</body>
</html>
```

### 表单属性

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        form{
            width: 100%;
            /* 最大宽度*/
            max-width: 640px;
            /* 最小宽度*/
            min-width: 320px;
            margin:0 auto;
            font-family: "Microsoft Yahei";
            font-size: 20px;
        }

        input{
            display: block;
            width: 100%;
            height:30px;
            margin:10px 0;
        }
    </style>
</head>
<body>
    <!--&lt;!&ndash; 表单新增属性&ndash;&gt;-->
    <!--<input type="text" class="name" />-->
    <!--
        placeholder:提示文字（占位符）
        autofocus:自动获取焦点
        autocomplete: 自动完成（填充的） on 开启（默认）  off 取消自动提示
        required: 必填
        multiple: 多选
        novalidate:关闭默认的验证功能（只能加给form）
        pattern: 自定义正则验证
        pattern="1\d{10}"
    -->
    <!--<form action="" novalidate>-->
    <form action="" >
        <fieldset>
            <legend>表单属性</legend>
            <label for="">
                用户名：<input type="text" placeholder="例如：李狗蛋" autofocus name="userName" autocomplete="on" required/>
            </label>

            <label for="">
                电话：<input type="tel" pattern="1\d{10}" />
            </label>

            <!-- 上次文件-->
            <input type="file" name="file" multiple/>

            <input type="submit" />
        </fieldset>
    </form>

</body>
</html>
```

### 表单事件

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        form{
            width: 100%;
            /* 最大宽度*/
            max-width: 640px;
            /* 最小宽度*/
            min-width: 320px;
            margin:0 auto;
            font-family: "Microsoft Yahei";
            font-size: 20px;
        }

        input{
            display: block;
            width: 100%;
            height:30px;
            margin:10px 0;
        }
    </style>
</head>
<body>
<form action="">
    <fieldset>
        <legend>表单事件</legend>
        <label for="">
            邮箱：<input type="email" name="" id="txt1"/>
        </label>
        <label for="">
            密码：<input type="text" name="" id="txt2"/>
        </label>

        <input type="submit" />
    </fieldset>
</form>
<script>
    //表单事件： oninput　当用户输入的时候
//        oninvalid 当验证不通过是触发
    var  txt1=document.getElementById('txt1');
    var  txt2=document.getElementById('txt2');
    var num=0;

    txt1.oninput=function(){
        num++;
//         将字数显示在txt2中
        txt2.value=num;
    }
//    oninvalid 当验证不通过是触发
//    一般用于设置验证不通过时的 提示文字
    txt1.oninvalid=function(){
//        用于设置验证不通过时的 提示文字
         this.setCustomValidity('亲，请输入正确的邮箱格式！');
    }

</script>
</body>
</html>
```

### 自己控制多媒体的进度条的样式

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <!-- 引入字体图标的文件-->
    <link rel="stylesheet" href="css/font-awesome.min.css"/>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        /*多媒体标题*/
        figcaption{
            text-align: center;
            line-height: 150px;
            font-family: "Microsoft Yahei";
            font-size:24px;
        }

        /* 播放器*/
        .palyer{
            width: 720px;
            height: 360px;
            margin:10px auto;
            border: 1px solid #000;
            background: url(images/loading.gif) center no-repeat #000;
            background-size:auto 100%;
            position: relative;
            border-radius: 20px;

        }

        .palyer video{
            height:100%;
            display: block;
            margin:0 auto;
            /*display: none;*/
        }

        /* 控制条*/

        .controls{
            width: 700px;
            height:40px;
            background-color: rgba(255, 255, 0, 0.3);
            position: absolute;
            bottom:10px;
            left:10px;
            border-radius: 10px;
        }
        /*开关*/
        .switch{
            position: absolute;
            width: 20px;
            height: 20px;
            left:10px;
            top:10px;

            text-align: center;
            line-height: 20px;
            color:yellow;

        }
        /*进度条*/
        .progress{
            width: 432px;
            height: 10px;
            position: absolute;
            background-color: rgba(255,255,255,0.4);
            left:40px;
            top:15px;
            border-radius: 4px;
            overflow: hidden;
        }
        /* 当前进度*/
        .curr-progress{
            width: 50%;
            height: 10px;
            background-color: #fff;
        }
        /* 时间模块*/
        .time{
            width: 120px;
            height: 20px;
            text-align: center;
            line-height: 20px;
            color:#fff;
            position: absolute;
            left:510px;
            top:10px;
            font-size:12px;

        }
        /*全屏*/
        .extend{
            position: absolute;
            width: 20px;
            height: 20px;

            right:20px;
            top:10px;

            text-align: center;
            line-height: 20px;
            color:yellow;
        }

    </style>
</head>
<body>
    <!-- 多媒体-->
    <figure>
        <!--  多媒体标题-->
        <figcaption>视频案例</figcaption>
        <div class="palyer">
            <video src="video/fun.mp4"></video>
            <!-- 控制条-->
            <div class="controls">
                <!-- 播放暂停-->
                <a href="#" class="switch  icon-play"></a>
                <div class="progress">
                    <!-- 当前进度-->
                    <div class="curr-progress"></div>
                </div>
                <!-- 时间-->
                <div class="time">
                    <span class="curr-time">00:00:00</span>/<span class="total-time">00:00:00</span>
                </div>
                <!-- 全屏-->
                <a href="#" class="extend  icon-resize-full"></a>
            </div>

        </div>
    </figure>

    <script>
        // 思路：
        /*
        * 1、点击按钮 实现播放暂停并且切换图标
        * 2、算出视频的总时显示出出来
        * 3、当视频播放的时候，进度条同步，当前时间同步
        * 4、点击实现全屏
        */

//        获取需要的标签
            var  video=document.querySelector('video');
//          播放按钮
            var  playBtn=document.querySelector('.switch');
//          当前进度条
            var  currProgress=document.querySelector('.curr-progress');
//          当前时间
            var  currTime=document.querySelector('.curr-time');
//          总时间
            var  totalTime=document.querySelector('.total-time');
//          全屏
            var extend=document.querySelector('.extend');

            var tTime=0;

//         1、点击按钮 实现播放暂停并且切换图标

           playBtn.onclick=function(){
//               如果视频播放 就暂停，如果暂停 就播放
               if(video.paused){
//                   播放
                   video.play();
                   //切换图标
                   this.classList.remove('icon-play');
                   this.classList.add('icon-pause');
               }else{
//                   暂停
                    video.pause();
//                   切换图标
                   this.classList.remove('icon-pause');
                   this.classList.add('icon-play');}
           }

//        2、算出视频的总时显示出出来
//        当时加载完成后的事件，视频能播放的时候
        video.oncanplay=function(){
//             获取视频总时长
            tTime=video.duration;
            console.log(tTime);

//          将总秒数 转换成 时分秒的格式：00：00:00
//            小时
            var h=Math.floor(tTime/3600);
//            分钟
            var m=Math.floor(tTime%3600/60);
//            秒
            var s=Math.floor(tTime%60);

//            console.log(h);
//            console.log(m);
//            console.log(s);

//            把数据格式转成 00:00：00
            h=h>=10?h:"0"+h;
            m=m>=10?m:"0"+m;
            s=s>=10?s:"0"+s;


            console.log(h);
            console.log(m);
            console.log(s);
//            显示出来
            totalTime.innerHTML=h+":"+m+":"+s;
        }
//   * 3、当视频播放的时候，进度条同步，当前时间同步
//         当时当前时间更新的时候触发
        video.ontimeupdate=function(){
//            获取视频当前播放的时间
//           console.log(video.currentTime);
//            当前播放时间
            var cTime=video.currentTime;
//           把格式转成00:00:00

            var h=Math.floor(cTime/3600);
//            分钟
            var m=Math.floor(cTime%3600/60);
//            秒
            var s=Math.floor(cTime%60);

//            把数据格式转成 00:00：00
            h=h>=10?h:"0"+h;
            m=m>=10?m:"0"+m;
            s=s>=10?s:"0"+s;

//            显示出当前时间
            currTime.innerHTML=h+":"+m+":"+s;

//            改变进度条的宽度： 当前时间/总时间
            var value=cTime/tTime;

            currProgress.style.width=value*100+"%";

        }

//        全屏
        extend.onclick=function(){
//            全屏的h5代码
            video.webkitRequestFullScreen();
        }

    </script>
</body>
</html>
```



