## 继承
### 继承的实现方式
当前没有的属性和方法，别人有，拿过来用 ，就是继承
	混入式继承
       

```
 for(var k  in obj){
            o[k] = obj[k];
        }
```


### 经典继承的实现


```
//        function jicheng(obj){
//            var o = {};
//            o.__proto__ = obj;
//            return o;
//        }
//
//        var o = jicheng({name:"张三"});
//        console.log(o);
```


#### 经典继承的语法


```
//Object.create(obj)
        //返回值为一个对象，继承自参数中的obj
        //这个方法是ES5中出来的，所以存在兼容性问题
		var o = {
           name:"周三"
       };

       var obj = Object.create(o);

       console.log(obj.name);
	//如何处理Object.create的兼容性问题
 //检测浏览器的能力，如果没有Object.create方法就给他添加一个（不推荐使用）
		//自己定义个函数
function create(obj){
            if(Object.create){
                return Object.create(obj);
            }else{
                function F() {
                }
                F.prototype = obj;
                return new F();
            }
        }
```


        
### 原型继承的实现
利用原型中的成员可以被和其相关的对象共享这一特性，可以实现继承
这种实现继承的方式，就叫做原型继承
	

```
	Person.prototype.sayHello = function () {
            console.log("我想死你了");
        }
```


1.给原型对象中添加成员（通过对象的动态特性） 不是严格意义上的继承
2.直接替换原型对象
注意：使用替换原型的方式实现继承的时候，原有原型中的成员就会丢失
	

```
	var parent = {
            sayHello : function () {
                console.log("我想你死了");
            }
        }
//
        Person.prototype = parent;
	3.利用混入的方式给原型对象添加成员
		for(var k in parent){
           Person.prototype[k] = parent[k];
       }
       
```


### 继承的应用
开发人员A想要的sayHello    开发人员B想要的sayHello
如果直接修改内置对象的原型，会印象整个开发团队
扩展内置对象（就是给内置对象新增成员）如何安全的扩展一个内置对象？
	

```
	function MyArray() {
            //我自己的属性
            this.name = "我是一个数组";
            this.sayHello = function () {
                console.log("我的sayHello方法");
            }
        }

        var arr = new Array();

        //继承之后，我的数组中就有了原生数组对象的所有的属性和方法
        MyArray.prototype = arr;

        MyArray.prototype.safdaf =function () {

        }

        //myArr这个对象就继承自arr
        var myArr = new MyArray();
```



接着就可以对myArr进行操作了
同理


```
var arr =  new Array();
        function BdeArray(){
            this.sayhello=function () {

            }
        }
        BdeArray.prototype = [];

        var arr = new BdeArray();
```


        
## 原型链
### 原型链
什么是原型链
每个构造函数都有原型对象
        //每个对象都会有构造函数
        //每个构造函数的原型都是一个对象
        //那么这个原型对象也会有构造函数
        //那么这个原型对象的构造函数也会有原型对象
        //这样就会形成一个链式的结构，称为原型链

#### 原型链的基本形式
	

```
	function Person(name){
            this.name = name;
        }
        var p = new Person();
        //p ---> Person.prototype --->Object.prototype---->null
```


####.当访问一个对象的成员的时候，会现在自身找有没有,如果找到直接使用，
		        //2.如果没有找到，则去当前对象的原型对象中去查找，如果找到了直接使用，
		        //3.如果没有找到，继续找原型对象的原型对象，如果找到了，直接使用
		        //4.如果没有找到，则继续向上查找，直到Object.prototype，如果还是没有，就报错
**原型继承概念**
		通过修改原型链结构实现的继承，就叫做原型继承
	
		
### 复杂的原型链
	

```
//动物--->人---->老师---->坏老师

        function Animal(){
            this.gender = "male";
        }

        Human.prototype = new Animal();
        Human.prototype.constructor = Human;

        function Human(){
            this.actionWay = "走路";
        }

        Teacher.prototype = new Human();
        Teacher.prototype.constructor = Teacher;
        function Teacher(){
            this.skill = "教书";
        }

        BadTeacher.prototype = new Teacher();
        BadTeacher.prototype.constructor = BadTeacher;
        function BadTeacher(){
            this.name = "吕超";
        }

        var t = new BadTeacher();
        console.log(t);
```


	
### Object.prototype的成员
constructor
原型对象内的一个属性，指向该原型对象相关联的构造函数
hasOwnProperty
一个方法，用来判断对象本身（不包含原型）是否拥有某个属性
propertyIsEnumerable
1. 判断属性是否属于对象本身
		

