### tab案例

```
 <style>
        body {
            margin: 0;
            padding: 0;
            background-color: #F7F7F7;
        }

        .tabs {
            width: 400px;
            margin: 30px auto;
            background-color: #FFF;
            border: 1px solid #C0DCC0;
            box-sizing: border-box;
        }

        .tabs nav {
            height: 40px;
            text-align: center;
            line-height: 40px;
            overflow: hidden;
            background-color: #C0DCC0;
            display: flex;
        }

        nav a {
            display: block;
            width: 100px;
            border-right: 1px solid #FFF;
            color: #000;
            text-decoration: none;
        }

        nav a:last-child {
            border-right: 0 none;
        }

        nav a.active {
            background-color: #9BAF9B;
        }

        .cont {
            overflow: hidden;
            display: none;
        }

        .cont ol {
            line-height: 30px;
        }
<div class="tabs">
    <nav>
        <a href="javascript:;" data-cont="local">国内新闻</a>
        <a href="javascript:;" data-cont="global">国际新闻</a>
        <a href="javascript:;" data-cont="sports">体育新闻</a>
        <a href="javascript:;" data-cont="funny">娱乐新闻</a>
    </nav>
    <section class="cont" id="local" >
        <ol>
            <li>河感在生矿难，死伤在全10</li>
            <li>禽流感在感在广1处继续蔓延，温家宝指示</li>
            <li>南方大旱，农作物减产绝收面积上亩</li>
            <li>猪流感在广在全国暴发</li>
            <li>禽流感在全国多处继续蔓延，温家宝指示</li>
            <li>南方大旱，农作物减产绝收面积上亩</li>
            <li>猪流感在广东群体性暴发</li>
        </ol>
    </section>
    <section class="cont" id="global">
        <ol>
            <li>河南再次发生矿难，死伤人数超过100</li>
            <li>禽流感次发生蔓延，温家宝指示</li>
            <li>南方大旱，农作物减产绝收面积上亩</li>
            <li>猪流感在广减产绝收发</li>
            <li>禽流感在全国多作物减产绝收面积上亩</li>
            <li>猪流感在广东群体性暴发</li>
        </ol>
    </section>
    <section class="cont" id="sports">
        <ol>
            <li>333河南再次发生矿难，死伤人数超过100</li>
            <li>禽流感在全国多处农作物农延，温家宝指示</li>
            <li>南方大旱，农作物减产绝收面积上亩</li>
            <li>猪流感在广东群体性暴发</li>
            <li>禽流感在全农作物继续蔓延，温家宝指示</li>
            <li>南方大农作物减产绝收面积上亩</li>
            <li>猪流感在广东群体性暴发</li>
        </ol>
    </section>
    <section class="cont" id="funny">
        <ol>
            <li>福建发生血腥命案:两女遭割喉 1男孩被砍数刀</li>
            <li>四川原副省长李成云被查 5年前曾违纪又复出</li>
            <li>胡歌反对粉丝探班：以前请吃饭现在会黑脸</li>
            <li>曝郑爽爸爸歌厅撩妹 与女子勾肩搭背显亲密</li>
            <li>宜宾公安副局长无证驾驶出车祸 弃车离开现场</li>
            <li>国子监大街门匾现错字 已悬挂近10年(图)</li>
            <li>猪流感在广东群体性暴发</li>
        </ol>
    </section>
</div>
<script>
    // 目标： 默认显示一个 当前的样式
    //  点击导航，实现切换
    //  key 表示的当前显示的是第几个

    (function(key){
//         获取所有的导航
        var navs=document.querySelectorAll('nav a');
//         遍历 给导航 绑定事件，并且添加当前样式
        for(var i=0;i<navs.length;i++){
//            如果是用户指定的当前样式
            if(key==i){
                navs[i].classList.add('active');
//              拿到要显示内容section的id
                var secId=navs[i].dataset['cont'];
//               获取对应的section标签
                document.querySelector('#'+secId).style.display='block';
            }

//            给每一个导航绑定点击事件
            navs[i].onclick=function(){
            // 排他
            // 之前有active样式的清除, 之前显示的section 隐藏
                var  currentNav=document.querySelector('.active');
//                获取对应的内容区域 ，让其隐藏
                var currentId=currentNav.dataset['cont'];
//                去掉导航的active 样式
                currentNav.classList.remove('active');
//                对应的内容区域
                document.querySelector('#'+currentId).style.display='none';

            //   突出显示自己 导航添加样式  对应的section 显示
//                给自己添加active样式
                this.classList.add('active');
//                对应的section模块显示出来
                var myId=this.dataset['cont'];
                document.querySelector('#'+myId).style.display='block';
            }
        }

    })(0);
</script>
```

### 拖拽案例

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box1,.box2{
            width: 400px;
            height: 400px;
            border: 1px solid #000;
        }

        .box1 div,.box2 div{
            width: 80px;
            width: 97px;
            height: 97px;
            background-color: red;
            border-radius: 50%;
            float: left;
            border: 1px solid #000;
            text-align: center;
            line-height: 100px;
        }

        .box2{
            position: absolute;
            left:600px;
            top:100px;
        }


    </style>
</head>
<body>
    <div class="box1">
        <div draggable="true">1</div>
        <div draggable="true">2</div>
        <div draggable="true">3</div>
        <div draggable="true">4</div>
        <div draggable="true">5</div>
        <div draggable="true">6</div>
        <div draggable="true">7</div>
        <div draggable="true">8</div>
    </div>
    <div class="box2">

    </div>

    <script>
        var box1=document.querySelector('.box1');
        var box2=document.querySelector('.box2');

        var boxs=document.querySelectorAll('.box1 div');

        var temp=null;

        for(var i=0;i<boxs.length;i++){
            boxs[i].addEventListener('dragstart',function(){
                temp=this;
            });
        }

        box2.addEventListener('dragover',function(e){
            e.preventDefault();
        });

        box2.addEventListener('drop',function(e){
           box2.appendChild(temp);
           temp=null;
        });
    </script>
</body>
</html>
```



