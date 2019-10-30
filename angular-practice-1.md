## 待办事项与完成事项


```html

<!DOCTYPE html>
<html lang="en" ng-app="App">
<head>
	<meta charset="UTF-8">
	<title>TodoList</title>
	<style>
		body {
			padding: 0;
			margin: 0;
		}

		.todo {
			width: 300px;
			margin: 100px auto;
		}

		.todo dd {
			overflow: hidden;
		}

		.todo input[type="checkbox"] {
			float: left;
		}

		.todo a {
			float: right;
		}
	</style>
</head>
<body>
	
	<div class="todo" ng-controller="TodoListController">
		<form ng-submit="addItem()">
			<label for="">添加事项</label>
			<input type="text" ng-model="todo">
		</form>
		<dl>
			<dt>待办事项</dt>
			<dd ng-repeat="todo in todos track by $index">
				<input type="checkbox" ng-checked="todo.checked" ng-click="done($index, $event)">
				{{todo.text}}
				<a ng-href="" ng-click="delete($index, todos)">删除</a>
			</dd>
			<dt>已办事项{{doneTodos.length}}</dt>
			<dd ng-repeat="todo in doneTodos track by $index">
				<input type="checkbox" ng-checked="todo.checked" ng-click="undone($index, $event)">
				{{todo.text}}
				<a ng-href="" ng-click="delete($index, doneTodos)">删除</a>
			</dd>
		</dl>
	</div>

	<script src="./libs/angular.min.js"></script>
  
```
```javascript
  <script>
		// 定义一个模块
		var App = angular.module('App', []);

		// 定义一个控制器
		App.controller('TodoListController', ['$scope', function($scope) {
			
			// 待办事项
			$scope.todos = [];

			// 已完成事项
			$scope.doneTodos = [];

			// 回车时调用ng-submit，往待办事项中添加数据
			$scope.addItem = function () {
				// 向数组中添加数据
				$scope.todos.push({text:$scope.todo, checked: false});
				// 清空输入框
				$scope.todo = '';
			}

			// 勾选时完成
			$scope.done = function (index, ev) {

				// 从待办事项中删除
				var tmp = $scope.todos.splice(index, 1);

				tmp[0].checked = !tmp[0].checked;

				// 将删除的事项添加到已完成里
				$scope.doneTodos = $scope.doneTodos.concat(tmp);

				ev.preventDefault();
			}

			// 取消已完成
			$scope.undone = function (index, ev) {
				// 从已完成数据中删除
				var tmp = $scope.doneTodos.splice(index, 1);

				tmp[0].checked = !tmp[0].checked;

				// 将事项添加到待办事项中
				$scope.todos = $scope.todos.concat(tmp);

			}

			// 删除事项，传递当前索引和完整数据
			$scope.delete = function (index, todos) {
				todos.splice(index, 1);
			}
		}])

	</script>
</body>
</html>


```

## angular跨域天气案例

```html
<body ng-app="Weather">
	
	<div ng-controller="WeatherController">
		<table>
			<tr ng-repeat="weather in weatherData">
				<td>{{weather.date}}</td>
				<td>{{weather.temperature}}</td>
				<td>{{weather.weather}}</td>
				<td>{{weather.wind}}</td>
				<td><img ng-src="{{weather.dayPictureUrl}}" alt=""></td>
				<td><img ng-src="{{weather.nightPictureUrl}}" alt=""></td>
			</tr>
		</table>
	</div>
```



```javascript
<script src="./libs/angular.min.js"></script>
	<script>
			
		var Weather = angular.module('Weather', []);

		Weather.controller('WeatherController', ['$scope', '$http', function ($scope, $http) {

			$http({
				url: 'http://api.map.baidu.com/telematics/v3/weather',
				method: 'jsonp',
				params: {
					location: '北京',
					output: 'json',
					ak: '0A5bc3c4fb543c8f9bc54b77bc155724',
					callback: 'JSON_CALLBACK'
				}
			}).success(function (info) {

				// console.log(info);

				$scope.weatherData = info.results[0].weather_data;

			});


		}]);

	</script>
```

## AngularJS $http服务

```html
<body ng-app="App">
	<h1>总结$http服务</h1>
	<div ng-controller="DemoController">
		<table>

		</table>
	</div>
```



```javascript
<script>
		var App = angular.module('App', []);

		// 杜子腾 肚子疼

		App.controller('DemoController', ['$scope', '$http' ,function($scope, $http) {

			// XMLHttpRequest

			// xhr = new XMLHttpRequest;

			// xhr.open('get', 'xx.php');

			// xhr.send('nane=itcast&age=10');

			$http({
				url: 'example.php',
				method: 'post',
				params: {sex: '男'}, // get 传参
				data: {name: 'itcast', age: 10}, // post 传参
				// restful
				// data: 'name=itcast&age=10',
				// headers: {
				// 	'Content-Type': 'application/x-www-form-urlencoded'
				// }
			}).success(function (data) {
				console.log(data);
			});

		}]);

		// angularjs默认支持restful接口
```

