## instanceof

instanceof  关键字

语法    对象 instanceof 构造函数

判断该构造函数的原型是否存在于该对象的原型链上

```
p---&gt;Person.prototype---&gt;Object.prototype---&gt;null

  var p = new Person\(\);

//构造函数的\*\*原型\*\*是否在该对象的原型链上！

 console.log\(p instanceof Person\);//ture
```
## Function也可以被当做一个构造函数
通过Function new出来函数可以被当做是实例化的对象
那么Function这个构造函数也有原型对象
Function的原型对象是一个空的函数
		ƒ () { [native code] }
Function的原型对象的原型对象是Object.prototype
		Object

### object和function的关系
Object构造函数 是 通过  Function 构造函数  实例化出来的
Function构造函数 也是 通过 Function 构造函数 实例化出来的（不要强行去理解）

### function与eval的区别
不同点
Function 创建出来的是函数，不会直接调用，除非手动调用
 eval 直接可以将字符串转换成代码，并执行
都可以将字符串转换成代码

## 对象方法中的this
	

```
var o = {
            name:"张三",
            sayHello:function () {
                this.sayHi();
            },
            sayHi:function(){
                console.log("Hello 我是" + this.name);
            }
        }
```

## 递归
在函数内调用函数自己，就是递归
没有递归结束条件的递归，就是死递归
1.自己调用自己
2.要有结束的条件
使用递归的方法
化归思想：
化归思想，将一个问题由难化易，由繁化简，由复杂化简单的过程称为化归，它是转化和归结的简称。
分析问题	

```
	 //1-100之间的和
        //1-1   1
        //1-2   1 + 2
        //1-3   1 + 2 + 3
        //1-4   1 + 2 + 3 + 4
        //1-n   1到(n-1)的和 + n
		function sum(n){
            if(n == 1)
            {
                return 1;
            }
            //return 1+2+3
            //return 1+2
            return sum(n-1) + n;
        }
```

### 递归示例
求阶乘
_求斐波那契数列_
遍历所有后代元素
给页面中所有的元素添加一个边框  1px solid pink
DOM中，没有提供直接获取后代元素的API
但是可以通过childNodes来获取所有的子节点
先找body的所有子元素
再找body的子元素的所有子元素

三种方式
		

```
	function getChildNode(node){
                //先找子元素
                var nodeList = node.childNodes;
                //在用子元素再找子元素  这里就可以递归了
                //for循环中的条件，就充当了结束的条件
                for (var i = 0; i < nodeList.length; i++) {
                    //childNode获取到到的节点包含了各种类型的节点
                    //但是我们只需要元素节点  通过nodeType去判断当前的这个节点是不是元素节点
                    var childNode = nodeList[i];
                    //判断是否是元素节点
                    if(childNode.nodeType == 1){
                        childNode.style.border = "1px solid pink";
                        getChildNode(childNode);
                    }
                }
getChildNode(document.body);
```


		

```
	function getChildNode(node){
                //先找子元素
                var nodeList = node.childNodes;
                //在用子元素再找子元素  这里就可以递归了
                //for循环中的条件，就充当了结束的条件
                for (var i = 0; i < nodeList.length; i++) {
                    //childNode获取到到的节点包含了各种类型的节点
                    //但是我们只需要元素节点  通过nodeType去判断当前的这个节点是不是元素节点
                    var childNode = nodeList[i];
                    //判断是否是元素节点
                    if(childNode.nodeType == 1){
                        allChildren.push(childNode)  //全局变量  不用返回
                        getChildNode(childNode);
                    }

                }
            }

            getChildNode(document.body);

            for (var i = 0; i < allChildren.length; i++) {
                var child = allChildren[i];
                child.style.border= "1px solid pink";

            }
```


		

```
	function getChildNode(node){
                //先找子元素
                var nodeList = node.childNodes;
                var result = [];  //局部变量  需返回
                //在用子元素再找子元素  这里就可以递归了
                //for循环中的条件，就充当了结束的条件
                for (var i = 0; i < nodeList.length; i++) {
                    //childNode获取到到的节点包含了各种类型的节点
                    //但是我们只需要元素节点  通过nodeType去判断当前的这个节点是不是元素节点
                    var childNode = nodeList[i];
                    //判断是否是元素节点
                    if(childNode.nodeType == 1){
                        result.push(childNode);
                        var temp = getChildNode(childNode);
                        result = result.concat(temp);
                    }

                }
                return result;
            }

            1.第一次调用时获取body的所有子元素,会把所有的子元素全部放到result里面
            2.每放进去一个 就找这个子元素的所有子元素  有返回值
            3.把这个返回值和我们存当前子元素的数组拼接起来 就变成了 子元素 和 孙子元素的集合


            var arr = getChildNode(document.body);

            for (var i = 0; i < arr.length; i++) {
                var child = arr[i];
                child.style.border= "1px solid pink";

            }
```



