# angularjs代码



## angularjs过滤器

### 过滤器

```html
<body ng-app="App">
	
	<ul ng-controller="DemoController">
		<li>{{price|currency:'￥'}}</li>
		<li>{{now|date:'yyyy/MM/dd hh:mm:ss'}}</li>
		<li>{{items|filter:'s'}}</li>
		<li>{{students|filter:{age: 16} }}</li>
		<li>{{students|json}}</li>
		<li>{{items|limitTo:-1}}</li>
		<li>{{str|uppercase|limitTo:3}}</li>
		<li>{{str|lowercase}}</li>
		<li>{{num|number:2}}</li>
		<li>{{items|orderBy: '':true}}</li>
		<li>{{students|orderBy: 'age': false}}</li>
	</ul>

	<script src="./libs/angular.min.js"></script>
```



```java

	<script>
		var App = angular.module('App', []);

		App.controller('DemoController', ['$scope', function ($scope) {

			$scope.price = 11.11;

			$scope.now = new Date;

			$scope.items = ['html', 'css', 'js'];

			$scope.students = [
				{name: '小红', age: 16},
				{name: '小明', age: 16},
				{name: '小米', age: 10}

			];

			$scope.str = 'hello Angular';

			$scope.num = '10.2345';


		}]);

```

### 自定义过滤器

```javascript
// 自定义过滤器
		App.filter('demo', function () {

			return function (input) {
				console.log('hello' + input);

				return 'hello' + input;
			}
		});

		App.filter('capitalize', function () {
			// console.log(input);传参在return后的函数内传，类似于这种写法错误

			return function (input, arg2) {
				// console.log(arg2);
				return input[0].toUpperCase() + input.slice(1);
			}

		});
```



## angularjs依赖注入

### 行内注入

```javascript
var App = angular.module('App', []);

		// 行内式注入
		App.controller('DemoController', ['$scope', '$http', function (abc, bcd) {

			abc.name = '依赖注入';

		}]);
```

### 推断式依赖注入(传递)

```javascript
var App = angular.module('App', []);

		// AngularJS 内置一些具有特殊功能的“模块”
		// 开发者在开发的时候可以直接使用这些“模块”

		// 推断式依赖注入，压缩可能会出错
		App.controller('DemoController', function ($scope, $http) {

		});
```

## angularjs服务

```javascript
var App = angular.module('App', []);

		// $location内置服务

		// AngularJS 专门提供了一个帮你获URL地址一个服务

		App.controller('DemoController', ['$scope', '$location', function($scope, $location) {
			
			$scope.title = '学习$location服务';

			// $location就是angularJS提前封装好的
			// 提供获取地址相关信息的服务
			console.log($location);

			$scope.absUrl = $location.absUrl();

			$scope.url = $location.url();//锚点后面的内容：...#/ascads

			$scope.host = $location.host();

			$scope.search = $location.search();

			$scope.hash = $location.hash();

			$scope.protocol = $location.protocol();

			$scope.port = $location.port();

		}]);
```

### 计时服务

```html
<div ng-controller="DemoController">
		<ul>
			<li>{{msg}}</li>
			<li>{{now|date: 'yyyy-MM-dd hh:mm:ss'}}</li>
			<li><button ng-click="stop()">停</button></li>
		</ul>
	</div>
```

```javascript
var App = angular.module('App', []);

		App.controller('DemoController', ['$scope', '$timeout', '$interval',function ($scope, $timeout, $interval) {

			$timeout(function () {
				// console.log('执行了');
				$scope.msg = '执行了';

			}, 3000);

			// var i = 0;

			var timer = $interval(function () {

				// console.log(++i);
				$scope.now = new Date;

			}, 1000);

			$scope.stop = function () {
				$interval.cancel(timer);
			}

		}]);
```

### 过滤器服务

```javascript
var App = angular.module('App', []);

		// $filter是过滤器
		App.controller('DemoController', ['$scope', '$filter', function ($scope, $filter) {

			// $filter是九种过滤器中任何一个
			$scope.price = 11.11;

			var currency = $filter('currency');

			$scope.price = currency($scope.price);

			$scope.str = 'hello angular';

			var uppercase = $filter('uppercase');

			$scope.str = uppercase($scope.str);

			$scope.str1 = $filter('limitTo')($scope.str, 2);


		}]);
```

