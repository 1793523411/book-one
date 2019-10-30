# angularjs代码2

## angularjs中的跨域

**jsonp与ajax没有关系**

PHP文件

```php
<?php

	$arr = array('name'=>'itcast','age'=>10);

	$result = json_encode($arr); // {"name": "itcast", "age": 10}

	$a = $_GET['a']; // fn

	echo $a . '(' . $result . ')'; // fn({"name": "itcast", "age": 10});
	

?>
```



### 原始 js 跨域

```javascript
<script>
		
		function fn(arg) {

			console.log(arg);

			document.write('111');

		}
</script>
<script src="./jsonp.php?callback=fn"></script>
```

### jQuery跨域

```javascript
$.ajax({
			url: 'example.php',
			type: 'post',
			dataType: 'jsonp'
		})
//创建元素
 var script = createElement('script');
		 script.src = url;
		 var head = document.querySelector('head');
		 head.appendChild(script);

$.ajax({
			url: '',
			type: 'get/post',
			dataType: 'jsonp',
			// data: {name: 'itcast', age: 10}, // name=itcast&age=10
			data: 'name=itcast&age=10',
			// 能不能设置请求头？
			success: function (data) {
				// data 返回的数据
			}
		});
// XMLHttpRequest; 是不能完成跨域访问的
//jsonp(跨域解决方案)与json（一数据格式）没一点关系
```

### angularjs中的跨域

```javascript
var App = angular.module('App', []);

		App.controller('DemoController', ['$http', '$scope', function ($http, $scope) {

			$http({
				url: 'jsonp.php?a=JSON_CALLBACK',
				method: 'jsonp' // 采用JSONP方式
			}).success(function (info) {
				console.log(info);
			});

		}]);


$http({
			url: 'example.php?call=JSON_CALLBACK',
			method: 'jsonp',
			headers: {}, // 请求头
			data: {}, // post
			params: {
				call: 'JSON_CALLBACK' // angular_callback.0({name: 1})
			}, // get
		}).success(function (info) {
			// 
		});
```

## 自定义服务

### factory

```javascript
var App =  angular.module('App', []);

		App.controller('DemoController', ['$scope', '$http', 'format', function ($scope, $http, format) {

			var data = {
				name: 'itcast',
				age: 10
			};

			// 测试自定义的服务
			// console.log(format(data));
			console.log(format.format(data));

			$http({
				url: 'example.php',
				method: 'post',
				headers: {
					'Content-Type': 'application/x-www-form-urlencoded'
				},
				data: format.format(data)
			}).success(function (info) {
				// info 
				console.log(info);
			});

		}]);

		// 提供了3种方法实现自定义服务
		// factory、service、value

		App.factory('format', ['$filter', function ($filter) {
			// 自定义服务，但依赖于$filter

			// 定义服务具体功能
			function format(arg) {
				var s = '';
				for(var key in arg) {
					s += key + '=' + arg[key] + '&';
				}

				s = s.slice(0, -1);

				return s;
			}

			// 具体功能
			function sayHello() {
				alert('你好')
			}

			// 返回出去以被调用
			return {
				format: format,
				sayHello: sayHello
			}

		}]);
```

#### service

```javascript
<div ng-controller="DemoController">
		<h1>{{now}}</h1>
	</div>
/*----------------------------*/

var App = angular.module('App', []);

		App.controller('DemoController', ['$scope', 'showTime', function ($scope, showTime) {

			$scope.now = showTime.now();

			showTime.sayHello();

		}]);

		// 自定义服务显示日期
		// 提供了3种方法实现自定义服务
		// factory、service、value
		App.service('showTime', ['$filter', function ($filter) {

			// return {
			// 	showTime: function () {

			// 	}
			// }

			var now = new Date;
			var date = $filter('date');

			// 向对象上添加具体方法
			this.now = function () {
				return date(now, 'yyyy/MM/dd hh:mm:ss');
			}

			// 添加具体方法
			this.sayHello = function () {
				alert('你好');
			}

		}]);
```

#### value(不像前两种一样可以定义对象和方法)

```javascript
<div ng-controller="DemoController">
		{{author}}
		{{version}}
	</div>
/*----------------------------*/
<script>
		var App = angular.module('App', []);

		// 自定义常量服务

		// 提供了3种方法实现自定义服务
		// factory、service、value

		App.value('author', 'zhaoyc');
		App.value('version', '1.0');

		// 本质上一个服务
		// 从表现形式上是一个常量
		// 常量就是不变的值与变对量相对应

		// 声明依赖调用服务
		App.controller('DemoController', ['$scope', 'author', 'version', function ($scope, author, version) {

			$scope.author = author;
			$scope.version =version;

		}])

	</script>

```

