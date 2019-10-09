### 记住用户名



```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    <label for="">
        用户名：<input type="text" class="userName"/>
    </label>
    <br/><br/>
    <label for="">
        密 码：<input type="text" class="pwd"/>
    </label>
    <br/><br/>
    <label for="">
        <input type="checkbox" class="check" id=""/>记住密码
    </label>
    <br/><br/>
    <button>登录</button>

    <script>
        var userName=document.querySelector('.userName');
        var pwd=document.querySelector('.pwd');
        var chk=document.querySelector('.check');
        var btn=document.querySelector('button');

//        当点击登录的时候 如果需要记住密码：  存储密码，否则 清除密码
        btn.onclick=function(){
            if(chk.checked){
//                记住数据
                window.localStorage.setItem('userName',userName.value);
                window.localStorage.setItem('pwd',pwd.value);
            }else{
//                清除数据
                window.localStorage.removeItem('userName');
                window.localStorage.removeItem('pwd');
            }
        }
//        下次登录的 ，如果记录的有数据 直接填充
        window.onload=function(){
            userName.value=window.localStorage.getItem('userName');
            pwd.value=window.localStorage.getItem('pwd');

        }
    </script>
</body>
</html>
```




