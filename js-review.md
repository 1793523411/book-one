## 数据类型
基本数据类型
    string  number  boolean
复杂数据类型（引用类型）
    Array  Date  Object  RegExp  String  Number  Boolean
如何获取一个数据的数据类型
使用关键字 typeof
	typeof返回值为string类型
	String  Number  Date  首字母大写的都是构造函数
两个空的类型
		    null
		    undefined
什么时候对象会是null
    //变量不可能为null值，除非手动去设置
	什么时候要给对象赋值为null？
    //要解除对象的占用（引用）的时候
## 全等于和等于的区别
=== 全等
    类型和值都要进行比较
	== 等于
    只比较值
    
## in关键字
 最常用的是在for in 循环中 遍历对象的键


```
		for(var k  in obj){
       console.log(typeof k);
       console.log(k);
   }

	判断属性是否存在于对象中
        //语法   属性名 in 对象
		var propName = "name";
   var isExsit = propName in obj;
   console.log(isExsit);
```


注意： 使用in关键字的时候，属性名称为字符串类型，需要用引号引起来
注意： in关键字操作数组的时候判断的是索引是否存在，而不是值
		

```
 var arr = [4, 6, 3, 4];

   console.log(0 in arr);（true）
    //这里会做一个隐式的类型转换
   console.log("0" in arr);（true）
	如何判断数组中是否存在指定的值
    //1. for循环 如果找到了就输出
    //2. indexOf  返回值为指定的数对应的索引，如果没有找到 返回-1
    console.log(arr.indexOf(9));
		for(var i=0;i<arr.length;i++){
  if(arr.indexOf(i) == target){
     console.log(arr.indexOf(i))
}
}
```



## 新建对象
	

```
var now = new Date();
    console.log(now);

    //GMT  格里尼治标准时间
    //UTC  世界协调时间
    
```


## 值类型和引用类型
### 说明
值类型：  string  number  boolean  undefined
    //  存储的就是数据本身的变量就是值类型的数据
		//引用类型：object
    // 存储的是数据在内存中的地址，数据在内存中单独存储 就是引用类型的数据

/引用类型赋值
    //引用类型赋值的时候，是将变量中存储的地址复制一份单独存储，但是两个变量共享同一个对象
    //修改其中一个对象，两外一个引用来访问的时候，也会访问到修改后的对象
###特征
//值类型的赋值
    //直接将存储的数据复制一份进行赋值，两份数据在内存中是完全独立的
		引用类型相反
	在函数中的使用
		值类型做函数的参数
    //函数内部的变量，也就是形参和实参只是简单的赋值操作，两个数据独立存储于内存中的
    //在函数内部对形参进行修改，不会影响外面的变量
		/引用类型做函数的参数
    //还是把实参存储的地址赋值给了形参，在函数内部，形参同样也指向该对象，
    //所以，在函数内部对该对象进行修改，会影响到外面的变量
		**注意**：如果在函数内部重新创建对象，为该形参赋值，那么两个对象将不再有关系
    //修改其中一个，另外一个不受影响
    
## 对象的动态特征
对象的动态性是指，在对象创建出来之后，为对象添加新的属性或者方法
	使用点语法进行赋值的时候，如果对象存在该属性，是修改操作
    //如果对象不存在该属性，是给该对象新增属性并且赋值
	对象是不是就是键值对儿的集合
    // 对象名[属性名]    注意这里的属性名 是字符串


```
console.log(obj["name"]);
```


//这里如果使用的键不是字符串类型，会隐式的转换成字符串类型
	/新增属性、方法的方式有：
    //1.点语法
    //2.通过 [] 的形式去添加
## 逻辑中断
即c中的短路
	
## delete关键字


```
//delete关键字可以用来删除对象的属性，还有未使用var声明的变量
		//    var num = 10;
//    var result = delete  num;
//    console.log(result);//false
	    //delete关键字有返回值 用来表示删除属性是否成功
	    //如果删除的是不存在的属性，返回值为true
		  var result=  delete obj.gender;
   console.log(result);
	    //如果删除的属性存在原型当中，那么返回值为true，但是并未删除
		 console.log(obj.toString()); //[object Object]
		var result = delete obj.toString;
    console.log(result);//true
    console.log(obj.toString());//[object Object]
    
```


