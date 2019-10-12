# 简单对象及数组高级api

## JS中的对象（Object）

#### 创建空白对象

var  obj  =  new  Object\(\);

## 构造函数（就是为了创建对象实例）

一、可以创建对象实例的函数。  
二、区别与普通函数，首字母大写。

### 创建自定义对象

#### This

一、this只出现在函数中。  
二、谁调用函数，this就指的是谁。  
三、new People\(\);   People中的this代指被创建的对象实例。

#### new

1.开辟内存空间，存储新创建的对象（ new Object\(\) ）  
2.把this设置为当前对象  
3.执行内部代码，设置对象属性和方法  
4.返回新创建的对象  
十进制的值 = 位值_进制（位数-1） +位值_进制（位数-1） +位值\*进制（位数-1）............

### 对象字面量个JSON

```
var obj = {aaa: 111};        var json = {“aaa”:111};
```

对象字面量定义方法和json很像，只有一点不同，json的key要求必须加“”;

### Json组成

```
Var json = {“aaa”: 1,“bbb”: 2,“ccc”: 3,“ddd”: 4}
```

Json由{}和key:value以及逗号组成，三部分。（只有一个键值对key:value时,可以没有逗号）

### For...in...

```
Var json = {“aaa”: 1,“bbb”: 2,“ccc”: 3,“ddd”: 4}
for(var key in json){
//key代表aaa,bbb.....等
//json[key]代表1,2,3....等
}
```

### 参数和传值问题

一、简单类型数据做参数，函数内部对参数的修改不应影响外部变量  
简单类型传数值。  
二、复杂类型数据做参数，函数内部对参数的修改会应影响外部变量  
复杂类型传地址。

## 高级数组api

### 侧重点（四点）

调用者：谁调用的。  
参数：有无，几个。  
返回值：有无，什么类型。  
功能：干什么用的。

### Array的内置方法

#### 判断数组和转换数组。

```
Instanceof:  是一个关键字。    判断A是否是B类型。
```

布尔类型值 = A Instanceof B ;

```
Array.isArray()    //HTML5中新增    判断是不是数组
```

布尔类型值 = Array.isArray\(变量\) ;  
调用者：Array            参数：变量\(被检测值\)        返回值：布尔类型

```
toString()        //把数组转换成字符串，每一项用,分割
```

字符串  =  数组.toString\(\);

```
valueOf()        //返回数组对象本身
```

数组本身 = 数组.valueOf\(\);

```
Join            //根据每个字符把数组元素连起来变成字符串
```

字符串  =  数组.join\(变量\);  
变量可以有可以没有。不写默认用逗号分隔，无缝连接用空字符串。

#### 数组增删和换位置（原数组讲被修改）

```
push()  //在数组最后面插入项，返回数组的长度
```

数组1改后的长度  =  数组1.push\(元素1\);

```
pop()    //取出数组中的最后一项，返回最后一项
```

被删除的元素  =  数组1.pop\(\);

```
unshift()   //在数组最前面插入项，返回数组的长度
```

数组1改后的长度  =  数组1.unshift\(元素1\);

```
shift()        //取出数组中的第一个元素，返回最后一项
```

被删除的元素  =  数组1.shift\(\);

```
reverse()    //翻转数组（原数组讲呗反转，返回值也是被反转后的数组）
```

反转后的数组  =  数组1.reverse\(\);

```
sort();    //给数组排序，返回排序后的数组。如何排序看参数。
从小到大排序后的数组  =  数组1.sort(function(a,b){
                                  return a-b;
});
```

无参：按照数组元素的首字符对应的Unicode编码值从小到大排列数组元素。  
带参：必须为函数（回调函数--callback）。函数中带有两个参数，代表数组中的        前后元素。如果计算后（a-b），返回值为负数，a排b前面。等于0不动。        返回值为正数，a排b后面。

#### 其他方法

```
concat()  //把参数拼接到当前数组
新数组 = 数组1.concat(数组2);
slice() //从当前数组中截取一个新的数组，不影响原来的数组，参数start从0开始,end从1开始
新数组 = 数组1.slice(索引1，索引2);
splice()//删除或替换当前数组的某些项目，参数start,deleteCount,options(要替换的项目)
新数组 = 数组1.splice(起始索引，结束索引，替换内容);
indexOf()、lastIndexOf()   //如果没找到返回-1
索引值 = 数组.indexOf/lastIndexOf(数组中的元素);

迭代方法 不会修改原数组
every()、filter()、forEach()、map()、some()
数组/boolean/无 = 数组.every/filter/forEach/map/some(
                            function(element,index,arr){
                                            程序和返回值；                          
   }
);
//对数组中每一项运行以下函数，如果都返回true，every返回true，如果有一项返回false，则停止遍历 every返回false；不写默认返回false
array.every(function(item,index,arr) {
})
//对数组中每一项运行以下函数，该函数返回结果是true的项组成的新数组
var arr = array.filter(function(item,index,arr) {
});
console.log(arr);  
//遍历数组
array.forEach(function(item,index,arr){
});
//对数组中每一项运行以下函数，返回该函数的结果组成的新数组
var arr = array.map(function(item,index,arr) {
    return "\"" + item + "\"";
})
//对数组中每一项运行以下函数，如果该函数对某一项返回true，则some返回true
var b =  array.some(function(item,index,arr) {
    if (item == "ww") {
        return true;
    }
    return false;
});
```

#### 清空数组

```
var array = [1,2,3,4,5,6];
array.splice(0,array.length); //删除数组中所有项目 
array.length = 0; //length属性可以赋值，其它语言中length是只读
array = [];  //推荐
```

  


## 构造函数的原理

function Num\(aaa\){

this\["\[\[PrimitiveValue\]\]"\] = num/1;

return aaa/1;

}

