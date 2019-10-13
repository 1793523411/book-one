# Ajax工具函数封装

* 原生Ajax写法回顾
原生使用Ajax主要分为五步,需要手写较多内容,如果每次我们使用Ajax都需要手写一遍,较为浪费时间,所以我们将公共代码抽取,封装为工具函数.

* 五步使用法:
建立XMLHTTPRequest对象
注册回调函数
当服务器回应我们了,我们想要执行什么逻辑
使用open方法设置和服务器端交互的基本信息
设置提交的网址,数据,post提交的一些额外内容
设置发送的数据，开始和服务器端交互
发送数据
更新界面
在注册的回调函数中,获取返回的数据,更新界面


* 示例代码:GET get的数据,直接在请求的url中添加即可


```

<script type="text/javascript">
  // 创建XMLHttpRequest 对象
  var xml = new XMLHttpRequest();

  // 设置跟服务端交互的信息
  xml.open('get','01.ajax.php?name=fox');
  xml.send(null);    // get请求这里写null即可

  // 接收服务器反馈
  xhr.onreadystatechange = function () {
      // 这步为判断服务器是否正确响应
      if (xhr.readyState == 4 && xhr.status == 200) {
          // 打印响应内容
          alert(xml.responseText);
      } 
  };
</script>
```




* 示例代码:POST



```
<script type="text/javascript">
  // 异步对象
  var xhr = new XMLHttpRequest();

  // 设置属性
  xhr.open('post', '02.post.php' );

  // 如果想要使用post提交数据,必须添加
  xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");

  // 将数据通过send方法传递
  xhr.send('name=fox&age=18');

  // 发送并接受返回值
  xhr.onreadystatechange = function () {
  // 这步为判断服务器是否正确响应
  if (xhr.readyState == 4 && xhr.status == 200) {
         alert(xhr.responseText);
       } 
  };
</script>
```

## 封装


```
// ajax get 五部曲
function ajax_get(url,data) {
	// 异步对象
	var ajax = new XMLHttpRequest();

	// url 方法
	// 如果是get发送数据 发送的格式为 xxx.php?name=jack&age=18
	// 所以 这里 需要拼接 url
	if (data) {
		// 如果有值 需要拼接字符串 
		// 拼接为xxx.php?name=jack&age=18
		url+='?';
		url+=data;
	}else{
	}

	ajax.open('get',url);
	// 发送
	ajax.send();

	// 注册事件
	ajax.onreadystatechange = function () {
		// 在事件中 获取数据 并修改界面显示
		if (ajax.readyState==4&& ajax.status==200) {
			console.log(ajax.responseText);
		}
	}
}

// ajax_post五部曲
function ajax_post(url,data) {
	// 异步对象
	var ajax = new XMLHttpRequest();

	// url 方法
	ajax.open('post',url);

	// 设置 请求报文 
	ajax.setRequestHeader("Content-type","application/x-www-form-urlencoded");

	// 发送
	if (data) {
		// 如果 有值 post请求 是在 send中 发送给服务器
		ajax.send(data);
	}else{
		ajax.send();
	}
	

	// 注册事件
	ajax.onreadystatechange = function () {
		// 在事件中 获取数据 并修改界面显示
		if (ajax.readyState==4&&ajax.status==200) {
			console.log(ajax.responseText);
		}
	}

}

// 将 get 跟post 封装到一起
/*
	参数1:url
	参数2:数据
	参数3:请求的方法
	参数4:数据成功获取以后 调用的方法
*/
function ajax_tool(url,data,method,success) {
	// 异步对象
	var ajax = new XMLHttpRequest();

	// get 跟post  需要分别写不同的代码
	if (method=='get') {
		// get请求
		if (data) {
			// 如果有值
			url+='?';
			url+=data;
		}else{

		}
		// 设置 方法 以及 url
		ajax.open(method,url);

		// send即可
		ajax.send();
	}else{
		// post请求
		// post请求 url 是不需要改变
		ajax.open(method,url);

		// 需要设置请求报文
		ajax.setRequestHeader("Content-type","application/x-www-form-urlencoded");

		// 判断data send发送数据
		if (data) {
			// 如果有值 从send发送
			ajax.send(data);
		}else{
			// 木有值 直接发送即可
			ajax.send();
		}
	}

	// 注册事件
	ajax.onreadystatechange = function () {
		// 在事件中 获取数据 并修改界面显示
		if (ajax.readyState==4&&ajax.status==200) {
			// console.log(ajax.responseText);

			// 将 数据 让 外面可以使用
			// return ajax.responseText;

			// 当 onreadystatechange 调用时 说明 数据回来了
			// ajax.responseText;

			// 如果说 外面可以传入一个 function 作为参数 success
			success(ajax.responseText);
		}
	}

}
```

