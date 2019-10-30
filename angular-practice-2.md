## 案例

**类似于tab切换，但是加入了路由**

```css
.music-box {
			width: 400px;
			margin: 100px auto;
		}

		nav {
			height: 40px;
			text-align: center;
			line-height: 40px;
			background-color: #000;
			display: flex;
		}

		a {
			display: block;
			flex: 1;
			color: #FFF;
			text-decoration: none;
		}

		ul {
			padding: 0 10px;
			margin: 0;
			list-style: none;
			border: 1px solid #CCC;
		}

		ul li {
			line-height: 1;
			padding: 5px 0;
			margin: 5px 0;
		}

		ul li:hover {
			background-color: #d8f0f0;
		}
```



```html
<div class="music-box">
		<nav ng-controller="NavController">
			<a href="#/{{nav.id}}" ng-repeat="nav in navs">{{nav.text}}</a>
		</nav>
		<div ng-view></div>
	</div>
```

模板html

```html
<ul>
	<li ng-repeat="list in lists">{{$index + 1}} {{list.text}}</li>
</ul>
```



```javascript
var App = angular.module('Music', ['ngRoute']);

		App.config(['$routeProvider', function($routeProvider) {
			$routeProvider.when('/:pid', {
				templateUrl: 'tpl.html',
				controller: 'ListController'
			});
		}])

		App.controller('NavController', ['$scope', '$http', function($scope, $http) {

			$http({
				method: 'get',
				url: 'navs.php'
			}).success(function (data) {
				$scope.navs = data;
			});
		}])

		App.controller('ListController', ['$scope', '$http', '$routeParams', function($scope, $http, $routeParams) {

			var pid = $routeParams.pid || 1;

			$http({
				method: 'get',
				url: 'list.php',
				params: {pid: pid}
			}).success(function (data) {
				$scope.lists = data;
			});

		}])
```

```php
//list.php
<?php

	$list = array(
		array('id'=>1, 'pid'=>2, 'text'=>'我很丑可是我很温柔'),
		array('id'=>2, 'pid'=>2, 'text'=>'浦公英的约定'),
		array('id'=>3, 'pid'=>2, 'text'=>'你我的约定'),
		array('id'=>4, 'pid'=>3, 'text'=>'pretty boy'),
		array('id'=>5, 'pid'=>3, 'text'=>'See You Again'),
		array('id'=>6, 'pid'=>2, 'text'=>'甜甜的'),
		array('id'=>7, 'pid'=>1, 'text'=>'再见 我的爱人'),
		array('id'=>8, 'pid'=>2, 'text'=>'心中的日月'),
		array('id'=>8, 'pid'=>3, 'text'=>'Let It Go'),
		array('id'=>10, 'pid'=>1, 'text'=>'不要说再见'),
		array('id'=>11, 'pid'=>3, 'text'=>'Rise'),
		array('id'=>12, 'pid'=>2, 'text'=>'再见'),
		array('id'=>13, 'pid'=>1, 'text'=>'追梦人'),
		array('id'=>14, 'pid'=>2, 'text'=>'不能说的秘密'),
		array('id'=>15, 'pid'=>4, 'text'=>'고속도로 로맨스'),
		array('id'=>16, 'pid'=>1, 'text'=>'昨日重现'),
		array('id'=>17, 'pid'=>3, 'text'=>'Love Me Like You Do'),
		array('id'=>18, 'pid'=>2, 'text'=>'好久不见'),
		array('id'=>19, 'pid'=>1, 'text'=>'独角戏'),
		array('id'=>20, 'pid'=>2, 'text'=>'K歌之王'),
		array('id'=>21, 'pid'=>1, 'text'=>'往事随风'),
		array('id'=>22, 'pid'=>2, 'text'=>'光辉岁月'),
		array('id'=>23, 'pid'=>3, 'text'=>'Just Like Fire'),
		array('id'=>24, 'pid'=>4, 'text'=>'涙の物语'),
		array('id'=>25, 'pid'=>4, 'text'=>'江南Style'),
		array('id'=>26, 'pid'=>4, 'text'=>'ガラガラ'),
		array('id'=>27, 'pid'=>1, 'text'=>'海阔天空'),
		array('id'=>28, 'pid'=>4, 'text'=>'天空之城'),
		array('id'=>29, 'pid'=>4, 'text'=>'사랑이었다'),
		array('id'=>30, 'pid'=>3, 'text'=>' Good Time'),
		array('id'=>31, 'pid'=>1, 'text'=>'不再犹豫'),
		array('id'=>32, 'pid'=>4, 'text'=>'さよならの夏 ～コクリコ坂から～'),
		array('id'=>33, 'pid'=>3, 'text'=>' Heart And Soul'),
		array('id'=>34, 'pid'=>4, 'text'=>'넘버나인 '),
		array('id'=>35, 'pid'=>1, 'text'=>'往事只能回味'),
		array('id'=>36, 'pid'=>3, 'text'=>'Bang Bang'),
		array('id'=>37, 'pid'=>4, 'text'=>'君が好きだと叫びたい'),
		array('id'=>38, 'pid'=>3, 'text'=>'Same Old Love'),
		array('id'=>39, 'pid'=>4, 'text'=>'君をのせて'),
		array('id'=>40, 'pid'=>1, 'text'=>'恋恋风尘')
	);

	// 接收pid
	$pid = $_GET['pid'];

	$result = array();

	foreach ($list as $key => $value) {

		if($value['pid'] == $pid) {
			$result[$key] = $value;
		}
	}

	echo json_encode($result);

?>
```

```php
//nvs.php
<?php

	// 单乐类型
	$navs = array(
		array('id'=>1, 'text'=>'流行'),
		array('id'=>2, 'text'=>'华语'),
		array('id'=>3, 'text'=>'欧美'),
		array('id'=>4, 'text'=>'日韩')
	);

	echo json_encode($navs);

?>
```

