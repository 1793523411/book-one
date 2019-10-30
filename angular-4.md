# angularjs代码3

## 模块加载

### 配置快

```html
<div ng-controller="DemoController">
		<h1>{{now}}</h1>
		<h2>{{str|capitalize}}</h2>
	</div>
```



```javascript
	var App = angular.module('App', []);

		// 配置$log服务(禁用debug)

		// config
		// 允许一次配置多个服务（块）
		// 传递的一个数组（依赖注入方式）
		App.config(['$logProvider', '$filterProvider', function ($logProvider, $filterProvider) {

			// $log.debug();
			// 禁用debug功能
			$logProvider.debugEnabled(false);

			// 默认9个过滤器，通过配置可以新增一些过滤器
			$filterProvider.register('capitalize', function () {
				// 新增一个过滤器
				return function (input) {
					return input[0].toUpperCase() + input.slice(1);
				}

			});

		}]);

		// App.config(['$filterProvider', function($filterProvider) {
			
		// 	// 默认9个过滤器，通过配置可以新增一些过滤器
		// 	$filterProvider.register('capitalize', function () {

		// 		return function (input) {
		// 			return input[0].toUpperCase() + input.slice(1);
		// 		}

		// 	});

		// }])

		App.controller('DemoController', ['$scope', '$log', function ($scope, $log) {

			// 测试配置后的结果
			$log.debug('debug');
			$scope.str = 'hello angular';

		}]);
```



### 运行快

```html
<div ng-controller="DemoController">
		{{name}}
	</div>
```



```javascript
var App = angular.module('App', []);

		// 直接运行$http、$rootScope服务
		// $rootScope根作域

		App.run(['$http', '$rootScope', function ($http, $rootScope) {

			// 直接调用$http
			$http({
				url: 'example.php',
				method: 'get'
			});

			// 根作用域
			$rootScope.name = '祖宗';

		}]);

		App.controller('DemoController', ['$scope', function($scope) {
			//
			// 
			$scope.name = '后代';
		}]) 
```



## 路由

### 监听锚点变化然后发送请求

```html
<div class="wrapper">
		<!-- 导航菜单 -->
		<ul>
			<li class="active">
				<a href="#index">Index</a>
			</li>
			<li>
				<a href="#introduce">Introduce</a>
			</li>
			<li>
				<a href="#contact">Contact Us</a>
			</li>
		</ul>
		<!-- 内容 -->
		<div class="content">
			Index Page
		</div>
	</div>
```

```php
<?php


	$hash = $_GET['hash'];

	switch ($hash) {
		case 'index':
			echo '<h1>Index Page!</h1>';
			break;

		case 'introduce':
			echo '<h1>Introduce Page!</h1>';
			break;
		case 'contact':
			echo '<h1>Contact Us Page!</h1>';
			break;
		default:
			# code...
			break;
	}

```



```javascript
// hashchange事件可以监听锚点变化
		window.addEventListener('hashchange', function () {
			// console.log(1);
			// 获取锚点
			var hash = location.hash;
			// 处理#
			hash = hash.slice(1);

			// 实例对象
			var xhr = new XMLHttpRequest;

			// 将锚点做为参数传递给服务端进处理
			xhr.open('get', '10-01.php?hash=' + hash);

			xhr.send(null);

			xhr.onreadystatechange = function () {
				if(xhr.readyState == 4 && xhr.status == 200) {
					var result = xhr.responseText;
					// 将返回结果添加到页面
					document.querySelector('.content').innerHTML = result;
				}
			}
		});
```

### 路由模块进行配置

```html
<div class="wrapper">
		<!-- 导航菜单 -->
		<ul>
			<li class="active">
				<a href="#/index">Index</a>
			</li>
			<li>
				<a href="#/introduce">Introduce</a>
			</li>
			<li>
				<a href="#/contact">Contact Us</a>
			</li>
			<li>
				<a href="#/list">List</a>
			</li>
		</ul>
		<!-- 内容 -->
		<div class="content">
			<!-- 占位符 -->
			<div ng-view></div>
		</div>

	</div>
	<!-- AngularJS核心框架 -->
	<script src="./libs/angular.min.js"></script>
	<!-- 路由模块理解成插件 -->
	<script src="./libs/angular-route.js"></script>
```

```php
<?php


	// 数组
	$items = array('html', 'css', 'js');

	echo json_encode($items);
```



```javascript
// 依赖ngRoute模块
		var App = angular.module('App', ['ngRoute']);

		// 需要对路由模块进行配置，使其正常工作
		App.config(['$routeProvider', function ($routeProvider) {

			$routeProvider.when('/index', {
				// template: '<h1>index Pages!</h1>',
				templateUrl: './abc.html'
			})
			.when('/introduce', {
				template: '<h1>introduce Pages!</h1>'
			})
			.when('/contact', {
				// template: '<h1>contact US Pages!</h1>',
				templateUrl: './contact.html',
				controller: 'ContactController' // 定义控制器
			})
			.when('/list', {
				templateUrl: './list.html', // 视图模板
				controller: 'ListController' // 定义控制器
			})
			.otherwise({
				redirectTo: '/index'
			});

		}]);

		// 列表控制器
		App.controller('ListController', ['$scope', '$http', function ($scope, $http) {
			// 模型数据
			// $scope.items = ['html', 'css', 'js'];

			$http({
				url: '10-02.php',
			}).success(function (info) {
				// console.log(info);

				$scope.items = info;
			});

		}]);

		App.controller('ContactController', ['$scope', '$http', function ($scope, $http) {

			$http({
				url: 'contact.php'
			}).success(function (info) {
				$scope.content = info;
			});

		}]);
```

### $routeParams服务

```html
<div class="wrapper">
		<!-- 导航菜单 -->
		<ul>
			<li class="active">
				<a href="#/index/5/abc/7">Index</a>
			</li>
			<li>
				<a href="#/introduce">Introduce</a>
			</li>
			<li>
				<a href="#/contact">Contact Us</a>
			</li>
			<li>
				<a href="#/list">List</a>
			</li>
		</ul>
		<!-- 内容 -->
		<div class="content">
			<!-- 占位符 -->
			<div ng-view></div>
		</div>

	</div>
```



```javascript
// 依赖ngRoute模块
		var App = angular.module('App', ['ngRoute']);

		// 需要对路由模块进行配置，使其正常工作
		App.config(['$routeProvider', function ($routeProvider) {

			$routeProvider.when('/index/:id/:page/:p', {
				templateUrl: 'abc.html',
				controller: 'IndexController'
			})
			.otherwise({
				redirectTo: '/index'
			});

		}]);

		// 提供了一个专门负责获取参数的一个服务$routeParams
		App.controller('IndexController', ['$scope', '$http', '$routeParams', function ($scope, $http, $routeParams) {

			$scope.content = '练习路由功能';

			console.log($routeParams);

		}]);
```

## angularjs中的jquery

```html
<div ng-controller="DemoController">
		<div class="box">普通一个盒子</div>
		<button>点击</button>
	</div>
```

```javascript
// angular.element() 方法可以将一个原生DOM对象转成jquery对象

		// 原生DOM对象
		var box = document.querySelector('.box');
		var btn = document.querySelector('button');
		// 转成jQuery对象
		box = angular.element(box);
		btn = angular.element(btn);

		btn.on('click', function () {
			// 
			// box.css('color', 'red');

			box.animate({
				fontSize: '40px'
			}, 400);
		});
		//要是用angularjs中没有的animate，需引入jQuery文件
		// 但是angularJS 只是实现了jquery对象部分方法
```

