_代码有点多_

# 小安卓
![](/assets/搜狗截图20191011211814.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background-color: rgba(47, 255, 243, 0.37);
        }
        .border {
            width: 600px;
            height: 440px;
            margin: 80px auto;
            background-color: rgba(70, 255, 142, 0.58);
        }
        .android {
            width: 340px;
            padding-top: 40px;
            margin: 0 auto;
            position: relative;
        }
        .head {
            width: 220px;
            height: 100px;
            margin: 0 auto ;
            background-color: #b2ff2f;
            border-radius: 100px 100px 0 0;
            position: relative;
        }
        .head::before,
        .head::after {
            content: '';
            display: block;
            width: 20px;
            height: 20px;
            background-color: #fff;
            border-radius: 10px;
            position: absolute;
            top: 40px;
        }
        .head::before {
            left: 50px;
        }
        .head::after {
            right: 50px;
        }
        .body {
            width: 220px;
            height: 180px;
            margin: 10px auto;
            background-color: #b2ff2f;
            border-radius: 0 0 20px 20px;
            position: relative;
        }
        .body::before,
        .body::after {
            content: '';
            display: block;
            width: 50px;
            height: 80px;
            background-color: #ffa436;
            border-radius: 0 0 25px 25px;
            position: absolute;
            bottom: -90px;
            /*margin-top: 10px*/
        }
        .body::before {
            /*margin-top: 10px;*/
            left: 40px;
        }
        .body::after {
            /*margin-top: 10px;*/
            right: 40px;
        }
        .arms {
            width: 340px;
            height: 150px;
            position: absolute;
            top: 150px;
        }
        .arms::before,
        .arms::after {
            content: '';
            display: inline-block;
            width: 50px;
            height: 150px;
            background-color: #ff7fde;
            border-radius: 25px;
            position: absolute;
        }
        .arms::before {
            left: 0;
        }
        .arms::after {
            right: 0;
        }
    </style>
</head>
<body>
<div class="border">
    <div class="android">
        <div class="head"></div>
        <div class="body"></div>
        <div class="arms"></div>
    </div>