### 日志服务

```javascript
var App = angular.module('App', []);

		// 使用日志服务
		App.controller('DemoController', ['$log', function ($log) {

			$log.info('普通信息');

			$log.warn('警告信息');

			$log.error('错误信息');

			$log.log('打印信息');

			$log.debug('调试信息');

		}]);
```

### $http服务

```php
<?php

	// echo 'success';

	echo $_POST['age'];
```



```javascript
var App = angular.module('App', []);

		App.controller('DemoController', ['$scope', '$http', '$log', function ($scope, $http, $log) {

			// 

			// $http 本质是对XMLHttpRequest对象封装
			// var xhr = new XMLHttpRequest;
			// 打开一个链接
			// xhr.open('get/post', 'example.php?name=itcast');

			// xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');

			// xhr.send('age=10');

			$http({
				url: 'example.php',
				// method: 'get',
				method: 'post',
				headers: {
					'Content-Type': 'application/x-www-form-urlencoded'
				
				},
				params: { // get 参数
					name: 'itcast',
					sex: '男'
				},
				// data: 'age=10'
                //jQuery帮转了，而angularjs没帮转
				data: { // post 传参
					age: 10
				}
			}).success(function (info) {
				// info 就是返回的数据
				$log.info(info);
			});

		}]);

		// 接口方式
		// SOAP RESTFUL

		// 一个说你该如何请求数据的文档

		// 请求地址: xxx/xxx.php
		// 请求方式：post
		// 参数：id [用户ID] page [页码]

		// 如下数据
		// [] '' {}


		// 传递的数据可以是'key=val&key=val'形式，这种形式叫formData
		// Content-Type 设成 application/x-www-form-urlencoded
		// 当请求数据类型不一样，后端在接收的时采取方法也不一样
		// 假如上述方式以PHP为例可以使用$_POST接收

		// application/json;charset=UTF-8 就是json对象形式传
		// Request Payload
		// 假如采用上述方式，以PHP为例$_POST就不能接收了
```



### 打印json数据

```php
<?php
	// PHP程序去获取数据

	$result = file_get_contents('./stars.json');

	echo $result;

```

```javascript
var App = angular.module('App', []);

		App.controller('StarController', ['$http', '$scope', '$log', function ($http, $scope, $log) {

			$scope.getData = function () {

				// 发送请求
				$http({
					url: './stars.php',
					method: 'get'
				}).success(function (info) {
					$log.info(info);

					$scope.stars = info;
				});

			}

		}]);
```

```html
<div ng-controller="StarController">
		<button ng-click="getData()">获取数据</button>
		<table>
			<tr>
				<td>姓名</td>
				<td>年龄</td>
				<td>性别</td>
				<td>头像</td>
				<td>专辑</td>
			</tr>
			<tr ng-repeat="star in stars">
				<td>{{star.name}}</td>
				<td>{{star.age}}</td>
				<td>{{star.sex}}</td>
				<td>{{star.photo}}</td>
				<td>{{star.ablum}}</td>
			</tr>
		</table>
	</div>
<script src="./libs/angular.min.js"></script>
```

```jso
[
	{
		"name": "王力宏",
		"photo": "./images/wlh.jpg",
		"ablum": "<<改变自已>>",
		"age": 39,
		"sex": "男"
	},
	{
		"name": "王力宏",
		"photo": "./images/wlh.jpg",
		"ablum": "<<改变自已>>",
		"age": 39,
		"sex": "男"
	},
	{
		"name": "王力宏",
		"photo": "./images/wlh.jpg",
		"ablum": "<<改变自已>>",
		"age": 39,
		"sex": "男"
	},
	{
		"name": "王力宏",
		"photo": "./images/wlh.jpg",
		"ablum": "<<改变自已>>",
		"age": 39,
		"sex": "男"
	}
]
```

