## 待办事项与完成事项


```html

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Tolist</title>
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
			  <input type="checkbox" ng-checked="todo.checked" ng-click="done($index,$event)">
			  {{todo.text}}
			  <a ng-href="" ng-click="delete($index,todos)">删除</a>
		  </dd>
		  <dt>已办事项{{doneTodos.length}}</dt>
		  <dd ng-repeat="todo in doneTodos track by $index">
				<input type="checkbox" ng-checked="todo.checked" ng-click="undone($index, $event)">
				{{todo.text}}
				<a ng-href="" ng-click="delete($index, doneTodos)">删除</a>
			</dd>
	  </dl>
  </div>
  <script src="angular.min.js"></script>
  
```
```javascript
  <script>
	  var app = angular.moudle('App',[]);
	  App.controller('TodoListController',['$scope',function($scope){
		  //待办事项
		  $scope.todos = [];
		  //已完成事项
		  $scope.doneTodos = [];
		// 回车时调用ng-submit，往待办事项中添加数据
		  $scope.addItem = function(){

			  $scope.todos.push({text:$scope.todo,checked:false});

			  $scope.tode='';
		  }
		  // 勾选时完成
		  $scope.done = function(index,ev){
			  var tmp = $scope.todos.splice(index,1);

			  tmp[0].checked = !tmp[0].checked;

			  $scope.doneTodos = $scope.doneTodos.concat(tmp);
				//阻止事件默认行为
			  ev.preeventDefault();
		  }
		  	// 取消已完成
		  $scope.undone = function(index,ev){
			  var tmp = $scope.doneTodos.splice(index,1);

			  tmp[0].checked = !tmp[0].checked;

			  $scope.todos = $scope.todos.conact(tmp);

		  }
		  // 删除事项，传递当前索引和完整数据
		  $scope.delete = function(index,todos){
			  todos.splice(index,1);
		  }
	  }])
  </script>
</body>
</html>


```

