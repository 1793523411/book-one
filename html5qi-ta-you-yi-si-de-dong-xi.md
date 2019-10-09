### 智能表单
伴随着互联网富应用以及移动开发的兴起，传统的Web表单已经越来越不能满足开发的需求，所以HTML5在Web表单方向也做了很大的改进，如拾色器、日期/时间组件等，使表单处理更加高效。
一起来了解HTML5表单的新增的特性，以及PC和移动设备间的差异，其兼容性较差


#### 	输入类型  (表单类型，表单元素，表单属性,表单事件.)
email 输入email格式
tel 手机号码  
url 只能输入url格式
number 只能输入数字
search 搜索框
range 范围 滑动条
color 拾色器
time	时间
date 日期 不是绝对的
--datetime 时间日期
month 月份
week 星期
部分类型是针对移动设备生效的，且具有一定的兼容性，在实际应用当中可选择性的使用。
####	表单元素（标签）
  

```
<datalist> 数据列表
  与input 配合使用
  <input type=”text” list=”data”>
 <datalist id=”data”>
 <option>男</option>
 <option>女</option>
 <option>不详</option> 
</datalist>
<keygen>  生成加密字符串
```


  keygen 元素  

      keygen 元素的作用是提供一种验证用户的可靠方法。 
      keygen 元素是密钥对生成器（key-pair generator）。当提交表单时，会生成两个键，    一个是私钥，一个公钥。 

    私钥（private key）存储于客户端，公钥（public key）则被发送到服务器。公钥可用于之后验证用户的客户端证书（client certificate）。


```
<output>   不可当做数据提交？
<meter>   表示度量器，不建议用作进度条
<progress></progress>
   <meter  value="81"    min="0" max="100"  low="60"  high="80" />
```



Max-width   
Min-width 
	 
####	表单属性
placeholder 占位符
autofocus 获取焦点
multiple 文件上传多选或多个邮箱地址  
autocomplete 自动完成，用于表单元素，也可用于表单自身(on/off)
form 指定表单项属于哪个form，处理复杂表单时会需要
novalidate 关闭验证，可用于<form>标签
required 必填项
pattern 正则表达式 验证表单
 手机号:
 `<input type="tel" name="tel" required="required"       pattern="^(\+86)?1[3,5,8](\d{9})$">`
    表单重写没有提及，自行验证，共包含
应用于提交按钮上，如：<input type="submit" formaction="xxx.php">
 
####	表单事件
`oninput` 用户输入内容时触发，可用于移动端输入字数统计
`oninvalid` 验证不通过时触发
 





