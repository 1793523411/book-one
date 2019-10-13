## 面向对象三大特征

### 封装

### 继承

javaScript当中的继承是指

```
//一个对象没有一些方法和属性，但是另外一个对象有
//把另外一个对象的属性和方法，拿过来使用，就是继承
混入式继承
//混入式继承（mix-in）  for in

for(var k in obj1){
            //k可以获取到对象的每一个属性
            //obj1[k]可以获取到对象的每一个属性的值
            //这里使用k给对象新增属性的时候，不可以使用点语法
            obj[k] = obj1[k];
        }
```

### 多态

多态是在强类型语言中比较常用，JavaScript中没有相应的体现  
父类的属性和方法供所有的子类共享 但是父类不能访问子类的属性和方法  
使用父类的引用（指针）指向子类的对象 就叫做多态  
//使用多态来隐藏不同

## 创建对象的方式

对象：字面量  
只能创建一次对象，复用性较差，如果要创建多个对象，代码冗余度太高

```
        var obj = {
//            name:"演员",
//            singer:"薛段子手",
//            type:"流行"
//        };
### 使用内置构造函数
        var obj = new Object();
        obj.name = "一千个伤心的母牛";
//        obj.singer = "张学友";
//        obj.sing = function () {
//            console.log("一千个伤心的母牛");
//        }
```

### 封装简单的工厂函数（不推荐使用了）

```
    function createSong(songName,singerName){
            var o =new Object();
            o.name = songName;
            o.singer = singerName;
            o.sing = function () {
                console.log("让我来唱首歌");
            }
            return o;//{name:"",singer:"",sing:function...}
        }
        var obj = createSong("演员","薛之谦");
        var obj1 = createSong("一言难尽","张宇");
```

### 自定义构造函数  Object Array

什么是构造函数?

```
 //构造函数其实也是函数，但是通常用来初始化对象
        //并且和new关键字同时出现
        new 是用来创建对象的
        //构造函数时用来初始化对象的(给对象新增成员)

        构造函数名，首字母要大写！！！以示区分
            function Person() {
            //默认隐含的操作，把刚才用new新创建出来的对象赋值给this
            this.name = "尼古拉斯凯奇";
            this.age = 50;
            this.sayHello = function () {
                console.log("Hey man");
            }
            //如果这里写其他的代码，会执行吗？  肯定会
            return null;
        }
        var p = new Person();//new Object();
        console.log(p);
        p.sayHello();
        构造函数的执行过程
        //1.使用new关键字创建对象
        //2.调用构造函数，把新创建出来的对象赋值给构造函数内的this
        //3.在构造函数内使用this为新创建出来的对象新增成员
        //4.默认返回新创建的这个对象 （普通的函数，如果不写返回语句，会返回undefined）
            new
        构造函数的返回值
        //1.如果不写返回值，默认返回的是新创建出来的对象 （一般都不会去写这个return语句）
        //2.如果我们自己写return语句 return的是空值（return;），或者是基本类型的值或者null，都会默认返回新创建出来的对象
        //3.如果返回的是object类型的值，将不会返回刚才新创建的对象，取而代之的是return后面的值
    自定义构造函数2
        对象是无序的键值对儿的集合
            // function Animal(name, type, barkWay) {
        //     this.name = name;
        //     this.type = type;
        //     this.bark = barkWay;
        // }’
        注意：如果像使用正常的函数一样使用构造函数
        //构造函数中的this将不再指向新创建出来的对象（因为根本就没有创建对象）
        //构造函数中的this这个时候指向的就是window全局对象
        //当使用this给对象添加成员的时候，全部都添加到了window上
             Animal("","",function () {
//            console.log("我是函数");
//        }); //这是一个错误的演示
 window.bark();
//        var dog = new Animal("大黄","BYD",function () {
//            console.log("汪汪汪");
//        });
//        console.log(dog);
        js中提供了两个方法来调用其他对象的方法
//        //call
//        //apply
        //获取具体类型的方式
//        //var typeStr = Object.prototype.toString.call(想获取类型的对象)
//        //typeStr = typeStr.slice(8, -1)
        var o = {};  //构造函数是Object
//        var b = [];  //构造函数Array
var c = /sdfa/;
```

## 传统构造函数存在的问题

/如果构造函数没有参数，那么在调用的时候 小括号 可以省略  
    如果在构造函数中定义函数，那么每次创建对象，都会重新创建该函数  
        //但是函数内部代码完全相同，就造成了资源浪费  
        //为了处理这个问题，我们要让所有的对象共用一个方法  
        //在构造函数外部定义好该函数，将该函数赋值给构造函数内的方法  
    使用这种方式写好的方法中的this指向的就是调用该方法的对象  
        //this 谁调用就是谁  
        //使用这种方式存在的问题  
        1.全局变量增多，造成污染  
        2.代码结构混乱，不易维护