</div>
</body>
</html>
```

# 哆啦A梦
![](/assets/8.gif)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .wrapper {
            margin: 50px 0 0 500px;
        }
        .doraemon {
            position: relative;
        }
        .doraemon .head {
            position: relative;
            width: 320px;
            height: 300px;
            /*原为150px*/
            border-radius: 50%;
            background: #3afffc;
            background: -webkit-radial-gradient(right top,#fff 10%,#07bbee 20%,#10a6ce 75%,#000);
            background: -moz-radial-gradient(right top,#fff 10%,#07bbee 20%,#10a6ce 75%,#000);
            background: -ms-radial-gradient(right top,#fff 10%,#07bbee 20%,#10a6ce 75%,#000);
            border:2px solid #555;
            box-shadow:-5px 10px 15px rgba(0,0,0,0.45);
        }
        .doraemon .face {
            position: relative;
            z-index: 2;
        }
        /*白色脸底*/
        .doraemon .face .white {
            width: 265px;
            height: 195px;
            /*原为150px*/
            border-radius: 150px;
            position: absolute;
            top: 75px;
            left: 25px;
            background:#fff;
            background: -webkit-radial-gradient(right top,#fff 75%,#eee 80%,#999 90%,#444);
            background: -moz-radial-gradient(right top,#fff 75%,#eee 80%,#999 90%,#444);
            background: –ms-radial-gradient(right top,#fff 75%,#eee 80%,#999 90%,#444);
        }
        .doraemon .face .nose {
            width: 30px;
            height: 30px;
            border-radius: 15px;
            background: #ff311b;
            position: absolute;
            top: 110px;
            left: 140px;
            z-index: 3;
            /*鼻子与白色脸底的关系*/
        }
        /*鼻子上的高光*/
        .doraemon .face .nose .light {
            width: 10px;
            height: 10px;
            border-radius: 5px;
            box-shadow: 19px 8px 5px #fff;/*阴影偏移*/;
        }
        .doraemon .face .nose_line {
            width: 3px;
            height: 100px;
            background: #333;
            position: absolute;
            top: 143px;
            left: 155px;
            z-index: 3;
        }
        .doraemon .face .mouth {
            width: 220px;
            height: 400px;
            /*通过底边加上圆角模拟微笑*/
            border-bottom: 3px solid #333;
            border-radius: 120px;
            position: absolute;
            top: -160px;
            left: 45px;
        }
        .doraemon .eyes {
            position: relative;
            z-index: 3;
        }
        .doraemon .eyes .eye {
            width: 72px;
            height: 82px;
            background: #fff;
            border:2px solid #000;
            border-radius: 35px 35px;
            position: absolute;
            top: 40px;
        }
        .doraemon .eyes .eye .black {
            width: 14px;
            height: 14px;
            background: #000;
            border-radius: 7px;
            position: absolute;
            top: 40px;
        }
        .doraemon .eyes .left {
            left: 82px;
        }
        .doraemon .eyes .right {
            left: 156px;
        }
        .doraemon .eyes .eye .bleft {
            left: 50px;/*相对于恶业定位，而不是eyes*/
        }
        .doraemon .eyes .eye .bright {
            left: 7px;
        }

        .doraemon .whiskers {
            width: 220px;
            height: 80px;
            background: #fff;
            border-radius: 15px;
            position: absolute;
            top: 120px;
            left: 45px;
            z-index: 2; /*在鼻子和眼睛下面*/
        }
        .doraemon .whiskers .whisker {
            width: 60px;
            height: 2px;
            background: #333;
            position: relative;
            z-index: 2;
        }
        .doraemon .whiskers .rTop {
            left: 165px;
            top: 25px;
        }
        .doraemon .whiskers .rMiddle {
            left: 167px;
            top: 45px;
        }
        /*右下胡子*/
        .doraemon .whiskers .rBottom {
            left: 165px;
            top: 65px;
        }
        /*左上胡子*/
        .doraemon .whiskers .lTop {
            left: 0;
            top: 25px;
        }
        /*左中胡子*/
        .doraemon .whiskers .lMiddle {
            left: -2px;
            top: 45px;
        }
        /*左下胡子*/
        .doraemon .whiskers .lBottom {
            left: 0;
            top: 65px;
        }
        .doraemon .whiskers .r160 {
            -webkit-transform: rotate(160deg);
            -moz-transform: rotate(160deg);
            -ms-transform: rotate(160deg);
            -o-transform: rotate(160deg);
            transform: rotate(160deg);
        }
        .doraemon .whiskers .r20 {
            -webkit-transform: rotate(200deg);
            -moz-transform: rotate(200deg);
            -ms-transform: rotate(200deg);
            -o-transform: rotate(200deg);
            transform: rotate(200deg);
        }
        .doraemon .choker {
            width: 230px;
            height: 20px;
            background: #c40;
            background: -webkit-gradient(linear,left top,left bottom,from(#c40),to(#800400));
            background: -moz-linear-gradient(center top,#c40,#800400);
            background: -ms-linear-gradient(center top,#c40,#800400);
            border:2px solid #000;
            border-radius: 10px;
            position: relative;
            top: -40px;
            left: 45px;
            z-index: 4;
        }
        .doraemon .choker .bell {
            width: 40px;
            height: 40px;
            _owerdlow:hidden;
            border:2px solid #000;
            border-radius: 50px;
            background-color: #f6ff3f;
            background: -webkit-gradient(linear, left top, left bottom, from(#f9f12a),color-stop(0.5, #e9e11a), to(#a9a100));
            background: -moz-linear-gradient(top, #f9f12a, #e9e11a 75%,#a9a100);
            background: -ms-linear-gradient(top, #f9f12a, #e9e11a 75%,#a9a100);
            box-shadow:-5px 5px 10px rgba(0,0,0,0.25);
            position: absolute;
            top: 5px;
            left: 90px;
        }
        .doraemon .choker .bell_line {
            width: 36px;
            height: 2px;
            background: #f5ff1d;
            border:2px solid #333;
            border-radius: 3px 3px 0 0;
            position: absolute;
            top: 10px;
        }
        .doraemon .choker .bell_circle { /*黑点*/
            width:12px;
            height: 10px;
            background: #000;
            border-radius: 5px;
            position: absolute;
            top: 20px;
            left: 14px;
        }
        .doraemon .choker .bell_under {
            width: 3px;
            height: 15px;
            background: #000;
            position: absolute;
            left: 18px;
            top: 27px;
        }
        .doraemon .choker .bell_light {
            width: 12px;
            height: 12px;
            border-radius: 10px;
            box-shadow: 19px 8px 5px #fff;
            position: absolute;
            top: -5px;
            left: 5px;
            opacity: 0.7;
        }
        /*身子*/
        .doraemon .bodys {
            position: relative;
            top:-310px;
        }
        .doraemon .bodys .body {
            width: 220px;
            height: 165px;
            background: #13d6ff;
            background: -webkit-gradient(linear,right top,left top,from(#07beea),color-stop(0.5, #0073b3),color-stop(0.75,#00b0e0), to(#0096be));
            background: -moz-linear-gradient(right center,#07beea,#0073b3 50%,#00b0e0 75%,#0096be 100%);
            background: -ms-linear-gradient(right center,#07beea,#0073b3 50%,#00b0e0 75%,#0096be 100%);
            border:2px solid #333;
            position: absolute;
            top: 265px;
            left: 50px;
        }
        .doraemon .bodys .wraps {
            width: 170px;
            height: 170px;
            background: #fff;
            background: -webkit-gradient(linear, right top, left bottom, from(#fff),color-stop(0.75,#fff),color-stop(0.83,#eee),color-stop(0.90,#999),color-stop(0.95,#444), to(#000));
            background: -moz-linear-gradient(right top,#fff,#fff 75%,#eee 83%,#999 90%,#444 95%,#000);
            background: -ms-linear-gradient(right top,#fff,#fff 75%,#eee 83%,#999 90%,#444 95%,#000);
            border:2px solid #000;
            border-radius: 85px;
            position: absolute;
            left: 72px;
            top: 230px;
        }
        .doraemon .bodys .pocket {
            width: 130px;
            height: 130px;
            border-radius: 65px;
            background: #fff;
            background: -webkit-gradient(linear, right top, left bottom, from(#fff),color-stop(0.70,#fff),color-stop(0.75,#f8f8f8),color-stop(0.80,#eee),color-stop(0.88,#ddd), to(#fff));
            background: -moz-linear-gradient(right top, #fff, #fff 70%,#f8f8f8 75%,#eee 80%,#ddd 88%, #fff);
            background: -ms-linear-gradient(right top, #fff, #fff 70%,#f8f8f8 75%,#eee 80%,#ddd 88%, #fff);
            border:2px solid #000;
            position: absolute;
            top: 250px;
            left: 92px;
        }
        .doraemon .bodys .pocket_mask {
            width: 134px;
            height: 60px;
            background: #fff;
            border-bottom: 2px solid #000;
            position: absolute;
            top: 259px;
            left: 92px;
        }
        /*左右手*/
        .doraemon .hand_right, .doraemon .hand_left {
            height: 100px;
            width: 100px;
            position: absolute;
            top: 272px;
            left: 248px;
        }
        /*左手*/
        .doraemon .hand_left {
            left: -10px;
        }
        .doraemon .arm {
            width: 80px;
            height: 50px;
            background: #23faff;
            background: -webkit-gradient(linear, left top, left bottom, from(#07beea),color-stop(0.85,#07beea), to(#555));
            background: -moz-linear-gradient(center top, #07BEEA, #07BEEA 85%, #555);
            background: -ms-linear-gradient(center top, #07BEEA, #07BEEA 85%, #555);
            border:1px solid #000;
            box-shadow: -10px 7px 10px rgba(0,0,0,0.35);
            z-index: -1;
            position: relative;
        }
        .doraemon .hand_right .arm {
            top:17px;
            -webkit-transform: rotate(35deg);
            -moz-transform: rotate(35deg);
            -ms-transform: rotate(35deg);
            -o-transform: rotate(35deg);
            transform: rotate(35deg);
        }
        .doraemon .hand_left .arm {
            top: 17px;
            background-color: #23faff;
            box-shadow: 5px -7px 10px rgba(0, 0, 0, 0.25);
            -webkit-transform: rotate(145deg);
            -moz-transform: rotate(145deg);
            -ms-transform: rotate(145deg);
            -o-transform: rotate(145deg);
            transform: rotate(145deg);
        }
        .doraemon .circle {
            width: 60px;
            height: 60px;
            border-radius: 30px;
            border:2px solid #000;
            background: #fff;
            background: -webkit-gradient(linear, right top, left bottom, from(#fff),color-stop(0.5,#fff),color-stop(0.70,#eee),color-stop(0.8,#ddd), to(#999));
            background: -moz-linear-gradient(right top, #fff, #fff 50%, #eee 70%, #ddd 80%,#999);
            background: -ms-linear-gradient(right top, #fff, #fff 50%, #eee 70%, #ddd 80%,#999);
            position: absolute;
        }
        .doraemon .hand_right .circle {
            left: 40px;
            top: 32px;
        }
        .doraemon .hand_left .circle {
            left: -20px;
            top: 32px;
        }
        .doraemon .arm_rewrite {
            height: 45px;
            width: 5px;
            background: #009bc5;
            position: relative;
        }
        .doraemon .hand_right .arm_rewrite {
            top: -45px;
            left: 22px;
        }
        .doraemon .hand_left .arm_rewrite {
            top: -45px;
            left: 60px;
            background: #009dc7;
        }
        /*脚部*/
        .doraemon .foot {
            width: 280px;
            height: 40px;
            position: relative;
            top: 55px;
            left: 20px;
        }
        .doraemon .foot .left, .doraemon .foot .right {
            width: 125px;
            height: 30px;
            background-color: #fff;
            background: -webkit-gradient(linear, right top, left bottom, from(#fff),color-stop(0.75,#fff),color-stop(0.85,#eee), to(#999));
            background: -moz-linear-gradient(right top, #fff, #fff 75%, #eee 85%, #999);
            background: -ms-linear-gradient(right top, #fff, #fff 75%, #eee 85%, #999);
            border:2px solid #333;
            border-radius: 80px 60px 60px 40px;
            box-shadow: -6px 0 10px rgba(0,0,0,0.35);
            position: relative;
        }
        .doraemon .foot .left {
            left: 8px;
            top: 65px;
        }
        .doraemon .foot .right {
            top: 31px;
            left: 141px;
        }
        .doraemon .foot .foot_rewrite {
            width: 20px;
            height: 10px;
            background-color: #fff;
            background: -webkit-gradient(linear, right top, left bottom, from(#666),color-stop(0.83,#fff), to(#fff));
            background: -moz-linear-gradient(right top, #666, #fff 83%, #fff);
            background: -ms-linear-gradient(right top, #666, #fff 83%, #fff);
            border:2px solid #000;
            /*border-bottom: none;*/
            border:none;
            border-radius: 40px 40px 0  0;
            top: -11px;
            left: 130px;
            _left:127px;
        }
        .doraemon .eyes .eye .black {
            width: 14px;
            height: 14px;
            background: #000;
            border-radius: 7px;
            position: absolute;
            -webkit-animation: eyemove 3s linear infinite;
            -moz-animation: eyemove 3s linear infinite;
            -ms-animation: eyemove 3s linear infinite;
            -o-animation: eyemove 3s linear infinite;
            animation: eyemove 3s linear infinite;
        }
        @-webkit-keyframes eyemove {
            70%{
                margin:0 0 0 0;
            }
            80%{
                margin:-22px 0 0 0;
            }
            85% {
                margin:-22px 0 0 5px;
            }
            90%{
                margin:-22px 10px 0 0 ;
            }
            93%{
                margin:-22px 0 0 5px;
            }
            96%{
                margin:0 0 0 0;
            }
        }
        @-moz-keyframes eyemove {
            70% {
                margin: 0 0 0 0;
            }

            80% {
                margin: -22px 0 0 0;
            }

            85% {
                margin: -22px 0 0 5px;
            }

            90% {
                margin: -22px 10px 0 0;
            }

            93% {
                margin: -22px 0 0 0;
            }

            96% {
                margin: 0 0 0 0;
            }
        }

        @-o-keyframes eyemove {
            70% {
                margin: 0 0 0 0;
            }

            80% {
                margin: -22px 0 0 0;
            }

            85% {
                margin: -22px 0 0 5px;
            }

            90% {
                margin: -22px 10px 0 0;
            }

            93% {
                margin: -22px 0 0 0;
            }

            96% {
                margin: 0 0 0 0;
            }
        }
        @keyframes eyemove {
            70% {
                margin: 0 0 0 0;
            }

            80% {
                margin: -22px 0 0 0;
            }

            85% {
                margin: -22px 0 0 5px;
            }

            90% {
                margin: -22px 10px 0 0;
            }

            93% {
                margin: -22px 0 0 0;
            }

            96% {
                margin: 0 0 0 0;
            }
        }
    </style>
</head>
<body>
    <div class="wrapper">
        <!--/*整体*/-->
        <div class="doraemon">
            <!--/*头部*/-->
            <div class="head">
                <div class="eyes">
                    <div class="eye left">
                        <div class="black bleft"></div>
                    </div>
                    <div class="eye right">
                        <div class="black bright"></div>
                    </div>
                </div>
                <div class="face">
                         <!--白色脸底-->
                    <div class="white"></div>
                    <div class="nose">
                        <div class="light"></div>
                    </div>
                    <div class="nose_line"></div>
                    <div class="mouth"></div>
                    <div class="whiskers">
                        <div class="whisker rTop r160"></div>
                        <div class="whisker rMiddle"></div>
                        <div class="whisker rBottom r20"></div>
                        <div class="whisker lTop r20"></div>
                        <div class="whisker whisker lMiddle"></div>
                        <div class="whisker lBottom r160"></div>
                    </div>
                </div>
            </div>
            <!--脖子和铃铛-->
            <div class="choker">
                <div class="bell">
                    <div class="bell_line"></div>
                    <div class="bell_circle"></div>
                    <div class="bell_under"></div>
                    <div class="bell_light"></div>
                </div>
            </div>
            <!--身子-->
            <div class="bodys">
                <!--肚子-->
                <div class="body"></div>
                <!--肚兜-->
                <div class="wraps"></div>
                <!--口袋-->
                <div class="pocket"></div>
                <!--遮住一般口袋-->
                <div class="pocket_mask"></div>
            </div>
            <!--右手-->
            <div class="hand_right">
                <!--手臂-->
                <div class="arm"></div>
                <!--手掌-->
                <div class="circle"></div>
                <!--线-->
                <div class="arm_rewrite"></div>
            </div>
            <!--左手-->
            <div class="hand_left">
                <div class="arm"></div>
                <div class="circle"></div>
                <div class="arm_rewrite"></div>
            </div>
            <!--脚-->
            <div class="foot">
                <div class="left"></div>
                <div class="right"></div>
                <div class="foot_rewrite"></div>
            </div>
        </div>
    </div>
</body>
</html>
```


