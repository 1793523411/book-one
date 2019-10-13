## 闭包的练习
线程：一个线程一次只能处理一件事情，多个线程就可以多个事情同时进行


```
		//问题代码
//        for(var i = 0 ; i < 10; i++){
//            setTimeout(function(){
//                console.log(j);
//            },0);
//        }
		for(var i = 0; i< 3; i++){

            function foo(j){
//                var j;
//                j = 实参
                //j = i
                return function(){
                    console.log(j);
                };
            }
            //0
            var f = foo(i);
            setTimeout(f, 0);
        }
```



### JS是单线程的
JS中，分了三个任务
1.渲染任务
2.js的代码执行任务
3.事件处理任务
#### JS代码的执行顺序
1.先把主任务（代码任务）执行完毕
2.再去执行次要的任务(包括setTimeOut和setInterval中的回调函数中的代码)
setTimeOut
至少在指定的时间后执行指定回调函数
因为要等主任务中的代码执行完毕之后，才回去检查，setTimeOut的回调函数，有没到执行时间
用闭包来解决回调函数在调用的时候访问的是全局的变量
在闭包中创建一个变量，来单独存储当前的回调函数需要的数据，
在调用的时候就会去使用这个单独的数据，而不是去访问全局变量
## 闭包的练习2


```
	for (var i = 0; i < divs.length; i++) {
                var div = divs[i];

//                function foo(j) {
//                    return function () {
//                        alert("我是第"+ (j+1) +"个div");
//                    }
//                }
//
//                var f = foo(i);
//
//                div.onclick = f;

                div.onclick = function (j) {
                    return function () {
                        alert("我是第"+ (j+1) +"个div");
                    }
                }(i);

            }
```


注册点击事件的时候
点击事件在触发的时候访问的是全局的变量
在闭包中创建一个变量，来单独存储当前的事件处理函数需要的数据，
在调用的时候就会去使用这个单独的数据，而不是去访问全局变量

## 闭包练习3


```
	       var arr = [{name: '张三1'},
            {name: '张三2'},
            {name: '张三3'},
            {name: '张三4'}];

        for (var i = 0; i < arr.length; i++) {

//            arr[i].sayHello = function () {   //问题代码
//                console.log(i);
//            }

            arr[i].sayHello = (function () {
                var j = i;
                return function () {
                    console.log(j);
                }
            }());
        }

        arr[0].sayHello();
        arr[1].sayHello();
//        for (var j = 0; j < arr.length; j++) {
//
//            arr[j].sayHello();
//
//        }
```

## 缓存
缓存：cache
缓存的作用，就是将一些常用的数据，存储起来，提供使用，提升性
硬件缓存
浏览器缓存
CDN
内存型数据库
	//数据库  高并发
        //非关系型数据库（内存型数据库） MongoDB  Redis
	//网站静态页面缓存机制
        //将网页静态化，存储在服务器端
### 如何用闭包实现缓存
    1、写一个闭包在闭包中创建一个对象，用来做缓存的存储对象
    2、在闭包中创建一个对象，用来做缓存的存储对象
    3、在闭包中创建一个数组，用来存储换中的键
    4、返回一个函数，这个函数需要两个参数，一个是key 一个是value
    5、在返回的函数中,判断传入的value是否为undefined
    6、如果为Undefined 则表示是获取值，就直接返回在第一步创建的缓存对象中指定的键对应的值
    7、如果不为Undefined 则表示是设置值
    8、在缓存对象中设置指定的key的值为value
    9、把key加入存储key的数组
    10、判断key数组是不是超出了缓存大小限制
    11、如果超出限制，删除数组第一个元素（使用shift），获取到删除的key
    12、使用删除的key删除缓存对象中存储的值（delete）
    
### 递归斐波那切数列的问题以及解决
使用数组存储数列，虽然可以提升性能，但是有局限性
可以求5的 也可以求10的，但是要求100呢 100000呢
定义一个缓存数组，存储已经计算出来的斐波那契数
1.先从cache数组中去取想要获取的数字
2.如果获取到了，直接使用
3.如果没有获取到，就去计算，计算完之后，把计算结果存入cache，然后将结果返回
#### 创建缓存容器	

```
	function createCache(){
            var cache = {};
            return function (key, value) {
                //如果传了值，就说名是设置值
                if(value !== undefined){
                    cache[key] = value;
                    return cache[key];
                }
                //如果没有传值，只穿了键，那就是获取值
                else{
                    return cache[key];
                }
            }
        }
	用缓存递归
		var count =0 ;
        function createFib(){
            var fibCache = createCache();
            function fib(n){
                count ++;
                //1.从cache中获取数据
                if(fibCache(n) !== undefined){
                    //如果缓存中有 直接返回
                    return fibCache(n) ;
                }
                //如果缓存中没有 就计算
                if(n <= 2){
                    //把计算结果存入数组
                    fibCache(n , 1) ;
                    return 1;
                }
                var temp = fib(n - 1) + fib(n - 2);
                //把计算结果存入数组
                fibCache(n, temp) ;
                return temp;
            }

            return fib;
        }

	调用
		var fib = createFib();
//        console.log(fib(6));
        fib(5);
        console.log(count);
```


### jQuery缓存实现分析
	