```
	console.log(p.propertyIsEnumerable("name"));
		        //    2. 判断属性是否可以被遍历
	Object.defineProperty();
        // 使用以上方法添加属性的时候，可以附加一些信息，
        // 例如这个属性是否可写 可读  可遍历
	toString 和  toLocaleString
		toString:  数字转字符串
		toLocaleString:  对象转字符串，并返回结果
		var o = {};
////        console.log(o.toString());  //[object Object]
////        console.log(o.toLocaleString());   //[object Object]
//
//        var now = new Date();
//        console.log(now.toString());  //时间：Fri Sep 06 2019 20:47:26 GMT+0800 (中国标准时间)
//        console.log(now.toLocaleString());  //时间2019/9/6 下午8:47:26
```

#### valueOf
获取当前对象的值
在对象参与运算的时候
        

```
//1.默认的会先去调用对象的valueOf方法，
        //2.如果valueOf获取到的值，无法进行运算 ，就去去调用p的toString方法  最终做的就是字符串拼接的工作
			function Person(){

        }
        var p = new Person();
 console.log( 1 + p);  //1+[object Object]
	 __proto__
		原型对象对象中的属性
		        //可以使用 对象.__proto__ 去访问原型对象
```

### 创建函数的几种方式
	

```
1.直接声明函数
		function funcName(/*参数列表*/){
            //函数体
        }
	2.函数表达式
		var funcName = function(){

        };
	3.new Function
		ar func = new Function();
```

### Function的几种使用
0.一个参数都不传的情况  创建的就是一个空的函数
       

```
 //var 函数名 = new Function()
		var func = new Function("console.log('我是动态创建的函数');console.log(1);");
       func();
```


1.只传一个参数的情况 这个参数就是函数体
 //var 函数名 = new Function("函数体")
		求数组中的最大值
var max = new Function("arr",
//                "var maxNum = arr[0];" +
//                "for(var i = 1;i<arr.length;i++){" +
//                "if(maxNum < arr[i]){" +
//                "maxNum = arr[i];" +
//                "}" +
//                "}" +
//                "return maxNum;"
//        )
console.log(max([1, 2, 3, 44, 5, 6]));
2.传多个参数的情况，最后一个参数为函数体，前面的参数都是该函数的形参名


```
		var sum = new Function("a", "b", "return a + b;");
//        console.log(sum(1, 1111));
	如何解决使用Funciton创建函数时，代码过长的问题
		1.可以使用字符串拼接 让代码换行
		        //2.使用模板的方式，将代码写在模板标签内，获取该标签的内容
			window.onload =function () {
            var script = document.getElementById("funcContent");
            var str = script.innerHTML;
            var max = new Function("arr", str);
            console.log(max([1, 2, 3, 44, 5, 6]));  //44
        }
			<script type="text/template" id="funcContent">
    var maxNum = arr[0];
    for(var i = 1; i<arr.length; i++){
        if(maxNum < arr[i]){
            maxNum = arr[i];
        }
    }
    return maxNum;
</script>
		        //3.使用反引号（`） 引住字符串，那么就可以 换行了
			var str = `adfafdsa
                asdfas`;
        console.log(str);
```

### arguments对象
利用 Function 创建一个函数,
 要求允许函数调用时传入任意个数参数,
并且函数返回这些数字中最大的数字.
函数内部的一个对象 arguments
当函数调用的时候，系统会将所有传入的实参，依次存入这个数组对象
	

```
	function max(){
        //    console.log(arguments);
            var maxNum = arguments[0];
            for (var i = 1; i < arguments.length; i++) {
                maxNum = maxNum > arguments[i] ? maxNum :arguments[i];
            }
            return maxNum;
        }

        console.log(max(1, 2, 34, 5, 6));
	使用Function创建一个函数，
        //给函数传入任意个数的参数，
        //在函数内进行去重操作，然后返回去重后的数组
		var distinct = new Function(`
            var arr = [];
            for (var i = 0; i < arguments.length; i++) {
                if(arr.indexOf(arguments[i])==-1){
                    arr.push(arguments[i]);
                }
            }
            return arr;
        `);
//        console.log(distinct(1, 2, 34, 34, 5, 5));
```

#### 有无形参
1.一个函数有形参的时候，调用的时候，可以不传参数
2.一个函数没有形参的时候，调用时后，可以传参   arguments对象
3.一个函数不管有没有形参，调用的时候都会把实参的值存入arguments对象
arguments.length  表示传入实参的个数
arguments.callee 指向当前函数  (匿名函数中使用，因为他没有名字)

### eval
val函数可以用来将字符串转换成JavaScript代码并且运行
	

```
//JSON格式的数据  JSON对象有兼容性问题
       var jsonData = '({"name":"zs", "age":18})';
    //   var o = JSON.parse(jsonData);  //兼容性问题
    //    console.log(o);
////
       eval("var o = "+ jsonData);
       var o = eval(jsonData);
       console.log(o);
```


使用eval来解析JSON格式字符串的时候，会将{}解析为代码块，而不是对象的字面量
1.在JSON格式的字符串前面拼接上 "var o ="
不推荐使用eval