## 定义函数
1.函数声明
        

```
function funcName(){
            //函数体
        }
	//2.函数表达式
        //在使用函数表达式声明函数的时候，function后面可以跟函数名
        //但是 这个函数名。只限在函数内部使用，外部无法访问
		 var funcName1 = function name(){
            //
            console.log("谁说不可以");
        }
funcName1();
	 //3.Function
        var funcName2 = new Function();
```


        
## DOM操作复习
	

```
//增
        //document.createElement
        //appendChild
	//删
        //removeChild
	//改
        //style
        //id
        //className
        //innerHTML
        //innerText
	//查
        //getElementById
        //getElementsByTagName
        //getELementsByClassName
```

## 异常处理
异常最大的特征，就是一旦出现异常，后面的代码将不会再执行
	        //那为了保证后面代码在出现异常之后，还能继续执行，所以就要进行异常处理
	注意 语法异常 try catch无法捕获
	异常捕获语句
  

```
      //try catch finally
		try{
////            a();
//            //可能会出现问题的代码
//
//            throw "你的代码坏了！！！";
//        }
//        catch(e){
//
//            //出现异常后的处理代码
//            console.log(e);
//        }
//
//        function test() {
//            console.log("我是之后的代码");
//        }

			try{
            sum(0);
        }
        catch(e){
            console.log(e.errMsg);
        }

        //异常捕获语句的完整形式

        try{
            //可能出现异常的代码
            xyz();

        }
        catch(e){
            //出现异常后的处理代码
        }
        finally{
            console.log("我是finally中的代码");
            //不管有没有出现异常，这里的代码都会执行
            //node.js
            //做释放资源的操作。
        }
	手动抛出异常信息 使用 throw关键字
		unction sum(num1, num2){
            if(num1 == undefined || num2 == undefined){
                throw {
                    errMsg: "能不能好好玩耍了，乖乖给我传参！！",
                    errCode: 13888888888
                };
            }else{
                return num1 + num2;
            }
        }
```


## 面向对象
### 概念
面向过程的思维方式：
            //就是把解决问题的关注点，放到解决问题的每一个详细的步骤上面！
		面向对象的思维方式：
            //就是把解决问题的关注点，放到解决问题需要的一些列对象身上
		在JS当中 什么是对象？
            //键值对儿的组合就是对象
		现实生活中的对象的特征对应到JS当中是对象的属性！

 现实生活中的对象的行为对应到JS当中就是对象方法


```
		//如何在一句话中找出所有的对象
        //名词提炼法！！！
        //小明在公交车上牵着一只叼着香肠的狗
        var xm = {
            name:"小明",
            age:12,
            liuDog:function () {
                console.log("遛狗啦！！！");
            }
        }
	编程
		要求创建出来一个div 并且设置样式，然后加到body标签当中
			面向过程
				1.创建div
//            var div = document.createElement("div");
//            //2.设置div的样式
//            div.style.height = "200px";
//            div.style.width = "200px";
//            div.style.border = "1px solid pink";
//            //3.添加div到body中去
//            document.body.appendChild(div);

			面向对象
				//使用面向对象的思维方式来解决js问题
            $("body").append("<div style='width:200px;height:200px;border:1px solid pink'></div>")
```

面向对象是对面向过程的封装，有了面向对象并不意味着，就可以抛弃面向过程
**为什么要学习面向对象**
看懂框架
		//编写代码的时候的原则：DRY
            //Don’ t repeat yourself
使用函数封装
			使用函数将代码封装，使得复用性更高

#### 使用函数封装带来的问题：
//1.全局变量污染
        //2.代码结构不够清晰，维护不方便
		使用对象封装
			/使用对象进行封装后的优势
        //1.暴露在全局的只有一个对象名 不会造成全局变量污染
        //2.使用对象将代码进行功能模块的划分，有利于日后的维护
	little tip: itar 敲tab就可以出现for循环