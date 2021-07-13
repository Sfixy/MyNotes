# AJAX

## AJAX简介

ajax全称为Asynchronous JavaScript And XML，就是异步的js和xml

ajax优点：无刷新获取数据

## XML简介

xml可扩展标记语言

xml被设计用来传输和存储数据

xml和html类似，不同的是HTML中都是预定义标签，而xml中没有预定义标签，全部是自定义标签，用来表示一些数据。

现在ajax中的xml已经被json代替。

## AJAX的特点

### AJAX的优点 

1.可以不需要刷新就可以获取页面与服务端通信

2.根据用户事件（鼠标键盘）更新页面内容

### AJAX的缺点

1. 没有浏览历史，不能回退
2. 存在跨域问题
3. SEO（搜索引擎优化）不友好

## HTTP

http协议【超文本传输协议】，协议详细规定了浏览器和万维网服务器之间的相互通信规则。

### 请求报文（发送内容）

重点是格式与参数：

四部分：

请求行：

​			三部分：（1）请求类型：GET/POST  （2）URL路径：（3）HTTP协议版本HTTP/1.1

请求头：

​			Host: atguigu.com

​			Cookie: name=guigu

​			Content-type(请求体是什么类型的): application/x-www-form-urlencoder

​			User-Agent: chrome 83

空行

请求体:（get请求，请求体是空的，Post请求，请求体不为空）username=admin&password=admin



### 响应报文（请求结果）

四部分：

行：

​			三部分：（1）HTTP版本：HTTP/1.1 （2）响应状态码：200 （3）响应状态字符串：ok

头：

​			Content-type：text/html;charset=utf-8

​			Content-length: 2048

​			Content-encoding:gzip

空行（必须有）：

体（返回结果）：比如html



























