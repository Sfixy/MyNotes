# Django

HTTP：

​		无状态、短链接

TCP：

​		不断开

WEB应用（网站）：

​		HTTP协议：

​				发送：



​				响应：

​		浏览器（socket客户端）

​				2.www.cnblogs.com（118.31.180.41，80（默认80端口））

​						sk.socket()

​						sk.connect((118.31.180.41，80))

​						sk.send('我想要xx')

​				5.接收

​				6.连接断开

​		博客园（socket服务端）

​				1.监听ip和端口号(118.31.180.41，80)

​							while True:

​									用户 = 等待用户连接

​									3.收到'我想要xx'

​									4.响应：“好”

​									用户断开

总结：

1.Http，无状态，短链接

2.

​		浏览器（socket客户端）

​		网站（socket服务端）

3.自己写网站

​		a.socket服务端

​		b.根据URL不同返回不同的内容

​				路由系统：

​						URL —> 函数

​		c.字符串返回给用户

​				模板引擎渲染：

​						HTML充当模板（特殊字符）

​						自己创造任意数据

​				字符串

4.Web框架：

​		框架种类：

   - a,b,c                                 ——>  Tornado

   - [第三方a],b,c                   ——>  wsgiref  —>  Django

   - [第三方a],b,[第三方c]     ——>  flask

     分类：

     		- Django框架
     		- 其他



## Django框架

wsgi：web服务网关接口

manage.py  网站所有的管理

```python
命令：
django-admin startproject mysite # 创建django文件
cd mysite
python manage.py runserver 127.0.0.1:8080  # 127.0.0.1:8080设置默认端口  启动监听8080端口
```

### Django程序目录

​		mystie

​				mysite

​					settings.py   # Django配置文件

​					url.py            # 路由系统：url->函数

​					wsgi.py         # 用于定义Django用socket，wsgiref，uwsgi

​		mange.py #对当前Django程序所有操作可以基于 python manage.py + 参数

### 创建Django步骤

1. 创建project

2. 模板路径template目录        templates（html）

3. 静态文件路径 static目录自建（css  js  图片）

   STATIC_URL = '/static/'

   STATICFILES_DIRS = (必须加，)
   
4. 额外配置

   MIDDLEWARE里面得Csrfi注释掉

