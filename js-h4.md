## 作用域
变量起作用的范围就是变量的作用域
### 块级作用域
JavaScript中没有块级作用域
如果有块级作用域下面的代码的显示结果为 undefined undefined


```
//        for(var i=0; i<10;i++){
//            var num = i;
//        }
//        console.log(i);
//        console.log(num);
```


### 词法作用域
就是在代码写好的那一刻，变量的作用域就已经确定了，这种作用域，就是所谓的词法作用域
和词法作用域相对的叫动态作用域 js中是词法作用域不是动态作用域


```
			var num = 123;
    function f1(){
        console.log(num);  //如果是动态作用域打印的就是456 如果是词法作用域 打印123
    }
    function f2(){
        var num = 456;
        f1();
    }
    f2();
```


```
### 在JavaScript中唯一能产生作用域的东西是 函数！
		var a = 1;
        function test(){
            var b = 10;
        }
```

### 词法作用域的规则
函数允许访问函数外的数据.
		        //整个代码结构中只有函数可以限定作用域.
		        //作用域规则首先使用提升规则分析
		        //如果当前作用域中有了该变量, 就不考虑外面的同名变量
		
## 变量和函数提升
js代码的执行分为两个步骤
### 预解析
	

```
		//提升（hoisting）
            //JavaScript代码在预解析阶段，会对以var声明的变量名，和function开头的语句块，进行提升操作（变量名提升，函数体提升）
			函数同名，如何提升
        //预处理的时候，会将两个函数全部提升，但是后面的函数会覆盖掉前面函数
			变量和函数同名
        //在提升的时候，如果有变量和函数同名，会忽略掉变量，只提升函数
		2.执行
			执行预解析后的代码
	变量的提升分作用域
		函数内单独提升
	函数表达式不会提升
		func();
var func = function(){
            alert("你猜我会不会被调用");
        }
//提升后的代码
        var func;
        func();
        func = function(){
            alert("你猜我会不会被调用");
        };//不会被调用
```
## 作用域链
只要是函数就可以创造作用域
函数中又可以再创建函数
函数内部的作用域可以访问函数外部的作用域
如果有多个函数嵌套，那么就会构成一个链式访问结构，这就是作用域链


```
	 //f1--->全局
        function f1(){
            //f2--->f1--->全局
            function f2(){
                //f3---->f2--->f1--->全局
                function f3(){
                }
                //f4--->f2--->f1---->全局
                function f4(){
                }
            }
            //f5--->f1---->全局
            function f5(){
            }
        }
```

## 变量与作用域
1 设置值的时候，也是访问变量
2. 获取值的时候，是访问变量
3.并不是在函数内部写了变量，这个变量就属于这个函数的作用域，
		        // 而是必须使用var来声明变量，这个变量才会属于这个作用域
		/函数在声明出来的时候，里面的代码不会执行，
		        //只有在调用的时候，代码才会执行
		声明函数时的函数名，其实也是一个变量名
		        //可以通过这个变量名来给其赋值
## 变量搜索原则
1.在使用变量的时候
            //* 首先在所在的作用域中查找
            //* 如果找到了 就直接使用
            //* 如果没有找到 就去上级作用域中查找
	重复以上步骤
            //* 如果直到0级作用域链也就是全局作用域还没有找到，报错
            
## 闭包
1.什么是闭包
一个具有封闭的对外不公开的, 包裹结构, 或空间
2、js中的闭包
  就是函数
3、闭包的原理就是作用域访问原则
 

```
//上级作用域无法直接访问下级作用域中的变量
		 function f1(){
//            var num = 123;
//            function f2(){
//                console.log(num);
//            }
//            f2();
//        }
```


4.闭包要解决什么问题？
	

```
	//1.闭包内的数据不允许外界访问
		            //2.要解决的问题就是间接访问该数据
		 function foo () {
           var num = 123;
           return num;
       }

       var x = foo();
       console.log(x);

       var y = foo();
       console.log(y);
       console.log( x === y );//false
			/用来说明函数的每次调用，返回的对象都是新的  每次都不一样
			使用return关键字将函数内部的数据返回，这个数据只能被使用一次
	闭包的基本模式
		 //在外部函数（foo）内创建函数(inner)，在这个内部函数(inner)中，可以操作foo中的数据
		        //将外部函数的返回值设置为内部函数
		        //在外部调用外部函数（foo）,就可以接受到返回值(内部函数)
		        //使用这个内部函数，就可以在外部对外部函数里的变量进行修改
		 function foo(){
            var num = 123;
            return function(a){
                //1.如果传参数，这里的a肯定不是Undefined，所以条件判断为true
                if(a !== undefined){
                    num = a;
                }else{
                    //如果不传参，代表要获取这个值，直接return
                    return num;
                }
            };
        }
        var func =  foo();
        //设置值
        func(789);

        //理想状态下的获取值
        var x = func();
        console.log(x);
```


        
### 闭包的作用
在函数外部想要修改数据
只能通过函数内部的方法
我们可以在函数内部定义的这个方法里
设置安全措施，校验之类的操作
可以保证系统的安全性和稳定性
最基本的作用：可以通过闭包返回的函数或者方法，来修改函数内部的数据
创建一个私有的空间，保护数据
外部想要访问数据，只能通过函数提供的方法
在提供的方法中，我们可以设置一些校验逻辑，让数据变得更加安全
### 使用闭包获取多个数据并设置值
	

```
function foo() {
           var name = "张国荣";
           var age = 18;

           return [
               function(){
                   return name;
               },
               function(){
                   return age;
               }
           ]
       }

       var getName = foo();
       console.log(getName[0]());
       console.log(getName[1]());


        // function foo() {
        //     var name = "张国荣";
        //     var age = 18;

        //     return {
        //         getName:function () {
        //             return name;
        //         },
        //         getAge:function () {
        //             return age;
        //         }
        //     }
        // }

        // var obj = foo();
        // console.log(obj.getName());
        // console.log(obj.getAge());
	function foo() {
            var name = "高金彪";
            var gender = "female";

            return {

                getName:function () {
                    return name;
                },
                setName:function(value){
                    name = value;
                    return name;
                },
                setGender:function(value){
                    gender = value;
//                    return gender;
                },
                getGender:function(){
                    return gender;
                }

            };
        }
```


## 作用域分段
	

```
<script>
        foo()
        function foo(){
            console.log("第一个script标签内的函数")
        };
    </script>

    <script>
        foo()
        function foo(){
            console.log("第2个script标签内的函数")
        }
    </script>
```


    
## 条件式函数声明
	

```
//条件式函数声明是否会被提升，取决浏览器
	        //条件式函数声明不推荐去写
	foo();//会报错，因为未被提升
        if(true){
            function foo(){

            }
        }
```

