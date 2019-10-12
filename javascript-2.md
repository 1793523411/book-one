## 数据类型

### 数据类型划分
**使用关键字typeof：查看方法：  typeof name   或者   typeof(name)**
#### 简单数据类型（值类型）
四种： 字符串		数字		布尔		 未定义		空
  String	  Number   Boolean	undefined    null
####　复杂数据类型（引用类型）
Object、function、Array、Date、RegExp、Error.......
### 字面量
固定的值，让你从“字面上”理解其含义。
数值字面量
var age = 18;  // 数值字面量，18为字面值
### 简单数据类型介绍
#### Number
1.进制
  进制包括2进制、8进制（011）、10进制、16进制（0xA）、制等....
2.浮点数
因为精度丢失问题，所以不判断计算后的两个浮点数是否相等。
3.数值范围
由于内存的限制，ECMAScript 并不能保存世界上所有的数值
最小值：Number.MIN_VALUE，这个值为： 5e-324
最大值：Number.MAX_VALUE，这个值为： 1.7976931348623157e+308
无穷大：Infinity
无穷小：-Infinity
4.NaN
* NaN 非数值（Not a Number的简写）


```
console.log(“abc”/18);  //结果是NaN
```


Undefined和任何数值计算为NaN;
NaN 与任何值都不相等，包括 NaN 本身
* isNaN() :任何不能被转换为数值的值都会导致这个函数返回 true 
（isNaN译为是否符合一个标准，什么标准呢？不是一个数字的标准，如果符合了那么就不是一个数字，不符合就是一个数字）


```
isNaN(NaN);// true
isNaN(“blue”); // true
isNaN(123); // false
```


3.3.2	String
1.字面量定义方式
用引号时，可单可双，唯独不可一单一双。可用.length看有几个字符。
var name = "zhangsan";
var name = 'zhangsan';
var name = 'zhangsan"; //错误，单引号和双引号要成对出现
2.转译
总结：无法输出的字符，先输出/，在输出字符。（“、\、换行等....）
3.字符串不可变
   	在内存中不会立刻消失，只能二次赋值，原有的字符在一定时间	内被	垃圾回收器回收。
4.字符串拼接
如果两个变量都是字符串，无论是否包含数字，只要是拼接，那么在前一个后面添加后一个字符串。（+与-情况不同，详情参考数据转换）
3.3.3	Booblean
1.Boolean类型有两个字面量：true和false，区分大小写。（大写不对）
虽然Boolean 类型的字面值只有两个，但 ECMAScript 中所有类型的值都有与这两个 Boolean 值等价的值
2.true
true、除0数字、“something”、Object(任何对象)为true
3.false
false、0 、“”、undefined 、null为false
4.if判断时会把（）内的值强行转换成boolean类型进行判断。
3.3.4	undefined和null
null和undefined有最大的相似性。看看null == undefined的结果(true)也就更加能说明这点。但是null ===undefined的结果(false)。不过相似归相似，还是有区别的，就是和数字运算时，10 + null结果为：10；10 + undefined结果为：NaN。
任何数据类型和undefined运算都是NaN;
任何值和null运算，null可看做0运算。
## 数据类型转换
一、转换成字符串类型
二、转换成数值类型
三、转换成布尔类型
4.1	任何简单类型转换成String（三种方法）
4.1.1	变量+“”   或者     变量+“abc”
4.1.2	String(变量)
4.1.3	变量.toSting() 	注意：undefined和null不可以
Null和undefined无toString方法。
4.2	任何简单类型转换成Number
此转换容易产生NaN，一旦被转换的变量中含有非数字字符，都容易出现NaN
4.2.1	变量-*/一个数字（有非数字字符会出现NaN）
例：var  num1  = “11”- 0;  var num2 =“11”* 1;var num =“11”/1;
JS底层做了一个强制类型转换，把字符串转换成了Number进行运算。
4.2.2	Number(变量)（有非数字字符会出现NaN）
var num1 = Number(“18”);		把字符变成了数字。
var num2 = Number(“18.99”);   结果为18.99数字型。（有小数也转换）
4.2.3	parseInt()和parseFloat()（译为取整和取浮点数）
空字符串parseInt()和parseFloat()返回NaN，Number("")返回0
parseInt(变量)：如果变量中收割字符为字母则结果为NaN。
否则取出现首个非数字前的整数。
123 = parseInt(“123.123aaaa”);

parseFloat(变量)：如果变量中收割字符为字母则结果为NaN。
否则取出现首个非数字前的浮点数。（没有小数取整）
123.123 = parseFloat(“123.123aaaa”);
4.2.4	提别提示
Boolean类型中：true数值为1；false为0；
null的数值类型为0；
undefined无数值类型或者为NaN;
4.3	任何简单类型转换成Boolean
任何数据类型都可以转换成boolean类型，所以和以往两个转换不同；
4.3.1	Boolean(变量)		
var bool = Boolean(“1111”);			bool为true；
4.3.2	！！变量
第一个逻辑非操作会基于无论什么操作数返回一个与之相反的布尔值
第二个逻辑非操作则对该布尔值求反
于是就得到了这个值真正对应的布尔值