```
function createCache(){
            //cache对象中以键值对的形式存储我们的缓存数据
            var cache = {};
            //index数组中该存储键，这个键是有顺序，可以方便我们做超出容量的处理
            var index = [];
            return function (key, value) {
                //如果传了值，就说名是设置值
                if(value !== undefined){
                    //将数据存入cache对象，做缓存
                    cache[key] = value;
                    //将键存入index数组中，以和cache中的数据进行对应
                    index.push(key);

                    //判断缓存中的数据数量是不是超出了限制
                    if(index.length >= 50){
                        //如果超出了限制
                        //删除掉最早存储缓存的数据
                        //最早存入缓存的数据的键是在index数组的第一位
                        //使用数组的shift方法可以获取并删除掉数组的第一个元素
                        var tempKey = index.shift();
                        //获取到最早加入缓存的这个数据的键，可以使用它将数据从缓存各种删除
                        delete cache[tempKey];
                    }
                }
                //如果没有传值，只穿了键，那就是获取值
//                else{
//                    return cache[key];
//                }
                return cache[key];
            }
        }

        var eleCache = createCache();
        eleCache("name","高金彪");
        console.log(eleCache("name"));
	function createCache() {
            var keys = [];
            function cache( key, value ) {
                // 使用(key + " ") 是为了避免和原生（本地）的原型中的属性冲突
                if ( keys.push( key + " " ) > 3 ) {
                    // 只保留最新存入的数据
                    delete cache[ keys.shift() ];
                }
                // 1 给 cache 赋值
                // 2 把值返回
                return (cache[ key + " " ] = value);
            }
            return cache;
        }
```


## 沙箱模式
与外界隔绝的一个环境，外界无法修改该环境内任何信息，沙箱内的东西单独属于一个世界
#### 360沙箱模式
将软件和操作系统进行隔离，以达到安全的目的
	苹果手的app使用的就是沙箱模式去运行
        //隔离app的空间，每个app独立运行
	JS中的沙箱模式
### 沙箱模式的基本模型


```
		 (function(){
//            var a = 123;
//        })();

			(function(){

            //在沙箱中将所有变量的定义放在最上方

            //中间就放一些逻辑代码

            //最后，如果需要，就给外界暴露一些成员（通过window）

            var sum = 0;
            for(var i = 1; i<=100;i++){
                sum+=i;
            }
            console.log(sum);
        })();
	 //为什么要使用立即执行函数表达式（IIFE）
        //因为IIFE不会再外界暴露任何的全局变量，但是又可以形成一个封闭的空间
        //刚好可以实现沙箱模式
	jQuery中的沙箱模式
		 (function(win){

            var itcast = {
                getEle:function () {

                }
            }

            //如果需要在外界暴露一些属性或者方法，就可以将这些属性和方法
            //加到window全局对象上去
            //但是这window全局对象不可以直接引用，因为直接引用会破坏沙箱原则
            //所以我们选择使用传参的形式将 window对象 传入沙箱内
            //此时沙箱内使用window对象的时候，不会再去全局搜索window对象
            //而使用的就是沙箱内部定义的形参

            win.itCast = win.$ = itcast;

        })(window)
```


### 沙箱模式一般应用在
书写第三方框架
 或者为第三方框架书写插件
 或者书写功能独立的一些组件
### 沙箱模式的优势
1.沙箱模式使用的是IIFE，不会再外界暴露任何的全局变量，也就不会造成全局变量污染
2.沙箱中的所有数据，都是和外界完全隔离的，外界无法对其进行修改，也就保证了代码的安全性
js中沙箱模式的实现原理就是
 函数可以构建作用域！上级作用域不能直接访问下级作用域中的数据
 
## 函数调用的四种模式
### 1.函数模式
            //this指向window全局对象
		 function test(){
            console.log(this);
        }
        test();
### 2.方法模式
            //this指向调用这个方法的对象
		var obj1 = {
            test:function(){
                console.log(this);
            }
        }
        obj1.test();
### 3.构造函数模式
            //this 使用new创建出来的对象
		 function Person(){
            console.log(this);
        }
        var obj =new Person();
### 4.上下文模式
#### 上下文调用模式
JS中的上下文
     

```
   //context 执行环境的意思
        //this
	//在上下文调用模式中，可以修改this的值，也就是可以修改函数的调用方式
		 var name = "莱昂纳多·自强·郭";
        function sayHello(a, b) {
            console.log(this.name + "吃了"+ (a * b) + "个馒头");
        }

    //    sayHello();  //

        var obj = {
            name:"尼古拉斯·电饭·锅"
        }

        var arr= []
        arr.push();
        arr.push();
        sayHello.apply(obj,arr);  //

        function test(a , b ,c){

        }
        sayHello.call(obj, 1, 2);
```


使用如下两个方法，可以修改函数调用上下文，也就是this的值
 apply
api文档中的语法语句中 [] 代表括起来的东西可有可无
  函数.apply(对象, 函数需要参数列表，是一个数组)
call
  函数.call(对象,arg1,arg2,arg3...argn)
### call和apply的区别
1.第一个参数都是要把this修改成的对象
2.当函数需要参数的时候，那么apply是用数组进行参数的传递
3.而call是使用单个的参数进行传递

call用于确定了函数的形参有多少个的时候使用
apply用于函数的形参个数不确定的情况

## 构造函数调用模式特征
1.构造函数的首字母要大写
2.一般情况下和new关键字一起使用
3.构造函数中的this指定而是new关键字创建出来的对象
4.默认的返回new创建出来的这个对象
构造函数的返回值
默认返回new创建创建出来的对，若是值类型的数据，没有影响
若是对象类型，则返回这个对象，不会返回原来创建出来的对象
### 工厂模式的构造函数
	

```
	function Person(name,age){
            var o = {
                name:name,
                age:age,
                sayHello:function(){

                }
            }
            return o;
        }

        var p = Person("张三", 18);
        console.log(p);
        //简单工厂模式的构造函数 创建出来的对象 跟该构造函数无关
        //简单工厂模式的构造函数，实际的调用模式是 函数模式
	寄生式构造函数
		function Person(name,age){
            var o = {
                name:name,
                age:age,
                sayHello:function(){

                }
            }
            return o;
        }

        var p = new Person();
        console.log(p);
```


