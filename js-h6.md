## apply补充
当时用call和apply传入的第一个参数为值类型的时候
会将值类型转换成对应的对象（引用类型） 然后赋值给this

       

```
 //当传入的第一个参数为 null或者Undefined的时候，
        //会把this赋值为  window
		//正确的代码
        var arr = [].concat.apply([],obj);
        //[].concat(obj[0],obj[1],obj[2])
        console.log(arr);

        function test() {
//            console.log(this.valueOf());
//            console.log(+this);
            console.log(""+this);
        }
        test.apply(1);
        test.apply("abc");
        test.apply(true)
        test.apply(undefined)
	  //借用构造函数 实现继承
		 function Person(){
            this.name = "张莎";
            this.age = 18;
        }

        function Student(){
            var stu = this;
            Person.apply(stu);
        }

        var stu = new Student();
        console.log(stu);
```
## 注册事件的兼容性处理
1.  ele.on事件类型 = function(){}
2.  addEventListener(事件类型,事件处理函数,useCapture)  第三个参数默认是false，冒泡阶段执行
3.  attachEvent(事件类型，事件处理函数)
封装成函数，问题是每次都会判断


```
//        function registeEvent(target, type, handler){
//            if(target.addEventListener){
//                target.addEventListener(type,handler)
//            }else if(target.attachEvent){
//                target.attachEvent("on"+type,handler)
//            }else{
//                target["on"+type] = handler;
//            }
//        }
```


1.在注册事件的时候，判断浏览器的注册事件的方式，然后直接使用该方式进行注册事件
 复用性太差
 2.将注册事件的代码封装到一个函数中
            //每次调用该函数，都会进行浏览器能力检测
3.在函数中返回函数，让外部函数只执行一次，判断也就只会执行一次
使用函数内创建的函数返回给外界，就可以重复使用该函数，进行事件的注册
	 

```
function createEventRegister(){
            if(window.addEventListener){
                return function(target, type, handler){
//                    this ---> window
                    target.addEventListener(type,handler)
                }
            }else if(window.attachEvent){
                return function(target, type, handler) {
                    target.attachEvent("on" + type, function(){
                        handler.call(target, window.event);
                    })
                }
            }else{
                return function(target, type, handler) {
                    target["on" + type] = handler;
                }
            }
        }

        var registeEvent = createEventRegister();


        window.onload =function () {
            var div = document.getElementById("div1");
            registeEvent(div,"click",function(e){
                console.log(e);
                console.log(this);
                //this---->该事件的触发对象
                alert("太阳天空照，花儿对我笑，小鸟说：完了")
            })
        }
```


使用更好的方式，避免了多次的判断
这里存在问题就是

我们使用统一的方式，进行事件注册

1、注册的事件的处理函数中的，this指向不一致
 使用addEventListener的方式注册的点击事件的回调函数中的this 指向target
 但是使用attachEvent的方式注册点击事件的回调函数中的this 指向window

2、3种注册事件的方式中，回调函数内获取事件对象的方式也是不一致的
要让他们统一，
 在第二种的事件注册方式（attachEvent）中，手动给handler传递window.event


```
			 div.addEventListener("click",function(e){
//            this
//            e.screenX;
//        })
//
//        div.attachEvent("onclick".function(){
////            this--->window
//            window.event.screenX
//        })
```

## 注册事件兼容性分析
	

```
 var div = document.getElementById("dvd1");

            function huidiao(e){
                console.log(e+"就是当前的事件对象")
                console.log( this+ "就是当前你点击的对象");
                alert("我是div的点击事件，所有浏览器中，我的功能都是弹出来这句话！");
            }
	 //通用的
//            div.onclick = huidiao;

            //ie9以上才支持
//            div.addEventListener("click",huidiao)

            //ie9（不包括9）以下支持的
//            div.attachEvent("onclick",function(){
//                huidiao.call(div, window.event);
//            })
```