## 原型

原型是个什么玩意儿？  
//在构造函数创建出来的时候，系统会默认的帮构造函数创建并关联一个神秘的对象，这个对象就是原型  
//原型默认的是一个空的对象

### 原型的作用

```
//原型中的属性和方法 可以被使用该构造函数创建出来的对象 使用
    如何访问构造函数的原型
        // 构造函数.prototype
        console.log(Person.prototype);//object
     console.log(p.prototype); //undefine//注意 prototype是构造函数的属性，跟对象没有关系
    如何给原型对象添加属性和方法？
        //使用对象的动态特性
        Person.prototype.exercise = function () {
            console.log("强身健体，保卫祖国");
        }

        p.exercise();
        当使用对象去访问属性和方法的时候
        //会首先在对象自己内部进行查找，如果找到了，就直接使用
        //如果没有找到，就去原型中查找，查找到之后，使用
        //如果原型中还没有， 如果是属性，就是Undefined
        //如果是方法，就报错
//        p.sing();  //本身和原型中都没有 就报错
```

## 相关概念的补充

```
/实例化
 //通过构造函数创建对象的过程 就叫做实例化
var p = new Person(); //实例化  person为构造函数
    //实例
        //通过构造函数实例化出来的对象就是该构造函数的一个实例
        //说实例的时候，一定要指定好构造函数  某某某 是 某某某构造函数的实例
```

## 原型使用方法

1.利用对象的动态特性给原型对象添加成员  
    2.直接替换原型对象  
        在替换原型之前创建的对象的原型 和 在替换原型对象之后的创建的对象  
的原型 不是同一个！  
        类似于基本类型的复制，将原型变成两份 原来的对替换之前创建的对象有效，替换过后的对替换后创建的对象有效

## 原型注意事项

1.使用对象访问属性的时候，如果在本身内找不到就会去原型中查找  
        但是使用点语法进行属性赋值的时候，并不会去原型中进行查找  
      使用点语法赋值的时候如果，对象中不存在该属性，就会给该对象新增该属性，而不会去修改原型中的属性  
2.如果在原型中的属性是引用类型的属性，  
       那么所有的对象共享该属性，并且一个对象修改了该引用类型属性中的成员，其他对象也都会受影响  
3.一般情况下不会将属性放到原型对象中  
        一般情况下原型中只会放需要共享的方法

## **proto**

```
    1.通过构造函数访问原型
//        Person.prototype
    //2.通过对象访问原型

        //__proto__属性
        //__proto__是一个非标准的属性
        //为了保证通用性 这个属性不推荐使用

        //__proto__属性的用途
        //主要用来做调试
    function Person() {

        }
 Person.prototype.msg = "在不在！";
        var p = new Person();
console.log(p.__proto__);
        p.__proto__.sayHello = function () {
            console.log("你好")
        }
        p.sayHello();
```

## constructor

```
/原型对象在创建出来的时候，会默认的有一个constructor属性
    //指向对应的构造函数
```

//        var o = Person.prototype;  
//        Person.prototype.constructor  
    var p1 = new p.constructor\("张学友1","19","male",x\);//相当于直接使用 new Person\(\)

## 构造函数属性相关问题

在使用新的对象替换掉默认的原型对象之后  
        //原型对象中的constructor属性会变成 Object  
        //为了保证整个  构造函数---原型----对象 之间的关系的合理性  
        //应做如下操作：  
        //在替换原型对象的时候，在新的原型对象中手动添加 constructor 属性  
        加constructor让其在指回来

```
function Person(){
        }

        console.log(Person.prototype.constructor);

        Person.prototype = {     //ƒ Person(){ }
            constructor : Person
        };
        // Person.prototype = {     //ƒ Object() { [native code] }

        // };

        console.log(Person.prototype.constructor);
```

## 使用原型解决传统构造函数的问题

```
function Person(name, age, gender) {
            this.name = name;
            this.age = age;
            this.gender = gender;
//            this.sayHello = function () {
//                console.log("你好我是" + this.name);
//            }
        }

        var p =new Person("张学友",18,"male");

        var p1 = new Person("刘德华",19,"male");

        Person.prototype.sayHello = function () {
            console.log("你好我是" + this.name);
        }

        Person.prototype["sing"] = function () {
            console.log("一千个伤心的母牛");
        }

        p.sayHello();
        p1.sayHello();

        p.sing();
        p1.sing();
```

如何使用原型来解决构造函数存在的问题？  
        构造函数的原型对象中的成员，可以被该构造函数创建出来的所有对象访问  
        而且，所有的对象共享该对象  
        所以，我们可以将构造函数中需要创建的函数，放到原型对象中存储  
        这样就解决 全局变量污染的问题 以及 代码结构混乱的问题

